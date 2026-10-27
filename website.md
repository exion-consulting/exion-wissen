# Playbook: Websites

Stand: 27.10.2026 · Quelle: `exion-website` (www.exion.consulting) – dort liegt der vollständige, funktionierende Code zum Abschauen.

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
