# Technischer Prüfbericht – FAS-DEV-0001

**Ergebnis:** Die Integration ist mit Docker Agent, Docker Sandboxes und LM Studio grundsätzlich plausibel. Der genaue Laufzeitstand der Ziel-Sandbox ist hier aber nicht bestätigt; daher ist der Konfigurationsentwurf unten ein dokumentengestützter Kandidat, noch keine freigegebene oder getestete Konfiguration.

## A. Bestandsbewertung

| Befund | Einordnung |
|---|---|
| Aktuelle Shell: PowerShell 7.6.5 auf `ADMINIT-R1KT2Q1` | In dieser Sitzung festgestellt; Zuordnung zum vorgesehenen Entwicklungs-PC nicht bestätigt |
| Git 2.56.0.windows.2 | In dieser Sitzung auf dem aktuellen Rechner nachgewiesen; Zustand des Test-Repositories und sein Baseline-Commit hier nicht geprüft |
| Docker Sandboxes `sbx` 0.48.0 | In dieser Sitzung nachgewiesen |
| Docker Agent / `cagent` auf dem Windows-Host | `docker`, `docker-agent` und `cagent` waren nicht auflösbar |
| Vorhandene Sandbox und Docker-Agent-Version darin | Offen: `sbx ls` scheiterte mit „docker login service unavailable“; die Existenz und der Zustand der genannten Sandbox konnten deshalb nicht bestätigt werden |
| LM Studio, Modell und API-Endpunkt | Laut Projektunterlagen historisch berichtet, hier nicht aktuell geprüft |
| Frühere Qwen-Verbindung zur Sandbox | Historisch berichtet; kein Nachweis für Docker-Agent-Toolaufrufe |
| Rollenrechte, Audit, Backup und Restore | Geplant, nicht technisch abgenommen |

Damit widerspricht der Arbeitsauftrag in mehreren Punkten dem aktuellen [Projektstatus](/C:/FAS-Agententeam_Plattform/PROJECT_STATUS.md): cagent ist dort offen, Sandboxes und LM Studio sind historisch berichtet. Die Angaben im Arbeitsauftrag zu Test-Repository, Sandbox, Modell und Agent-Diagnose behandle ich daher nicht als aktuelle Bestätigung.

Zusätzlich widersprechen sich Dokumente in Status und Pfad: Dokument 005 nennt sich im Kopf „Freigegeben“, im Änderungsprotokoll aber „nicht freigegeben“. Die Planungsdokumente 001/003/005 führen noch `D:\FAS-Agententeam_Plattform`; der bestätigte Plattform-Root ist laut README und Projektstatus `C:\FAS-Agententeam_Plattform`. Für diesen Bericht gilt der C:-Pfad; daraus folgt keine Freigabe, dort Dateien anzulegen.

## B. Integrationsarchitektur

