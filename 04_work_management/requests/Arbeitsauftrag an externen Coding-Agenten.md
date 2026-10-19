# FAS – Arbeitsauftrag an externen Coding-Agenten
**Auftragskennung:** FAS-DEV-0001  
**Projekt:** FAS-Agententeam-Plattform  
**Phase:** 2 – Docker-Agent-Laufzeit und lokale Modellanbindung  
**Status:** Zur Bearbeitung – Analyse und Vorbereitung freigegeben, keine Systemänderungen

## 1. Deine Rolle

Du bist ein erfahrener Coding-Agent, Softwarearchitekt und Integrationsspezialist.

Deine Aufgabe ist, uns beim Aufbau einer dauerhaft erweiterbaren KI-Multiagenten-Plattform zu unterstützen.

Arbeite eigenständig, erkenne technische Probleme und schlage begründete Lösungen vor. Warte nicht auf detaillierte Einzelaufträge, solange du innerhalb des freigegebenen Analyseumfangs arbeiten kannst.

**Wichtig:** Du besitzt keine eigenständige Freigabe für Installationen, Systemänderungen oder Änderungen produktiver Projektdateien.

## 2. Langfristiges Projektziel

Auf einem Windows-11-Entwicklungs-PC entsteht eine Plattform spezialisierter KI-Agenten mit:

- Koordinator zur Auftragsverteilung
- Entwicklungsagenten für Programmieraufgaben
- Unabhängigem Prüfagenten
- Testagenten für automatisierte Qualitätssicherung
- Kontrolliertem, ausschließlich lesendem FAS-Wissenszugang
- Git-Versionierung, Audit, Sicherheitskontrollen und menschlicher Freigabe

Die vollständige Zielarchitektur muss erhalten bleiben. Einzeltests dienen nur dem schrittweisen Aufbau.

## 3. Bereits nachgewiesener Projektstand

**Verbindlicher Plattformpfad:**

