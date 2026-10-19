FAS – Zielarchitektur und technische Schutzgrenzen
Datei: 02_ZIELARCHITEKTUR.md
Zweck: Einzige normative Beschreibung von Zielsystem, Komponenten, Rollen, Sicherheitsarchitektur und Soll-Verzeichnisstruktur. Zur operativen Reihenfolge siehe 03_UMSETZUNGSPLAN.md; zu KI-Arbeitsregeln siehe 01_MASTER_PROMPT.md.
Zielbild
Ziel ist ein langfristig erweiterbares, Docker-basiertes FAS-KI-Agententeam auf dem Entwicklungs-PC, das Aufträge koordiniert, Code erstellt, unabhängig prüft und testet. Docker Agent (vormals cagent) ist der bevorzugte Orchestrierungsansatz für Koordinator und spezialisierte Agenten; seine Eignung für die Gesamtaufgabe ist praktisch nachzuweisen. Docker Sandboxes sind ein davon getrenntes Mittel zur isolierten Ausführung. Wenn ein Baustein ungeeignet ist, darf eine nachweislich sichere Alternative dafür geprüft werden. Ein Wechsel des Orchestrierungsframeworks oder die Aufgabe des Docker-basierten Gesamtziels erfordert eine ausdrückliche Architekturentscheidung.

Das Team erhält später kontrollierten, zunächst ausschließlich lesenden Zugriff auf ausdrücklich bereitgestellte Exporte aus dem getrennten FAS-Projektgedächtnis. Die Architektur wird als Ganzes entworfen, ihre Funktionen werden schrittweise aktiviert. Erfolg ist sichere, reproduzierbare Zusammenarbeit und nicht die Anzahl installierter Werkzeuge.
Komponenten und Rollen
Bestandteil	Aufgabe und Grenze
Mensch	Ziele, Risiko- und Budgetgrenzen; ausdrückliche Autorisierung geschützter Eingriffe
Koordinator	Auftragszerlegung, Delegation, Abhängigkeits- und Ressourcensteuerung; keine Selbstfreigabe geschützter Änderungen
Entwicklungsagent(en)	Implementierung ausschließlich in zugewiesenen, isolierten Bereichen
Unabhängiger Prüfagent	Prüfung fremder Ergebnisse mit eigenen, technisch getrennten Berechtigungen; keine Selbstprüfung
Testagent/CI	Reproduzierbare Tests und prüffähige Befunde
Technische Durchsetzung	Externe Policy-Gates, Identitäten, Dateirechte, Sandbox-/Netzwerkgrenzen, Freigabesperren und Abbruchmechanismen
Wissenszugang	Ausschließlich genehmigte, nachvollziehbare FAS-Exporte, zunächst lesend; keine Originaldatei-Mounts


Entwicklungsagenten dürfen unabhängige Prüf- und Testergebnisse weder manipulieren noch selbst als unabhängig bestätigen. Wirksame Berechtigungs- und Integritätsgrenzen müssen Prüfkonfigurationen und Befunde schützen. Separate VMs oder Container sind nicht zwingend, wenn die Trennung anderweitig technisch nachgewiesen ist.

