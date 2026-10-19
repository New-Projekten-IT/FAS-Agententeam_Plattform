# FAS – Infrastruktur- und Umsetzungsplan für das KI-Agententeam

**Dokumentenkennung:** FAS-AGENTENTEAM-PLAN-2026-10-17-001  
**Revision:** 002 – konsolidierter Korrekturentwurf zur externen Gegenprüfung  
**Stand:** 17. Oktober 2026  
**Dokumentenart:** Planungs-, Entscheidungs- und Übergabedokument  
**Status:** Überarbeiteter Planungsentwurf zur Gegenprüfung; keine Ausführungsfreigabe  
**Geltungsbereich:** Agententeam und getrenntes Testprojekt; keine Änderung produktiver FAS-Originaldateien

**Dokumentenlenkung:** Diese Revision ist ein eigenständiger Korrekturentwurf von Dokument 001. Die ursprüngliche Fassung von Dokument 001 sowie Dokument 003 und das dort erwähnte Dokument 002 bleiben unverändert. Eine inhaltliche Überarbeitung von Dokument 003 und eine verbindliche Gesamtfreigabe stehen aus. Referenzen auf G0–G7 bezeichnen die derzeitige, unveränderte Fassung von Dokument 003.

## 1. Zweck und verbindliches Projektziel

Auf dem leistungsstarken Entwicklungs-PC soll ein dauerhaft nutzbares Team spezialisierter KI-Agenten entstehen, das Softwareentwicklungsaufträge koordiniert, implementiert, unabhängig prüft und testet. Freigegebenes Projektwissen soll später kontrolliert aus dem eigenständigen FAS-Projektgedächtnis bereitgestellt werden. Der Mensch bleibt letzte Entscheidungs- und Freigabeinstanz. Maßstab des Erfolgs ist die nachweisliche Zusammenarbeit der Agenten, nicht die Anzahl installierter Komponenten.

Der ältere Plan unterscheidet einen Alltags-PC für Planung und ungefährliche Vorversuche vom Entwicklungs-PC für den eigentlichen Agentenbetrieb und lokale Modelle. Diese Arbeitsteilung bleibt als Planung erhalten; die aktuelle Rechnerzuordnung einzelner PowerShell-Ausgaben wurde im Gespräch nicht technisch bestätigt.

## 2. Festgestellter Kenntnisstand und Evidenz

| Gegenstand | Festgestellter Stand | Nachweis / Einschränkung |
|---|---|---|
| Docker Sandboxes | Version 0.48.0 laut aktuellem `winget list --name Docker` registriert | Installation im aktuellen PowerShell-Kontext nachgewiesen, Startbarkeit dort noch ungeklärt |
| Sandbox-Funktionstest | Laut späterem Übergabebericht 14 Diagnoseprüfungen, Test-Sandbox `fas-isolationstest`, lokale Modellanfrage erfolgreich | Historische Berichtsaussage, keine erneute aktuelle Laufzeitprüfung |
| Sandbox-Netzwerk | Laut Bericht `Locked Down`, gezielte Freigabe für LM Studio Port 1234 | Sicherheitsprüfung nicht vollständig abgeschlossen |
| LM Studio | Laut Bericht API-Zugriff auf lokales Qwen-Modell aus Sandbox erfolgreich | Funktion von Docker Agent mit demselben Endpunkt noch nicht nachgewiesen |
| Ollama | Windows-Installation und Modellreferenzen laut Übergabebericht vorhanden | Kein aktiver Modellbetrieb für Agententeam nachgewiesen |
| WSL2/Docker Engine | Auf Entwicklungs-PC laut Bericht vorhanden | Bestehende Umgebung erhalten; keine Neuinstallation geplant |
| Hyper-V / FAS-Codex | VM, SSH und vorbereitete Docker-Images laut Bericht vorhanden | Noch kein vollständiger Codex-Auftrag innerhalb dieser VM nachgewiesen |
| Cline | Docker-Images und früherer isolierter Coding-Test laut Bericht vorhanden | Noch nicht mit Koordinator verbunden |
| Docker Agent (`cagent`) | Als Orchestrierungsansatz ausgewählt | Weder installierte Version noch lauffähiger Aufruf bestätigt |
| Git unter Windows | Git 2.56.0 laut Entwicklungs-PC-Bericht bestätigt | Verfügbarkeit in der aktuell verwendeten PowerShell noch nicht erneut geprüft |
| PowerShell-Suche | `Get-Command docker, docker-sandbox, cagent` ohne Ergebnis; `where.exe docker` ohne Fund; `docker-sandbox --help` nicht gefunden; `WinGet\Links` ohne Ausgabe | Belegt nur fehlende Auflösbarkeit dieser Befehle im untersuchten Windows-Kontext; keine Widerlegung der früheren Sandbox-Tests |
| FAS-GIT-001 | Kein neuer Freigabestatus; Git-Aufrufisolation und SHA-256-Integrität noch offen | Kein Commit, keine Git-Umstellung und keine Änderungen an FAS-Originaldateien autorisiert |