Docker Agent und Docker Sandboxes erfüllen verschiedene Aufgaben: Docker Agent führt Agentenkonfiguration und Werkzeuge aus; die Sandbox isoliert deren Ausführung. Docker dokumentiert ausdrücklich `sbx run docker-agent` als unterstützten Sandbox-Kit-Weg. [Docker Agent in Sandboxes](https://docs.docker.com/ai/sandboxes/agents/docker-agent/)

Für einen Aufruf vom Sandbox-Agenten zu LM Studio auf dem Windows-Host ist `127.0.0.1` im Agenten **nicht** die passende Hostadresse. Docker dokumentiert `host.docker.internal`; der Sandbox-Proxy leitet diesen Namen an `localhost` auf dem Host weiter. In der Sandbox-Netzwerkregel ist deshalb `localhost:1234` freizugeben, während die Agentenkonfiguration `host.docker.internal:1234` verwendet. [Hostdienste aus einer Sandbox erreichen](https://docs.docker.com/ai/sandboxes/workflows/development/)

Empfohlen ist eine **nur für die betroffene Sandbox geltende Freigabe auf Port 1234**. Wenn die installierte Sandbox-Version es unterstützt, kann die Regel zusätzlich auf die benötigten API-Pfade und Methoden beschränkt werden: `GET /v1/models` sowie `POST /v1/chat/completions`. Docker weist darauf hin, dass Regeln auch sandboxbezogen und nach HTTP-Methode/Pfad eingegrenzt werden können. [Lokale Netzwerkregeln](https://docs.docker.com/ai/sandboxes/governance/access-controls/local/)

LM Studio sollte dafür nicht unnötig auf alle Netzwerkschnittstellen exponiert werden. Die dokumentierte Proxy-Weiterleitung ermöglicht den Hostzugriff über den Sandbox-Pfad, ohne für diesen Entwurf eine LAN-Freigabe vorauszusetzen.

## C. Konfigurationsentwurf

Docker Agent dokumentiert benannte Custom Provider mit `base_url`, `api_type` und einem Modellbezug. LM Studio bietet die OpenAI-kompatible Chat-Completions-API unter `/v1/chat/completions`. [Docker Agent Custom Provider](https://github.com/docker/docker-agent/blob/main/docs/providers/custom/index.md), [LM Studio OpenAI-kompatible Endpunkte](https://lmstudio.ai/docs/developer/openai-compat)

Der Entwurf nutzt deshalb eine explizite lokale Modellreferenz statt `auto` oder eines Cloud-Modells:

```yaml
version: 16

providers:
  lmstudio:
    provider: openai
    api_type: openai_chatcompletions
    base_url: http://host.docker.internal:1234/v1

models:
  local_qwen:
    provider: lmstudio
    model: <exakte Modellkennung aus LM Studio>

runtime:
  safety: strict

agents:
  root:
    model: local_qwen
    description: Isolierter Funktionstest
    instruction: Verwende nur das ausdrücklich freigegebene Testprojekt.
```

**Vor Verwendung zu bestätigen:**

- `version: 16` entspricht dem aktuellen Docker-Agent-Dokumentationsstand, nicht einer hier nachgewiesenen installierten Version. Docker Agent verwendet versionierte Konfigurationsschemata; deshalb muss die Datei gegen die tatsächlich vorhandene Version geprüft werden. [Konfigurationsübersicht und Schema-Versionierung](https://github.com/docker/docker-agent/blob/main/docs/configuration/overview/index.md)
- `<exakte Modellkennung …>` ist ein Platzhalter. Sie muss aus der von LM Studio gelieferten Modellkennung stammen; `qwen` allein ist keine geprüfte Kennung.
- `token_key` ist weggelassen, weil für einen lokalen LM-Studio-Endpunkt nicht ungeprüft ein API-Schlüssel angenommen werden sollte. Ist Authentifizierung aktiviert, muss deren sichere Injektion separat geklärt werden.
- Die Projektdatei muss in der Sandbox verfügbar sein. Docker dokumentiert, dass die Sandbox keine benutzerweite Host-Konfiguration übernimmt, sondern nur die Projektkonfiguration im Arbeitsverzeichnis sieht. [Docker Agent in Sandboxes](https://docs.docker.com/ai/sandboxes/agents/docker-agent/)
- `strict` in YAML allein reicht nicht als Laufzeitnachweis: Die Sandbox-Dokumentation nennt als Docker-Agent-Startvorgabe `docker-agent run --yolo`. Für den Test muss `--safety strict` explizit beim Start übergeben werden; laut Docker CLI hat die explizite Option Vorrang. [Sandbox-Startvorgabe](https://docs.docker.com/ai/sandboxes/agents/docker-agent/), [Docker-Agent-CLI](https://docs.docker.com/ai/docker-agent/features/cli/)

Der Auftrag nennt zudem `anthropic/claude-sonnet-5` als derzeitiges Standardmodell. Das ist ein weiterer Grund, die lokale Modellkennung explizit zu setzen und den lokalen Modellaufruf zu verifizieren. `strict` steuert Tool-Freigaben; es verhindert **nicht** selbstständig Cloud-Modellverkehr. Dafür muss zusätzlich geprüft werden, dass keine Cloud-Provider-Credentials oder Cloud-Netzfreigaben für den Test verfügbar sind.

## D. Vorgesehener Testplan

Die folgenden Tests wurden **nicht ausgeführt**.

1. **Verbindung und Modellkennung:** Aus der Ziel-Sandbox `GET http://host.docker.internal:1234/v1/models` abfragen. Erfolg: Verbindung über die sandboxbezogene Portfreigabe funktioniert, und die genaue lokal geladene Modellkennung ist sichtbar.
2. **API-Tool-Calling isoliert prüfen:** Eine Chat-Completions-Anfrage mit einem ungefährlichen Dummy-Werkzeug wie `return_test_value` senden. Erfolg: Antwort enthält einen korrekt geparsten `tool_calls`-Eintrag mit gültigen JSON-Argumenten. Dieser API-Test sollte das Werkzeug nur anfordern lassen; er muss die Dummy-Funktion nicht ausführen.
3. **Docker-Agent-Werkzeugaufruf:** Erst danach einen Agenten mit explizitem lokalen Modell und einem minimalen Werkzeug in der Sandbox starten, mit `--safety strict`. Erfolg: Docker Agent verwendet das lokale Modell, fordert das Werkzeug an, wartet auf die erforderliche Freigabe und verarbeitet danach das Ergebnis. Keine FAS-Dateien einbinden.

LM Studio weist darauf hin, dass Tool-Aufrufe von Modell und Chat-Template abhängen: Native Tool-Unterstützung ist belastbarer; bei nicht passenden Modellen kann eine Werkzeuganforderung als normaler Text statt als `tool_calls` zurückkommen. Qwen ist in der LM-Studio-Dokumentation unter den Modellen mit nativer Tool-Unterstützung aufgeführt, aber die konkrete Modellvariante und ihr Template müssen geprüft werden. [LM Studio: Tool Use und Modellunterstützung](https://lmstudio.ai/docs/developer/openai-compat/tools)

## E. Sicherheitsbewertung

- **Dateisystem:** Die gemeldete Sandbox ohne Host-Workspace wäre ein guter Ausgangspunkt. Das muss für die konkrete Sandbox bestätigt werden. Docker Sandboxes geben dem Agenten weitreichende Rechte **innerhalb** der Sandbox; ein eingehängter Workspace wäre daher eine relevante Grenze. [Docker-Sandbox-Sicherheitsmodell](https://docs.docker.com/ai/sandboxes/security/)
- **Netzwerk:** `Locked Down` nicht als Beweis für diese Integration behandeln. Aktive Regeln und eventuelle Kit-Regeln der konkreten Sandbox müssen vor dem Lauf geprüft werden. Docker weist darauf hin, dass Agent-Kits zusätzliche Freigaben beisteuern können. [Netzwerkregeln und Kit-Freigaben](https://docs.docker.com/ai/sandboxes/governance/access-controls/local/)
- **Cloud-Verkehr:** lokales Modell explizit konfigurieren, keine automatische Modellauswahl verwenden und unnötige Cloud-Zugangsdaten/Freigaben ausschließen. `strict` allein sperrt weder Cloud-Modelle noch Netzwerkziele.
- **Tool-Sicherheit:** Wegen der dokumentierten Sandbox-Vorgabe `--yolo` muss `--safety strict` ausdrücklich gesetzt und im Lauf bestätigt werden. Andernfalls würde die Sicherheitsannahme des Tests nicht stimmen.
- **Geheimnisse und Daten:** Keine Schlüssel in YAML, Protokolle oder Chat-Ausgaben schreiben. Modellabfragen enthalten den jeweiligen Prompt; daher nur künstliche Testdaten verwenden.
- **Abbruch:** Bei unerwartetem Cloud-Modell, unerwarteter Netzwerkfreigabe, fehlender Host-Workspace-Abgrenzung oder nicht erklärbaren Toolausführungen den Test abbrechen.

## F. Umsetzungsempfehlung und nächster Schritt

Zusätzliche Installationen, Docker Model Runner, Git-Server, Kubernetes, eine weitere VM oder Monitoring sind für diesen ersten Nachweis nicht begründet. Die vorhandene Sandbox-CLI ist aktuell erreichbar; Docker Agent auf dem Host nicht. Der zielgerichtete Weg ist daher, zunächst den Docker-Agent-Stand **in der bestehenden Sandbox** festzustellen und die bereits berichtete Infrastruktur nicht neu aufzubauen.

**Ein nächster Schritt:** ausschließlich lesende Vorprüfung der vorhandenen Sandbox und des LM-Studio-Endpunkts: Sandbox identifizieren, darin Agent-Version und vorhandene Startkonfiguration ermitteln sowie den aktiven Modellnamen und die Erreichbarkeit der LM-Studio-API feststellen. Das ist Voraussetzung, um die Konfiguration an die installierte Version anzupassen. In dieser Sitzung ließ sich die Sandbox wegen des fehlgeschlagenen `sbx ls`-Aufrufs nicht identifizieren; ich habe weder eine Anmeldung ausgelöst noch einen Agenten gestartet.

Vor einer späteren YAML-Übertragung oder -Anlage, sandboxbezogenen Netzwerkfreigabe oder Agentenausführung ist eine **konkrete menschliche Freigabe** nötig. Diese Maßnahmen sowie Installation, FAS-Zugriff und Systemänderungen wurden nicht vorgenommen.

## Änderungen und Prüfungen in dieser Sitzung

Keine Dateien oder Systeme wurden geändert. Ausgeführt wurden nur lesende Versions-/Verfügbarkeitsabfragen für Host, Shell, Git und `sbx`; die Sandbox-Auflistung scheiterte an der nicht verfügbaren Docker-Login-Prüfung. Dokumentationsrecherche erfolgte anhand der verlinkten offiziellen Docker- und LM-Studio-Quellen.