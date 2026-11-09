# Playbook: Arbeitsumgebung (JJs PC, Werkzeuge, Anleitungen für JJ)

Stand: 09.11.2026 · Entstanden beim Aufräumen von `erkenntnisse.md` (Einträge 27.10.–06.11.2026 aus justluxx-ERP, exion-workspace, exion-wissen).
Gilt für alle Projekte auf JJs Windows-11-PC (PowerShell 5.1 + Git Bash).

## Werkzeuge auf dem PC

- **Python:** `python` startet nur den Microsoft-Store-Hinweis. Seit 31.10. ist `uv` per winget installiert und bringt Python je Projekt mit (`uv run …`). In alten Terminals ist es nicht im PATH; Pfad: `%LOCALAPPDATA%\Microsoft\WinGet\Packages\astral-sh.uv_*\uv.exe`. Ohne Projekt keine Python-Einzeiler einplanen. Am 09.11. trotzdem passiert: `python` scheiterte, der folgende `git commit` lief aber und sicherte einen halben Stand → für Textersetzungen ein kleines Node-Skript nehmen (`node` ist installiert). (29.10./31.10./09.11.)
- **Befehlsketten:** Folgeschritte (z. B. Commit, Push) immer mit `&&` an den Erfolg des vorigen Schritts koppeln, nie per Zeilenumbruch oder `;`. (09.11.)
- **GitHub-CLI (`gh`):** seit 28.10. installiert und angemeldet (`exion-consulting`, HTTPS). Damit lassen sich Probeläufe (Actions) verfolgen. Pfad: `C:\Program Files\GitHub CLI\gh.exe`. (exion-wissen, 27.10./28.10.)
- **Git-Identität** ist seit 27.10. global gesetzt (`Jadranko Jelavic`, `jj@exion.consulting`); vorher brach der erste Commit in neuen Repos ab. (exion-wissen, 27.10.)
- **Umlaute in PowerShell 5.1:** Ohne Kodierung werden Umlaute falsch gelesen oder geschrieben („ü“ → „Ã¼“) → immer `-Encoding UTF8` beim Lesen, beim Schreiben UTF-8 ohne BOM: `[IO.File]::WriteAllText(..., New-Object Text.UTF8Encoding $false)`. (alle Projekte, 27.10.)
- **Port bleibt nach Server-Ende belegt:** Ein übrig gebliebener node-Prozess hielt Port 3100, Browser-Tests starteten nicht → `Get-NetTCPConnection -LocalPort 3100` (PowerShell) und nur diesen Prozess beenden. (justluxx-ERP, 30.10.)
- **PowerShell + `ssh "…\"…\"…"`:** Verschachtelte Anführungszeichen kommen auf dem Server kaputt an („unexpected EOF“) → solche Befehle nicht als Einzeiler: erst `ssh benutzer@server`, dann den Befehl dort einfügen. (justluxx-ERP, 29.10.)
- **API-Guthaben im Max-Abo:** Das Max-Abo enthält 100 $ API-Guthaben pro Monat, einmal über den Link in der Meldung in Claude Code aktivieren. Nutzen für Demos, Tests und Schulungsbeispiele (z. B. n8n mit Claude), nicht für den Echtbetrieb bei Kunden (dort eigenes API-Konto je Kunde oder klare Weiterberechnung). Bedingungen (Verfall, erlaubte Nutzung) vor dem Einlösen prüfen; keine personenbezogenen Daten ohne AVV mit Anthropic, für Demos nur Testdaten. (exion-workspace, 03.11.)

## Sitzungen, Sicherung, GitHub

- **Sitzung immer im Projektordner starten.** Claude Code lief einmal aus `C:\Users\SIWAIT`; Verlauf und Projektgedächtnis landeten unter `.claude\projects\C--Users-SIWAIT\`, die nächste Sitzung im Projekt fand nichts. Bei Verdacht in `.claude\projects\*` nach Änderungsdatum suchen und das Gedächtnis in den Projekt-Ordner kopieren. (justluxx-ERP, 30.10.)
- **Jeden Arbeitsordner sofort als privates GitHub-Repo anlegen.** Der exion-workspace lag anfangs nur lokal. JJ legt das Repo im Browser an, Claude richtet `.gitignore` (ohne `node_modules`/`.env`) ein und lädt hoch. (exion-workspace, 28.10.)
- **Push scheitert mit „fatal error in commit_refs_rules“:** Störung bei GitHub, nicht im Repo → Push im Hintergrund minütlich wiederholen (bis 10 Versuche), danach mit `git fetch` prüfen, dass `origin/main` stimmt. (justluxx-ERP, 06.11.)
- **Kontext-Dateien aktuell halten:** Offene Punkte standen noch drin, obwohl sie längst erledigt waren → am Ende jeder Sitzung `context/current-data.md` bzw. die offenen Punkte der Projekt-`CLAUDE.md` aktualisieren. (exion-workspace, 27.10.)
- **Fertige Hilfsagenten beenden:** Ein Umsetzer hatte noch Hintergrundarbeit (Testlauf, Überwachung) und meldete sein Ergebnis in Schleife → fertige Agenten gezielt beenden (TaskStop) und im Auftrag verlangen: „keine Hintergrundprozesse zurücklassen“. (justluxx-ERP, 05.11.)

## Anleitungen für JJ (Befehle, Klickwege)

- **Jeder Befehl in einem eigenen Kopierblock,** dazu sagen, woran man den Erfolg erkennt. Bei `sudo bash -c '…'` ging beim Kopieren der Anfang verloren, der Server meldete „No such file or directory“. (justluxx-ERP, 01.11.)
- **Reihenfolge-Fallen ausdrücklich nennen:** „Erst X, ohne X nicht weiter.“ Ein Server wurde ohne SSH-Schlüssel erstellt, weil ein abgekürzter Wert mit „…“ kopiert wurde, und musste neu angelegt werden. Werte zum Kopieren nie abkürzen, lieber per `Set-Clipboard` in die Zwischenablage legen (bei `Get-Content | Set-Clipboard` kann ein unsichtbarer Zeilenumbruch mitrutschen → `.Trim()`). (justluxx-ERP, 29.10.)
- **Anleitungen von Hilfsagenten gegen die echten Skripte prüfen,** bevor JJ oder ein Kunde sie nutzt: Backslashes in Windows-Pfaden gingen verloren, `sudo` fehlte bei root-Ordnern. (justluxx-ERP, 29.10.)
- **Browser-Anmeldefenster (Basic Auth) merkt sich falsche Versuche:** Login klappte nicht, obwohl die Daten stimmten → im privaten Fenster (Strg+Umschalt+N) neu versuchen; Claude kann die Daten vorher per `Invoke-WebRequest` mit Authorization-Header prüfen. (justluxx-ERP, 29.10.)