**Einordnung:** Docker Agent und Docker Sandboxes sind verschieden. Docker Agent ist das geplante Framework für Agentendefinition und Delegation. Docker Sandboxes stellen isolierte Ausführungsumgebungen bereit. Die tatsächliche Integration beider Produkte muss gesondert erprobt werden. Aus dem Video-Transkript folgt, dass einfache YAML-basierte Agentendefinitionen und ein einzelner Log-Analyse-Agent demonstriert werden; es ist kein Nachweis eines fertigen mehrteiligen FAS-Agententeams.

## 3. Architekturentscheidung – vorläufig und Dokumentenzuständigkeit

**Abgrenzung:** Dokument 003 (`FAS-AGENTENTEAM-ARCH-2026-10-17-003`) beschreibt die angestrebte Zielarchitektur, Aufsicht, Verzeichnis-Zielstruktur und übergeordnete Freigabegates G0–G7. Das vorliegende Dokument 001 definiert **innerhalb des derzeitigen Planungsstands die einzige operative Reihenfolge** (Phasen 0–6), mit Vorbedingungen und Abnahmekriterien. Die Gates von Dokument 003 ersetzen keine operativen Phasen und begründen insbesondere keine Ausführungsfreigabe. Bei Abweichungen wird nicht eigenmächtig gehandelt: Die jeweilige Abhängigkeit wird vor Ausführung geklärt und dokumentiert. Diese Aufgabenteilung ist eine **vorgeschlagene Konsolidierungsregel**, die erst mit gemeinsamer Freigabe beider Dokumentrevisionen verbindlich wird.

1. **Orchestrierung:** Offizieller Docker Agent (`cagent` / Docker Agent) als bevorzugter, aber noch nicht endgültig technisch bestätigter Kandidat für Koordinator und spezialisierte Unteragenten. Konkrete Version, Bezugsweg und Kompatibilität erst vor Installation anhand offizieller Angaben prüfen.
2. **Modellversorgung:** Vorrangig vorhandenes LM Studio mit lokalem Modell; Ollama als mögliche Alternative. Für den Agentenbetrieb Tool-Calling und Endpunktkompatibilität praktisch testen.
3. **Ausführungsisolation:** Vorhandene Docker Sandboxes bevorzugt weiterverwenden, sofern die Kompatibilitäts- und Sicherheitsanforderungen erfüllt sind. Historisch berichtete Prüfungen nicht ohne neue Fragestellung wiederholen; für den konkreten Einsatz notwendige, noch nicht nachgewiesene Kontrollen ergänzen. Ein früherer `Locked Down`-Test ersetzt keine Sicherheitsabnahme der Agenten-Integration.
4. **Bestandsschutz:** WSL2, Hyper-V-Codex und Cline-Images vorerst erhalten, weder ersetzen noch parallel unnötig ausbauen. Ob und wie die bestehenden Codex-/Cline-CLIs von Docker Agent aus steuerbar sind, ist offen; Agentenrollen sind nicht automatisch gleichbedeutend mit diesen CLIs.
5. **Versionierung:** Neues, vollständig separates Testrepository mit Git und eigenen Arbeitsbereichen. Kein Zugriff auf produktive FAS-Originaldateien und keine Vermischung mit `D:\FAS_Projektgedaechtnis_Git`.
6. **Freigabegrenze:** Agenten bearbeiten ausschließlich kontrollierte Testdaten; Übernahme in geschützte Projektstände nur nach menschlicher Genehmigung.

