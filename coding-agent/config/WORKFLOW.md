# WORKFLOW – Coding-Agent

## Vorbereitung und Freigabe
1. Die ausführende KI erstellt einen eindeutig abgegrenzten Auftrag mit ID, Ziel, Pfaden, Aufgaben, Grenzen, Ergebnissen und überprüfbaren Abschlusskriterien.
2. Die Kontrollinstanz prüft unabhängig. Nur die ausdrückliche Zustimmung **beider** KI-Instanzen zur **gleichen konkreten Fassung** gilt als fachliche Freigabe; Schweigen ist keine Zustimmung. Die Zustimmung muss im Kommunikationsverlauf eindeutig der Auftrags-ID und Fassung zuordenbar sein. Keine zusätzliche Freigabedatei.
3. Nach fachlicher Einigung wird eine unveränderte Fassung bereitgestellt. Vor dem Agentenstart müssen ein überprüfter Integritäts-/Übergabemechanismus und die technischen Sperren gegen Änderungen an Regeln und Aufträgen bestehen. Ein Hash allein ist weder Freigabe noch Schutz vor nachträglicher Manipulation.

## Technische Vorbedingungen vor dem ersten Auftrag
- Tatsächlichen Zugriffspfad, Agentenidentität, Berechtigungen und die ggf. verwendete Synchronisation auf dem Entwicklungs-PC lesen und prüfen.
- Durchsetzbare Lese-/Schreibgrenzen sicherstellen: Regeln, freigegebene Aufträge und Vorlagen für den Agenten unveränderbar; Ergebnisse nur in zulässigen Bereichen schreibbar.
- Einen geeigneten, technisch überprüften Mechanismus gegen unbeabsichtigte gleichzeitige Ausführung **derselben** Auftrags-ID einsetzen (z. B. atomare exklusive Sperre im zentralen Ausführungsmechanismus). Alle ausführenden Instanzen müssen ihn beachten.
- Der Mechanismus darf nach Abbruch oder Teilbearbeitung keine ungeprüfte Wiederholung auslösen. Vor Fortsetzung bisherigen Zustand untersuchen.
- Diese technischen Maßnahmen gehören zum später gesondert abzustimmenden **Abschnitt 2**. Die Zustimmung zu Abschnitt 1 autorisiert keine Rechteänderungen, Docker-Eingriffe, Synchronisation oder Agentenausführung.

## Ausführung
4. Der Coding-Agent liest vor der Bearbeitung in dieser Reihenfolge: `config/GUARDRAILS.md`, `config/WORKFLOW.md`, konkrete Auftragsdatei. Er prüft Regeln, Freigabe und reale Berechtigungen; bei Konflikt nur betroffene Tätigkeiten stoppen.
5. Er führt ausschließlich die freigegebenen Tätigkeiten aus und dokumentiert Abweichungen.
6. Er legt Ergebnisse ausschließlich im zur ID gehörenden Ergebnisverzeichnis ab.
7. Sein Abschlussbericht benennt ID, durchgeführte Schritte, Dateien/Artefakte, Nachweise, nicht ausgeführte Schritte, Risiken, Fehler, offene Fragen und Empfehlungen.
8. Die ausführende KI kontrolliert die Ergebnisse anhand der Abschlusskriterien und unabhängiger Nachweise. Vor einem erneuten Lauf wird geprüft, ob und was bereits erledigt wurde.
9. Neue Aufträge bedürfen wieder ausdrücklicher fachlicher Einigung beider KI-Instanzen. Nicht strittige, bereits genehmigte Arbeiten können fortgesetzt werden, soweit keine Abhängigkeiten/Risiken entgegenstehen.
