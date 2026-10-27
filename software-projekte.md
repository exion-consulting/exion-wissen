# Playbook: Softwareprojekte (Webanwendungen, interne Tools, ERP)

Stand: 27.10.2026 · Quelle: `justluxx-ERP` (Next.js, ~Etappe 1b). Vollständige Beispiele für Spezifikation, Plan, Entscheidungen und Handbuch liegen dort unter `docs/`.

## Vorgehen

1. **Gesamtkonzept** (Spezifikation) mit dem Kunden abstimmen und freigeben lassen: Ziele, Module, Rollen/Rechte, Etappen, Schnittstellen, Datenschutz/GoBD.
2. In **Etappen** liefern: Etappe 0 = Fundament (Anmeldung, Rechte, Stammdaten, Import/Export, API), dann fachliche Etappen. Jede Etappe: eigene Spezifikation → eigener Plan (Aufgaben, Tests) → Umsetzung → Handbuch.
3. Während der Umsetzung **Entscheidungsprotokoll** führen (`docs/technik/entscheidungen-etappe-X.md`): Tabelle „Entscheidung | Grund | Falls falsch“ plus „Vor dem Echtbetrieb erledigen“ und „Kleinigkeiten“. Das ist Gold für die spätere Wartung.
4. Zwei Dokumentarten: **Handbuch für Mitarbeitende** (ohne Fachjargon) und **Betrieb und Entwicklung** (für EXION).
5. Klare Ablage: `docs/superpowers/specs/` (Spezifikationen), `docs/superpowers/plans/` (Pläne), `docs/handbuch/`, `docs/technik/`, `docs/api/`.

## Bewährte Architektur-Regeln

- **Fachlogik nur in Services** (`src/modules/<modul>/service.ts`). Seiten, API, Import rufen nur Services auf → überall dieselben Regeln.
- **Rechte immer serverseitig prüfen** (`assertCan`); Ausblenden in der Oberfläche ist nie der einzige Schutz. Bei geschützten Feldern prüfen, dass sie über **keinen Nebenweg** durchsickern (Suche, Export, API, Historie).
- **Änderungsprotokoll nur anhängbar** (Datenbankregel gegen Ändern/Löschen) – GoBD. Stammdaten nie löschen, nur archivieren.
- Datenbankänderungen **nur über Migrationen**; bestehende Migrationen nie nachträglich ändern.
- Excel-Import: Vorschau und Import über dieselben Services in **einer Transaktion** (alles oder nichts); Grenzen für Zeilen und Dateigröße.
- Dezimalzahlen eindeutig (nur Komma), Geschäftsdatum immer `Europe/Berlin`.

## Sicherheit (Standard für Anwendungen mit Login)

Passwort ≥ 12 Zeichen (Argon2id), Zwei-Faktor (TOTP) Pflicht, Sperre nach 5 Fehlversuchen, Sitzungsende nach Inaktivität, Tokens nur als Hash speichern, Geheimnisse verschlüsselt (Schlüssel in `.env` – **Schlüsselverlust = 2FA unbrauchbar**, sicher aufbewahren). Admin-Wiederherstellung (Passwort/2FA zurücksetzen) von Anfang an einplanen. Vier-Augen-Prinzip bei Rechten.

## Technik-Stolpersteine (Next.js / Node)

- **Next.js ändert sich schnell:** vor dem Coden die mitgelieferte Doku in `node_modules/next/dist/docs/` lesen (steht in `AGENTS.md`).
- **Datenbankverbindung auf `globalThis`** halten – sonst lädt Next.js mehrere Instanzen (veraltete Sitzungen).
- **PGlite** nur für Entwicklung/Tests; nur ein Prozess pro Datei (App und Worker gleichzeitig → PostgreSQL nötig).
- **PDF mit `@react-pdf/renderer`:** statische TTF-Schriften verwenden (nicht die variable Google-Schrift); Schriften vor dem ersten PDF „aufwärmen“ (Fehler in fontkit lässt nach Umlauten Zeichen verschwinden); kein `lineHeight` auf Seitenebene (sonst fehlt „Seite x von y“); Logos nur PNG/JPEG.
- **E-Rechnung (XRechnung/ZUGFeRD):** CII-XML direkt aus den fertig gerechneten Daten erzeugen (keine zweite Rechenlogik), mit `pdf-lib` ins PDF einbetten, vor der Freigabe mit dem KoSIT-Prüfer validieren (nur `error` blockiert, Warnungen gelten als bestanden). Steuerfälle früh mit dem Steuerberater klären. Was der Prüfer konkret verlangt hat:
  - XRechnung: Geschäftsprozess (BT-23) und E-Mail des Käufers (BT-49) sind Pflicht.
  - Ohne USt-ID des Verkäufers braucht es die Handelsregisternummer (BR-CO-26).
  - „Nicht steuerbar“ (O) darf nicht mit anderen Steuerfällen auf einer Rechnung stehen → Ersatzregel festlegen (z. B. normales PDF für Auslandskunden).
  - EU-Lieferung (K) braucht ein Lieferdatum, auch bei Anzahlungen und deren Gutschriften (BR-IC-11).
  - Positionsname nie leer (BR-25).
