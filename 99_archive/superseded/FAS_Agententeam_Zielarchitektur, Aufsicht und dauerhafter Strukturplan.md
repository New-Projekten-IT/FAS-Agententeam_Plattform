FAS – Zielarchitektur, Aufsicht und dauerhafter Strukturplan
1. Dokumentenlenkung
- Dokumentenkennung: FAS-AGENTENTEAM-ARCH-2026-10-17-003
- Revision: 002 – abgestimmter Architektur-Korrekturentwurf zur Gegenprüfung
- Datum: 17. Oktober 2026
- Status: Zielarchitektur und Einrichtungsvorschlag zur Gegenprüfung; keine Ausführungsfreigabe
- Art: Eigenständiges drittes Planungs- und Übergabedokument. Die Ursprungsfassung von Dokument 003 sowie Dokument 002 bleiben unverändert.
- Geltung: Agententeam-Plattform; keine Freigabe für FAS-Originaldateien, FAS-GIT-001, Systeminstallationen oder produktive Änderungen.
- Bezug: Dokument 001, Revision 002 (vom Nutzer für die Dokumentenabstimmung genehmigt), definiert die maßgebliche operative Abfolge Phase 0–6. Dieses Dokument 003 definiert Zielarchitektur, übergeordnete Aufsicht und Freigabegates G0–G7. Gates sind keine alternative Ausführungsreihenfolge und geben keine Maßnahmen selbst frei.
- Änderungsgrundsatz: Diese Revision ersetzt keine frühere Datei stillschweigend. Beide Dokumentrevisionen müssen vor praktischer Anwendung als zusammengehöriger Stand geführt werden; bei ungeklärter Abweichung nicht ausführen, sondern menschlich entscheiden und dokumentieren.
2. Leitbild und Ausbauprinzip
- Ziel ist eine langfristig erweiterbare Entwicklungsplattform mit Koordinator, Entwicklungsagenten (ggf. Codex und Cline), unabhängigem Prüfer, Tester und kontrolliert lesendem FAS-Gedächtniszugang.
- Die vollständige Zielarchitektur wird von Beginn an geplant und in der Verzeichnisstruktur sichtbar gemacht. Das Anlegen leerer Ordner ist nur nach gesonderter Freigabe zulässig und aktiviert keine Funktionen. Funktionen werden nach überprüfbaren Meilensteinen aktiviert – große Planung, kontrollierte Inbetriebnahme; keine vermeintlich endgültige Minimalarchitektur.
- Erfolg wird an reproduzierbarer Delegation, Qualität, Sicherheit, Nachvollziehbarkeit und Wiederherstellbarkeit gemessen, nicht an installierten Komponenten.
3. Wer überwacht wen?
- Menschliche Gesamtaufsicht: Auftrag, Risikogrenzen, Budget, Architekturfreigaben und Freigabe geschützter Änderungen. Die menschliche Freigabe darf technisch nicht durch den Koordinator ersetzt werden.
- Koordinator (Docker Agent als Kandidat): verteilt Teilaufträge, überwacht Status, Zeit-/Budgetgrenzen, Abhängigkeiten und Eskalationen. Der Koordinator ist kein unabhängiger Sicherheitsauditor.
- Prüfagent: prüft Änderungen unabhängig und mit mindestens getrenntem Schreibbereich; darf eigene Befunde nicht selbst als endgültig freigeben.
- Testagent/CI: führt reproduzierbare Tests aus und liefert nachvollziehbare Ergebnisnachweise. Signaturen oder manipulationsgeschützte Nachweise sind Zielanforderungen, nicht bereits belegte Funktionen.
- Technische Aufsicht: Policy-Gates, Dateisystemberechtigungen, Sandbox-Netzwerkregeln, Ressourcengrenzen, secrets-sichere Protokollierung und Stop-/Quarantänemechanismen. Diese wirken auch bei Fehlern oder Regelverletzungen der Agenten.
- Betriebsaufsicht: zunächst Mensch anhand eines Betriebs-/Freigabeprotokolls; später eigenständige Healthchecks/Benachrichtigungen, deren Meldewege ausdrücklich konfiguriert und getestet werden. Kein stillschweigender 24/7-Betrieb.
4. Automatisierungs- und Freigabegrenzen
- Automatisch innerhalb freigegebener Testbereiche: Aufgaben zerlegen, isolierten Code erstellen, lokale Tests starten, Diffs und Prüfberichte erzeugen, Fehler nach festen Wiederholungsgrenzen korrigieren und Ergebnisse zur Freigabe vorlegen.
- Nicht automatisch: Software installieren, Firewall-/Host-Richtlinien ändern, privilegierte Container starten, Secrets exportieren, produktive FAS-Dateien beschreiben, geschützte Branches mergen, Releases veröffentlichen, produktive Daten löschen oder FAS-GIT-001 ausführen.
- Jeder Lauf erhält: eindeutige Auftrags-ID, Agent/Version, Modell/Version, Konfigurationsrevision, Eingabereferenz, Werkzeugaufrufe, Dateien/Diffs, Prüf-/Testergebnisse, Zeiten, Fehler, Freigabeentscheid und Abschlussstatus.
- Abbruchregeln: begrenzte Iterationen/Token-/Zeit-/Kostenbudgets, Stop bei unzulässigen Zugriffen, auffälligem Verhalten, fehlender Testabdeckung oder nicht verifizierbaren Resultaten. Eskalation an den Menschen.
5. Sicherheits- und Nachweisarchitektur
- Identität und Rechte: Rollenmatrix, getrennte Ausführungsidentitäten, kleinste notwendige Rechte; keine Host-Adminrechte oder freien Docker-Socket-Zugriffe für Agenten.
- Isolation: Sandbox-/VM-Grenzen mit eigenen Arbeitsverzeichnissen; Netz nur nach Allowlist; keine FAS-Originaldatei-Mounts. Historischer Locked-Down-Test ist kein vollständiger Sicherheitsnachweis.
- Git: eigene Testrepositorys, nachvollziehbare Diffs/Branches und manuell kontrollierte Baselines; Git ist kein Audit- oder Backup-Ersatz. Bestehendes FAS-Repository D:\FAS_Projektgedaechtnis_Git bleibt getrennt.
- Secrets: ausschließlich geeigneter Secret Store oder kontrollierte Laufzeitinjektion; niemals Schlüssel in Git, Protokollen oder Vorlagen; im Verzeichnis secrets_metadata liegen nur Richtlinien/Referenzen.
- Audit: append-only oder vergleichbar manipulationsgeschützt als Ziel, Zeitstempel/Korrelation und Aufbewahrungsregeln; Integrität und Löschschutz technisch nachzuweisen. Ein Ordner allein ist keine unveränderbare Auditablage.
- Qualität: Code Review, reproduzierbare Tests, statische Analysen, Dependency-Prüfung, genehmigungsbedürftige Übernahme.
- Backup/Restore: separate gesicherte Ablage und tatsächlich getestete Wiederherstellung; keine Backups produktiver FAS-Daten ohne separate Genehmigung.
- Betrieb: Ressourcenlimits für CPU/RAM/GPU, Wiederholungs- und Parallelitätsgrenzen, Monitoring, Incident-/Quarantäneabläufe, Patch- und Rollback-Verfahren.
6. Strukturbaum – dauerhafte Zielstruktur
D:\FAS-Agententeam_Plattform\
|-- 00_governance\
|   |-- charter\
|   |-- policies\
|   |-- roles_permissions\
|   |-- approvals\
|   `-- architecture_decisions\
|-- 01_architecture\
|   |-- diagrams\
|   |-- interfaces\
|   |-- threat_model\
|   `-- capacity_planning\
|-- 02_configuration\
|   |-- docker_agent\
|   |   |-- coordinator\
|   |   |-- developer\
|   |   |-- reviewer\
|   |   |-- tester\
|   |   `-- memory_reader\
|   |-- model_endpoints\
|   |-- sandbox_policies\
|   |-- tool_allowlists\
|   `-- templates\
|-- 03_operations\
|   |-- inventory\
|   |-- runbooks\
|   |-- healthchecks\
|   |-- monitoring\
|   |-- incidents\
|   `-- recovery\
|-- 04_work_management\
|   |-- requests\
|   |-- task_specs\
|   |-- handoffs\
|   |-- review_reports\
|   |-- test_reports\
|   `-- releases\
|-- 05_workspaces\
|   |-- templates\
|   |-- development\
|   |-- review\
|   |-- testing\
|   `-- quarantine\
|-- 06_repositories\
|   |-- sandbox_examples\
|   |-- manifests\
|   `-- integration_staging\
|-- 07_knowledge\
|   |-- approved_exports\
|   |-- decision_index\
|   |-- lessons_learned\
|   `-- provenance\
|-- 08_audit\
|   |-- events\
|   |-- tool_calls\
|   |-- agent_runs\
|   |-- integrity_manifests\
|   `-- retention_policies\
|-- 09_security\
|   |-- access_reviews\
|   |-- network_rules\
|   |-- secrets_metadata\
|   |-- vulnerability_reports\
|   `-- isolation_tests\
|-- 10_quality\
|   |-- test_suites\
|   |-- evaluation_cases\
|   |-- quality_gates\
|   `-- benchmark_results\
|-- 11_backup_restore\
|   |-- backup_plans\
|   |-- restore_tests\
|   `-- inventories\
|-- 12_reports\
|   |-- milestones\
|   |-- status\
|   `-- handovers\
|-- 13_automation\
|   |-- scripts\
|   |-- schedules\
|   `-- guards\
`-- 99_archive\
    |-- superseded\
    `-- historical\

7. Strukturregeln und Verantwortlichkeit
- 00–04: Regeln, Architektur, Konfiguration, Betrieb und Auftragssteuerung (bevorzugt versioniert, revisionsprüfbar).
- 05–06: ausschließlich Test-/Agentenarbeitsbereiche und getrennte Repository-Kopien; kein unkontrollierter Zugriff auf Originaldateien. Test-Repositories werden erst im operativ vorgesehenen Schritt aus Dokument 001 eingerichtet.
- 07: nur freigegebene Exporte aus FAS, Herkunftsnachweis und Freigabestatus; nicht FAS selbst.
- 08–09: Audit- und Sicherheitsartefakte; sensible Protokolle ggf. extern mit restriktiven Berechtigungen und Retention.
- 10–13: Qualität, Recovery, Berichte, kontrollierte Automatisierung; 99 nur archivierte, nicht mehr aktuelle Artefakte.
- Verzeichnisse sind zunächst Strukturplatzhalter. Ihre Existenz begründet keine Berechtigungs-, Backup-, Audit- oder Integrationsfunktion.
8. Freigabegates – vollständig geplant, gestuft nachgewiesen
Verbindliche Zuordnung: Die Phasen 0–6 in Dokument 001, Revision 002, bilden die einzige operative Reihenfolge. Die Gates G0–G7 in diesem Dokument bezeichnen Architektur- und Sicherheitsnachweise beziehungsweise Freigabeentscheidungen. Die Nummerierung der Gates ist keine zweite chronologische Schrittfolge. Ein Gate darf nur dann als erfüllt gelten, wenn seine konkreten Voraussetzungen belegt, die Entscheidung dokumentiert und erforderliche Einzelmaßnahmen separat freigegeben sind. Vorarbeiten und Nachweise aus mehreren Phasen können zu einem Gate gehören.
Zwingende Vorbedingungen für die erste schreibende Maßnahme (einschließlich leerer Ordner): Rechner und Ausführungskontext eindeutig identifizieren; Zielpfad und betroffene Schutzpfade festlegen; Kollisionen und Abgrenzung zu bestehenden FAS-Verzeichnissen prüfen; verantwortliche Person und auf diese Maßnahme begrenzte menschliche Freigabe dokumentieren. Diese frühen Governance-Mindestkontrollen gelten bereits vor G1, unabhängig davon, dass die vollständige Ausarbeitung des Governance-Modells unter G2 erfolgt. Ohne dokumentierten Nachweis und Freigabe keine Anlage.
Gate	Architektur-/Aufsichtsnachweis	Einordnung zu Dokument 001, Revision 002
G0 – Architekturfreigabe	Rechner-/Speicherort, vorgeschlagene Zielstruktur, Schutzgrenzen und Verantwortlichkeit schriftlich bestätigen; keine pauschale Ausführungsfreigabe	Nach lesender Bestandsaufnahme in Phase 0, vor ersten Schreiboperationen
G1 – Verzeichnisstruktur	Falls benötigt: nur ausdrücklich freigegebene, leere Ordner am bestätigten Pfad; Kollisions-/Schutzpfadprüfung, Ist-/Soll-Nachweis und konkrete Einzelfreigabe. Die Mindestkontrollen gelten vor G1	Freigabepflichtige Vorbereitung vor schreibenden Schritten aus Phase 1; der vollständige Baum kann als leere Zielstruktur angelegt werden, ist aber keine technische Sicherheitsabnahme
G2 – Governance	Rollenmatrix, Auftragskennungen, Änderungs-/Freigabeprozess, Sicherheitsrichtlinien, Geheimnis-/Netzwerkkonzept, Audit-Schema und Backup-Plan stufenweise ausarbeiten; für jeden Test die jeweils nötigen Kontrollen vorab wirksam machen	Frühe Mindestkontrollen vor G1; weitergehende Kontrollen vor den betreffenden Tests in Phasen 1–4, spätere Betriebsnachweise in Phase 6
G3 – Git- und Testgrundlage	Separates Testrepository, Test-Branchverfahren, Testwerkzeuge, freigegebene Baseline und praktisch geprüfter Test-Rücksetzpunkt; kein FAS-GIT-001	Phase 1 und konkrete Vorbedingungen für Phasen 2–4; noch keine vollständige Betriebswiederherstellung
G4 – Agent-Laufzeit	Docker Agent als bevorzugten Kandidaten auf Bezugsweg, Version und Verträglichkeit prüfen; Installation nur nach gesonderter Zustimmung; lokalen Modell- und Tool-Aufruf im Einzelagententest belegen	Phase 2; technische Eignung vor endgültiger Produktentscheidung nachweisen
G5 – Multiagenten-Teamabnahme	Koordinator, Entwickler, unabhängiger Prüfer und Tester mit getrennten Rechten; Ende-zu-Ende-Auftrag einschließlich Tests, Zugriffsprüfung und menschlicher Freigabesperre	Phase 3 ist nur der Zwei-Agenten-Zwischenmeilenstein; G5 ist frühestens nach vollständigem Team-Test in Phase 4 erfüllbar
G6 – Bestandsintegration	Codex/Cline nur nach Kompatibilitäts- und Berechtigungsprüfung; vorhandene Sandboxes als isolierte Ausführungsoption testen, Hyper-V/WSL bis zur Entscheidung erhalten	Fachlich überwiegend Phase 5; soweit Isolation bereits für sicheren Team-Test nötig ist, muss sie vor/innerhalb Phase 4 nachgewiesen werden, ohne G6-Gesamtintegration vorwegzunehmen
G7 – Wissen und Betriebsfestigkeit	Freigegebener, nur lesender FAS-Wissensexport; Audit-Retention, Monitoring, Restore-, Langzeit- und Eskalationstests für kontrollierten Betrieb	Wissensintegration in Phase 5, vollständige Betriebsabnahme in Phase 6; expliziter Nachweis der Betriebswiederherstellung, nicht bloß Test-Rücksetzpunkt

Wiederherstellung – klare Trennung: G3 verlangt einen praktisch verifizierten Rücksetzweg für das isolierte, wegwerfbare Testprojekt. G7 verlangt einen gesicherten, dokumentierten und tatsächlich geprüften Restore der für den Betrieb benötigten Konfigurationen und Artefakte; bei produktiven FAS-Daten ist eine separate Genehmigung notwendig.
**G1-Abschluss bei Verzicht auf eine Verzeichnisanlage:** Wird keine Verzeichnisanlage benötigt oder vorgesehen, erhält G1 den dokumentierten Abschlussstatus „nicht erforderlich“. Hierzu sind die Begründung, die verantwortliche Person, das Entscheidungsdatum und die ausdrückliche menschliche Entscheidung festzuhalten. Dieser Status gilt ausschließlich für die entfallende Verzeichnisanlage und stellt weder eine Ausführungsfreigabe noch eine Genehmigung späterer schreibender Maßnahmen dar. Wird die Verzeichnisanlage später erforderlich, ist G1 erneut zu prüfen und die konkrete Maßnahme gesondert freizugeben.
**G2-Abschluss und Abgrenzung:** Die frühen Governance-Mindestkontrollen sind vor den jeweils betroffenen Maßnahmen nachzuweisen und zu dokumentieren. Ihre Erfüllung bedeutet nicht, dass G2 insgesamt abgeschlossen ist. G2 gilt erst dann als vollständig erfüllt, wenn sämtliche für den festgelegten Zielumfang erforderlichen Governance-Artefakte – insbesondere Rollenmatrix, Auftragskennungen, Änderungs- und Freigabeprozess, Sicherheitsrichtlinien, Geheimnis- und Netzwerkkonzept, Audit-Schema sowie Backup-Plan – vorliegen, geprüft und durch die zuständige menschliche Instanz dokumentiert abgenommen wurden. Die praktische Betriebswirksamkeit der vorgesehenen technischen Schutz-, Audit-, Monitoring- und Wiederherstellungsmaßnahmen ist gesondert an den dafür zuständigen späteren Gates nachzuweisen. Eine teilweise G2-Erfüllung darf nicht als vollständiger Gate-Abschluss ausgewiesen werden.
Allgemeine Gate-Dokumentation: Für jedes Gate sind Sollkriterium, prüfbarer Nachweis, verantwortliche Person, Entscheidungsstatus, Datum und Rückfallweg zu erfassen. Erfolgreiche Einzeltests ersetzen weder spätere Nachweise noch menschliche Genehmigungen. Die vollständige operative Ausführung und die jeweils nächsten Schritte stehen ausschließlich in Dokument 001.
9. Bestehender Sachstand und Grenzen
- Entwicklungs-PC laut früherem Bericht: Windows 11 Pro, Ryzen 7 9700X, 64 GiB RAM, RTX 4090; LM Studio, Ollama, WSL2/Docker Engine, Hyper-V-Codex und Cline-/Codex-Images vorhanden.
- Docker Sandboxes 0.48.0 ist im zuletzt geprüften Windows-Kontext über winget registriert. Die früheren Sandbox- und Qwen-Endpunkttests sind berichtet; die CLI war in späteren PowerShell-Versuchen nicht über docker/docker-sandbox/cagent aufrufbar. Ursache und Rechnerkontext sind nicht abschließend bestätigt.
- Docker Agent ist als bevorzugter Orchestrierungskandidat beschlossen, aber weder erfolgreiche Installation noch Teamdelegation nachgewiesen.
- Verfügbare Git-Version ist im historischen Entwicklungs-PC-Bericht dokumentiert, nicht durch die zuletzt angefragte git --version-Ausgabe dieses Gesprächs bestätigt.
- FAS-GIT-001 hat keine neue Freigabe; vorhandene Git-/Integritäts-Einwände bleiben separat zu klären.
10. Nächster Architektur- und Freigabeschritt (keine alternative operative Anweisung)
- Die operative Reihenfolge ist ausschließlich in Dokument 001, Revision 002, Abschnitt 5 (Phasen 0–6) und Abschnitt 8 (unmittelbarer nächster Arbeitsschritt) festgelegt. Zuerst nur lesend: Rechner- und Shell-Kontext identifizieren sowie Git-/Docker-Agent-Verfügbarkeit klären (Phase 0). Dieses Dokument ordnet die dazugehörigen Architekturfreigaben zu und löst keinen eigenen Ausführungsauftrag aus.
- Danach den vorgeschlagenen Zielpfad D:\FAS-Agententeam_Plattform am eindeutig bestimmten Entwicklungs-PC zur Entscheidung vorlegen. Der Standort ist bewusst außerhalb von D:\FAS-Agent und D:\FAS_Projektgedaechtnis_Git vorgesehen; Existenz, Eignung und Kollisionsfreiheit sind noch zu verifizieren.
- Vor jeder leeren Verzeichnisanlage: Zielpfad, Schutzpfade, Rechneridentität, verantwortliche Person, Freigabeumfang und Kollisionsprüfung dokumentieren; erst danach kann der Mensch die konkrete Maßnahme freigeben. Das vollständige Governance-Konzept (G2) wird anschließend stufenweise aufgebaut; spätere Agenten- oder Systemaktionen benötigen jeweils eigene Kontrollen und Freigaben.
- Der in der Ursprungsfassung erwähnte PowerShell-Strukturplaner liegt unter den beiden zur Prüfung vorliegenden Dokumenten nicht als prüfbare Anlage vor. Seine Parameter -Root und -Apply, seine tatsächliche Wirkung sowie die behaupteten Schutzmechanismen sind daher nicht verifiziert. Ohne Vorlage, Sichtprüfung und separate Freigabe darf das Skript nicht als geprüfte Schutzmaßnahme verwendet oder ausgeführt werden.
- Sofern ein entsprechendes Skript später geprüft und freigegeben wird, sind vor einer Ausführung die betroffenen Pfade und geplanten Änderungen offenzulegen; der Ist-/Soll-Vergleich und das Ergebnis gehören in die Übergabeunterlagen. Weder die Revision dieses Dokuments noch eine allgemeine Gate-Entscheidung ersetzt die konkrete Ausführungsfreigabe.
11. Offene Entscheidungen
- Ist D:\FAS-Agententeam_Plattform auf dem Entwicklungs-PC frei und gewünscht? Welche Laufwerke dienen Daten, Logs und unabhängigen Backups?
- Wie werden Auditlogs revisionssicher abgelegt und wer darf sie einsehen/löschen?
- Welche Aktionen dürfen ohne Bestätigung laufen; welche benötigen jeden einzelnen Auftrag zur Zustimmung?
- Welche Verbindung zwischen Alltags-PC und Entwicklungs-PC ist später erforderlich (derzeit nicht genehmigt)?
- Welcher Secret Store, welche Modelle, welche Docker-Agent-Version und welche Sandbox-Anbindung werden nach Kompatibilitätstest gewählt?
- Wann erfolgt die getrennte Sicherheits- und Betriebs-Restore-Abnahme für dauerhaften Betrieb, und wer verantwortet den Nachweis?
- Wo befindet sich der tatsächlich vorgesehene PowerShell-Strukturplaner, und wer prüft dessen Schutzpfad- und Ausführungslogik vor einer eventuellen Freigabe?
12. Übergabe- und Änderungskontrolle
- Diese Fassung ist Revision 002 von Dokument 003 und ersetzt die Ursprungsfassung nicht stillschweigend. Die ursprünglichen Dokumente 001, 002 und 003 bleiben als historische Fassungen erhalten; der abgestimmte Bezugsstand ist Dokument 001, Revision 002.
- Änderungen an Architektur und Freigabegates erhalten Revisions- beziehungsweise Änderungskennungen, Datum, Begründung und gegebenenfalls einen dokumentierten Freigabeentscheid. Änderungen an operativen Phasen erfolgen federführend in Dokument 001; Verweise sind anschließend abzugleichen.
- Der geplante Verzeichnisbaum ist bis zum technisch belegten Nachweis ein Soll-Zustand, kein installierter Ist-Zustand. Dasselbe gilt für Audit-, Backup-, Monitoring-, Rollen- und Sicherheitssysteme.
- Kein Skript wird durch die Dokumenterstellung ausgeführt; keine Verzeichnisanlage, Installation, Systemänderung, Git-Operation oder produktive FAS-Änderung wird hiermit autorisiert.
13. Revisionsprotokoll
Fassung	Datum	Inhalt	Status
Ursprungsfassung 001	17.10.2026	Ursprüngliche Zielarchitektur, Aufsicht, Strukturbaum und Gates G0–G7	Unverändert aufbewahrt
Revision 002	17.10.2026	Dokumentenautorität gegenüber Dokument 001 präzisiert; G0–G7 operativen Phasen zugeordnet; Mindestkontrollen vor G1 festgelegt; Zwischen- und Gesamtabnahmen sowie Test-Rücksetzpunkt und Betriebs-Restore getrennt; nächste Schritte harmonisiert; fehlende Skriptanlage als Nachweislücke gekennzeichnet	Prüfentwurf zur Gegenprüfung; keine Ausführungsfreigabe


Grenze der Revision: Es fand keine neue technische Prüfung von Windows, Git, Docker Agent, Sandboxes, LM Studio, Netzwerkrechten oder Sicherungen statt. Die Sachstandsangaben aus Abschnitt 9 bleiben historische beziehungsweise dokumentierte Berichtsstände, soweit nicht ausdrücklich anders belegt.