# FAS-Agententeam-Plattform – Projektstatus

**Dokumentstatus:** Nicht normative, konsolidierte **Prüffassung** vom 22.10.2026. Noch keine unabhängige Abschlussprüfung dieser Fassung und keine menschliche Freigabe zur Übernahme oder Git-Versionierung. Keine allgemeine Betriebs-, Schreib- oder Agentenausführungsfreigabe.

**Berichtsstand:** 22.10.2026. Historische Prüfungen behalten ihren jeweiligen Zeitpunkt und ihre Nachweisgrenzen. **Aktuelle Projektphase:** 2 – Einzelagent (noch nicht abgenommen).

**Plattform-Root:** `C:\FAS-Agententeam_Plattform\` (Standortentscheidung des Nutzers vom 17.10.2026). Die drei normativen Quellen bleiben allein für KI-Verhalten, Zielarchitektur und Umsetzungsreihenfolge zuständig; dieser Statusbericht ersetzt keine von ihnen.

## 1. Gesicherte historische Grundlagen

| Gegenstand | Dokumentierter Befund und Nachweisgrenze |
|---|---|
| Standort und Struktur | C: als dauerhafter Plattform-Root entschieden; historisch 15 Haupt- und 68 Unterverzeichnisse dokumentiert. Ordnerexistenz ist kein ACL- oder Funktionsnachweis. Die separate mobile Arbeitskopie auf D: ist nicht der aktive Root. |
| Bestandsinventar | `03_operations\inventory\FAS-Bestandsaufnahme.txt` ist eine historische Strukturauflistung (17.10.2026), kein Sicherheitsgutachten. |
| Dokumentenübernahme | Archivierung dreier historischer Planungsdokumente und Übernahme bereinigter Dokumente laut früheren Nachweisen; Prüfentscheidung 037 vom 19.10.2026. Frühere SHA-256-Prüfungen sind keine aktuelle Gesamtabnahme. |
| Git-Baseline | Auftrag `FAS-AUS-062`, Abschlussbericht 067 und Prüfentscheidung 068: Root-Commit `91f62c0a57487eb4e1c6d8e5e034e67825360454`, Branch `main`, 16 Dateien (15 Dokumentationsdateien und `.gitignore`). Die historische SHA-256-Zuordnung aller älteren Fassungen ist nicht vollständig unabhängig belegt. |
| LM Studio | Frühere Nutzerprüfungen 008–010: `qwen3.8-27b` und `text-embedding-nomic-embed-text-v1.5` lokal gespeichert; damals kein laufender API-Server und kein geladenes Modell. Sekundär überlieferter Prüfblock 015 (20.10.2026): Server gestoppt, Qwen laut `lms ps` `GENERATING`, Kontext 32.768, Parallelität 4. Originalkonsolenbeleg zu 015 liegt hier nicht vor; aktueller stabiler Zustand ungeklärt. |
| Historischer Testauftrag | `FAS-P2-LMSTUDIO-001`, Revision 02, nicht als vollständig abgenommen belegt. Kontrollentscheidung 006 `NICHT BEURTEILBAR` ist aus späterer Kontrollüberlieferung berichtet; vollständige Originalunterlagen liegen hier nicht vor. |
| Sicherheits-/Betriebsabnahme | Unabhängige Rollenprüfung, manipulationsgeschütztes Audit, Systembackup und tatsächlicher Restore sind nicht vollständig nachgewiesen. FAS-Originalbereiche und FAS-GIT-001 bleiben geschützt. |

## 2. Technische Nutzer-Nachweise vom 22.10.2026

Die folgenden Befunde stammen aus in der Unterhaltung übermittelten PowerShell-Ausgaben. Sie sind **durch Nutzer-Konsolenausgaben dokumentiert**, nicht von einer unabhängigen Kontrollinstanz auf dem Host reproduziert oder als Gesamtfunktion abgenommen.

### 2.1 Ollama und Nemotron auf dem Windows-Host

- Ollama erreichbar unter `http://127.0.0.1:11434/api/tags`; die Modelle `nemotron-3.5-lightning:30b`, `glm-4.7-flash:latest`, `gpt-oss-20b-32k:latest` und `gpt-oss:20b` wurden aufgelistet.
- Nemotron: Modellkennung `nemotron-3.5-lightning:30b`, Digest beginnt mit `e7a64ff15fb1`, GGUF, Architektur `nemotron_h_moe`, 32,9B Parameter, `Q4_K_M`; native Ollama-API nennt Fähigkeiten `completion`, `tools`, `thinking`. Diese Angaben allein sind kein Tool-Calling-Nachweis.
- Erster direkter Inferenztest: `done=True`, 64 Tokens, leeres `response`-Feld, Gesamtdauer 50,54 s (Ladezeit 32,70 s). Ursache der Leerausgabe nicht abschließend nachgewiesen.
- Zweiter direkter Inferenztest: Antwort **`TEST_OK`**, `done_reason=stop`, `thinking` 552 Zeichen, 155 generierte Tokens, 8,12 s. Damit ist eine funktionierende **direkte lokale Ollama-Inferenz** dokumentiert, jedoch keine Agenteninferenz.
- Ressourcenprüfung bei geladenem Nemotron: `ollama ps` meldete `21%/79% CPU/GPU`, geladene Größe 26 GB, Kontext 4096, Runner `llamacpp`. Der Prozentwert bezeichnet die gemeldete Modellverteilung, nicht momentane Prozessorlast. Weitere Leistungs- und Stabilitätsprüfungen stehen aus.

