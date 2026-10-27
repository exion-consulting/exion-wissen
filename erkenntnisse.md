# Erkenntnisse und Stolpersteine

Kurz, datiert, neueste oben. Format: **Thema** – was passiert ist → was wir seitdem tun. (Projekt)
Wird über `/erkenntnisse` gepflegt. Ausführliches gehört in das passende Playbook.

## 2026-10

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
