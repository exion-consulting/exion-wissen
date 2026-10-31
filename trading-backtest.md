# Playbook: Trading-Strategien testen (Backtest)

Stand: 01.11.2026 · Quelle: Projekt `Trading Platform`, Etappe 1 (Bericht und Entscheidungen in `docs/technik/`). Keine Anlageberatung.

## Vorgehen

- **Kriterien vor dem Ergebnis committen:** Regeln, Parameter, Zeiträume, Kosten und Bestehens-Grenzen festschreiben, bevor Kursdaten vorliegen. Ein zweiter Versuch gilt als neue, gekennzeichnete Strategie; nachträgliches Drehen an Werten macht den Test wertlos. Beispiel: `docs/technik/bestehens-kriterien.md`.
- **Limits vorab durchrechnen:** Risiko je Trade, Gesamtgrenze und üblicher Stop-Abstand ergeben zusammen die mögliche Investitionsquote. Beispiel: 1 % Gesamtrisiko bei rund 17 % Stop-Abstand erlaubt nur rund 6 % investiertes Kapital. Das vor dem Bau rechnen, nicht erst im Ergebnis sehen.
- **Laufkosten gegen Kapital rechnen:** 50 € im Monat sind bei 10.000 € schon 6 % im Jahr. Plattform-, Daten- und KI-Kosten gehören in die Erfolgsrechnung.

## Rechnen und Vergleichen

- **Endabgleich als Pflichttest:** Startkapital + Summe der Trades − Kosten = Endwert, auch mit offenen Positionen am Ende. Sonst fehlen die Verkaufskosten und der Endwert fällt zu gut aus.
- **Vergleich von derselben Basis starten:** Der Benchmark beginnt beim Kapital, nicht beim ersten Schlusskurs. Sonst fehlen Einstiegskosten und die Bewegung der ersten Kerze.
- **Ertrag zu Rückgang kehrt sich bei Verlusten um:** Ein negatives Verhältnis wird durch einen größeren Rückgang „besser“, eine Verlust-Strategie kann so bestehen. Immer zusätzlich eine Mindestrendite prüfen, zum Beispiel über Tagesgeld.
- **„0 Ablehnungen“ heißt nicht „Regel wirkte nicht“:** Limits kappen Positionen oft still. Kappungen getrennt zählen, bevor man über die Wirkung einer Regel urteilt.

## Grenzen im Bericht nennen

Heutige Coin-Liste (Survivorship Bias), Stops zum Stop-Kurs sind im Kurssturz zu günstig, ein Zeitraum ist keine Garantie. Bereits gesehene Daten sind kein unberührter Test mehr; die echte Prüfung ist danach ein Paper-Lauf ab heute.
