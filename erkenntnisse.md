# Erkenntnisse und Stolpersteine

Kurz, datiert, neueste oben. Format: **Thema** – was passiert ist → was wir seitdem tun. (Projekt)
Wird über `/logbuch` gepflegt. Ausführliches gehört in das passende Playbook.
Eingangskorb, keine Dauerablage: Bewährtes wandert ins Playbook. Zuletzt aufgeräumt am 09.11.2026 (alle Einträge verteilt auf `arbeitsumgebung.md`, `software-projekte.md`, `ki-agents-skills.md`, `datenschutz-recht.md`, `trading-backtest.md`).

## 2026-11

- **Dokumente erzeugen: Datenblätter als PDF + Word aus einer Datendatei** – Alle Inhalte stehen in einer Datei (`data.mjs`), daraus entstehen das PDF (HTML → Edge, siehe `arbeitsumgebung.md`) und die bearbeitbare Word-Datei (npm `docx@9.0.2`, Tabellen ohne Rahmen als Layout). So bleiben beide Fassungen gleich. Logo, Farben und Schriftgrößen aus einem Referenz-PDF holen mit npm `mupdf@1.0.0` (Bilder extrahieren, Schriften auflisten, Seite als PNG rendern). Zur Kontrolle jede Seite als Bild ausgeben und ansehen, nicht nur die Seitenzahl prüfen. (justluxx-Datenblätter, 17.11. – Beispiel: `justluxx\Datenblätter\_build\`)
- **Dokumente erzeugen: Herstellerunterlagen widersprechen sich oft** – Datenblatt, Werbebilder und Katalog nannten verschiedene Werte (Effizienz, LED-Marke, Dimmung, Spannung) → Abweichungen auflisten und JJ zeigen, das speziellste Dokument bevorzugen, unbelegte Werbeaussagen (z. B. „50 % Stromersparnis“) weglassen, Quellen im Projektordner ablegen. Fehlende Werte stehen oft in Messekatalogen (Aussteller-Downloads, z. B. Messe Frankfurt). (justluxx-Datenblätter, 17.11.)
- **Fremdprodukt unter eigener Marke (White-Label)** – Wer ein Produkt unter eigenem Namen in der EU verkauft, gilt meist selbst als Hersteller → eigene CE-Konformitätserklärung nötig, Prüfzeichen (CE, RoHS …) nur mit Nachweis aufs Datenblatt. Herstellernamen/-logos weglassen, nur Produktfotos ohne sichtbares Logo verwenden, Nutzungsrechte an Herstellerfotos schriftlich klären. Keine Rechtsberatung – im Zweifel Fachanwalt/Produktsicherheits-Berater. (justluxx-Datenblätter, 17.11.)