## 4. Mindestvoraussetzungen und gestufte Nachweise

**Vor der ersten schreibenden Maßnahme (auch bloße Ordneranlage):** Rechneridentität und Ausführungskontext feststellen; Zielpfad und betroffene Schutzpfade dokumentieren; Kollisionen und Abgrenzung zu bestehenden FAS-Verzeichnissen prüfen; Verantwortliche und konkrete menschliche Freigabe für genau diesen Schritt protokollieren. Der vorgeschlagene Plattformpfad aus Dokument 003 (`D:\FAS-Agententeam_Plattform`) ist noch zu bestätigen. Vollständige spätere Governance- und Betriebsfunktionen müssen für eine genehmigte, ausschließlich leere Verzeichnisanlage noch nicht aktiviert sein. Eine Ordnerstruktur ist kein Nachweis wirksamer Rollenrechte, Backups oder manipulationsgeschützter Auditlogs.

**Vor dem ersten Code- oder Agentenlauf:** Technisch wirksame Zugriffsgrenzen, erlaubte Testdaten und Arbeitsverzeichnisse, Netz- und Werkzeugfreigaben, Protokollierung und Abbruchmöglichkeit festlegen und entsprechend dem konkreten Test nachweisen. Agenten erhalten keinen Zugriff auf produktive FAS-Originaldateien; geschützte Änderungen bleiben genehmigungspflichtig.

**Zwei Arten von Wiederherstellungsnachweisen:** Ein **Test-Rücksetzpunkt** belegt früh, dass ein wegwerfbares Testprojekt wiederhergestellt oder verworfen werden kann. Eine **Betriebswiederherstellung** umfasst später gesicherte Konfigurationen/Artefakte, tatsächlich erprobten Restore und dokumentierte Zuständigkeiten. Der erste Nachweis erfüllt den zweiten nicht.

| Element | Mindestanforderung | Zeitpunkt |
|---|---|---|
| Docker Agent | Eindeutig identifizierte, startbare CLI mit Versionsnachweis | Vor Agenten-Test |
| Modellanbindung | Erreichbarer lokaler Endpunkt und erfolgreich getesteter Tool-Aufruf | Vor Delegationstest |
| Git-Testrepository | Leeres oder ungefährliches Beispielprojekt, initialer Test-Commit manuell freigegeben | Vor Coding-Test |
| Arbeitsbereiche | Getrennte Verzeichnisse / Branches für Entwicklung und unabhängige Prüfung | Vor Coding-Test |
| Zugriffsregeln | Kein Mount produktiver FAS-Dateien, minimal notwendige Dateisystem- und Netzwerkrechte | Vor Ausführung |
| Testwerkzeuge | Beispielsweise Python und pytest; zusätzliche Tools nur projektbezogen | Vor Coding-Test |
| Auftragsprotokoll | Auftragskennung, Eingabe, Agent, Modell, Änderungen, Testergebnis, Freigabe | Ab erstem Test |
| Rücksetzpunkt | Reproduzierbares Testprojekt und Möglichkeit, Änderungen zu verwerfen | Vor Coding-Test |

Kein Kubernetes, kein zusätzlicher Git-Server, keine weitere virtuelle Maschine und keine umfassende Monitoring-Plattform für den ersten Nachweis erforderlich.

## 5. Verbindliche operative Abfolge mit Erfolgskriterien

