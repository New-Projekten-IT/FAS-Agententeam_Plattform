# Auftrag: Lesende Untersuchung des vorhandenen Docker-Agenten

**Auftrags-ID:** auftrag-001  
**Erstellt am:** 2026-11-03  
**Ausführungsstand:** Nur vorbereitet; die Erstellung ist keine Ausführungsfreigabe.

## Ziel
Den Ist-Zustand des vorhandenen Docker-Agenten anhand einer ausschließlich lesenden Untersuchung nachvollziehbar erfassen und priorisierte, abgegrenzte Folgeaufträge empfehlen.

## Arbeitsbereich
- Zu untersuchender Docker-Agent: **genauer Pfad und tatsächlich erreichbare Komponenten auf dem Entwicklungs-PC vor Freigabe ergänzen**.
- Ergebnisverzeichnis: `coding-agent/ergebnisse/auftrag-001/` (nur bei später technisch nachgewiesenem Schreibrecht).
- Kein Zugriff auf andere Projekte oder produktive Bereiche außerhalb einer konkret freigegebenen Liste.

## Aufgaben
1. Projektstruktur und relevante Dateien dokumentieren.
2. Architektur und wesentliche Komponenten beschreiben.
3. Docker-Integration und bestehende Konfigurationen lesend untersuchen.
4. Vorhandene und unvollständige Funktionen identifizieren.
5. Start- und Betriebsmechanismen anhand vorhandener Dateien beschreiben; nicht starten.
6. Technische Probleme und Sicherheitsrisiken bestimmen.
7. Vorhandene Dokumentation und Tests sichten; keine Tests mit Seiteneffekten ausführen.
8. Abhängigkeiten und Entwicklungsbedarf erfassen.
9. Kleine, priorisierte Folgeaufträge mit Ziel, Komponenten und Abschlusskriterien vorschlagen.

## Einschränkungen
- Ausschließlich lesend im untersuchten Zielsystem: keine Quellcode-, Docker-, Container-, Netzwerk-, Konfigurations- oder Berechtigungsänderungen.
- Keine Starts, Neustarts, Softwareinstallationen, automatischen Reparaturen oder Schreibtests.
- Keine Werkzeuge mit nicht ausgeschlossenen Schreibnebenwirkungen; nur nachweislich nicht verändernde Verfahren bzw. ausdrücklich zugelassene technische Isolation.
- Keine Einsicht oder Ausgabe von Secrets, soweit für die Untersuchung nicht erforderlich; keine externe Übertragung.
- Noch nicht bekannte Zielpfade und verfügbare Lesezugänge müssen vor fachlicher Auftragsfreigabe konkretisiert werden.

## Ergebnisse
Strukturierter Bericht: Ist-Zustand, Architektur, Funktionen, Probleme, Risiken/Unsicherheiten, priorisierte Empfehlungen, kleine Folgeaufträge sowie Fakten vs. Annahmen vs. ungeprüfte Eigenschaften.

## Ergebnisverzeichnis
`coding-agent/ergebnisse/auftrag-001/`

## Abschlusskriterien
- Alle neun Untersuchungsbereiche sind im Bericht behandelt oder mit präzisem Grund als nicht verifizierbar gekennzeichnet.
- Wesentliche Befunde nennen nachvollziehbare Datei-/Konfigurationsbezüge oder andere nicht verändernde Nachweise.
- Keine unbeauftragten Änderungen am Zielsystem.
- Risiken und Empfehlungen sind priorisiert; Folgeaufträge nennen Ziel, betroffene Komponenten und objektiv überprüfbare Kriterien.
- Die ausführende KI prüft Bericht und verfügbare Nachweise gesondert.

**Ausführungssperre:** Dieser Entwurf darf erst nach Ergänzung des exakten Arbeitsbereichs, Zustimmung beider KI-Instanzen zu genau dieser Fassung und Erfüllung der technischen Voraussetzungen aus Abschnitt 2 ausgeführt werden.
