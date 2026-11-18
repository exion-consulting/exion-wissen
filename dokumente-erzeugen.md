# Playbook: Dokumente aus Daten erzeugen (Datenblätter, PDF, Word)

Stand: 18.11.2026 · Quelle: `justluxx\Datenblätter` (Design v2, 2-seitige Produktdatenblätter als PDF; altes Design PDF + Word). Vollständiges Beispiel: `_build\build-html-v2.mjs`, `_build\build-pdf-v2.ps1`, Regeln `docs\design-regeln.md`.

## Grundprinzip

- **Eine Datendatei je Dokument** (`data.mjs`), daraus HTML → PDF per Edge ohne Fenster (Befehl: `arbeitsumgebung.md`). Word bei Bedarf mit npm `docx@9.0.2` aus denselben Daten. So bleiben alle Fassungen gleich. (17.11.)
- **Vorlage statt Einzelstück:** Bausteine optional und zählbar halten (z. B. 2–6 Varianten, 3–5 Kennzahlen, 3–6 Vorteile, Diagrammtypen „SVG aus Daten“ oder „fertiges Bild“). Die Vorlage **mit einem Extremfall testen** – bei justluxx ein altes Datenblatt mit 6 Varianten, Hochformatbild und anderem Diagramm. Erst das zeigte nicht umbrechende Maße und Überläufe. (18.11.)
- **Edles Datenblatt (bewährt, GPT-Sparring 9/10):** Seite 1 verkauft (Produkt groß auf heller Fläche, 3–5 Kennzahlen, Vorteile mit Nutzen, Anwendungsbild), Seite 2 informiert (Tabelle mit einer Spalte je Variante, gemeinsame Werte über alle Spalten, Diagramme). Feine Linien statt grauer Balken, eine Schrift, Markenfarbe nur als Akzent. Mindestgrößen: Tabelle ~8,4 pt, Nebentexte und Rechtstext 7,5 pt. (18.11.)

## Qualität automatisch absichern

- **Überlauf erkennen:** Bei festen A4-Seiten mit `overflow: hidden` bleibt die Seitenzahl korrekt, obwohl Inhalt abgeschnitten ist → ein kleines Skript in der HTML-Seite misst nach `document.fonts.ready` `scrollHeight > clientHeight` und schreibt „UEBERLAUF Seite N (+x mm)“ sichtbar ins PDF. Edge braucht dafür `--virtual-time-budget=5000`, sonst druckt es vor dem Skript. Das Build-Skript liest den PDF-Text mit npm `mupdf` und warnt. (18.11.)
- **Kennzahlen gegen die Tabelle prüfen:** Jede hervorgehobene Zahl ist an ihre Tabellenzeile gebunden (`row`). Gilt sie nur für eine Variante, muss diese angegeben sein (`scope`), sonst bricht der Build ab. Das verhindert falsche Verallgemeinerungen wie „2,8 µmol/J“ für alle Varianten. Mit absichtlich falschen Daten gegentesten. (18.11.)
- **Entwürfe kennzeichnen:** Feld `draft: true` → rotes „ENTWURF“ in der Fußzeile + Warnung beim Erzeugen; ohne Feld verschwindet es automatisch. (18.11.)
- **Jede Seite als PNG rendern und ansehen** (npm `mupdf@1.0.0`), nicht nur die Seitenzahl prüfen. Schriften im PDF prüfen: Namen mit Präfix wie `AAAAAA+Inter-Regular` = als Teilsatz eingebettet. (17./18.11.)

## Satz und Schrift

- **Schrift lokal einbinden:** npm `@fontsource/inter@5.1.0` (feste Version), woff2-Dateien in `assets\fonts\` kopieren, `@font-face` mit `font-display: block`. Keine Google-Fonts-Abrufe (Datenschutz, Offline-Build).
- **Inter: `font-feature-settings: "tnum"` nicht global setzen** – damit standen Bindestriche mit Lücken da („Grow - Light“). Gleich breite Ziffern nur für Kennzahlen (`font-variant-numeric: tabular-nums`). (18.11.)
- **Einheiten automatisch setzen:** Leerzeichen zwischen Zahl und Einheit per Regex (`54.000h` → `54.000 h`), „x“ zwischen Zahlen als `×<wbr>` (zweimal ersetzen, weil sich die Treffer überlappen) – sonst brechen lange Maße wie „586x473x165mm“ in schmalen Spalten nicht um. (18.11.)
- **Feste Abstände statt Verteilen:** `justify-content: space-between` ergab bei wenig Inhalt große Lücken → feste Abstände (z. B. 6,5 mm), den Restplatz bekommt das Hauptbild (`flex: 1`, Bild absolut mit `object-fit: contain`). (18.11.)
- **„k.A.“ wirkt unfertig:** einzelne fehlende Werte → „auf Anfrage“, Zeilen ganz ohne Wert ausblenden, offene Werte als Rückfragenliste führen. (18.11.)

## Inhalt und Recht

- **Herstellerunterlagen widersprechen sich oft:** Datenblatt, Werbebilder und Katalog nannten verschiedene Werte → Abweichungen auflisten und JJ zeigen, das speziellste Dokument bevorzugen, unbelegte Werbeaussagen weglassen, Quellen im Projektordner ablegen. Fehlende Werte stehen oft in Messekatalogen. (17.11.)
- **Fremdprodukt unter eigener Marke (White-Label):** Wer in der EU unter eigenem Namen verkauft, gilt meist selbst als Hersteller → eigene CE-Konformitätserklärung, Prüfzeichen nur mit Nachweis. Herstellernamen/-logos weglassen, Nutzungsrechte an Fotos schriftlich klären. Keine Rechtsberatung. (17.11.)
- **Fachbegriffe Leuchten:** Schutzart (IP) ≠ Stoßfestigkeit (IK) ≠ elektrische Schutzklasse – getrennte Zeilen. IP65 = staubdicht + strahlwassergeschützt, nicht „wasserdicht“. Superlative ohne Beleg („exzellent“, „minimale Leistungsaufnahme“) durch die Eigenschaft ersetzen. Daten genau lesen: „20/40/60/80/100 %“ ist stufig, nicht „stufenlos“ dimmbar (Fehler fiel erst im Sparring auf). (18.11.)

## Bilder

- **Vorgaben je Bildplatz** festlegen (Seitenverhältnis, Hintergrund, Mindestpixel – z. B. Produkt freigestellt ≥ 2.000 px, Anwendung 5:3). Produktbild immer einpassen (nie beschneiden), Anwendungsbild zuschneiden, Diagramm-Bilder nie verzerren und in der Höhe begrenzen. Lieferantenbilder sind oft nur 750 px breit – reicht für den Bildschirm, für den Druck größere anfragen. (18.11.)
- **Bilder mit KI aufbereiten** (freistellen, vergrößern, Logo entfernen) ist sinnvoll, aber **das Produkt darf sich nicht verändern** (KI erfindet LEDs, Halterungen, Formen dazu → irreführende Werbung). Jedes Bild mit dem Original vergleichen (Prüfliste), echt wirkende Anwendungsszenen als „Symbolbild“ kennzeichnen (siehe `datenschutz-recht.md`). Fertiger KI-Auftrag + Prüfliste: `justluxx\Datenblätter\docs\design-regeln.md`. (18.11.)
