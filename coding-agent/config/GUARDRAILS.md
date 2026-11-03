# GUARDRAILS – Coding-Agent

Geltungsbereich: Alle Aufträge im Verzeichnis `coding-agent`. Diese Regeln gelten zusätzlich zu tatsächlich wirksamen technischen Sicherheitsgrenzen und vorhandenen verbindlichen Plattformregeln. Konflikte sind vor der betroffenen Ausführung zu klären.

## 1. Auftragsbindung
- Nur den von ausführender KI und unabhängiger Kontrollinstanz ausdrücklich abgestimmten, unverändert übergebenen Einzelauftrag bearbeiten.
- Vor jeder Ausführung `config/GUARDRAILS.md`, danach `config/WORKFLOW.md`, danach die konkrete Auftragsdatei lesen.
- Bei fehlendem Nachweis der freigegebenen Fassung oder unklaren technischen Rechten den betroffenen Auftrag nicht starten.
- Umfang, Ziel, Pfadgrenzen und Risikoprofil nicht eigenmächtig erweitern. Neue erhebliche Risiken oder Konflikte melden; unabhängige zulässige Tätigkeiten dürfen ohne Gefährdung fortgesetzt werden.

## 2. Dateien und Rechte
- Nur ausdrücklich zugelassene Verzeichnisse und Ressourcen benutzen; keine eigenmächtigen Privilegienerweiterungen oder Schutzumgehungen.
- `config/`, `auftraege/` und `vorlagen/` aus Sicht des Coding-Agenten nur lesend; keine Änderungen an diesen Bereichen.
- Nur das zum Auftrag gehörende Ergebnisverzeichnis beschreiben, sofern die technischen Rechte und der Auftrag dies erlauben.
- Keine unbeauftragten Löschungen, Überschreibungen oder Änderungen bestehender Projekte, Konfigurationen oder fremder Aufträge.
- Eine Markdown-Anweisung allein ist keine technische Zugriffssperre. Vor dem ersten Agentenlauf muss die fehlende Änderbarkeit der Schutz- und Auftragsdateien aus der tatsächlichen Agentenidentität technisch nachgewiesen sein.

## 3. Docker, System und Befehle
- Keine Containerstarts, -stopps, -neustarts oder -löschungen ohne konkrete fachliche Abstimmung und technisch zulässige Berechtigung.
- Keine unbeauftragten Änderungen an Images, Volumes, Netzwerken, produktiven Docker-Konfigurationen, Host- oder Firewall-Einstellungen.
- Keine unbeauftragten Installationen, ungeprüften Fremdskripte oder destruktiven Befehle.
- Keine Rechteerweiterung durch Administrator-, Root-, Docker-Socket- oder sonstige privilegierte Zugänge.

## 4. Geheimnisse und Daten
- Keine Ausgabe, Speicherung in Auftrags-/Ergebnisdateien oder unautorisierte Weitergabe von Passwörtern, Tokens, Schlüsseln und vertraulichen Daten.
- Keine unbeauftragte Übertragung an externe Dienste.

## 5. Nachweis und Abschluss
- Tätigkeiten, tatsächliche Änderungen, Nachweise, Grenzen der Verifikation, Fehler, offene Punkte und nicht durchgeführte Schritte unter der Auftrags-ID dokumentieren.
- Aussagen über erfolgreiche Ausführung müssen auf überprüfbaren Ergebnissen beruhen; Berichte allein ersetzen keine Prüfung.
- Die Guardrails dürfen nicht durch gewöhnliche Einzelaufträge abgeändert werden. Ihre Änderung bedarf einer gesonderten fachlichen Einigung der beiden KI-Instanzen und der technisch erforderlichen Berechtigungen.