- **ZUGFeRD-PDF (PDF/A-3):** echtes sRGB-Profil (`registry.color.org/rgb-registry/profiles/sRGB2014.icc`), XMP mit Factur-X-Erweiterungsschema, Info-Dictionary passend zum XMP, `PDFDocument.load(..., { updateMetadata: false })` – sonst überschreibt pdf-lib Producer/Datum. Zeichen, die die Schrift nicht hat (Emojis), vor dem Rendern ersetzen (sonst `.notdef` → PDF/A ungültig). CMYK-JPEG-Logos ablehnen (RGB-OutputIntent). Prüfdienst (KoSIT + veraPDF) als eigener Docker-Dienst, Zeitlimit + Größenlimit für Antworten. Beispiel: `justluxx-ERP/src/modules/sales/einvoice/`.
- `LIKE`-Suchen: Platzhalterzeichen (`%`, `_`) im Suchtext maskieren.
- `npm audit`: nur „high/critical“ zwingend beheben; bewusst akzeptierte Meldungen im Betriebsdokument begründen.

## E-Mail aus der Anwendung (nodemailer)

- Mail **einmal** bauen (`MailComposer`), Zeilenenden auf CRLF vereinheitlichen, **genau diese Bytes** senden und als `.eml` archivieren – sonst weicht das Archiv vom Gesendeten ab (SMTP ergänzt CRLF). Archivieren erst nach Annahme durch den Server; scheitert das Archiv, Mail in einen Notfall-Ordner schreiben.
- nodemailer wirft **nur, wenn alle** Empfänger abgelehnt werden → `info.rejected` selbst auswerten und anzeigen („Nicht zugestellt an …“).
- STARTTLS erzwingen (`requireTLS: true`), Zertifikatsprüfung nie abschalten; Steuerzeichen (CR/LF) in Absendername, Host, Benutzer ablehnen.
- Postfach-Passwort verschlüsselt speichern, nie an die Oberfläche/ins Protokoll; rohe Fehlertexte des Mailservers nie weitergeben (können den Anmeldedialog enthalten).
- Fehlerarten unterscheiden: nicht erreichbar (503), Anmeldung (409), Empfänger (422).
- Tests gegen einen lokalen Test-SMTP (`smtp-server`), nie gegen ein echtes Postfach. Beispiel: `justluxx-ERP/src/modules/mail/`, `src/modules/sales/email.ts`.

## Qualität

- `npm run check` (Typen + Lint + Tests) muss vor jedem Commit grün sein; Browser-Tests (Playwright) mit eigener Test-Datenbank.
- **Test-Datenbank einmal aufbauen und kopieren:** Führt jede Test-DB alle Migrationen neu aus, laufen die Tests bei vielen Kernen in Zeitüberschreitungen. PGlite: einmal migrieren, `dumpDataDir()`, je Test `PGlite.create({ loadDataDir })` (ca. 6× schneller). Timeouts nicht einfach hochsetzen.
- Testgetrieben arbeiten: erst Test, dann Code – besonders bei Rechnen, Rechten, Steuern.

## Betrieb (vor dem Echtbetrieb)

- Server (z. B. Hetzner Cloud), Docker, PostgreSQL, HTTPS, Worker als eigener Dienst mit Neustart.
- **Externe Datensicherung** (nicht nur auf demselben Server) für Datenbank **und** Dateiablage/Archiv, in einem anderen Rechenzentrum, verschlüsselt; der Server darf Sicherungen nur hinzufügen, nicht löschen (Schutz bei Hack/Erpressung); Wiederherstellung einmal je Quartal testen.
- **Revisionssicheres Archiv (GoBD):** Archivdateien per Datenbankregel gegen Ändern/Löschen sperren, Prüfwert (SHA-256) speichern, „Aufbewahren bis“ (Jahresende + 10 Jahre) mitführen, Funktion „Archiv prüfen“ anbieten.
- **Heruntergeladene Werkzeuge** (Java, Prüfprogramme): in `*.part` laden, Prüfsumme prüfen, dann umbenennen; beim Start erneut prüfen.
- Alarm per E-Mail bei Auffälligkeiten (Sperren, Fehlversuche, Fehler).
- Sicherheits-Header/CSP, Migrationen nur gezielt ausführen.