### 2.2 Bestehende Docker-Sandbox und Docker-Agent-CLI

- Sandbox `fas-docker-agent-test` durch `sbx exec` erfolgreich gestartet; Agenten-CLI gibt **`docker-agent version v1.142.0`**, Commit `99bdcf84c832570ebc4b37c29f58dde077dd4dcd` aus. CLI-Hilfe für `run`, einschließlich `--model`, `--dry-run`, `--exec` und `--safety`, wurde ausgegeben; noch kein erfolgreicher Docker-Agent-Modellaufruf.
- `sbx inspect fas-docker-agent-test --json`: Agent `docker-agent`, Image `docker/sandbox-templates:docker-agent-docker`, Digest `sha256:763d685f341fc19cab53f942652ec1028b2ea07bd9861f3dbfded1515531d472`, 2 CPUs, 4 GB RAM, Netzwerk `fas-docker-agent-test`, globale Netzwerkpolicy, Proxy `172.17.0.2:3128`, `runtime_mounts: []`, 0 Sessions beim Inspektionszeitpunkt, `mcp_gateway: true`, registrierter Secret-Name `mcpgateway`, Daemon v0.48.0. Zustand `stopped` gilt nur für diesen Inspektionszeitpunkt.
- `sbx policy ls ... --wide` zeigte allgemein geltende `filesystem:read`- und `filesystem:write`-Standardregeln für `**`. Ein leeres `runtime_mounts`-Array allein beweist nicht, dass alle sonstigen Host-/Workspace-Zugriffe unmöglich sind.
- `docker-agent models --provider ollama --format table` meldete `No models available`; vorher wurde ein fehlgeschlagener GitHub-Self-Update-Check mit HTTP 403 ausgegeben. Das ist **kein** erfolgreicher Provider- oder Modellfunktionstest und erfordert nach aktuellem Nachweis keine zusätzliche Modellinstallation.

### 2.3 Netzwerkregel und tatsächliche Sandbox-HTTP-Verbindung

- Vor der Änderung: `sbx policy check network --sandbox fas-docker-agent-test` verweigerte `host.docker.internal:11434`, `localhost:11434`, `api.openai.com:443` und `api.anthropic.com:443` (jeweils `default deny`).
- **Richtlinienänderung (Nutzer-Konsolenausgabe):** Der Nutzer führte `sbx policy allow network --sandbox fas-docker-agent-test --protocol tcp localhost:11434` aus. Die Ausgabe bestätigte Regel-ID `8775d165-c40a-467c-a178-343f4e5471ff` mit Scope `sandbox:fas-docker-agent-test`, Protokoll TCP und Ziel `localhost:11434`. Damit ist die Einrichtung dieser Regel dokumentiert; ihre Bedeutung für einen anderen Zielnamen ist daraus allein nicht ableitbar.
- Danach lieferte die Policy-Abfrage `Allowed` für `localhost:11434` und weiterhin `Denied` für `api.openai.com:443` und `api.anthropic.com:443`. Die beiden Cloudziel-Prüfungen allein beweisen keine allgemeine Cloud-Fallback-Sperre.
- **Gesonderter HTTP-Befund (Nutzer-Konsolenausgabe):** Die aus `fas-docker-agent-test` abgesetzten Befehle `curl http://host.docker.internal:11434/api/tags` und `curl http://host.docker.internal:11434/v1/models` lieferten Modelllisten einschließlich Nemotron. Der erfolgreiche Zugriff auf `host.docker.internal:11434` ist damit dokumentiert. **Eine kausale Zuordnung dieses Erfolgs zur Freigaberegel für `localhost:11434` wurde nicht gesondert nachgewiesen.** Die HTTP-Abfragen waren **keine Modellinferenz durch Docker Agent**.
- Es ist noch ungeklärt, welche weiteren Provider-/MCP-/Host-Kommunikationswege effektiv verfügbar sind und ob Cloud-Fallback bei der künftigen Agentenausführung zuverlässig technisch unterbunden ist.

