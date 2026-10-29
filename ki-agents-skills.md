# Playbook: Skills und Agents für Claude Code bauen

Stand: 29.10.2026 · Erstes Beispiel: LinkedIn-Redaktion `/social-media` mit 4 Agents (`exion-workspace\.claude\skills\social-media\`, `.claude\agents\sm-*.md`, Konzept und Tests in `exion-workspace\social-media\docs\`).

Begriffe: **Skill** = Ablaufanleitung, die in der Hauptsitzung läuft. **Agent** = Spezialist mit eigener Rollendatei für eine Teilaufgabe, ohne Gedächtnis zwischen zwei Aufträgen.

## Aufbau

- **Skill steuert, Agents arbeiten zu.** Agents können keine weiteren Agents starten – die Steuerung (wer wann was bekommt, Schleifen, Rückfragen) gehört immer in den Skill. Nur der Skill spricht mit dem Menschen.
- **Übergabe über Dateien:** Agents vergessen alles nach dem Auftrag. Alles, was später noch gebraucht wird (Stichworte, Themen, Antworten, Prüfbefunde), in Dateien festhalten – z. B. ein Plan je Woche. Jedem Auftrag alle Pfade (absolut) und das heutige Datum mitgeben.
- **Gleichartige Aufträge parallel starten** (z. B. 5 Texte gleichzeitig), aber Regeln über mehrere Ergebnisse hinweg (z. B. „Angebot höchstens 1× pro Woche“) vorher zentral festlegen und im Auftrag mitgeben – parallele Agents sehen sich gegenseitig nicht.
- **Fließband statt Warten:** Die Prüfer für einen Text sofort starten, wenn genau dieser Text fertig ist – nicht warten, bis alle Texte fertig sind. Überarbeiten erst, wenn **beide** Prüfer eines Textes zurück sind, damit der Schreiber alle Befunde in einem Auftrag bekommt. (Woche mit 5 Posts, 29.10.2026)

## Produktfähig bauen (Ablauf und Kunde trennen)

- Skill und Agents **markenneutral**: alles Kundenspezifische (Pfade, Wochenplan, Ton, Zielgruppe, Fakten, No-Gos) in **eine Konfigurationsdatei + Profile**. Für einen neuen Kunden werden nur diese getauscht.
- **Neutralitäts-Test:** Suche nach Kunden-/Markennamen in Skill- und Agent-Dateien muss leer bleiben.

## Prüfen und Qualität

- **Prüfer getrennt vom Schreiber:** Prüfer-Agents bekommen **kein Schreibrecht** (`tools` ohne Write/Edit) und **nur das Ergebnis**, nicht die Begründung des Schreibers. Verschiedene Blickwinkel = verschiedene Prüfer (z. B. Fakten vs. Wirkung).
- **Nach jeder Änderung erneut prüfen** – auch wenn nur der „weiche“ Prüfer Mängel hatte; beim Überarbeiten schleichen sich neue Behauptungen ein. Nachbessern auf 2 Runden begrenzen, Rest an den Menschen melden.
- **Prüfer widersprechen sich – Fakten haben Vorrang:** Der Wirkungsprüfer hat Formulierungen vorgeschlagen, die sachlich falsch waren (Gesetzeswortlaut verdreht, „mit vier Zahlen“ obwohl es mehr sind). Die Steuerung markiert solche Widersprüche im Überarbeitungsauftrag ausdrücklich („Vorschlag X nicht übernehmen, siehe Faktenprüfer“).
- **Kleine sachliche Hinweise sofort umsetzen:** Ein als „optional“ gemeldeter Hinweis des Faktenprüfers wurde in der nächsten Runde zum Mangel und kostete eine Extra-Schleife → kurze, eindeutige Korrekturen gleich mit in den Überarbeitungsauftrag geben.
- **Erfindungen verhindern:** Agents (auch Prüfer in Verbesserungsvorschlägen) erfinden gern Erlebnisse, Zahlen, Anlässe. Regel: Neues, das nicht belegt ist, nur als `[RUECKFRAGE: …]` – nie als fertigen Satz.
- **Sperre vor der Freigabe:** Offene Rückfragen oder Prüfmängel blockieren die Freigabe; nur auf ausdrückliches „trotzdem“ des Menschen.
- **Quellen in Stufen:** `oeffentlich` (zitierbar) · `intern-erzaehlbar` (Erfahrung ja, Zahlen/Namen nein) · `intern` (nur Hintergrund). Freigegebene Kernfakten in einer Liste im Profil – die gelten als belegt.

## Testen

- **Prüfer-Test mit absichtlich schlechtem Beispiel:** eingebaute Fehler notieren, Lösungsschlüssel **in eigener Datei**, die der Prüfer nicht lesen darf. Erwartung: alle Fehler gefunden, Gesamturteil „Mängel“.
- **Neue Agents sind erst nach Neustart registriert.** Zum Testen in derselben Sitzung einen allgemeinen Agent die Rollendatei wörtlich befolgen lassen (Werkzeug-Beschränkung wird dabei nicht mitgetestet).
- **Gesamtprüfung durch frischen Agent** (stärkstes Modell) mit Konzept, Plan und den Grenzfällen – hat beim ersten Mal 2 kritische Lücken gefunden.

## Betrieb

- **Berechtigungen** in `.claude\settings.json` des Projekts: nur das Nötige erlauben (z. B. `WebSearch`, `WebFetch`, `Edit(<zielordner>/**)` – `Edit(...)` gilt auch für Write), Zusatzordner über `additionalDirectories`, Zugangsdaten (`.env`) und Datenordner per `deny` sperren. Sonst stoppen parallele Agents an Rückfragen.
- **Rückfragen an JJ als Auswahl** (AskUserQuestion: 2–4 Optionen, Empfehlung zuerst, eigener Vorschlag möglich) – bei klaren Entscheidungen, auch in Skills, die für ihn oder Kunden gebaut werden. **Ausnahme: Texte und Gestaltung im Gespräch.** Bei der Freigabe von Posts hat JJ Auswahl-Dialoge zu Einstieg und Freigabe abgebrochen und lieber eigene Fassungen geschrieben.
- **Freigabe-Ablauf, der sich bewährt hat:**
  1. Den fertigen Text zeigen.
  2. Ehrlich einschätzen: was stark ist, dazu 2–4 konkrete Änderungen.
  3. Eine gekürzte Fassung mit den Worten des Menschen vorschlagen.
  4. Mit einer offenen Frage enden.
  5. Danach den Faktenprüfer erneut ansetzen. Er hat in einer eigenen Fassung eine rechtliche Ungenauigkeit gefunden.
  6. Lernregeln per Mehrfachauswahl abfragen.

  Agent-Entwürfe dienen so als Vorlage und Kritik, nicht als Endtext. (exion-workspace, KW45, 29.10.2026)
- **Datenschutz & AI Act:** Wer veröffentlicht, trägt die redaktionelle Verantwortung → menschliche Freigabe als Pflichtschritt einbauen; keine Daten Dritter ohne Zustimmung.
