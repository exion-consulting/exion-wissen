# Erkenntnisse und Stolpersteine

Kurz, datiert, neueste oben. Format: **Thema** – was passiert ist → was wir seitdem tun. (Projekt)
Wird über `/logbuch` gepflegt. Ausführliches gehört in das passende Playbook.

## 2026-10

- **Gesetzesänderung: auch fertige Office-Dateien prüfen** – nach der Neufassung von Art. 4 AI Act (Juli 2026) waren Skripte und Website schon aktuell, aber Leistungsmappe, Handzettel und Angebot (PPTX/DOCX) enthielten noch alten Wortlaut → Text in Office-Dateien durchsuchen mit `unzip -p datei.pptx | grep -c "Suchwort"`, danach neu erzeugen. Bei Rechtsthemen den Faktencheck ernst nehmen: der Prüf-Agent hatte die Änderung gefunden. (exion-workspace, 28.10.)
- **Skills und Agents bauen** → eigenes Playbook `ki-agents-skills.md`. (exion-workspace, 28.10.)

- **Datum in der Oberfläche einen Tag verschoben** – `toISOString()` liefert Weltzeit (UTC), nachts stand der Vortag da → Datum immer mit `Intl.DateTimeFormat("de-DE", { timeZone: "Europe/Berlin" })` formatieren. (justluxx-ERP, 28.10.)
- **Windows-Zeilenenden verändern Datenbankdateien** – nach einem Wechsel des Arbeitszweigs schrieb Git (`core.autocrlf=true`) eine SQL-Migration mit Startdaten (E-Mail-Vorlagen) mit CRLF um → Vorlagen mit `\r` in der Datenbank, Test rot → in jedem neuen Projekt sofort `.gitattributes` mit `*.sql text eol=lf`. (justluxx-ERP, 28.10.)
- **Gesamtprüfung am Ende nie weglassen** → jetzt feste Regel in `software-projekte.md` (Qualität). (justluxx-ERP, 28.10.)
- **Seltsame Testabweichung nicht wegdefinieren** – ein Testwert wurde geändert, weil „das Auslesen spinnt“; die unabhängige Untersuchung fand einen echten Fehler in allen PDFs → bei unerklärlichen Abweichungen Ursache klären, Test nicht anpassen. (justluxx-ERP, 27.10.)
- **Steuer-Sonderfälle zeigen sich erst im E-Rechnungs-Prüfer** – Ware + „nicht steuerbar“ auf einer Rechnung, Anzahlung ins EU-Ausland → früh mit Steuerberater klären und Ersatzregel festlegen. (justluxx-ERP, 27.10.)
- **GitHub-CLI (`gh`) nicht installiert** – Claude kann Repos nicht selbst anlegen → JJ legt das Repo im Browser an (privat, leer, ohne README), Claude verbindet und lädt hoch. Optional `gh` installieren. (exion-wissen, 27.10.)
- **Keine globale Git-Identität** – erster Commit in neuen Repos brach ab → seit 27.10. global gesetzt (`Jadranko Jelavic`, `jj@exion.consulting`). (exion-wissen, 27.10.)
- **Umlaute in PowerShell 5.1** – ohne Kodierung werden Umlaute falsch gelesen/geschrieben („ü“ → „Ã¼“) → immer `-Encoding UTF8` beim Lesen, beim Schreiben UTF-8 (ohne BOM: `[IO.File]::WriteAllText(..., New-Object Text.UTF8Encoding $false)`). (alle Projekte, 27.10.)
- **Kontext-Dateien veralten** – offene Punkte standen noch drin, obwohl sie längst erledigt waren → am Ende jeder Sitzung `context/current-data.md` bzw. die offenen Punkte der Projekt-`CLAUDE.md` aktualisieren. (exion-workspace, 27.10.)
- **Rechtliche Aussagen in Vorträgen** – Aussagen zum AI Act vor dem Einsatz an der Quelle prüfen und die Quelle in die Sprechernotiz schreiben. (Vortrag 3, 27.10.)
- **PDF-Schrift verliert Zeichen nach Umlauten** – Fehler in fontkit → Schriften vor dem ersten PDF „aufwärmen“. (justluxx-ERP, 27.10.)
- **Next.js lädt Datenbank doppelt** – zwei Instanzen, veraltete Sitzungen → Verbindung auf `globalThis`. (justluxx-ERP, 27.10.)
- **Datenschutz-Generator mit Umsatzgrenze** – datenschutz-generator.de kostenlos nur bis 5.000 € Umsatz → e-recht24 (kostenlos, Quellenangabe Pflicht). (exion-website, 24.10.)
- **rclone liest `RCLONE_...`-Variablen als Optionen** → Variablen anders benennen. (exion-website, 22.10.)
- **`apt-get` auf GitHub Actions hängt** → Werkzeuge als feste Version mit Prüfsumme herunterladen. (exion-website, 22.10.)
- **Hetzner Webhosting S hat kein SSH** – rsync scheitert → SFTP mit rclone. Server-Fingerabdruck mit beiden Schlüsseltypen hinterlegen. (exion-website, 22.10.)
- **Gmail: Mail an eigenen Alias** landet nur unter „Gesendet“ → an die Hauptadresse schicken. (exion-website, 22.10.)
- **n8n-Testabo 14 Tage** – danach fällt das Formular still aus → Tarif rechtzeitig wählen, Ablaufdatum notieren. (exion-website, 22.10.)
