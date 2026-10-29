# FAS-Agententeam-Plattform – PROJECT_STATUS

**Stand:** 30.10.2026  
**Projektphase:** Phase 2 – Einzelagent  
**Abnahmestatus:** Nicht abgenommen  
**Aktueller Schwerpunkt:** Sichere Docker-Agent-Werkzeugausführung ohne unkontrollierten MCP-Gateway-Zugriff

## 1. Gesamtstatus

Die lokale Modellanbindung und die Konfiguration des ersten Docker-Agent-Werkzeugs funktionieren. Der tatsächliche Werkzeugaufruf wurde noch nicht durchgeführt.

Das bisherige zentrale Hindernis ist die nicht ausreichend begrenzte MCP-Gateway-Erreichbarkeit innerhalb von Docker Sandboxes.

Die Gateway-Ursache wurde durch konkrete Netzwerk- und Proxy-Prüfungen eingegrenzt. Ein externer Coding-Agent hat einen alternativen Ausführungsweg vorgeschlagen, der nun auf technische Umsetzbarkeit und Sicherheit geprüft werden soll.

**Phase 2 bleibt nicht abgenommen.**

## 2. Technischer Entwicklungsstand

| Projektbereich | Aktueller Status |
|---|---|
| Docker Agent | v1.142.0, lokale Modellinferenz erfolgreich |
| Docker Sandboxes | v0.48.0 |
| Ollama | Lokale Modellversorgung funktionsfähig |
| Agentenkonfiguration | YAML-Schema 16 erfolgreich validiert |
| Erstes Werkzeug | `get_environment_info` erfolgreich konfiguriert |
| Werkzeugliste | Genau ein Werkzeug durch `debug toolsets --json` bestätigt |
| Echter Werkzeugaufruf | Noch nicht durchgeführt |
| MCP-Gateway | Aktiviert, nicht ausreichend isoliert |
| Netzwerkpolicy | Gateway-Adressen explizit gesperrt; Ollama erlaubt |
| Gateway-Proxy | Trotz Sperren über daemonverwalteten Alias erreichbar |
| Dateisystemschutz | Vollständige Isolation nicht nachgewiesen |
| Docker-Socket | Einzelne Schutztests erfolgreich, Gesamtschutz offen |
| Credential-Isolation | Nicht vollständig nachgewiesen |
| VS-Code-Analyseumgebung | Eingerichtet und funktionsfähig |
| Codex-Sicherheitsprüfung | Konkrete Schreib- und Shell-Versuche technisch blockiert |
| Geschützte FAS-Originale | Keine unautorisierten Änderungen dokumentiert |

## 3. Aktuelle Konfiguration

**Entwicklungs-PC:**

- FAS-Plattform: `C:\FAS-Agententeam_Plattform`
- Analyse-Workspace: `C:\FAS-VSCode-Analyse`
- Codex-Testumgebung: `C:\FAS-Codex-TestHome`

**Docker-Sandbox:**

- Name: `fas-docker-agent-test`
- Ressourcen: historisch 2 CPUs und 4 GB RAM
- MCP-Gateway: `true`
- Gateway-Secret: `mcpgateway`, Quelle `uploaded`
- Netzwerkpolicy: `sandbox`
- Runtime-Mounts: keine ausgewiesen

**Agenten-Testkonfiguration:**

- Hostkopie: `C:\FAS-VSCode-Analyse\fas_environment_test.yaml`
- Sandbox-Kopie: `/home/agent/workspace/fas_environment_test.yaml`
- Modell: `nemotron-3.5-lightning:30b`
- Provider: Ollama
- Modellendpunkt: `http://host.docker.internal:11434/v1`
- Toolset: `environment`
- Aufgelöstes Werkzeug: ausschließlich `get_environment_info`

Die ursprüngliche Modelltest-Konfiguration `fas_nemotron_minimal.yaml` bleibt separat vorhanden.

## 4. Wesentliche Sicherheitsbefunde

### MCP-Gateway und Proxy

Für folgende Adressen wurden explizite Sandbox-Netzwerksperren eingerichtet:

- `mcp-gateway.docker.internal`
- `gateway.docker.internal`

Die Policy-Prüfung bestätigte für beide die Verweigerung.

Tatsächliche HTTP-Tests lieferten dennoch HTTP 400.

Das Netzwerkprotokoll bestätigte einen zugelassenen Zugriff:

```text
host:       mcp-gateway.docker.internal:80
proxy_type: forward
rule:       <daemon-managed alias>
count:      2
```

Ein anderer DNS-Zugriffsweg wurde durch die Proxy-Policy blockiert.

**Bewertung:** Die bisherigen Gateway-Sperren erfassen den daemonverwalteten Kommunikationsweg nicht ausreichend. Die vollständige interne Ursache ist noch ungeklärt.

Die HTTP-Antwort belegt keine erfolgreiche MCP-Sitzung.

### Sonstige Sicherheitsgrenzen