**Reihenfolge und Freigabeprinzip:** Die folgenden Phasen sind die vorgeschlagene einzige operative Arbeitsfolge. Die G-Gates aus Dokument 003 sind zusätzliche, übergeordnete Entscheidungspunkte, **keine zweite To-do-Reihenfolge**. Eine Phase oder ein technischer Schritt darf erst umgesetzt werden, wenn seine konkret einschlägigen Schutz- und Freigabevoraussetzungen erfüllt und nachgewiesen sind. Die Umsetzung der in Dokument 003 beschriebenen leeren Zielverzeichnisse ist – falls freigegeben – als begrenzter Vorbereitungsschritt **nach Phase 0 und vor den schreibenden Maßnahmen der Phase 1** einzuordnen. Sie ist nicht automatisch verpflichtend, falls die Zielpfadentscheidung noch offen ist; vorläufig kann nur lesend geplant werden.

### Phase 0 – Ausgangslage fixieren (kurz, lesend)

- Festhalten, auf welchem Rechner und in welcher Shell weitergearbeitet wird; den Rechnerkontext der früheren Befehle weiterhin als ungeklärt behandeln, bis ein Nachweis vorliegt.
- Docker-Agent-Verfügbarkeit und Git-Version mit lesenden Befehlen feststellen.
- Nur wenn für die Integration zwingend erforderlich: tatsächlichen Sandbox-Aufruf ermitteln. Keine generelle Neuprüfung der 14 früheren Diagnosen.

- Zielverzeichnis aus Dokument 003 und Schutzpfade als Vorschlag dokumentieren; noch keine Ordner erzeugen.

**Abnahme:** Startpunkt und vorhandene Werkzeuge eindeutig dokumentiert; keine Installations- oder Projektänderung.

**Zwischenentscheidung vor Phase 1:** Rechner und Zielpfad bestätigen, betroffene Schutzpfade und bestehende Verzeichnisse prüfen und die für eine leere Verzeichnisanlage oder ein neues Testrepository jeweils notwendige schriftliche Einzelgenehmigung festhalten. Der in Dokument 003 erwähnte PowerShell-Strukturplaner liegt **unter den beiden für diese Revision übermittelten Dokumenten nicht vor**; weder seine Existenz an anderer Stelle noch seine Schutzwirkung sind hier überprüft. Ohne vorliegendes und geprüftes Skript keine Aussage über dessen sichere Ausführung treffen. Dry-Run/`-Apply` nur als **Plan aus Dokument 003**, nicht als verifizierte Funktion eines geprüften Skripts behandeln.

### Phase 1 – Geschütztes Git-Testprojekt

- Freigegebenen Testpfad verwenden; gegebenenfalls die separat genehmigte leere Zielstruktur nach geprüfter Kollisions- und Schutzpfadkontrolle anlegen, bevor Repository-Dateien entstehen.
- Neues Testverzeichnis und separates Repository außerhalb produktiver FAS-Pfade auswählen; Anlage des Repositorys ist eine eigene schreibende Maßnahme und erfolgt erst nach dazugehöriger Freigabe.
- Beispielcode, Tests, `.gitignore`, `README` und einfaches Auftrags-/Ergebnisprotokoll vorbereiten.
- Initialen Commit nur nach expliziter Freigabe im Testprojekt durchführen.
- Entwickler- und Prüf-Arbeitsbereich strikt trennen; keine gemeinsamen Schreibrechte.

**Abnahme:** Ein reproduzierbarer, wegwerfbarer Teststand existiert; der Test-Rücksetzpunkt wurde praktisch nachgewiesen; FAS-Originaldateien bleiben unverändert. Damit ist noch keine Betriebswiederherstellung nachgewiesen.

### Phase 2 – Docker Agent als Einzelagent

- Offizielle Docker-Agent-Distribution, unterstützte Windows-/WSL-Variante und Voraussetzungen prüfen.
- Nach Freigabe Docker Agent installieren oder vorhandene Installation nutzen.
- YAML-Konfiguration eines Testentwicklers und lokalen Modellendpunkt konfigurieren.
- Kleinen ungefährlichen Auftrag inklusive Tool-Aufruf ausführen.

