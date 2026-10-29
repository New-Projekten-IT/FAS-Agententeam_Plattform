# FAS-Agententeam-Plattform – Projektstatus

Stand: 29.10.2026 · Entwicklungs-PC · Abschluss der heutigen Arbeitssitzung

&#x20;VS-Code-Vorbereitung erfolgreich

## 1. Gesamtstatus

Die praktische Einrichtung des lokalen VS-Code-Analysearbeitswegs ist deutlich vorangekommen. Der separate Workspace ist eingerichtet, Codex funktioniert mit einem lokalen Ollama-Modell und ein konkreter Schreibschutztest wurde erfolgreich durchgeführt.

Die FAS-Plattform befindet sich weiterhin in Phase 2 – Einzelagent (nicht abgenommen).

| Projektbereich                              | Aktueller Status                                                                                        |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| Drei FAS-Grundlagendokumente vom 29.10.2026 | Fachliche Grundlage; autorisierte Übernahme in die geschützten Originalbereiche noch nicht nachgewiesen |
| V2-Transferpaket                            | 11 Dateien vorhanden und in Analyse-Workspace kopiert                                                   |
| VS-Code-Analyse-Workspace                   | Eingerichtet und erfolgreich geöffnet                                                                   |
| Lokale Modellversorgung                     | Ollama und LM Studio verfügbar                                                                          |
| Codex mit GPT-OSS 20B                       | Erfolgreiche lokale Modellinferenz                                                                      |
| Codex mit Qwen3.8-27B                       | Modellanfrage wegen Chat-Template-Fehler fehlgeschlagen                                                 |
| Codex-Schreibschutz                         | Konkrete Schreibversuche technisch blockiert                                                            |
| MCP-/Werkzeugisolation                      | Noch nicht vollständig geklärt                                                                          |
| `FAS-P2-GATEWAY-001`                        | Technische Untersuchung durch Analyseagenten steht noch aus                                             |
| Docker-Agent-Tool-Calling                   | Weiterhin nicht freigegeben oder durchgeführt                                                           |

## 2. Wesentliche Ergebnisse vom 29.10.2026

### VS Code und Transferpaket

- VS Code `1.143.1` vorhanden.
- Codex CLI `0.162.1` vorhanden.
- Cline `4.1.26` installiert, bisher nicht erneut getestet.
- Continue nicht installiert.
- V2-Transferpaket unter `D:\FAS-Agententeam_Plattform\Prompts\FAS Phase 2 – Transferordner VS Code-Dateien\v2` vorhanden.
- Alle elf Dateien nach `C:\FAS-VSCode-Analyse` kopiert.
- Dateianzahl und relative Pfade stimmen überein.
- Workspace in VS Code erfolgreich geöffnet.

### Lokale Modelle

Ollama: Nemotron 3.5 Lightning 30B, GLM 4.7 Flash, GPT-OSS 20B 32K und GPT-OSS 20B.

LM Studio: Qwen3.8-27B, Nemotron 3.5 Super VL 120B A12B sowie Nomic Embedding.

Qwen wurde erfolgreich geladen und die LM-Studio-API auf Port 1234 gestartet. Die Codex-Anfrage scheiterte jedoch mit `HTTP 500` und `Jinja Exception: System message must be at the beginning`.

Dagegen lieferte Codex mit `gpt-oss-20b-32k:latest` über Ollama erfolgreich:

`FAS_CODEX_MODELL_OK`

Der Test endete mit `CODEX_EXITCODE=0`.

### Sicherheitsprüfungen

Der Testagent verwendete:

- `sandbox: read-only`
- `approval: never`
- `--ignore-user-config`
- `--ephemeral`
- das separate `CODEX_HOME` unter `C:\FAS-Codex-TestHome`

Beim konkreten Schreibschutztest wurde eine angeforderte Berechtigungserweiterung zurückgewiesen. Auch der anschließende Shell-Schreibversuch wurde mit `blocked by policy` verhindert.

Die Testdatei `C:\FAS-VSCode-Analyse\FAS_SANDBOX_SCHREIBTEST.txt` enthielt anschließend unverändert:

`ORIGINAL_UNVERAENDERT`

Nachweisgrenze: Die technisch wirksame Blockierung dieser konkreten Schreibversuche ist dokumentiert. Eine vollständige Dateisystem-, MCP-, Netzwerk- oder Agentenisolation ist damit nicht nachgewiesen.

## 3. Offene Arbeiten

1. Effektiv verfügbare MCP- und sonstige Codex-Agentenwerkzeuge in der getrennten Testumgebung feststellen.
2. Zulässige lesende Dateizugriffe und deren technische Begrenzung gezielt überprüfen.
3. Den Analyseagenten mit den V2-Unterlagen auf `FAS-P2-GATEWAY-001` ansetzen.
4. Einen konkreten Lösungsweg für die Docker-Agent-Gateway-/Tool-Isolation erarbeiten.
5. Erst nach wirksamen technischen Schutzgrenzen den späteren Docker-Agent-Werkzeugtest vorbereiten.

Die bisherigen abgeschlossenen Prüfungen werden nicht ohne neuen sachlichen Anlass wiederholt.

## 4. Startpunkt für die nächste Sitzung

Nächster Arbeitsschritt – Schritt 20

Die tatsächliche MCP- und Werkzeugverfügbarkeit des getrennten Codex-Analyseagenten gezielt feststellen.

Dabei beibehalten:

- Workspace: `C:\FAS-VSCode-Analyse`
- Codex-Testumgebung: `C:\FAS-Codex-TestHome`
- Modell: `gpt-oss-20b-32k:latest` über Ollama
- Sicherheitsparameter: `read-only`, `approval: never`
- Keine Änderungen an geschützten FAS-Bereichen

PowerShell-Prüfungen möglichst sinnvoll bündeln. Zustandsändernde Schritte einzeln durchführen und anhand der Nutzer-Ausgabe kontrollieren.

## 5. Dokumentations- und Übergabestatus

Die technischen Kurzberichte zu den Schritten 12–16b und 17b–19b wurden in der Unterhaltung erstellt.

Dieser Projektstatus ist eine operative Momentaufnahme und keine Änderung der normativen FAS-Dokumente. Er wurde noch nicht in die lokale `PROJECT_STATUS.md` übernommen und nicht durch einen neuen Git-Commit versioniert. Die heute auf dem Alltags-PC bereits erfolgte Statusversionierung bleibt davon unberührt.

Abschlussbewertung: Der heutige Fortschritt ist technisch nachvollziehbar. Die lokale Codex-Modellkommunikation funktioniert, der separate Analyse-Workspace ist einsatzbereit und ein konkreter Shell-Schreibzugriff wurde nachweislich blockiert. Die eigentliche Gateway-Analyse ist der nächste Schwerpunkt.

Damit haben wir einen klaren Wiederaufnahmepunkt für die nächste Sitzung.