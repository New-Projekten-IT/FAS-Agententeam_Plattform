# FAS-Agententeam-Plattform – Agenten-Arbeitsregeln

**Status:** Erstbefüllungsentwurf, nicht als aktive Agentenkonfiguration oder technische Zugriffssperre abgenommen  
**Stand:** 17.10.2026  
**Dauerhafter Plattform-Root:** `C:\FAS-Agententeam_Plattform\`

## Auftrag und Grenzen

Die Plattform ist für ein langfristiges, menschlich beaufsichtigtes Team mit Koordinator, Entwickler, unabhängigem Prüfer und Tester vorgesehen. Ein späterer Wissensleser darf ausschließlich genehmigte FAS-Exporte lesen. Jede Automatisierung ist nur innerhalb freigegebener Testbereiche und tatsächlich erzwungener technischer Rechte zulässig.

## Vorgaben für kompatible Coding-Agenten

1. Verwende als **Plattform-Root ausschließlich** `C:\FAS-Agententeam_Plattform\`. `D:\FAS-Agententeam_Plattform\` ist eine getrennte Arbeitskopie auf einer mobilen Festplatte und kein zweiter aktiver Entwicklungsplattform-Root. Eine Nutzung dieser Kopie als Quelle sowie jede Dateiänderung oder -verschiebung erfordert den jeweils freigegebenen Auftrag.
2. Nutze `README.md` als Einstieg, `PROJECT_STATUS.md` als Evidenzstand und `DOCUMENT_INDEX.md` als Verzeichnis maßgeblicher Quellen. Bei Widersprüchen nicht selbst entscheiden, sondern stoppen und eine menschliche Klärung verlangen.
3. Änderungen an produktiven FAS-Originaldateien und an `D:\FAS_Projektgedaechtnis_Git` sowie die Ausführung von FAS-GIT-001 sind **nicht freigegeben**. Kein Mount von FAS-Originalen.
4. Installationen, privilegierte Ausführung, Host-/Netz-/Firewall-Änderungen, Secrets-Export, externe Datenübermittlung, Löschen, geschützte Merges und Releases benötigen jeweils ausdrückliche menschliche Freigabe.
5. Die bloße Existenz der Bereiche `05_workspaces`, `06_repositories`, `08_audit` und `11_backup_restore` erteilt keine Schreibrechte und belegt keinen funktionierenden Audit-/Restore-Schutz.
6. Jeder künftige freigegebene Auftrag benötigt ID, Zweck, konkrete Pfad- und Toolgrenzen, Agent-/Modell-/Konfigurationsbezug, Änderungen, Testergebnisse, Prüfungen, Fehler und menschlichen Freigabestatus. Keine Secrets in Protokollen.
7. Entwickler-, Prüf- und Testrollen verwenden getrennte Arbeits- und Schreibbereiche; technisch wirksame Grenzen sind vor Ausführung separat nachzuweisen. Der Koordinator darf Ergebnisse nicht endgültig selbst freigeben.
8. Bei unklaren, widersprüchlichen oder unlogischen Anweisungen Risiken benennen, tatsächliche Nachweise von Planung trennen und nicht eigenmächtig ausführen.

## Autorität und Inkraftsetzung

Die operativen Phasen und ihre Reihenfolge regelt `03_operations\runbooks\03_UMSETZUNGSPLAN.md`. Die maßgebliche Zielarchitektur, die technischen Schutzgrenzen und die Sollstruktur regelt `01_architecture\02_FAS – Zielarchitektur und technische Schutzgrenzen.md`. Die maßgeblichen KI-Arbeits- und Verhaltensregeln enthält `00_governance\policies\01_FAS – Master-Prompt-Agententeam.md`. Die früheren Dokumente 001/003/004/005 sind historische Planungsstände und keine parallel gültige normative Hierarchie. Diese Datei gilt **erst nach menschlicher inhaltlicher Freigabe und tatsächlicher Übernahme** als lokale Arbeitsanweisung für Agenten, die `AGENTS.md` überhaupt unterstützen. Sie ersetzt keine ACLs, Sandboxes, Policy-Gates, Backups oder andere technische Sicherheitsmaßnahmen.
