# Architekturentscheidung – dauerhafter Plattformstandort C:

**Entwurfs-ID:** FAS-ADR-STANDORT-2026-10-17-001  
**Datum der menschlichen Entscheidung:** 17.10.2026  
**Entscheidung:** `C:\FAS-Agententeam_Plattform\` bleibt der dauerhafte Root-Pfad der FAS-Agententeam-Plattform.

## Grundlage

Nutzerbestätigung am 17.10.2026 und vorgelegte PowerShell-Inventur: 15 Hauptordner, 68 Unterordner, vier zunächst leere Root-Markdown-Dateien und `03_operations\inventory\FAS-Bestandsaufnahme.txt` befinden sich unter C:.

## Abweichung

Dokumente 001/003/004/005 nennen bisher den älteren Vorschlag `D:\FAS-Agententeam_Plattform\`. Dieser Vorschlag ist für den Plattform-Root überholt. Andere bereits bestehende D:-Schutzpfade, z. B. `D:\FAS_Projektgedaechtnis_Git`, sind hiervon nicht betroffen und dürfen **nicht** automatisch umgeschrieben werden.

## Konsequenzen

- Keine neue Struktur auf D: erzeugen; keine bestehende Struktur von C: verschieben.
- In **neuen, versionsgeführten Revisionen** der führenden Planungsdokumente die Plattform-Root-Verweise korrigieren und die Pfadentscheidung referenzieren.
- Die Entscheidung ist **keine pauschale Ausführungsfreigabe** für Installationen, Git, Rechteänderungen oder Agentenläufe.
- Ursprüngliche Dokumentrevisionen unverändert aufbewahren.

**Vorgesehene lokale Ablage (noch nicht durchgeführt):** `C:\FAS-Agententeam_Plattform\00_governance\architecture_decisions\FAS-ADR-STANDORT-2026-10-17-001.md`.

**Hinweis:** Die Entscheidung selbst ist durch den Nutzer bestätigt; die Erstellung der lokalen Datei und die Freigabe ihres konkreten Wortlauts sind separate Vorgänge.
