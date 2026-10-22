# FAS-Agententeam-Plattform – Dokumentenindex

**Dokumentstatus:** Nicht normative Fundstellen- und Versionsübersicht. Bereinigte Fassung vom 22.10.2026; durch die unabhängige Kontrollprüfung vom 22.10.2026 als **FREIGABEFÄHIG** bewertet. Die menschliche Dateiübernahmefreigabe wurde im bisherigen Gespräch ausdrücklich mit „freigabe“ erteilt. Diese Entscheidung betraf ausschließlich die damals bezeichnete Fassung und umfasste deren Sicherung, Übernahme und Kontrolle, nicht deren Git-Versionierung. Keine allgemeine Betriebs-, Schreib- oder Ausführungsfreigabe.

**Redaktioneller Bearbeitungsstand:** 22.10.2026. Historische Entscheidungen und Nachweise behalten ihre ursprünglichen Daten und Geltungsgrenzen.

**Plattform-Root:** `C:\FAS-Agententeam_Plattform\` (vom Nutzer am 17.10.2026 als dauerhaft bestätigt).

## 1. Führende Planungsquellen

| Rolle | Verbindlicher relativer Pfad | Einordnung |
|---|---|---|
| Normatives Stammdokument 01 | `00_governance\policies\01_FAS – Master-Prompt-Agententeam.md` | KI-Verhalten, Arbeitsdisziplin, menschliche Aufsicht und Evidenz |
| Normatives Stammdokument 02 | `01_architecture\02_FAS – Zielarchitektur und technische Schutzgrenzen.md` | Zielarchitektur, technische Schutzgrenzen und Sollstruktur |
| Normatives Stammdokument 03 | `03_operations\runbooks\03_UMSETZUNGSPLAN.md` | Operative Phasen 0–6 und deren Umsetzung |
| Standortentscheidung | `00_governance\architecture_decisions\FAS-ADR-STANDORT-2026-10-17-001.md` | Dokumentierte Entscheidung für C: |
| Bestandsnachweis | `03_operations\inventory\FAS-Bestandsaufnahme.txt` | Historische Bestandsaufnahme; keine Betriebsfreigabe |
| Projektübergabe | `12_reports\handovers\FAS-Agententeam–Korrigierte Projektstatus.md` | Nicht normative Übergabe; technische Angaben nach Evidenzgrad unterscheiden |

## 2. Historische Planungsfassungen

Die früher verwendeten Dokumentenkennungen 001/003/004/005 bezeichnen die historische Dokumentensystematik. Sie sind nicht mit der Anzahl der archivierten Dateien gleichzusetzen und bilden keine aktuell verbindliche normative Dokumentenhierarchie.

Die folgenden drei konkreten historischen Planungsdateien befinden sich nach dokumentierter Archivierung unter `99_archive\superseded\`:

1. `FAS_Agententeam_Infrastruktur_Umsetzungsplan_Revision_002_Pruefentwurf.md`
2. `FAS_Agententeam_Zielarchitektur, Aufsicht und dauerhafter Strukturplan.md`
3. `FAS–Agententeam_Konsolidierte Struktur_Aufbauplan.md`

Ihre historischen Revisions- und Freigabeangaben bleiben als Dokumentationsnachweise erhalten. Aus ihnen ergibt sich keine gegenwärtige normative Geltung oder Ausführungsfreigabe.

Maßgeblich sind die drei in Abschnitt 1 benannten normativen Stammdokumente.

## 3. Steuernde Entscheidung zum Plattformpfad

**Entscheidung (durch Nutzer bestätigt, 17.10.2026):** `C:\FAS-Agententeam_Plattform\` ist der dauerhafte Standort.

Die frühere Festlegung von D: als dauerhaftem Plattform-Root ist überholt. Unter `D:\FAS-Agententeam_Plattform\` befindet sich laut bisheriger Dokumentation eine separate bereinigte Arbeitskopie auf einer mobilen Festplatte. Die aktive Entwicklungsplattform bleibt auf C:.

Die Standortentscheidung ist unter `00_governance\architecture_decisions\FAS-ADR-STANDORT-2026-10-17-001.md` dokumentiert.

Eine weitere Migration oder Neuanlage wird daraus nicht abgeleitet.

## 4. Git-Versionsreferenz der Dokumentation

Die dokumentationsbezogene Git-Baseline der Plattform wurde im Rahmen des Auftrags **FAS-AUS-062** erstellt und mit **Prüfentscheidung 068 vom 19.10.2026** fachlich abgenommen.

**Historische Versionsreferenz:**

- **Repository:** `C:\FAS-Agententeam_Plattform\`
- **Branch:** `main`
- **Root-Commit:** `91f62c0a57487eb4e1c6d8e5e034e67825360454`
- **Commit-Nachricht:** `docs: initialize FAS platform documentation baseline`
- **Umfang:** 16 genehmigte Dateien (15 Dokumentationsdateien und `.gitignore`)
- **Technischer Nachweis:** Abschlussbericht 067 mit Nutzer-PowerShell-Ausgaben; sauberer Git-Status nach dem damaligen Commit
- **Fachliche Entscheidung:** Prüfentscheidung 068

**Nachweisgrenzen:**

Die historische SHA-256-Identität sämtlicher früher bestätigter Dokumentfassungen ist nicht vollständig unabhängig belegt. Diese Nachweisgrenze wurde im Rahmen der damaligen Kontrollentscheidung 068 akzeptiert.

Der Root-Commit ist eine historische Versionsreferenz. Er begründet weder eine aktuelle Unverändertheit des Arbeitsverzeichnisses noch eine technische Sicherheits-, Phase-2- oder Betriebsabnahme.

Die am 22.10.2026 vom Nutzer übermittelten Git-Konsolenausgaben bestätigen die Existenz des Plattform-Repositorys auf `main` und den Root-Commit `91f62c0`. Zu diesem Prüfzeitpunkt waren `DOCUMENT_INDEX.md` und `PROJECT_STATUS.md` verändert und noch nicht für einen Commit vorgemerkt.

Der vollständige Root-Commit-Hash stammt aus den früheren dokumentierten Nachweisen; die aktuelle Konsolenausgabe zeigte dessen Kurzform.

Die vorliegende redaktionelle Bereinigung ist **nicht Bestandteil des historischen Root-Commits**. Für sie ist noch kein neuer Commit nachgewiesen.

## 5. Root-Dateien

- `README.md` – Einstieg / Zweck / Grundgrenzen.
- `PROJECT_STATUS.md` – einzige vorgesehene führende, nicht normative Momentaufnahme des Projektfortschritts.
- `DOCUMENT_INDEX.md` – dieses Register; enthält keine implizite Quellenfreigabe.
- `AGENTS.md` – ergänzende lokale Anweisungen für kompatible Coding-Agenten; keine technische Zugriffssperre.

## 6. Dokumentenlenkung

Historische Dateien einschließlich Originalrevisionen unverändert erhalten. Jede neue Revision benötigt Kennung, Entscheidung, Datum, Begründung und verantwortliche Instanz. Eine im Dokument erwähnte Freigabe darf nicht als nachgewiesen gelten, wenn sich die Dokumentangaben widersprechen.

Die Ablageorte der drei aktuellen normativen Stammdokumente wurden nach früheren Nachweisen auf dem Entwicklungs-PC durch Dateiprüfungen und SHA-256-Vergleiche bestätigt.

Die kontrollierte Dokumentenübernahme wurde am 19.10.2026 mit Prüfentscheidung 037 fachlich abgenommen. Historische Planungsfassungen sind davon getrennt zu behandeln.

Die redaktionelle Bereinigung dieser Indexfassung vom 22.10.2026 ist von den früheren Prüfentscheidungen 037 und 068 zu unterscheiden. Beide Entscheidungen werden durch diese Überarbeitung nicht erweitert.

Die unabhängige fachliche Kontrollprüfung der bereinigten Fassung vom 22.10.2026 ergab **FREIGABEFÄHIG**. Der Nutzer autorisierte anschließend ausdrücklich die Sicherung, Übernahme und Integritätskontrolle der damals bezeichneten Fassung.

Laut dem im Gespräch dokumentierten SHA-256-Vergleich wiesen die lokale `DOCUMENT_INDEX.md` und die Sicherungsdatei `DOCUMENT_INDEX_vor_Bereinigung_20261022_224706_1112160.md` zum Prüfzeitpunkt denselben Hash auf:

`1184D08F890AC743B3A2E3E20E24055112A9416DDBC795766A5C6875DB048824`

Damit wurde die Inhaltsgleichheit dieser beiden Dateien zum Prüfzeitpunkt dokumentiert. Eine eigenständige Übereinstimmung mit der fachlich geprüften Sollfassung wird daraus nicht abgeleitet.

Der Kopierversuch aus dem Downloads-Ordner scheiterte wegen der fehlenden Quelldatei. Eine erfolgreiche Dateiübernahme durch diesen Kopiervorgang wird deshalb nicht behauptet. Der Name der Sicherungsdatei ist kein Nachweis dafür, dass sie einen Zustand vor der Bereinigung enthält.

Die Git-Versionierung dieser Fassung ist noch nicht erfolgt und erfordert eine gesonderte ausdrückliche menschliche Autorisierung. Frühere Prüfentscheidungen 037 und 068 werden durch diese redaktionelle Aktualisierung nicht erweitert.