**Abnahme:** Der Agent erzeugt in seinem Testbereich nachvollziehbaren Code und dokumentierte Ergebnisse.

### Phase 3 – Zwei-Agenten-Delegation

- Koordinator und Entwickler in Docker Agent konfigurieren.
- Koordinator delegiert eine abgegrenzte Aufgabe; Entwickler liefert Artefakte und Rückmeldung.
- Übergaben, Fehlerfälle, Kontextgröße und Modellfähigkeit beobachten.

**Abnahme (Zwischenmeilenstein):** Eine vollständige, protokollierte Delegation zwischen Koordinator und Entwickler ist reproduzierbar erfolgreich. Dies ist **nicht** die vollständige Multiagenten-Teamabnahme nach G5 des Architekturplans.

### Phase 4 – Prüfung, Tests und sichere Ausführung

- Unabhängigen Prüfer und Tester mit getrennten Rechten hinzufügen.
- Sandbox-Ausführung mit minimalen Mounts, Netzwerkrechten und Testdaten integrieren.
- Automatisierte Tests; Prüfung von Änderungsumfang und Protokollen.
- Menschliche Freigabe vor jeder Übernahme in geschützte Branches.

**Abnahme (vollständiger Team-Test):** Eine Änderung wird erstellt, unabhängig geprüft und getestet; unzulässige Schreibzugriffe bleiben unterbunden und die menschliche Freigabesperre wird geprüft. Dieser Nachweis ist Grundlage der Multiagenten-Abnahme gemäß G5, sofern sämtliche dortigen zusätzlichen Anforderungen erfüllt sind.

### Phase 5 – Bestehende Werkzeuge und FAS-Gedächtnis

- Technisch klären, ob Codex-CLI und Cline als bestehende Werkzeuge eingebunden werden können oder besser getrennte Ausführungsrollen bleiben.
- Nur freigegebene FAS-Informationen lesend bereitstellen; kein Zugriff auf Originalschreibpfade.
- Doppelarbeiten durch dokumentierte Entscheidungen, Aufgabenstatus und Wissensabruf begrenzen.

**Abnahme:** Agenten berücksichtigen nachweislich freigegebenes Vorwissen ohne Änderung des FAS-Quellbestands.

### Phase 6 – Betriebsfestigkeit

- Konfigurationen versionieren; Sicherung und Wiederherstellung prüfen.
- Rollenrechte, Geheimnisverwaltung, Audit-Protokolle, Neustart und Fehlerbehandlung testen.
- Langzeittest mit definierten Abbruch- und Eskalationsregeln.

**Abnahme:** Tatsächlich geprüfte Betriebswiederherstellung, nachvollziehbarer und kontrollierter Betrieb einschließlich Audit-/Rechte-/Abbruchkontrollen; erst danach dauerhafte Nutzung. Ein früher Test-Rücksetzpunkt genügt dafür nicht.

## 5a. Einordnung der Freigabegates aus Dokument 003

Die nachstehende Tabelle ist eine **inhaltliche Zuordnung**, keine Freigabe und keine 1:1-Gleichsetzung. Dokument 003 ist in der vorhandenen Fassung unverändert. Seine Gate-Kriterien sind vor praktischer Anwendung anhand der final abgestimmten Dokumentrevisionen zu konkretisieren.