Zu integrierende oder auf Eignung zu prüfende Bestandskomponenten: Docker Agent; Docker Sandboxes oder gleichwertige sichere Isolation; LM Studio mit lokalem Modell und gegebenenfalls Ollama; vorhandene WSL2-/Docker-, Hyper-V-/Codex- und Cline-Komponenten. Bestehende Infrastruktur hat Vorrang vor unnötiger Doppelinstallation. Agentenrollen bedeuten nicht automatisch Kompatibilität mit Codex-/Cline-CLIs.
Technische Schutzgrenzen
- Identitäten und Dateien: Separate Identitäten und Arbeitsbereiche mit minimalen Rechten; keine pauschalen Administratorrechte, unkontrollierten Docker-Socket-Zugriffe oder ungeprüften Host-Mounts.
- Netzwerk und Modelle: Nur ausdrücklich genehmigte Verbindungen und Endpunkte. Eine Netzwerkfreigabe ist keine Erlaubnis, Projektinhalte an externe Dienste zu übermitteln. Lokale Modellkommunikation über genehmigte LM-Studio-/Ollama-Endpunkte ist zulässig. Bei lokal vorgesehenen Läufen muss die tatsächlich wirksame Modellauswahl geprüft und unbeabsichtigtes Cloud-Fallback technisch verhindert werden. Die bloße Angabe eines lokalen Modells im Prompt reicht nicht. Vorhandene Cloud-Credentials dürfen keine unbeabsichtigte externe Inferenz ermöglichen; für Cloud-Nutzung oder externe Datenübermittlung ist eine gesonderte ausdrückliche und zweckgebundene menschliche Autorisierung erforderlich.
- Geheimnisse: Nur geeignete Secret Stores oder kontrollierte Laufzeitbereitstellung; keine Klartext-Secrets in Git, Dokumenten oder Logs. Zugriff auf Umgebungsvariablen und Provider-Zugangsdaten ist auf den notwendigen Umfang zu begrenzen.
- Genehmigte Automatisierung: Innerhalb eines vorab genehmigten, begrenzten Testauftrags dürfen Delegation, Codeänderungen, Diffs, unabhängige Reviews, Tests und Korrekturschleifen ohne wiederholte Einzelfreigaben ablaufen. Technische Grenzen umfassen Arbeitsbereich, Tools, Netzwerk und Ressourcen.
- Nicht selbst autorisierbar: Installationen, Host-/Rechte-/Firewalländerungen, produktive FAS-Schreibzugriffe, Eingriffe in FAS-GIT-001, Merge in geschützte Branches, Releases, Löschung produktiver Daten und externe Datenübermittlung.
- Qualität: Unabhängiges Code Review, reproduzierbare Tests, statische Codeanalyse sowie Abhängigkeits- und Schwachstellenprüfungen werden gemäß vorab festgelegtem Risiko und Qualitätsanspruch aktiviert. Vorgeschriebene Prüfungen dürfen nicht eigenmächtig ausgelassen werden.
- Audit und Nachweise: Jeder Lauf besitzt eine eindeutige Auftragskennung und referenziert Eingaben, Agent/Modell/Konfiguration, relevante Toolaufrufe, Änderungen, Tests, Befunde, Fehler, Zeiten und gegebenenfalls die separate menschliche Ausführungsentscheidung. Geheimnisse sind zu entfernen. Audit braucht Manipulationsschutz und Aufbewahrungsregeln; Git ersetzt weder Audit noch Backup.
- Ressourcen und Ausfälle: CPU-/RAM-/GPU-, Zeit-, Token-, Kosten- und Wiederholungsgrenzen sowie Stop-/Quarantänemechanismen sind durchzusetzen. Bei Ausfall des Koordinators müssen unabhängige technische Kontrollen unzulässige Ausführung verhindern beziehungsweise betroffene Läufe stoppen. Nicht überprüfbare Ergebnisse sind kein Erfolg.
- Wiederherstellung: Sicherungen getrennt halten und Restore praktisch testen. Dauerbetrieb setzt gesonderte technische Abnahme voraus.
Geschützte Bestandsbereiche
Als historisch berichtete und vor konkretem Eingriff zu verifizierende geschützte Bestandsorte gelten D:\FAS-Agent und D:\FAS_Projektgedaechtnis_Git. FAS-Originaldateien und das eigenständige Vorhaben FAS-GIT-001 bleiben außerhalb der Agenten-Testbereiche. Keine pauschalen Lese- oder Schreibrechte auf die Originale. Die genannten D:-Schutzpfade sind nicht mit dem verbindlichen Plattform-Root auf C: zu verwechseln; ihre bloße Nennung belegt nicht ihre aktuelle Existenz.
Verbindliche Soll-Verzeichnisstruktur
Der vom Nutzer festgelegte und im bisherigen Aufbau bestätigte Plattformstamm ist C:\FAS-Agententeam_Plattform\. Der folgende Baum ist die führende Strukturdefinition mit 15 Hauptverzeichnissen und 68 Unterverzeichnissen. Seine Dokumentation ersetzt keine aktuelle ACL- oder Funktionsprüfung.
C:\FAS-Agententeam_Plattform\
├── 00_governance\
│   ├── charter\
│   ├── policies\
│   ├── roles_permissions\
│   ├── approvals\
│   └── architecture_decisions\
├── 01_architecture\
│   ├── diagrams\
│   ├── interfaces\
│   ├── threat_model\
│   └── capacity_planning\
├── 02_configuration\
│   ├── docker_agent\
│   │   ├── coordinator\
│   │   ├── developer\
│   │   ├── reviewer\
│   │   ├── tester\
│   │   └── memory_reader\
│   ├── model_endpoints\
│   ├── sandbox_policies\
│   ├── tool_allowlists\
│   └── templates\
├── 03_operations\
│   ├── inventory\
│   ├── runbooks\
│   ├── healthchecks\
│   ├── monitoring\
│   ├── incidents\
│   └── recovery\
├── 04_work_management\
│   ├── requests\
│   ├── task_specs\
│   ├── handoffs\
│   ├── review_reports\
│   ├── test_reports\
│   └── releases\
├── 05_workspaces\
│   ├── templates\
│   ├── development\
│   ├── review\
│   ├── testing\
│   └── quarantine\
├── 06_repositories\
│   ├── sandbox_examples\
│   ├── manifests\
│   └── integration_staging\
├── 07_knowledge\
│   ├── approved_exports\
│   ├── decision_index\
│   ├── lessons_learned\
│   └── provenance\
├── 08_audit\
│   ├── events\
│   ├── tool_calls\
│   ├── agent_runs\
│   ├── integrity_manifests\
│   └── retention_policies\
├── 09_security\
│   ├── access_reviews\
│   ├── network_rules\
│   ├── secrets_metadata\
│   ├── vulnerability_reports\
│   └── isolation_tests\
├── 10_quality\
│   ├── test_suites\
│   ├── evaluation_cases\
│   ├── quality_gates\
│   └── benchmark_results\
├── 11_backup_restore\
│   ├── backup_plans\
│   ├── restore_tests\
│   └── inventories\
├── 12_reports\
│   ├── milestones\
│   ├── status\
│   └── handovers\
├── 13_automation\
│   ├── scripts\
│   ├── schedules\
│   └── guards\
└── 99_archive\
    ├── superseded\
    └── historical```

Der zusätzlich vorhandene Root-Ordner **`Prompts`** ist ein vom Nutzer angelegter **temporärer Dokumenteneingangs- und Bearbeitungsbereich außerhalb des verbindlichen 15+68-Sollbaums**. Er begründet **keine vierte normative Dokumentenquelle**. Seine endgültige Einordnung oder Auflösung erfordert eine ausdrückliche Strukturentscheidung. Bis dahin bleibt er unangetastet; die dort abgelegten Dokumente gelten nur in ihrer ausdrücklich bezeichneten, maßgeblichen Version. Bei künftiger Versionierung des gesamten Plattform-Roots ist der Bereich durch eine geeignete `.gitignore`-Regel vor unbeabsichtigtem Commit zu schützen; dies ist **noch keine Aussage, dass ein entsprechender Ausschluss bereits eingerichtet wurde**. Die `.gitignore` eines untergeordneten Testrepositories erfasst diesen Root-Ordner nicht.

## Datenverantwortung und Zugriffsprinzip

Die folgende Matrix beschreibt **Sollrechte**, keine bereits eingerichteten ACLs.

| Bereich | Führender Inhalt / Verantwortung | Zugriffs- und Versionsprinzip |
|---|---|---|
| `00_governance` | Grundsätze, Mandat, Freigabeentscheidungen / Mensch | Agenten grundsätzlich lesend; freigegebene Texte kontrolliert versionierbar |
| `01_architecture` | Systementwurf und Architektur / Architekturverantwortung | Lesend; geprüfte Quellen kontrolliert versionierbar |
| `02_configuration` | Agenten-, Modell- und Sicherheitskonfiguration / Konfigurationsverantwortung | Änderungen genehmigt; nicht geheime Quellen versionierbar |
| `03_operations` | Runbooks und Betrieb / Betriebsverantwortung | Runbooks versionierbar, Laufzeitdaten gesondert |
| `04_work_management` | Auftragseingang (`requests`), detaillierte Arbeitsaufträge (`task_specs`), Übergaben (`handoffs`), unabhängige Befunde / zuständige Rollen | Vorgangsbezogene Rechte; kein pauschales Entwicklerrecht auf Reviews; Laufdaten nicht pauschal im Git |
| `05_workspaces` | Flüchtige Arbeitsstände / ausführender Agent | Nur eigene Bereiche; keine normative Git-Versionierung |
| `06_repositories` | Getrennte Testrepositorys / Entwicklung und Integration | Git nur im freigegebenen Testrepo und zulässigen Branch |
| `07_knowledge` | Genehmigte Exporte und Herkunft / Wissensverantwortung | Für Agenten kontrolliert lesend; keine Original-Mounts |
| `08_audit` | Tool- und Laufereignisse / unabhängige Auditfunktion | Agenten ohne Änderungs- und Löschrechte; unabhängig geschützt |
| `09_security` | Richtlinien und Sicherheitsprüfungen / Sicherheitsverantwortung | Kontrollierte Änderungen; keine Klartext-Secrets |
| `10_quality` | Prüfvorgaben und unabhängige Ergebnisse / Prüf- und Testrollen | Entwickler dürfen fremde Befunde nicht verändern |
| `11_backup_restore` | Sicherungspläne und Restore-Nachweise / Betrieb | Pläne kontrolliert versionierbar, Backup-Nutzdaten getrennt |
| `12_reports` | Anlassbezogene Meilensteine, Statusnachweise und Übergaben / zuständige Rollen | `status` ist **keine** zweite führende Projektstatusquelle |
| `13_automation` | Skripte und technische Guards / Automation | Quellen versionierbar; Ausführung separat genehmigen |
| `99_archive` | Historische, ersetzte Unterlagen / Dokumentation | Keine aktive Anweisungsquelle; eingeschränkte Änderungen |

Flüchtige Workspaces, vollständige Auditdaten, Geheimnisse und Backup-Nutzdaten bleiben außerhalb der normativen Git-Versionierung. Physische Auslagerung, ACLs, Integritätsschutz und Aufbewahrung sind vor produktiver Nutzung praktisch zu prüfen.

## Dokumenten- und Datenformate

- **Markdown** ist die normative Textquelle. DOCX/PDF sind allenfalls abgeleitete Lesefassungen und begründen keine zweite Autorität.
- `README.md` beschreibt den jeweiligen Bereich. `AGENTS.md` enthält ausschließlich ergänzende **lokale** Agentenanweisungen und widerspricht den drei Stammdokumenten nicht.
- `DOCUMENT_INDEX.md` dient als **nicht normative** Fundstellen-/Versionsübersicht. `PROJECT_STATUS.md` ist die **einzige vorgesehene führende, nicht normative Momentaufnahme** des Plattform-Fortschritts; Auftrags- und Laufnachweise liefern die Einzelnachweise. `12_reports/status` dient nur anlassbezogenen historischen Berichten, nicht einem zweiten synchronisierten Fortschrittssystem.
- YAML nur für von den verwendeten Werkzeugen tatsächlich unterstützte Konfigurationen; JSON für definierte strukturierte Aufträge/Ergebnisse; JSONL für schemagebundene Ereignisse. Keine Scheinkonfiguration.
- Git-Historie ersetzt keine manipulationsgeschützten Auditdaten und keine Backups.

Die früheren Architektur-Gates G0–G7 entfallen als **separate operative Abfolge**. Ihre relevanten Sicherheits- und Qualitätsanforderungen sind in dieser Architektur und den Abnahmekriterien von `03_UMSETZUNGSPLAN.md` abgebildet. Die Phasen **0–6** sind die einzige operative Reihenfolge.

Der hier festgelegte Baum ersetzt konkurrierende Strukturvorschläge. Vor neuen Eingriffen sind tatsächlicher Zielort, Existenz, Schutzpfade, Berechtigungen, Kollisionsfreiheit und konkreter Umfang zu prüfen. Bestehende Dateien oder Ordner dürfen nicht ungeprüft verschoben oder überschrieben werden.