Die allgemeine Sandbox-Dateisystempolicy enthält weiterhin `filesystem:read **` und `filesystem:write **`.

Die frühere Überdeckung von `/run/docker.sock` war in begrenzten Einzeltests erfolgreich, aber nicht als durchgängige Schutzgrenze für den ausführenden Agenten nachgewiesen.

Lokale Ollama-Endpunkte sind durch die Netzwerkpolicy erlaubt. Eine vollständige Cloud-Fallback- und Credential-Isolation ist noch offen.

## 5. Externe Coding-Agent-Prüfungen

### Gesamtprüfung Phase 2

Der externe Coding-Agent bestätigte die grundsätzliche Eignung des bisherigen Entwicklungsansatzes, wies aber auf die fehlenden technischen Sicherheitsnachweise hin.

Seine Aufwandsschätzung von 10–23 Stunden ist eine unverbindliche Planungsannahme. Sie stellt keine Mindestdauer dar.

### Einzelauftrag 1 – Gateway-Isolation

**Ergebnis:** Docker Sandboxes stellt standardmäßig einen MCP-Gateway bereit.

`--static-mcp` beschränkt die dynamische MCP-Serverauswahl, deaktiviert aber den Gateway nicht.

Eine wirksame vollständige Gateway-Abschaltung für Docker Sandboxes v0.48.0 wurde nicht nachgewiesen.

**Technischer Lösungsvorschlag:** Docker Agent ohne die bisherige Sandbox-Gateway-Integration betreiben und ausschließlich das eingebaute `environment`-Toolset verwenden.

### Sicherheitsbewertung des Lösungsvorschlags

Ein direkter Docker-Agent-Start auf Windows ohne zusätzliche Isolation ist nicht ausreichend abgesichert.

Daher wurde ein zweiter gezielter Coding-Agent-Auftrag vorbereitet.

**Einzelauftrag 2 – Sicherer Direktstart:**

Untersuchen, wie Docker Agent v1.142.0 ohne Sandbox-MCP-Gateway innerhalb einer technisch begrenzten Laufzeit betrieben werden kann.

Ein Ergebnis dieses Auftrags liegt noch nicht vor.

## 6. Offene Arbeiten

| Priorität | Arbeitspaket | Ziel |
|---|---|---|
| 1 | Sicheren Ausführungsweg bestimmen | Gateway-unabhängige oder wirksam begrenzte Agentenausführung |
| 2 | Werkzeugrechte absichern | Ausschließlich `get_environment_info` nutzbar |
| 3 | Dateisystem und Docker isolieren | Keine unautorisierten Host- oder FAS-Zugriffe |
| 4 | Netzwerk und Credentials begrenzen | Ausschließlich erforderliche Endpunkte und Berechtigungen |
| 5 | Ressourcen und Abbruchmechanismen absichern | Kontrollierbarer Testbetrieb |
| 6 | Tatsächlichen Werkzeugaufruf durchführen | Reproduzierbarer Aufruf mit überprüfbarer Rückgabe |
| 7 | Einzelagentenauftrag prüfen | Funktions- und Sicherheitsnachweis, unabhängige Prüfung, Abnahmeentscheidung |

Zusammengehörige Prüfungen werden gebündelt. Bereits abgeschlossene Bestandsaufnahmen und Tests werden nur bei konkretem Erkenntnisbedarf wiederholt.

## 7. Nächster Arbeitsschritt

**Ergebnis des externen Coding-Agent-Einzelauftrags 2 auswerten.**

Gesucht wird ein konkreter technischer Entwurf für die sichere Ausführung von Docker Agent ohne die bisherige MCP-Gateway-Abhängigkeit.

Anschließend:

1. Bevorzugten Ausführungsweg auswählen.
2. Schutzmaßnahmen innerhalb des autorisierten Handlungsrahmens gezielt umsetzen und prüfen.
3. Erst bei wirksamen Schutzgrenzen den echten Werkzeugaufruf durchführen.

Keine weiteren allgemeinen CLI-Inventuren oder wiederholten Gateway-Policy-Abfragen ohne neuen Erkenntnisbedarf.

## 8. Dokumentations- und Abnahmestatus

Dieser Projektstatus ist eine operative Momentaufnahme. Er ändert keine normativen FAS-Grundlagendokumente.

Die aktuellen Gateway-Prüfergebnisse stammen aus den übermittelten PowerShell-Ausgaben. Sie wurden nicht durch unabhängigen direkten Zugriff auf den Entwicklungs-PC reproduziert.

Diese Fassung wird im maßgeblichen Projekt-Repository auf D: versioniert.

**Abschlussbewertung:** Die Modell- und Werkzeugkonfiguration ist vorbereitet und geprüft. Die entscheidenden offenen Arbeiten betreffen die sichere Werkzeugausführung und deren technische Nachweise.

**FAS-P2-GATEWAY-001: Offen.**

**Phase 2 – Einzelagent: Weiterhin nicht abgenommen.**