| Gate aus Dokument 003 | Bezug zur operativen Reihenfolge in Dokument 001 | Abgrenzung des Nachweises |
|---|---|---|
| G0 Architekturfreigabe | Nach den lesenden Feststellungen aus Phase 0, **vor** ersten schreibenden Vorbereitungen | Rechner, Zielpfad, Grenzen und Verantwortlichkeit schriftlich bestätigt; keine Installationserlaubnis per se |
| G1 Verzeichnisbaum | Optionaler, ausdrücklich freizugebender Vorbereitungsschritt vor schreibenden Tätigkeiten aus Phase 1 | Nur freigegebene leere Ordner; Prüfung von Kollisionen/Schutzpfaden und Ist-/Soll-Protokoll; keine wirksamen Sicherheitsfunktionen allein aus Ordnerexistenz ableiten |
| G2 Governance | Mindestvorgaben vor G1/Phase 1; vollständige Ausarbeitung stufenweise vor den jeweils betroffenen Tests | Frühe Mindestkontrollen nicht mit späterem vollständigem Rollen-, Geheimnis-, Audit- und Netzwerkmodell verwechseln; die im Architekturplan genannte Gate-Reihenfolge muss hierfür bei der Revision präzisiert werden |
| G3 Git- und Testgrundlage | Phase 1 sowie testbezogene Vorbedingungen vor Phase 2–4 | Reproduzierbares Testprojekt, Baseline, technisch geprüfter **Test-Rücksetzpunkt**; keine vollständige Betriebs-Restore-Abnahme |
| G4 Agent-Laufzeit | Phase 2 | Startbare CLI, geprüfter Modell-/Tool-Aufruf, erprobter Einzelagent; Installation nur nach Freigabe |
| G5 Multiagenten | Phase 3 als Zwischenmeilenstein; vollständiger Teamnachweis erst Phase 4 | Zwei-Agenten-Delegation ersetzt nicht unabhängigen Prüfer, Tester, Rechteprüfung und Freigabesperre |
| G6 Bestand integrieren | Phase 5, soweit erforderlich | Codex/Cline und Sandbox-Kopplung nur bei geprüfter Eignung; vorhandene Umgebungen bewahren |
| G7 Wissen/Betrieb | Phasen 5 und 6 | Lesender, genehmigter Wissenszugang und später Audit-Retention, Monitoring, Langzeittest sowie **Betriebs-Restore** getrennt nachweisen |

**Offene Abstimmung mit Dokument 003:** Dort steht G2 zeitlich nach G1, obwohl gewisse Schutz- und Freigabevorgaben bereits vor einer Ordneranlage gelten müssen. Die vorstehenden Mindestkontrollen sind deshalb ausdrücklich **Vorbedingungen** von G1; bei der späteren Revision von Dokument 003 ist G2 in „früh erforderliche Mindestkontrollen“ und „anschließende vollständige Governance-Ausgestaltung“ zu präzisieren, ohne die ursprüngliche Historie stillschweigend umzuschreiben.

## 6. Regeln gegen Zielverlust und Wiederholungsarbeit

1. Jede Maßnahme muss auf ein konkretes Abnahmekriterium der nächsten Phase einzahlen.
2. Berichtsstände als **nachgewiesen**, **historisch berichtet**, **offen** oder **geplant** kennzeichnen.
3. Nur eine technische Frage pro Schritt; lesende Prüfung vor Änderungen.
4. Bereits bestandene Prüfungen nicht ohne neue Fragestellung wiederholen.
5. Neue Software, neue Berechtigungen und Systemänderungen nur nach expliziter Freigabe.
6. Jede abgeschlossene Aufgabe mit Befehl, Resultat, betroffenen Pfaden, Fehlern und Folgeschritt protokollieren.
7. Für neue Gespräche dieses Dokument und den letzten Ergebnisbericht als Übergabegrundlage verwenden.
8. Änderungen am vorliegenden Plan dokumentieren (Revision, Datum, Entscheidung, Begründung), nicht stillschweigend überschreiben. Ursprungsfassungen und andere Dokumente unverändert aufbewahren.

## 7. Offene Entscheidungen und Abgrenzungen

- Auf welchem Rechner werden die aktuell gezeigten PowerShell-Befehle ausgeführt? Ein bloßer Prompt `C:\Users\Administrator` identifiziert den Rechner nicht eindeutig.
- Wo soll Docker Agent konkret laufen: Windows nativ oder bestehendes WSL2? Entscheidung nach Prüfung der unterstützten Installationswege und der Modell-/Sandbox-Integration.
- Welche lokalen Modelle unterstützen die für den jeweiligen Agenten erforderlichen Werkzeugaufrufe zuverlässig?
- Sollen ausschließlich lokale Modelle genutzt werden? Bis zur Entscheidung keine Cloud-Anbindung voraussetzen.
- Wie Docker Agent, Sandboxes und vorhandene Codex-/Cline-Installationen technisch zusammenwirken, ist noch zu validieren.
- FAS-GIT-001 bleibt ausdrücklich außerhalb dieses neuen Testrepository-Projekts und bedarf einer gesonderten Freigabe.