`C:\FAS-Agententeam_Plattform\`

Die Struktur besitzt 15 Hauptordner und 68 Unterordner.

**Git-Testrepository:**

`C:\FAS-Agententeam_Plattform\06_repositories\sandbox_examples\fas-agenten-test`

- Git 2.56.0.windows.2 funktioniert.
- Python 3.14.7 funktioniert.
- Baseline-Commit: `c24bb677b3422fb56767311c2689294213cd4a66`
- Python-Test erfolgreich.
- Funktionaler Wiederherstellungstest erfolgreich.
- Repository nach der Prüfung sauber.

**Docker Sandboxes:**

- Vorhandene Sandbox-CLI: `sbx.exe`
- Bestehende Test-Sandbox: `fas-isolationstest`
- Neue Sandbox: `fas-docker-agent-test`
- Agententyp: `docker-agent`
- 2 CPUs, 4 GiB RAM
- Kein Host-Workspace eingebunden
- Docker-Agent-CLI innerhalb der Sandbox ausführbar

**Docker-Agent-Diagnose:**

- Benutzerkonfiguration: OK
- Modellkatalog abrufbar
- Docker Model Runner nicht installiert
- Automatische Aktualisierung wegen GitHub HTTP 403 fehlgeschlagen
- Diagnose endet mit `No issues found`
- Standardmodell derzeit: `anthropic/claude-sonnet-5`

**Lokale Modelle:**

LM Studio und Ollama sind laut bisherigen Berichten vorhanden. Eine frühere Verbindung von Docker Sandboxes zu einem lokalen Qwen-Modell wurde erfolgreich getestet.

Die aktuelle Verbindung zwischen Docker Agent und LM Studio ist noch nicht nachgewiesen.

## 4. Dein konkreter Auftrag

Untersuche, wie wir den bereits vorhandenen Docker Agent innerhalb von Docker Sandboxes mit LM Studio und einem lokal betriebenen Modell verbinden können.

Bearbeite insbesondere:

1. Ermittle anhand der zur installierten Version passenden Dokumentation die korrekte Konfiguration für einen lokalen OpenAI-kompatiblen LM-Studio-Endpunkt.
2. Prüfe, wie Docker Agent den lokalen Modellprovider, die Modellkennung und die notwendige API-Adresse erhält.
3. Berücksichtige, dass `127.0.0.1` innerhalb einer Sandbox nicht automatisch den Windows-Host bezeichnet.
4. Entwickle eine Lösung für eine möglichst eng begrenzte Netzwerkverbindung zur lokalen Modell-API.
5. Prüfe, ob das lokale Modell Tool-Calling für einen Coding-Agenten zuverlässig unterstützt.
6. Konzipiere einen ersten ungefährlichen Agententest ohne eingebundenes FAS-Verzeichnis.
7. Berücksichtige den Sicherheitsmodus `strict` und verhindere eine unbeabsichtigte Nutzung des voreingestellten Cloud-Modells.
8. Stelle fest, ob für diese Integration zusätzliche Komponenten tatsächlich notwendig sind. Bevorzuge vorhandene Infrastruktur.

## 5. Sicherheitsgrenzen

Nicht erlaubt ohne zusätzliche menschliche Genehmigung:

- Docker Engine oder Docker Model Runner installieren
- Software oder Modelle herunterladen
- Bestehende Sandboxes löschen oder zurücksetzen
- Firewall-, Host- oder Netzwerkrichtlinien verändern
- FAS-Originaldateien bearbeiten
- Geschützte Git-Repositories verändern
- Cloud-Modelle ohne Zustimmung verwenden
- Zugangsdaten offenlegen
- Neue Dateien auf dem Entwicklungs-PC schreiben
- Agenten selbstständig mit erweiterten Rechten starten

Verwende keine erfundenen YAML-Schlüssel, API-Adressen oder Befehlsoptionen. Nicht bestätigte Annahmen sind ausdrücklich zu kennzeichnen.

## 6. Erwartete Ergebnisse

Liefere einen zusammenhängenden technischen Bericht mit:

**A. Bestandsbewertung:** Welche Komponenten sind nachgewiesen, welche nur historisch berichtet und welche offen?

**B. Integrationsarchitektur:** Wie verbindet sich Docker Agent in der bestehenden Sandbox sicher mit LM Studio?

**C. Konfiguration:** Konkreter, dokumentationsgestützter Konfigurationsentwurf einschließlich Modellprovider, Modellkennung, Endpunkt und Sicherheitsmodus.

**D. Testplan:** Ein kleiner reproduzierbarer Funktionstest und ein separater Tool-Calling-Test mit eindeutigen Erfolgskriterien.

**E. Sicherheitsbewertung:** Dateisystem, Netzwerk, Cloud-Verbindungen, Geheimnisse, Freigabegrenzen und Abbruchmöglichkeiten.

**F. Umsetzungsempfehlung:** Welche konkreten Schritte sind tatsächlich erforderlich, welche unnötig und welche benötigen eine menschliche Freigabe?

## 7. Arbeitsweise

Arbeite möglichst selbstständig innerhalb des Analyseauftrags. Unterscheide konsequent zwischen bestätigtem Ergebnis, historischem Bericht, Annahme und offenem Punkt.

Prüfe widersprüchliche Anforderungen kritisch und begründe, wenn du von einer vorgeschlagenen Lösung abrätst.

Erstelle keine zweite konkurrierende Plattformstruktur.

Wenn du direkten Zugriff auf Dokumente oder Dateien benötigst, benenne sie konkret. Behaupte keinen Zugriff, den du nicht tatsächlich hast.

## 8. Abschluss und Übergabe

Liefere einen prüffähigen Bericht an die FAS-Projektarchitektur und Kontrollinstanz.

**Wichtig:**

Noch keine Installation, keine Konfigurationsänderung und keine Agentenausführung.

Dein Ziel ist zunächst ein belastbarer, möglichst unmittelbar umsetzbarer Integrationsvorschlag.

Beende deinen Bericht mit dem **einen nächsten empfohlenen Umsetzungsschritt**, seinem konkreten Umfang, den erforderlichen Voraussetzungen und der dazu benötigten Freigabe.