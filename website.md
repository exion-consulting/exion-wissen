# Playbook: Websites

Stand: 28.10.2026 · Quelle: `exion-website` (www.exion.consulting) – dort liegt der vollständige, funktionierende Code zum Abschauen.

## Standard-Technik

| Baustein | Wahl | Warum |
|---|---|---|
| Generator | **Astro** (statisch), einfaches CSS mit Variablen, wenig Vanilla-JS | schnell, sicher, gut für Google, kein CMS zu warten |
| Hosting | **Hetzner Webhosting** (Deutschland) | DSGVO, AVV in konsoleH, günstig |
| Deployment | GitHub Action bei Push auf `main` → Build → Upload per **SFTP mit rclone** | Webhosting S hat kein SSH, daher kein rsync |
| Formulare | statisches HTML-Formular → **n8n-Webhook** → Mail (siehe `n8n-automatisierung.md`) | kein eigener Server nötig |
| Schriften | lokal (`@fontsource/...` oder woff2 in `public/fonts/`) | **nie** von Google-Servern laden – Abmahnrisiko |
| Bilder | Astro `<Image>`, WebP/AVIF, feste Maße | Ladezeit, Lighthouse |

## Ablauf eines Website-Projekts

1. Entwurf der Startseite als einzelne HTML-Datei abstimmen (`referenz/entwurf-startseite.html`), dann in Astro-Komponenten zerlegen.
2. Projekt-`CLAUDE.md` anlegen: Quellen, Technik, Seitenliste, Markenstil, Pflichtregeln, offene Punkte (Checkliste „von Kunde zu liefern“).
3. Seiten aufbauen, Texte aus dem Kontext des Kunden ableiten; Fehlendes als `[PLATZHALTER]` – nichts erfinden (keine Zahlen, Kundenstimmen, Referenzen).
4. Impressum und Datenschutz (siehe `datenschutz-recht.md`).
5. Hosting, Domain, SSL, Deployment einrichten.
6. Qualität prüfen: mobil zuerst, Tastatur, Kontrast, Lighthouse > 90 in allen Kategorien.

**Bei jeder Textänderung (auch klein):**
- Vor dem Veröffentlichen ansehen: `npm run build`, `npx astro preview --port 4321` im Hintergrund, dann Bildschirmfoto ohne Fenster mit Edge: `msedge.exe --headless=new --hide-scrollbars --window-size=1280,1400 --screenshot="<pfad>.png" http://localhost:4321/<seite>` (für Handy-Ansicht `--window-size=390,1400`). Erst nach OK des Kunden committen und pushen.
- Nach dem Push prüfen, ob es live ist: Seite mit Zufallsparameter abrufen (`curl -sL "https://<domain>/<seite>?v=$RANDOM" | grep -q "<neuer Satz>"`), im Hintergrund alle 10 s, max. ~7 min. Bei exion.consulting war die Änderung nach ca. 30 s live. (`gh` ist nicht installiert, daher kein Blick auf den Action-Lauf.)

## Deployment-Details (Hetzner + GitHub Actions)

- Eigener Deploy-Schlüssel je Projekt; öffentlicher Teil in konsoleH → Logindaten → Öffentliche SFTP-Schlüssel, privater Teil als GitHub-Secret.
- Secrets: `HETZNER_HOST`, `HETZNER_USER`, `HETZNER_PORT`, `HETZNER_SSH_KEY`.
- rclone **als feste Version mit Prüfsumme herunterladen**, nicht per `apt-get` (hängt auf GitHub oft minutenlang).
- Umgebungsvariablen **nicht** `RCLONE_...` nennen – rclone liest sie sonst als eigene Optionen.
- Server-Fingerabdruck fest hinterlegen, **beide** Schlüsseltypen (ed25519 und rsa), sonst „key mismatch“.
- `rclone sync dist/ ...` mit `--exclude '.well-known/**'` (sonst wird die SSL-Prüfung gelöscht) und `--sftp-shell-type none`.
- `concurrency: deploy`, damit nie zwei Uploads gleichzeitig laufen.
- Vorlage: `exion-website/.github/workflows/deploy.yml`.

## Server-Regeln (`public/.htaccess`, Apache)

Vorlage: `exion-website/public/.htaccess` – enthält:
- immer HTTPS + immer `www` (eine Adresse für Google), Ausnahme `/.well-known/`
- saubere Adressen ohne `.html`, Weiterleitung alter Adressen, eigene 404-Seite
- Sicherheits-Header (HSTS, nosniff, Frame-Options, Referrer-, Permissions-Policy)
- Caching: HTML `no-cache`, `/_astro/` ein Jahr `immutable`, Bilder ein Monat
- PDFs zum Download mit `X-Robots-Tag: noindex`

## Domain und DNS

- **Nur** A/CNAME für Domain und `www` ändern. **MX, SPF, DKIM, DMARC nie anfassen** – sonst fallen die E-Mails aus.
- Vor jeder DNS-Änderung erklären, was passiert, und Bestätigung abwarten.
- SSL im Hosting-Panel aktivieren; Ablaufdatum notieren.
- **checkdomain – Unteradresse auf eigenen Server zeigen lassen** (z. B. `test-erp.domain.de` auf Hetzner): Domains › Domain › „checkdomain Nameserver“ › ganz unten **„Profi-Einstellungen“** › leere Zeile: Hostname, TTL 300, Typ A, Wert = Server-IP › Speichern. **Nicht** „Subdomains“ (zeigt aufs checkdomain-Webhosting) und **nicht** die „Haupt-IP-Adresse“ ändern (sonst ist die Website weg). Ein eigener Eintrag hat Vorrang vor dem Platzhalter `*.domain.de`. Prüfen: `Resolve-DnsName name -Server 1.1.1.1` – war bei checkdomain sofort sichtbar. (justluxx-ERP, 29.10.2026)

## SEO und Barrierearmut (Mindeststandard)

- Seitentitel, Meta-Beschreibung (max. ~155 Zeichen), Open-Graph-Bild, `sitemap.xml`, `robots.txt`
- echte Buttons und Links, Alt-Texte, ausreichender Kontrast, per Tastatur bedienbar, Animationen bei `prefers-reduced-motion` abschalten
- Danke-Seiten und reine Hilfsseiten auf `noindex`

## Formulare – Bauprinzip

- Funktioniert **auch ohne JavaScript** (normales `POST`, n8n leitet auf eine Danke-Seite weiter); mit JavaScript per `fetch` und `?js=1`, Meldung direkt im Formular.
- Spam-Falle: unsichtbares Feld `website` (Honeypot) statt Captcha – kein externer Dienst nötig.
- Bei Fehlern immer die E-Mail-Adresse als Ausweg anzeigen.
- Vorlage: `exion-website/src/components/ContactForm.astro`, `DownloadForm.astro`.

## Angebot an Kunden

„Websites, die mitarbeiten“: Website plus Automatisierung (Formular → Mail/CRM, Download per Mail, Terminbuchung). Eigene Website als Referenz zeigen. Wartung/Hosting-Betreuung als laufende Leistung anbieten.