## 8. Unmittelbarer nächster Arbeitsschritt

**Zunächst ausschließlich lesend:** Die aktive Rechnerumgebung und Shell eindeutig feststellen; Git und Docker Agent auf genau diesem Rechner prüfen. Anschließend Zielpfad, bestehende Schutzpfade, Verantwortliche und Umfang der ersten zulässigen schreibenden Maßnahme (gegebenenfalls nur leere Ordner) festlegen und **gesondert zur menschlichen Freigabe vorlegen**. Erst nach Dokumentation dieser Mindestkontrollen und konkreter Freigabe dürfen Verzeichnisse oder Testrepository-Dateien angelegt werden. Installation, Agentenausführung und sonstige Systemänderungen benötigen weiterhin eigenständige spätere Freigaben. Der nicht vorliegende PowerShell-Strukturplaner darf bis zur Sichtprüfung nicht als geprüfte Schutzmaßnahme vorausgesetzt werden.

## 9. Quellen- und Dokumentenstatus

- `000_FAS_Bericht_Agententeam_Docker_Stand_2026-10-17(1).md`: ursprünglicher Plan mit Zwei-PC-Aufteilung, Docker-Agent-/Sandbox-Unterscheidung sowie FAS-Git-Freigabegrenzen.
- `Eingefügtes Markdown(20261017-072028).md`: späterer konsolidierter Sachstands- und Übergabebericht für den Entwicklungs-PC.
- `Eingefügter Text(20261017-084206).txt`: Video-Transkript als Anschauungsbeispiel für YAML-Agentenkonfiguration und Einzelagentbetrieb; kein technischer Nachweis für die eigene Umgebung.
- Aktuelle PowerShell-Ausgaben im Gespräch: `Get-Command`, `where.exe`, `docker-sandbox --help`, Dateisuche, `winget list --name Docker`, `WinGet\Links`.

**Bewertungsprinzip:** Historische Angaben werden als Berichtsstand übernommen, nicht nachträglich als aktuelle Laufzeitnachweise ausgegeben. Architekturentscheidungen in diesem Dokument sind Empfehlungen, keine bereits umgesetzten Tatsachen.

**Freigabestatus dieser Revision:** Keine Verzeichnisanlage, keine Installation, keine Systemänderung, keine Ausführung von FAS-GIT-001, keine Änderung produktiver FAS-Dateien und kein Commit durch dieses Dokument autorisiert.

## 10. Änderungsprotokoll dieser Revision

| Revision | Datum | Art der Änderung | Status |
|---|---|---|---|
| Ursprungsfassung 001 | 17.10.2026 | Originaler Infrastruktur- und Umsetzungsplan | Unverändert erhalten |
| Korrekturentwurf 002 | 17.10.2026 | Dokumentenautorität als vorgeschlagene Regel; Zuordnung G0–G7 zu Phase 0–6; frühe Mindestkontrollen vor Dateianlagen; getrennte Nachweise für Zwei-Agenten-/Teamabnahme und Test-Rücksetzpunkt/Betriebs-Restore; konkrete nächste Schritte und Skript-Nachweislücke präzisiert | Zur Prüfung durch zweite KI; **nicht freigegeben** |

**Nicht vorgenommene Änderungen:** Keine technische Neuverifikation der Rechnerumgebung, keine Ausführung von PowerShell, Docker oder Git, keine Änderung an Dokument 003 oder den historisch aufgeführten Quellen. Diese Revision harmonisiert Aussagen aus den beiden bereitgestellten Planungsdokumenten; sie beweist keine bislang offenen technischen Tatsachen.