## 3. Git- und Dokumentationsstand am 22.10.2026

- Nutzerseitig nachgewiesener **neuer Commit** auf `main`: `2243a618866a10d8f54d0f1c6c44194f76091ab8`, Nachricht `docs: consolidate FAS document index and Git baseline references`. Ausgabe von `git diff-tree` nennt als **einzige Commit-Datei** `DOCUMENT_INDEX.md`; 66 Einfügungen und 14 Löschungen.
- Die bereinigte Indexfassung erhielt nach gezielter Statuskorrektur laut Nutzer-PowerShell den SHA-256-Hash `7E54AFFB25220F68D9D273EAF95316C745FDD0398C19043B7C401A211F819C28`. Dieser Hash ist ein Nutzer-Messwert vor dem genannten Commit, keine Behauptung erneuter Hashverifikation am jetzigen Zeitpunkt.
- Eine frühere, andere Indexfassung und die Sicherung `DOCUMENT_INDEX_vor_Bereinigung_20261022_224706_1112160.md` wiesen zum damaligen Prüfzeitpunkt übereinstimmend den Hash `1184D08F890AC743B3A2E3E20E24055112A9416DDBC795766A5C6875DB048824` auf. Dies beweist die Gleichheit jener beiden Dateien, **nicht** automatisch Identität mit einer externen Sollfassung oder eine Sicherung des Zustands vor Bereinigung. Ein damaliger Kopierversuch aus `Downloads` scheiterte.
- Weitere Sicherung der Fassung vor der letzten Statuskorrektur: `C:\Users\Administrator\Documents\FAS_Backups\DOCUMENT_INDEX_vor_Statuskorrektur_20261022_230035_6321044.md` (Erstellung laut PowerShell-Ausgabe; Sicherungsinhalt hier nicht unabhängig gelesen).
- Die **letzte übermittelte Git-Statusausgabe nach dem Commit** zeigte ausschließlich ` M PROJECT_STATUS.md`. Diese Datei wurde ausdrücklich nicht in den Index-Commit aufgenommen. Ein Git-Commit der vorliegenden Projektstatus-Prüffassung ist **nicht** erfolgt.
- Der technische Übergabebericht vom 22.10.2026 wurde vom Nutzer unter dem temporären Bereich `Prompts` gesichert (genaue aktuelle Benennung siehe lokale Datei). `git check-ignore -v -- Prompts/` zeigte `.gitignore:7:*`; der Bereich ist damit bei diesem Test vom Root-Repository ignoriert. Die Übergabe ist ein nicht normativer Beleg, kein weiterer führender Projektstatus.

## 4. Abgrenzung und offene Abnahmekriterien

**Bereits belegt:** Direkte lokale Ollama-Modellinferenz; Sandbox-CLI-Aufrufbarkeit; gezielte Ollama-Portfreigabe; erfolgreiche HTTP-Erreichbarkeit der nativen und OpenAI-kompatiblen Ollama-Modelllisten aus der Sandbox; nachvollziehbarer separater Git-Commit des Dokumentenindex.

**Nicht nachgewiesen bzw. nicht abgenommen:**

