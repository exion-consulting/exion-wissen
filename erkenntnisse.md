# Erkenntnisse und Stolpersteine

Kurz, datiert, neueste oben. Format: **Thema** – was passiert ist → was wir seitdem tun. (Projekt)
Wird über `/logbuch` gepflegt. Ausführliches gehört in das passende Playbook.

## 2026-10

- **Gesetzesänderung: auch fertige Office-Dateien prüfen** – nach der Neufassung von Art. 4 AI Act (Juli 2026) waren Skripte und Website schon aktuell, aber Leistungsmappe, Handzettel und Angebot (PPTX/DOCX) enthielten noch alten Wortlaut → Text in Office-Dateien durchsuchen mit `unzip -p datei.pptx | grep -c "Suchwort"`, danach neu erzeugen. Bei Rechtsthemen den Faktencheck ernst nehmen: der Prüf-Agent hatte die Änderung gefunden. (exion-workspace, 28.10.)
- **Skills und Agents bauen** → eigenes Playbook `ki-agents-skills.md`. (exion-workspace, 28.10.)

- **Seltsame Testabweichung nicht wegdefinieren** – ein Testwert wurde geändert, weil „das Auslesen spinnt“; die unabhängige Untersuchung fand einen echten Fehler in allen PDFs → bei unerklärlichen Abweichungen Ursache klären, Test nicht anpassen. (justluxx-ERP, 27.10.)
- **Steuer-Sonderfälle zeigen sich erst im E-Rechnungs-Prüfer** – Ware + „nicht steuerbar“ auf einer Rechnung, Anzahlung ins EU-Ausland → früh mit Steuerberater klären und Ersatzregel festlegen. (justluxx-ERP, 27.10.)
- **GitHub-CLI (`gh`) nicht installiert** – Claude kann Repos nicht selbst anlegen → JJ legt das Repo im Browser an (privat, leer, ohne README), Claude verbindet und lädt hoch. Optional `gh` installieren. (exion-wissen, 27.10.)
- **Keine globale Git-Identität** – erster Commit in neuen Repos brach ab → seit 27.10. global gesetzt (`Jadranko Jelavic`, `jj@exion.consulting`). (exion-wissen, 27.10.)
- **Umlaute in PowerShell 5.1** – ohne Kodierung werden Umlaute falsch gelesen/geschrieben („ü“ → „Ã¼“) → immer `-Encoding UTF8` beim Lesen, beim Schreiben UTF-8 (ohne BOM: `[IO.File]::WriteAllText(..., New-Object Text.UTF8Encoding $false)`). (alle Projekte, 27.10.)
- **Kontext-Dateien veralten** – offene Punkte standen noch drin, obwohl sie längst erledigt waren → am Ende jeder Sitzung `context/current-data.md` bzw. die offenen Punkte der Projekt-`CLAUDE.md` aktualisieren. (exion-workspace, 27.10.)
- **Rechtliche Aussagen in Vorträgen** – Aussagen zum AI Act vor dem Einsatz an der Quelle prüfen und die Quelle in die Sprechernotiz schreiben. (Vortrag 3, 27.10.)
