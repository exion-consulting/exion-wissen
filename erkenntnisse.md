# Erkenntnisse und Stolpersteine

Kurz, datiert, neueste oben. Format: **Thema** – was passiert ist → was wir seitdem tun. (Projekt)
Wird über `/logbuch` gepflegt. Ausführliches gehört in das passende Playbook.

## 2026-10

- **Klick-Anleitungen für JJ: Reihenfolge-Fallen ausdrücklich nennen** – Server wurde ohne SSH-Schlüssel erstellt (Schlüssel-Eingabe war abgelehnt worden, weil ein abgekürzter Wert mit „…“ kopiert wurde) → musste gelöscht und neu angelegt werden. Seitdem: „Erst X, ohne X nicht weiter“ klar sagen; Werte zum Kopieren nie abkürzen, lieber per `Set-Clipboard` direkt in die Zwischenablage legen (bei `Get-Content | Set-Clipboard` kann ein unsichtbarer Zeilenumbruch mitrutschen → `.Trim()`). (justluxx-ERP, 29.10.)
- **PowerShell + `ssh "…\"…\"…"`** – verschachtelte Anführungszeichen kommen auf dem Server kaputt an („unexpected EOF“) → solche Befehle nicht als Einzeiler geben: erst `ssh benutzer@server`, dann den Befehl dort einfügen. (justluxx-ERP, 29.10.)
- **Einrichtungsskript „durchgelaufen“, aber Benutzer fehlte** – der erste Lauf war unbemerkt abgebrochen → Skript mit `2>&1 | tee /root/setup.log | tail -40` starten und auf die Schlusszeile („Fertig“) achten; danach gezielt prüfen (z. B. `id jj`). (justluxx-ERP, 29.10.)
- **Browser-Anmeldefenster (Basic Auth) merkt sich falsche Versuche** – Mailpit-Login klappte nicht, obwohl die Daten stimmten → im privaten Fenster (Strg+Umschalt+N) neu versuchen; Claude kann die Daten vorher per `Invoke-WebRequest` mit Authorization-Header prüfen. (justluxx-ERP, 29.10.)
- **Start-Beitrag ohne Reichweite** – 160 Kontakte, Profil lange ruhig → nur 5 erreichte Mitglieder; Vorgehen siehe `social-media-linkedin.md` → „Reichweite“. (exion-workspace, 29.10.)
- **Server-Skripte vom Windows-PC** – mit CRLF-Zeilenenden brechen `.sh`-Dateien auf dem Server ab → `.gitattributes` mit `*.sh`, `deploy/** text eol=lf` (wie schon für `*.sql`). (justluxx-ERP, 29.10.)
- **Probeläufe testen das Ausrollen nicht** – dem Update-Job fehlte `packages: read`, das private Programmpaket wäre am Server „denied“ gewesen; nur die Gesamtprüfung fand es → den Weg auf den echten Server immer gezielt gedanklich durchspielen lassen. (justluxx-ERP, 29.10.)
- **Frischer Ubuntu-Server: Paketinstallation gesperrt** – in den ersten Minuten hält das automatische Update die apt-Sperre → `apt-get -o DPkg::Lock::Timeout=600`. (justluxx-ERP, 29.10.)
- **Rücksprung muss auch beim Startfehler greifen** – `set -e` wirkt nicht in einer Funktion, die in `if` aufgerufen wird → jeden Schritt mit `|| return 1` absichern und den Rücksprung im Probelauf mit einer absichtlich kaputten Version testen. (justluxx-ERP, 29.10.)
- **Anleitungen von Hilfsagenten** – Backslashes in Windows-Pfaden gingen verloren, `sudo` fehlte bei root-Ordnern → jeden Befehl einer Anleitung gegen die echten Skripte prüfen lassen, bevor der Kunde/JJ ihn nutzt. (justluxx-ERP, 29.10.)
- **Arbeitsordner ohne Sicherung** – der exion-workspace (Schulungen, Folien-Generator, Social-Media-Redaktion) lag nur lokal → jeden Arbeitsordner sofort als privates GitHub-Repo anlegen (JJ legt Repo im Browser an, Claude richtet `.gitignore` ohne `node_modules`/`.env` ein und lädt hoch). (exion-workspace, 28.10.)
- **LinkedIn einrichten** → eigenes Playbook `social-media-linkedin.md`; Recht → `datenschutz-recht.md` „Social-Media-Auftritt“. (exion-workspace, 28.10.)

- **Gesetzesänderung: auch fertige Office-Dateien prüfen** – nach der Neufassung von Art. 4 AI Act (Juli 2026) waren Skripte und Website schon aktuell, aber Leistungsmappe, Handzettel und Angebot (PPTX/DOCX) enthielten noch alten Wortlaut → Text in Office-Dateien durchsuchen mit `unzip -p datei.pptx | grep -c "Suchwort"`, danach neu erzeugen. Bei Rechtsthemen den Faktencheck ernst nehmen: der Prüf-Agent hatte die Änderung gefunden. (exion-workspace, 28.10.)
- **Skills und Agents bauen** → eigenes Playbook `ki-agents-skills.md`. (exion-workspace, 28.10.)

- **Seltsame Testabweichung nicht wegdefinieren** – ein Testwert wurde geändert, weil „das Auslesen spinnt“; die unabhängige Untersuchung fand einen echten Fehler in allen PDFs → bei unerklärlichen Abweichungen Ursache klären, Test nicht anpassen. (justluxx-ERP, 27.10.)
- **Steuer-Sonderfälle zeigen sich erst im E-Rechnungs-Prüfer** – Ware + „nicht steuerbar“ auf einer Rechnung, Anzahlung ins EU-Ausland → früh mit Steuerberater klären und Ersatzregel festlegen. (justluxx-ERP, 27.10.)
- **GitHub-CLI (`gh`)** – seit 28.10. installiert und angemeldet (`exion-consulting`, HTTPS); Claude kann damit Probeläufe (Actions) verfolgen. Pfad: `C:\Program Files\GitHub CLI\gh.exe`. (exion-wissen, 27.10./28.10.)
- **Keine globale Git-Identität** – erster Commit in neuen Repos brach ab → seit 27.10. global gesetzt (`Jadranko Jelavic`, `jj@exion.consulting`). (exion-wissen, 27.10.)
- **Umlaute in PowerShell 5.1** – ohne Kodierung werden Umlaute falsch gelesen/geschrieben („ü“ → „Ã¼“) → immer `-Encoding UTF8` beim Lesen, beim Schreiben UTF-8 (ohne BOM: `[IO.File]::WriteAllText(..., New-Object Text.UTF8Encoding $false)`). (alle Projekte, 27.10.)
- **Kontext-Dateien veralten** – offene Punkte standen noch drin, obwohl sie längst erledigt waren → am Ende jeder Sitzung `context/current-data.md` bzw. die offenen Punkte der Projekt-`CLAUDE.md` aktualisieren. (exion-workspace, 27.10.)
- **Rechtliche Aussagen in Vorträgen** – Aussagen zum AI Act vor dem Einsatz an der Quelle prüfen und die Quelle in die Sprechernotiz schreiben. (Vortrag 3, 27.10.)