1. Ob die vorgeschlagene Docker-Agent-YAML für **v1.142.0** tatsächlich gültig ist; der bisher diskutierte Inhalt ist ein **ungetesteter Entwurf**, keine aktivierte Konfiguration.
2. Erfolgreiche Nemotron-Inferenz **durch Docker Agent** mit ausdrücklich festgelegtem lokalen Provider und wirksamer Cloud-Fallback-Sperre.
3. Für Toolaufrufe: technisch belegte Werkzeug-/Dateisystem-/Mount-/MCP-/Netzwerk-Isolation, Rechte, Stop-/Rollback-Möglichkeit und zulässige Testpfade; die Default-Dateisystemregeln sind allein nicht ausreichend.
4. Reproduzierbares Tool-Calling und ein begrenzter, genehmigter, erfolgreich dokumentierter Einzelagentenauftrag (Abnahmekriterien der Phase 2).
5. Spätere unabhängige Qualitätssicherung, Audit-/Backup-/Restore-Abnahme und dauerhafter Betrieb (nachgeordnet gemäß Phasen 3–6).

## 5. Unmittelbare Fortsetzung

1. Diese Projektstatus-Prüffassung fachlich kontrollieren; erst nach ausdrücklicher menschlicher Autorisierung in `PROJECT_STATUS.md` übernehmen. Sie ersetzt die vorhandene Arbeitsfassung nicht automatisch.
2. Nach erlaubter Übernahme: ausschließlich tatsächlichen Inhalt, Git-Diff/Staging und Nachweisreferenzen kontrollieren. Ein Git-Commit erfordert eine **eigene** ausdrückliche Autorisierung; keine starre Verpflichtung zu zwei Commits.
3. Technisch in Phase 2 weiterarbeiten: Den minimalen **werkzeuglosen** Docker-Agent-Konfigurationsentwurf für den bestehenden Ollama-Endpunkt zunächst auf Eignung für v1.142.0 und auf mögliche Nebenwirkungen der vorgesehenen Prüfbefehle untersuchen. Ein `--dry-run` ist **lediglich ein geplanter, noch nicht ausgeführter Prüfschritt**; sein tatsächliches Verhalten und seine Nebenwirkungsfreiheit sind nicht nachgewiesen. Seine Ausführung sowie anschließende Modellinferenz erfolgen erst im konkret geklärten und menschlich autorisierten Umfang. Vor ausführenden Agenten-Toolaufrufen die in Abschnitt 4 genannten Schutzgrenzen wirksam nachweisen und autorisieren.
4. Keine unnötigen Wiederholungsinventuren, weiteren Modellinstallationen oder Eingriffe in FAS-Originale beziehungsweise FAS-GIT-001.

## 6. Nachweise / Fundstellen

- Normative Quellen: `00_governance\policies\01_FAS – Master-Prompt-Agententeam.md`; `01_architecture\02_FAS – Zielarchitektur und technische Schutzgrenzen.md`; `03_operations\runbooks\03_UMSETZUNGSPLAN.md`.
- Historische Belege: `03_operations\inventory\FAS-Bestandsaufnahme.txt`, `03_operations\inventory\FAS_Phase2_Technische_Ausgangslage.md`, Abschlussbericht 067, Prüfentscheidungen 037/068 und ältere Nutzer-PowerShell-Ausgaben (insbesondere Prüfungen 002–010). Angaben aus Prüfblock 015 ausdrücklich nur sekundär überliefert.
- Nutzer-PowerShell-Ausgaben in der Unterhaltung vom 22.10.2026: `ollama list`, `/api/tags`, `/api/generate`, `ollama ps`, `sbx exec`, `sbx inspect --json`, `sbx policy ls/check/allow`, `curl /api/tags`, `curl /v1/models`, `docker-agent version/run --help/models`, Git-Diffs, Hashwerte und abschließende Commit-/Statusausgabe.
- Technischer Übergabebericht vom 22.10.2026 im temporären `Prompts`-Bereich; nicht normativ. Bei Abweichungen gehen konkrete zeitlich zugeordnete Konsolennachweise und die jeweiligen normativen Quellen vor.

**Bearbeitungsvermerk:** Diese Fassung wurde außerhalb des Windows-Entwicklungs-PCs als redaktioneller Prüfvorschlag erstellt. Sie enthält keine behauptete erneute Hostmessung, keine neue technische Abnahme und keine Schreib- oder Commit-Freigabe.
