# FAS – Konsolidierte Struktur-, Datei- und Abhängigkeitsspezifikation

**Dokumentenkennung:** FAS-AGENTENTEAM-STRUKTUR-2026-10-17-005  
**Bezeichnung:** Vierte konsolidierte Strukturspezifikation (viertes Planungsdokument der aktuellen Arbeitsgruppe; Dokumentenkennung 005 zur Vermeidung einer Kollision mit dem bestehenden Master-Prompt 004)  
**Revision:** 001 – neuer Prüfentwurf  
**Stand:** 17. Oktober 2026  
**Status:** Freigegeben  
**Geltung:** Geplante Agententeam-Plattform, nicht produktive FAS-Originaldateien  
**Geplanter Root-Pfad:** `D:\FAS-Agententeam_Plattform\` – **noch nicht bestätigt**

> **Unmittelbare Schutzregel:** Dieses Dokument plant nur. Es autorisiert weder Ordneranlagen noch Skriptausführung, Installation, Git-Operationen, Zugriffsänderungen, Agentenläufe oder FAS-GIT-001. Die ursprünglichen Dokumente und FAS-Originaldateien bleiben unverändert.

## 1. Ziel, Nutzen und Dokumentenzuständigkeiten

Langfristiges Ziel ist eine erweiterbare Plattform auf dem Entwicklungs-PC, in der ein menschlich beaufsichtigter Koordinator Entwicklungsaufträge delegiert und voneinander getrennte Entwicklungs-, Prüf- und Testrollen zusammenarbeiten. Genehmigtes FAS-Wissen wird später nur lesend eingebunden. Nachweisbare Sicherheitsgrenzen, Genehmigungen, Audit und Restore gehören zur Zielarchitektur. Der erste Test ist ein Meilenstein, nicht die endgültige Ausbaustufe.

| Quelle | Führende Zuständigkeit | Abgrenzung |
|---|---|---|
| Dokument 001, Revision 002 | **Einzige operative Schrittfolge Phase 0–6**, einschließlich nächstem Arbeitsschritt und Phasenabnahme | Die vorliegende Spezifikation darf diese Reihenfolge nicht ersetzen |
| Dokument 003, Revision 002 | Zielarchitektur, menschliche/technische Aufsicht, 15 Hauptbereiche, Gate-Kriterien G0–G7 | Gates sind Nachweis-/Freigabepunkte, **keine zweite To-do-Liste** |
| Master-Prompt mit Kennung 004 | Arbeits-, Quellen-, Sicherheits- und Übergabedisziplin der beratenden KI | Ein Entwurf verleiht keine Systemberechtigung |
| Diese neue Spezifikation (Kennung 005) | **Einheitlicher konkreter Soll-Strukturbaum**, Dateizwecke, Schreib-/Leseregeln, Reifegrade und Abhängigkeitsmatrix | Für technische Ausführung gelten stets 001 und die Einzelgenehmigungen |
| Zusätzlich eingereichter Markdown-Text vom 17.10.2026 | Historische Vorschläge zu Dateiformaten, Orientierungsdateien und Strukturdetails | Nicht als gleichrangige freigegebene Architektur behandeln |

**Dokumentenlenkung:** Die vierte Strukturspezifikation erhält die eindeutige Kennung **005**, weil der bestehende Master-Prompt bereits die Kennung **004** führt. „Vierte“ bezeichnet ihre Stellung als zusätzliches Planungsdokument und **keine** Neuvergabe der bestehenden Kennungen. Dieser Namensentscheid ist ein Vorschlag; die offizielle Registrierung bleibt zur Freigabe offen.

## 2. Prioritätenprinzip: Was muss erledigt sein, bevor der nächste Schritt erlaubt ist?

**Vier Prioritätsstufen:**
- **P0 – zwingend vorher:** Ohne Erfüllung kein nachfolgender betroffener Schreib-/Ausführungsschritt.
- **P1 – für den nächsten Meilenstein:** Muss vor dem jeweiligen Test/Übergang erfüllt sein, nicht pauschal vor jeder leeren Ordneranlage.
- **P2 – vor erweitertem Agententeam/Integration:** Muss vor unabhängigem Prüf-/Testbetrieb oder Wissenszugriff umgesetzt sein.
- **P3 – vor dauerhaftem Betrieb:** Muss vor produktionsähnlichem, kontinuierlichem Betrieb nachgewiesen sein.

**Sperrlogik:** Ein offener P0-Punkt blockiert den betroffenen Schritt. Ein P2/P3-Punkt blockiert **nicht** die vorher ausdrücklich freigegebene rein lesende Planung oder isolierte Vorbereitung. „Gate erfüllt“ und „konkreter Schreibauftrag freigegeben“ sind zwei unterschiedliche Entscheidungen. Kein Agent darf sich selbst eine Freigabe erteilen.

### 2.1 Abhängigkeiten in der einzig maßgeblichen operativen Reihenfolge       Erledigt

### 2.2 Universelle Startprüfung für **jede** schreibende oder ausführende Maßnahme     Erledigt

## 3. Ein einziger konsolidierter Verzeichnis-Sollbaum       ERledigt

## 4. Speicherzonen, Eigentümerschaft und Rechte

Die folgende Matrix definiert **gewünschte Rechte**, keine bereits technisch implementierten ACLs. Die Namen „Plattformverwalter“, „Koordinator“, „Entwickler“, „Prüfer“, „Tester“, „Wissensleser“ und „Audit/Betrieb“ sind **logische Rollen**; konkrete Windows-/WSL-/Container-Identitäten sind noch offen. Die menschliche Aufsicht ist für geschützte Freigaben zuständig. Jeder Schreibzugriff muss später technisch überprüft und auf den konkreten Arbeitsbereich begrenzt werden.

| Zone / Bereiche | Datentypen und typische Formate | Vorgesehene Verantwortlichkeit | Agentenrechte als Ziel | Git/Backup-Leitlinie |
|---|---|---|---|---|
| **Steuerungsquellen:** Root, 00, 01 | Markdown für Regeln/Entscheidungen, Indizes, Diagrammquellen | Mensch + benannter Dokumentenverantwortlicher | Agenten selektiv **lesen**, Änderungsanträge erstellen; keine eigene endgültige Regelfreigabe | Geeignete nichtgeheime Quellen versionieren; genehmigte Sicherung |
| **Konfiguration:** 02 | validiertes YAML und dokumentierte Endpunkte/Tool-Allowlist, keine Klartext-Secrets | Plattformverwalter; Mensch genehmigt Änderungen | Nur freigegebene Konfiguration lesen, keine unkontrollierte Selbständerung | Nichtgeheime Konfigurationsquellen versionieren |
| **Betriebsverfahren:** 03 | Runbooks, Inventar, Healthcheck-Spezifikationen; später Betriebsdaten | Betreiber | Ausgewählte Logs/Status lesen; Wartungsänderungen genehmigungspflichtig | Dokumente versionierbar; volatile Betriebsdaten getrennt |
| **Aufträge/Ergebnisse:** 04 | Auftrag-JSON, Handoff/Prüf-/Testergebnisse, Status-MD | Koordinator (steuernd); Reviewer/Tester für eigene Berichte | Koordinator schreibt Auftrag/Status im zugewiesenen Bereich; Prüfer nur eigenen Bericht, Tester nur Testbericht | Genehmigte strukturierte Artefakte je Sensitivität; Retention definieren |
| **Arbeitsbereiche:** 05 | Laufzeitcode, Testartefakte, temporäre Dateien | Einzelne getrennte Ausführungsidentitäten | Entwickler schreibt **nur** development; Prüfer liest definierten Snapshot und schreibt **nur** review; Tester schreibt **nur** testing; Quarantäne gesperrt | Wegwerfbar; nicht pauschal in Steuerungs-Git oder Backup aufnehmen |
| **Test-Repositories:** 06 | Git-Testprojekte, Revisions-/Integrationsmanifeste | Plattformverwalter + Projektverantwortliche | Nur explizit freigegebene Test-Repos, keine produktiven FAS-Pfade; geschützte Übernahme menschlich | Eigenes Git-Repo/Worktree nach Freigabe; keine Vermischung mit FAS-GIT-001 |
| **Freigegebenes Wissen:** 07 | exportiertes MD/JSON, Provenienz, Freigabereferenz | Verantwortliche Stelle des FAS-Gedächtnisses | Agenten nur **lesen** genehmigter Exporte; kein Mount der Originale | Herkunft/Version dokumentieren; Exporte getrennt behandeln |
| **Audit:** 08 | Ereignisse/Toolaufrufe/Run-Protokolle (ggf. JSONL) | Unabhängige Audit-/Betriebsinstanz | Agenten dürfen Ereignisse an kontrollierten Sammler senden, **nicht** Audit löschen/umschreiben | Manipulationsschutz, gesonderte Retention, unabhängige Sicherung technisch nachweisen |
| **Sicherheit:** 09 | Prüfberichte, Regeln, **Secrets-Metadaten ohne Schlüsselwerte** | Sicherheitsverantwortliche | Agenten möglichst nur notwendige Policy-Auszüge lesen | Keine Zugangsdaten in Git oder Dokumentation |
| **Qualität:** 10 | Test-Suiten, Evaluationsfälle, Gates, Benchmarks | Unabhängige Prüf-/Qualitätsverantwortliche | Entwickler keine selbstbestätigte Qualitätsfreigabe; Tester/Reviewer schreiben eigene Nachweise | Testdefinitionen versionieren, Laufzeitresultate nach Retention |
| **Recovery:** 11 | Backup-Pläne, Inventare, Restore-Protokolle | Betreiber/Recovery-Verantwortliche | Agenten keine Befugnis, unabhängige Sicherungen zu löschen | Tatsächliche Backupdaten **separat**, nicht bloß in diesem Ordner |
| **Berichte:** 12 | Status, Meilensteine, Übergaben | Dokumentations-/Projektverantwortliche | Berichte vorschlagen, Freigabestatus nicht eigenmächtig setzen | Nichtgeheime Berichte versionieren; Archivregel |
| **Automatisierung:** 13 | geprüfte `.ps1`/`.sh`/`.py`, Zeitpläne, Schutzprüfungen | Plattformverwalter + menschliche Genehmigung | Keine freie Skriptausführung aufgrund bloßer Dateiablage | Skriptquellen nach Prüfung versionieren; Ausführung separat genehmigen |
| **Archiv:** 99 | ersetzte Fassungen, historische Berichte | Dokumentenverantwortliche | Nur aufgabenbezogen lesen, kein aktiver Regelvorrang | Unveränderte historische Fassungen mit Kennung/Status aufbewahren |

**Physische Trennung ist noch zu entwerfen und zu prüfen:** Ein gemeinsamer Root ist **keine** geeignete technische Trennung zwischen Arbeitskopien, manipulationsgeschütztem Audit, Secret Store und unabhängigen Backupmedien. Insbesondere bleiben Secret-Werte außerhalb `09_security/secrets_metadata`, echte unabhängige Backups außerhalb der einzigen Plattformplatte und – je nach Bedrohungsmodell – Audit-Sammler/-Speicher außerhalb von Agenten-Schreibbereichen. Tatsächliche Laufwerke/Accounts/ACLs sind noch offen.

## 5. Dateispezifikation, Namensregeln und Erstellungsauslöser

### 5.1 Root-/Orientierungsdateien

| Soll-Datei | Inhalt / maßgebliche Referenz | Verantwortlichkeit und Änderungsregel | Vorbedingung für Erstellung |
|---|---|---|---|
| `README.md` | Plattformzweck, Navigator, Schutzgrenzen und Links | Menschlich geprüfte Quelle, keine Duplikation von Policies | Genehmigte Dateianlage nach bestätigtem Root/G0 |
| `AGENTS.md` | Zentrale Anweisungen **für tatsächlich kompatible Coding-Agenten**; verweist auf maßgebliche Policies | Änderungen genehmigungspflichtig; keine Sicherheit allein durch Prompt | Bei Bedarf vor dem ersten solchen Agenteneinsatz; automatische Einlesung praktisch prüfen |
| `PROJECT_STATUS.md` | Ist-Stand je Komponente: geplant, bestätigt, historisch berichtet, offen; letzte Prüfung und nächste Phase | Projekt-/Dokumentationsverantwortliche, evidenzbasiert | Mit geregelter Projektdokumentation; nur tatsächlich nachgewiesene Zustände eintragen |
| `DOCUMENT_INDEX.md` | Kennung, Titel, Revision, Pfad, Rolle, Status (`Entwurf`, `freigegeben`, `ersetzt`, `archiviert`), Eigentümer, Gültigkeit | Dokumentationsverantwortliche; keine automatische Entwurfsaufwertung | Mit geregelter Projektdokumentation; abweichende Referenzen klären |
| `00` bis `99` jeweils `README.md` | Zweck, Zuständigkeit, erlaubte Formate, Datenklassifizierung, Quellen der Regeln | Bereichsverantwortliche | **Nach** separater Dateianlage-Freigabe, nicht durch bloße G1-Ordnerfreigabe |

Ein `FAS_AGENTEN_START.md` ist im Zusatztext als weiterer Navigator vorgeschlagen. **Entscheidungsvorschlag:** vorerst **keine fünfte redundante zentrale Orientierungsdatei**; Einstieg über Root-`README.md` mit Links zu `AGENTS.md`, `PROJECT_STATUS.md` und `DOCUMENT_INDEX.md`. Falls ein technischer Agentenstart nachweislich eine eigene Datei verlangt, später als dünnen Verweis ergänzen (offene Architekturentscheidung AD-03).

### 5.2 Formate und Beispielartefakte (keine erfundenen lauffähigen Schemas)

| Format | Geplanter Zweck | Beispiel-Sollort / Bedingung | Nicht daraus ableiten |
|---|---|---|---|
| `.md` | Führende Dokumentation: Ziele, Architektur, Entscheidungen, Übergaben | Root, 00/01/03/12; erst genehmigte Dateianlage | Entwürfe sind nicht automatisch freigegeben |
| `.docx` | Optionaler, **aus freigegebener Markdown-Quelle** erzeugter Lese-/Weitergabeexport | Berichte bei Bedarf, keine zweite Wahrheitsquelle | Keine unabhängige Word-Pflege |
| `.yaml` / `.yml` | Deklarative Agent-/Modell-/Werkzeug-/Sandbox-Konfiguration soweit vom Produkt unterstützt | `02_configuration/docker_agent/`, `model_endpoints/`, `sandbox_policies/` | Namen wie `team.yaml` sind **Vorschläge**, keine validierten Docker-Agent-Schemas |
| `.json` | Auftrags-/Ergebnisobjekte, Manifeste, Schemas nach Definition | `04_work_management/requests/`, `06_repositories/manifests/` | `task.schema.json` noch **nicht** spezifiziert/technisch verbindlich |
| `.jsonl` | Fortlaufende Laufzeitereignisse nach geprüftem Schema und Retention | logische Ansicht unter `08_audit/events/` | Datei an sich ist **kein** unveränderbares Audit |
| `.ps1` / `.sh` | Geprüfte Struktur-/Verwaltungs-/Automatisierungsskripte | `13_automation/scripts/` nach Codeprüfung | Das früher erwähnte Strukturplaner-Skript liegt **nicht geprüft** vor |
| `.py` | Projektbezogene Prüfwerkzeuge, Tests, Tools | 10 oder isoliertes Testrepo | Keine pauschale Ausführungserlaubnis |
| `.gitignore` | Ausschluss von Secrets, Logs, Binär- und Laufzeitdaten aus Testrepo | Im **separat genehmigten** Testrepo von Phase 1 | `.gitignore` ist keine Zugriffssperre und entfernt keine bereits historisierten Secrets |

**Namenskonventionen – Vorschlag:** Dokumente mit eindeutiger Kennung, Datum/Revision/Status im Index; Aufgaben mit eindeutiger ID (beispielsweise `FAS-DEV-0001`, erst nach Freigabe des Schemas); technische Dateinamen ASCII/kebab- oder snake_case konsistent pro Tool, nicht blind umbenennen; Protokolle mit UTC-Zeitstempel, Lauf-ID und Datenschutz-/Retentionregeln. Dateinamen gelten erst nach überprüfter Toolkompatibilität als fest.

**Beispiel der fachlichen Zuordnung:** `team.yaml` → künftig Docker-Agent-Konfiguration; `models.yaml` → `02_configuration/model_endpoints/` **falls** diese Aufteilung unterstützt wird; `sandbox-policy.yaml` → `02_configuration/sandbox_policies/` **falls** Format unterstützt; `task.schema.json` → vorgeschlagen `02_configuration/templates/` oder eine später genehmigte spezifische Schemazone; `FAS-DEV-0001.json` → `04_work_management/requests/`; `events.jsonl` → logische Auditansicht `08_audit/events/`. Diese Beispiele sind **nicht** zur automatischen Erstellung bestimmt.

## 6. Informationsfluss und nachweisbarer Auftrag

**Geplante Richtung:** Mensch genehmigt Auftrag und Grenzen → Koordinator liest nur aktuelle, freigegebene Regeln/Statusreferenzen → Entwickler erhält minimale Testquellen und einen eigenen Schreibbereich → unabhängiger Prüfer bewertet definierten Diff/Snapshot → Tester prüft in eigenem Bereich → externer Policy-/Freigabeprozess entscheidet über eine geschützte Übernahme → Audit und Status werden von berechtigter Stelle protokolliert. Der Koordinator darf die menschliche Freigabe nicht ersetzen.

Jeder spätere Lauf enthält mindestens: Lauf-/Auftrags-ID, verantwortliche Instanz, erlaubte Pfade und Tools, Agent-/Modell-/Konfigurationsversion, Eingabe-/Dokumentenreferenzen, Werkzeuge, Änderungen/Diffs, Testergebnisse, Prüfbefunde, Fehler, Zeiten, Freigabe- und Abschlussstatus. Geheimnisse werden nicht mitprotokolliert. Technische Verbindlichkeit ergibt sich erst aus geprüften Schemas, Zugriffsgrenzen und tatsächlicher Ausführung.

**Vor einem Wissensexport:** Quelle und Berechtigung prüfen → Umfang minimieren → Export menschlich genehmigen → Provenienz/Version dokumentieren → nur freigegebene Exportkopie lesend in `07_knowledge` anbieten → Zugriff und Widerruf testen. **Kein Original-Mount und kein Schreiben in FAS-Gedächtnis.**

## 7. Sicherheits-, Versions-, Backup- und Betriebsregeln

1. **Keine Pauschalrechte:** Least Privilege, getrennte technische Identitäten und getrennte Schreibbereiche; niemals unkontrollierter Host-/Docker-Socket-Zugriff oder privilegierte Container.
2. **Keine Scheinsicherheit:** `AGENTS.md`, YAML, `.gitignore`, Verzeichnisnamen und Git ersetzen weder ACLs noch Policy-Enforcement, Auditintegrität oder Backups.
3. **Netzwerk:** lokale Modellverbindung und erforderliche ausgehende Ziele explizit erlauben und technisch prüfen; frühere `Locked Down`-Berichte sind kein Integrations-Sicherheitszertifikat.
4. **Secrets:** nur kontrollierte Laufzeitinjektion/geeigneter Secret Store; `secrets_metadata` enthält ausschließlich Richtlinien/Referenzen; keine Schlüssel in Git/Logs/Templates.
5. **Git:** Nur getrennte Test-Repositories nach Phase-1-Freigabe; weder FAS-GIT-001 noch `D:\FAS_Projektgedaechtnis_Git` verändern. Geschützte Branches nur menschlich freigeben.
6. **Audit:** Append-only oder vergleichbar manipulationsgeschützt als **Zielanforderung**; Integrität, Korrelation, Retention und Löschschutz unabhängig nachweisen. Lokale JSONL-Datei ist dafür allein nicht ausreichend.
7. **Backup:** Test-Rücksetzpunkt **vor** Coding-Test praktisch prüfen; **gesondert** später vollständigen Betriebs-Restore einschließlich Konfigurationen/Artefakten und Zuständigkeiten testen. Unabhängige Sicherung außerhalb des Root vorsehen.
8. **Stop/Rollback:** definierte CPU-/RAM-/GPU-/Token-/Zeit-/Kostenbudgets, maximale Iterationen/Parallelität, Stop bei Rechteverletzung, unverifiziertem Ergebnis, ungeplantem Netzwerkzugriff oder fehlender Freigabe; Quarantäne-/Wiederanlaufverfahren erst nach Test aktivieren.
9. **Dokumentenhygiene:** Historische Revisionen erhalten; widersprüchliche aktuelle Dokumente nicht stillschweigend harmonisieren; Entscheidungsprotokoll, Versionsverweise und Freigabestatus pflegen.

## 8. Nachgereichten Text und bestehende Unterordner abgleichen: Entscheidungstabelle

**Status sämtlicher nachstehender Veränderungen:** Vorschläge für die gemeinsame Dokumentenfreigabe; keine stillschweigende Änderung am Architekturbericht 003.

| ID | Zusatztext / möglicher Konflikt | Führende vorhandene 003-Struktur | Konsolidierungsentscheidung als Vorschlag | Status |
|---|---|---|---|---|
| AD-01 | `02_configuration/models/` gegenüber bestehendem Modellbereich | `02_configuration/model_endpoints/` | **Vorhandenen Ordner behalten**, nur bei echter Schnittstellenanforderung später ändern | Zur Freigabe |
| AD-02 | `02_configuration/sandboxes/` gegenüber `sandbox_policies/` | `02_configuration/sandbox_policies/` | **Vorhandenen Ordner behalten**, keine Paralleldubletten | Zur Freigabe |
| AD-03 | Eigene `FAS_AGENTEN_START.md` neben Root-Navigator | Root `README.md`, `AGENTS.md`, `PROJECT_STATUS.md`, `DOCUMENT_INDEX.md` als Soll | Erst **Root-README als Einstieg**; eigene Startdatei nur nach konkretem Integrationsnachweis | Zur Freigabe |
| AD-04 | `02_configuration/schemas/` fehlt im Architekturbaum 003 | `02_configuration/templates/` | Schemaablage **noch offen**: zunächst dort nur planen; vor erster tatsächlicher Schemaanlage Konsolidierungsentscheid treffen, ggf. explizit versionierte Ergänzung von 003 | Offen |
| AD-05 | Konkrete Namen `team.yaml`, `models.yaml`, `sandbox-policy.yaml` | Agenten-/Modell-/Sandbox-Bereiche 003 | **Nur logische Beispiele**, endgültiger Zuschnitt nach gültiger Docker-Agent-/Sandbox-Dokumentation und Test | Offen |
| AD-06 | Pro Hauptbereich `README.md`, zusätzliche `AGENTS.md` nach Bedarf | Strukturbaum 003 benennt Ordner, nicht Dateien | Regel als vorgeschlagene **Dateibefüllung** übernehmen; keine Dateien durch Freigabe nur leerer Ordner | Zur Freigabe |
| AD-07 | Zusatztext schlägt „jetzt“ komplette Ordner und Dateien vor | Dokument 001 verlangt lesende Phase 0, Mindestkontrollen und konkrete Schreibfreigaben | **001 hat Vorrang**: zuerst Entwurf und Bestandsprüfung, dann Einzelentscheidung; „jetzt“ ist **keine** Freigabe | Geklärt als Schutzgrenze |
| AD-08 | „Vierte“ Spezifikation vs. schon belegte Kennung 004 | Master-Prompt `...-004` bleibt unverändert | Neuen Entwurf als **005** kennzeichnen, vierter Planungsbaustein | Zur Freigabe |
| AD-09 | Audit unter Root versus unabhängiger unveränderbarer Speicher | `08_audit/` als logische Struktur | Verzeichnis bleibt; externer Audit-Speicher/ACLs/Retention in Sicherheitsdesign verbindlich klären | Offen |
| AD-10 | Backups innerhalb Root versus separate unabhängige Ablage | `11_backup_restore/` enthält Pläne/Restore-Nachweise | Keine alleinige Sicherung in Root; tatsächlicher Backup-Zielort später gesondert genehmigen | Offen |

## 9. Dokumentationsvorlagen und Statusdisziplin (nur geplante Inhalte)

### 9.1 Minimaler Eintrag im Projektstatus

| Feld | Bedeutung |
|---|---|
| Komponente / Arbeitsphase | eindeutiger Teil des Zielsystems und Bezug Phase 0–6 |
| Reifegrad | `geplant` / `historisch berichtet` / `bestätigt` / `offen` / `freigegeben` (Freigabe getrennt von technischem Test) |
| Quelle, Rechner, Umgebung, Zeit | konkreter Nachweis oder erkennbar fehlender Nachweis |
| letzter Test / Ergebnis | nur tatsächlich ausgeführte Prüfung |
| offener Blocker und Priorität | P0 bis P3, konkret betroffener Folgeschritt |
| Freigabe-ID / Entscheider | keine erfundene Genehmigung |
| nächster zulässiger Schritt / Rückfallweg | eindeutig, überprüfbar, begrenzt |

### 9.2 Minimaler Eintrag im Dokumentenindex

Dokumentenkennung; Titel; Revisionsnummer; Dateipfad; Quelle/Autorität; Status; Freigabedatum/Entscheider (falls vorhanden); ersetzt-durch; Zuordnung zu Phase/Gate; Vertraulichkeits-/Zugriffsmerkmal. Die Quelle mit höchstem Geltungsrang muss explizit ersichtlich sein.

### 9.3 Minimaler Entscheidungs-/Freigabenachweis

Entscheidungs-ID; betroffene Quellen; konkrete Aktion/Pfade; Begründung; Vorbedingungen; Prüfergebnis; Schutz-/Rollbackplan; verantwortliche Person; Entscheidung (`offen`, `genehmigt`, `abgelehnt`); Datum; Gültigkeits-/Änderungsumfang. Ohne dokumentierte Entscheidung keine technische Umdeutung.

## 10. Offene Entscheidungen, in der Reihenfolge ihrer tatsächlichen Blockadewirkung

| Priorität | Entscheidung / fehlender Beleg | Blockiert unmittelbar |
|---|---|---|
| **P0-1** | Eindeutige Identität von Entwicklungs-PC und aktueller Shell; Lesebefehle Git/Docker Agent auf genau diesem Rechner | Belastbare Phase-0-Abnahme / nächste PC-Maßnahme |
| **P0-2** | Ziel-Root `D:\FAS-Agententeam_Plattform`, existierende Verzeichnisse, Schutzpfade und Kollisionen | Jede dortige Anlage |
| **P0-3** | Fachliche Abnahme **dieser Strukturrevision**, Entscheidung zu AD-01 bis AD-10 soweit für bevorstehende Schritte relevant | Umsetzung einer verbindlichen Sollstruktur |
| **P0-4** | Verantwortliche und **separate** Freigabe für exakt die beabsichtigte erste Schreibmaßnahme; geprüfter Skriptinhalt falls Skript verwendet | Leere Ordner/Dateien/Repositoryanlage |
| **P1-1** | Testrepo-Freigabe, Testdaten-/Berechtigungskonzept, Rücksetztest, Git-Baseline | Erster Coding-Test |
| **P1-2** | Offizielle Docker-Agent-Version/Installationsweg, lokales Tool-Calling und Schnittstellenkompatibilität | Einzelagent/Delegation |
| **P2-1** | Rollen/Identitäten, Policy-Gates, Container-/Sandbox-Mount-/Netzprüfung, unabhängiger Reviewer/Tester | Vollständiges G5-Team |
| **P2-2** | Freigegebene FAS-Exporte, Codex/Cline-Eignung, Quell-/Freigabe-Nachweise | Phase-5-Integration |
| **P3-1** | Externe/geschützte Auditspeicherung, Secret Store, Backupziel, technischer Restore, Monitoring und Incident-Tests | Dauerbetrieb / G7-Abschluss |

**Offene Strukturfrage AD-04 darf nicht durch „vorsorgliches“ Anlegen eines weiteren Unterordners beantwortet werden.** Erst nach Freigabe die eine gültige Variante in den Strukturbaum und im Architekturverweis nachführen.

## 11. Konkreter nächster Schritt und Übergabe

**Jetzt zulässig:** Diese Markdown-Spezifikation als **externen Entwurf** lesen, fachlich überprüfen, kommentieren und vorläufig als Prüfunterlage herunterladen. Ihre Erstellung in der Gesprächsumgebung ist **keine** Anlage am Entwicklungs-PC.

**Als Nächstes nach Dokument 001, Phase 0:** Auf dem eindeutig bestimmten PC **nur lesend** System/Shell identifizieren und Git/Docker-Agent-Aufrufbarkeit prüfen, bestehende Ziel- und Schutzpfade feststellen. Verfügbare historische Sandbox-Prüfungen nur bei konkretem Bedarf ergänzen. Dann Root, Verantwortlichkeiten, AD-Abweichungen und erste konkrete Schreibmaßnahme zur menschlichen Entscheidung vorlegen. **Keine** Installation, kein Git-Commit, kein Strukturplaner-Aufruf vor individueller Freigabe.

**Erfolgskriterium dieses Dokumententwurfs:** Ein einziger vollständiger Sollbaum ohne konkurrierende Parallelordner; alle 15 Hauptbereiche und ihre Unterordner erhalten; Datei-/Rollen-/Datenzonen bestimmt; P0–P3-Abhängigkeiten bis Dauerbetrieb nachvollziehbar; offene Punkte explizit; keine fingierte Freigabe oder technische Behauptung.

## 12. Quellen-, Revisions- und Abgrenzungsvermerk

**Grundlagen (bereitgestellte Dateien, keine neue Laufzeitprüfung):**
1. `FAS_Agententeam_Infrastruktur_Umsetzungsplan_Revision_002_Pruefentwurf(1).md` – Dokument 001, Revision 002.
2. `FAS_Agententeam_Zielarchitektur, Aufsicht und dauerhafter Strukturplan.md` – Dokument 003, Revision 002.
3. `FAS_Agentsteam_MASTER_PROMPT_2026-10-17.md` – Kennung 004, Master-Prompt-Entwurf.
4. `Eingefügtes Markdown(20261017-115141).md` – ergänzende historische Format-/Dateivorschläge.

| Revision | Datum | Änderungen | Freigabestatus |
|---|---|---|---|
| 001 | 17.10.2026 | Erstfassung: konsolidierter Sollbaum, Dateiregeln, Rollen-/Speicherzonen, P0–P3-Abhängigkeiten, Konflikt-/Entscheidungsregister AD-01 bis AD-10, Trennung von Test-Rücksetzpunkt und Betriebs-Restore | **Zur Prüfung; nicht freigegeben** |

**Nicht ausgeführt:** Keine Befehle auf dem Entwicklungs-PC, keine Zielverzeichnisanlage, keine Prüfung des nicht vorliegenden PowerShell-Strukturplaners, keine Installation, keine Git-Aktion und keine Änderung der vorhandenen FAS-Dokumente oder Originaldaten. Alle vorgeschlagenen technischen Funktionen müssen gesondert nachgewiesen werden.
