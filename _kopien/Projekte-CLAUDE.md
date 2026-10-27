# Projekte – gemeinsame Regeln für alle Projekte von EXION

Diese Datei wird in **jedem** Unterordner von `Projekte\` automatisch geladen. Sie gilt zusätzlich zur `CLAUDE.md` des jeweiligen Projekts (die Projektdatei hat bei Widersprüchen Vorrang).

## Ordner

- `exion-workspace\` – EXION selbst: Kontext (`context\`), Schulungen, Vorträge, Angebote, Folien-Generator
- `exion-website\` – www.exion.consulting (Astro, Hetzner, n8n-Formulare) – erste Referenz für Kundenwebsites
- `justluxx\justluxx-ERP\` – ERP für justluxx GmbH (Next.js, PostgreSQL) – Referenz für größere Softwareprojekte
- `_wissen\` – Wissensablage: bewährte Vorgehen aus allen Projekten (siehe unten)
- Neue Kunden: `Projekte\<kunde>\<projekt>\` – je Projekt eigene `CLAUDE.md`, eigenes Git-Repo

## Wissensablage `_wissen\` – bei Bedarf lesen

Nicht alles auf einmal lesen, nur die Datei zum Thema der Aufgabe:

| Datei | Lesen bei |
|---|---|
| `_wissen\website.md` | Website bauen, ändern, veröffentlichen, Domain/DNS, SEO |
| `_wissen\n8n-automatisierung.md` | Formulare, Workflows, E-Mail-Versand, Webhooks, Schnittstellen |
| `_wissen\software-projekte.md` | Webanwendungen, interne Tools, ERP – Planung, Aufbau, Tests, Betrieb |
| `_wissen\datenschutz-recht.md` | personenbezogene Daten, AVV, Formulare, Werbung, AI Act, Rechtstexte |
| `_wissen\erkenntnisse.md` | vor jedem neuen Projekt kurz überfliegen: Stolpersteine und Lösungen |

**Pflege:** Wenn in einem Projekt etwas Wiederverwendbares gelernt wird (Lösung, Stolperstein, bewährtes Vorgehen), am Ende der Etappe in die passende Datei eintragen – JJ kann dafür `/logbuch` aufrufen.

**Wichtig:** In `_wissen\` steht nur allgemeines Wissen – **nie Kundendaten**, Zugangsdaten, Preise oder Interna eines Kunden. Was nur für ein Projekt gilt, bleibt in dessen eigener `CLAUDE.md` bzw. `docs\`.

## Gemeinsame Regeln für Kundenprojekte

1. **Secrets** nur in `.env` (steht in `.gitignore`), dazu eine `.env.example` ohne echte Werte. Nie Zugangsdaten, Kundendaten oder Exporte committen.
2. **EU-Hosting und AVV:** Dienste mit Sitz/Region EU bevorzugen (Hetzner, n8n Cloud Frankfurt). Für jeden Dienst, der personenbezogene Daten verarbeitet, einen AVV abschließen und in der Datenschutzerklärung nennen.
3. **Dokumentation für die Wartung:** Jedes Projekt hat `README.md` (Start in 5 Schritten), `CLAUDE.md` (Regeln, Stand, offene Punkte) und bei größeren Projekten `docs\` mit Entscheidungen („Entscheidung – Grund – falls falsch“).
4. **Erst Plan, dann Umsetzung;** große Projekte in Etappen mit eigener Spezifikation und eigenem Plan.
5. **Kleine Git-Commits** mit englischen Messages, Kommentare im Code auf Deutsch, Texte für Kunden ohne Fachjargon.
6. **Pragmatisch:** bewährte, einfache Technik vor Experimenten; wenige Abhängigkeiten; Versionen fest angeben.
7. **Wiederkehrende Umsätze mitdenken:** Wartung, Support, Hosting-Betreuung im Angebot vorsehen.
