# Playbook: Skills und Agents für Claude Code bauen

Stand: 20.11.2026 (Prüfregel für fremde Skills; 18.11.: Sparring auch für Gestaltung, Liste „bewusst nicht umgesetzt“, Abschlussprüfung) · Erstes Beispiel: LinkedIn-Redaktion `/social-media` mit 4 Agents (`exion-workspace\.claude\skills\social-media\`, `.claude\agents\sm-*.md`, Konzept und Tests in `exion-workspace\social-media\docs\`).

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
- **Zahlen von Prüf-Agenten selbst nachmessen:** Ein Prüfer nannte 344,21 als Mehrverlust, der echte Lauf ergab 376,50; GPT nannte einen Text „unter 200 Zeichen“, es waren ca. 215 → Zahlen und Längen aus Prüfberichten und Zweitmeinungen nie ungeprüft übernehmen. (Trading Platform, 01.11.; exion-workspace, 03.11.)
- **Amtliche Quelle nicht erreichbar:** Die BMF-Seiten zur E-Rechnung lieferten mehrere Tage Fehler 503, Web-Archive waren für das Abruf-Werkzeug gesperrt → seriöse Zweitquellen nutzen (IHK, Fachverband, Gesetzestext auf gesetze-im-internet.de), den Vorbehalt offen an JJ melden („Original vor Freigabe gegenlesen“) und nicht auf „später nachlesen“ verlassen. JJ entscheidet und öffnet die Quelle kurz vor der Veröffentlichung selbst. (exion-workspace, Social Media KW45, 29.10./01.11.)
- **Erfindungen verhindern:** Agents (auch Prüfer in Verbesserungsvorschlägen) erfinden gern Erlebnisse, Zahlen, Anlässe. Regel: Neues, das nicht belegt ist, nur als `[RUECKFRAGE: …]` – nie als fertigen Satz.
- **Sparring mit einer zweiten KI (z. B. GPT) – von Hand:** Ein Agent schreibt ein „Paket“ mit fertigen Kopierblöcken (Rolle, Regeln, Inhalt, Antwortformat mit Note 1–10); der Mensch kopiert sie in die zweite KI und bringt die Antwort zurück. Ins Paket nur, was ohnehin veröffentlicht wird – keine Kundendaten, Namen Dritter, internen Zahlen. **Die Antworten selbst kritisch bewerten** (übernehmen / prüfen / verwerfen mit Grund): GPT meldete Tippfehler, die nicht im Text standen, zählte die Länge falsch und schlug „stärkere“ Fassungen vor, die Erlebnisse voraussetzen, die es nicht gab. Für einen Kampagnenplan brachte das Sparring über 3 Runden echte Verbesserung (Note 6 → 8 → 9/10). Gleicher Chat für Folgerunden, damit die KI ihre eigene Kritik kennt. (exion-workspace, Social Media, 16.11.2026)
  - **Auch für Gestaltung bewährt** (Datenblatt-Vorlage, 3 Runden, Note 7,5 → 8,5 → 9,0): Seiten als PNG anhängen, feste Rahmenbedingungen ins Paket („bitte nicht dagegen vorschlagen“). Ab Runde 2 eine Liste **„bewusst nicht umgesetzt – mit Grund“** mitschicken, dann wiederholt GPT abgelehnte Vorschläge nicht. Letzte Runde als **Abschlussprüfung**: Freigabe ja/nein, höchstens 3 Punkte, Fehlerliste mit genauer Stelle. GPT rechnete dabei alle Effizienzwerte nach und fand einen echten Fehler von Claude („stufenlos“ statt 5 Stufen). Je Vorschlag festhalten: übernommen / teilweise / verworfen + Grund (`sparring\auswertung.md`). Nach Runde 2 lag das Risiko laut GPT nicht mehr im Design, sondern in den Daten → Prüfung im Code statt weiterer Runden. (justluxx-Datenblätter, 18.11.2026)
- **Abbruchregel bei vielen Prüfrunden:** Nach 4–5 Runden schwankten die Noten des internen Wirkungsprüfers (7 → 6), weil jeder neue Prüfer-Aufruf die umgesetzten Vorschläge des vorigen neu bewertet und neue findet. Bewährt: Prüfer → 2 Runden mit der zweiten KI → höchstens 1 Feinschliff → der Mensch entscheidet. Fortschritt (Note steigt) ist das Kriterium, nicht „bis der Prüfer zufrieden ist“. (exion-workspace, 16.11.2026)
- **Ankündigungen gegen den Plan prüfen:** Kündigt ein Text spätere Inhalte an („am Donnerstag zeige ich …“, eine Wochen-Übersicht), fand der Faktenprüfer dreimal Widersprüche zum Plan (falsche Woche, mehr versprochen als geplant, Woche vergessen). Solche Ankündigungen erst nach der Plan-Freigabe schreiben, wortgenau gegen den Plan prüfen und den späteren Text an die Ankündigung binden. (exion-workspace, 16.11.2026)
- **Sperre vor der Freigabe:** Offene Rückfragen oder Prüfmängel blockieren die Freigabe; nur auf ausdrückliches „trotzdem“ des Menschen.
- **Quellen in Stufen:** `oeffentlich` (zitierbar) · `intern-erzaehlbar` (Erfahrung ja, Zahlen/Namen nein) · `intern` (nur Hintergrund). Freigegebene Kernfakten in einer Liste im Profil – die gelten als belegt.

## Testen

- **Prüfer-Test mit absichtlich schlechtem Beispiel:** eingebaute Fehler notieren, Lösungsschlüssel **in eigener Datei**, die der Prüfer nicht lesen darf. Erwartung: alle Fehler gefunden, Gesamturteil „Mängel“.
- **Neue Agents:** Früher erst nach Neustart registriert; am 16.11.2026 waren neu angelegte Agents ohne Neustart verfügbar (Claude Code meldet sie). Erst nachsehen, ob sie in der Liste stehen; sonst neu starten oder zum Testen einen allgemeinen Agent die Rollendatei wörtlich befolgen lassen (Werkzeug-Beschränkung wird dabei nicht mitgetestet).
- **Gesamtprüfung durch frischen Agent** (stärkstes Modell) mit Konzept, Plan und den Grenzfällen – hat beim ersten Mal 2 kritische Lücken gefunden.

## Fremde Skills nutzen (z. B. skills.sh, find-skills)

- **Keine fremden Skills ungeprüft installieren.** Ein Skill läuft mit denselben Rechten wie Claude: Er hat Zugriff auf Workspace, Kundenordner und `.env`. Ein bösartiger oder schlampiger Skill kann Daten nach außen schicken. Bei Kundendaten wäre das ein Datenschutzvorfall.
- **Der Suchhelfer „find-skills“ (Vercel) wird nicht installiert.** Er sucht in skills.sh und installiert mit einem Befehl (`npx skills add …`). Sortiert wird nach Anzahl der Installationen, und beliebt heißt nicht sicher. Stattdessen sucht Claude auf Zuruf im Netz und zeigt die Treffer, ohne etwas zu installieren.
- **Prüfregel vor jeder Installation, in drei Schritten:**
  1. Die Prüfseite des Skills auf skills.sh ansehen. Dort prüfen Gen Agent Trust Hub, Socket und Snyk.
  2. Den Skill komplett lesen, besonders mitgelieferte Skripte und **Hooks**. Hooks sind Befehle, die bei bestimmten Ereignissen von selbst starten. Kein Prüfdienst untersucht sie gezielt, und sie können nach dem Entfernen des Skills weiterlaufen.
  3. JJ in einfachen Worten erklären, was der Skill tut. Erst nach seinem Ja wird installiert.
- **Bekannte Quellen bevorzugen**, zum Beispiel Anthropic oder große Hersteller. Gute Ideen lieber in eigene Skills übernehmen.
- **In Kundenprojekten keine fremden Skills einsetzen.**
- Hintergrund: Snyk („ToxicSkills“, Februar 2026) hat rund 4.000 Skills von skills.sh und ClawHub geprüft. 76 waren nachweislich bösartig, 13 % hatten mindestens ein schweres Problem. Die Zahlen stammen von einem Anbieter von Prüfsoftware. Stand der Angaben geprüft am 20.11.2026. (exion-workspace, 20.11.2026)

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
- **Ältere Entwürfe vor der Freigabe auffrischen.** Do und Fr entstanden, bevor JJ seine Korrekturen gemacht hatte; sie enthielten die gelernten Regeln nicht. Vor der Freigabe alter Entwürfe die Stimme-Datei anwenden lassen und erneut prüfen. (exion-workspace, KW45, 01.11.2026)
- **Nach einer eigenen Fassung des Menschen die Nebenangaben nachziehen.** Quellentabelle und „Gewählt“-Zeile belegten danach noch den alten Text. Text bleibt unangetastet, ein Schreiber-Auftrag stellt nur diese Abschnitte um, dann kurze Schlussprüfung. Parallele Änderungen an derselben Datei vermeiden. (exion-workspace, KW45, 01.11.2026)
- **Lernen aus Kennzahlen (Statistik, Klicks, Antworten):** in den bestehenden Skill einbauen statt einen neuen anzulegen, wenn dieser die Daten schon kennt. Bei `/social-media` ist das „Modus Auswertung“. Den Ablauf sofort bauen, Regeln erst ab einer festen Datenmenge vorschlagen (dort 20 Beiträge, Muster in mindestens 3 Fällen je Seite). In einer Datei drei Abschnitte trennen: „Beobachtungen“ (nur Hinweis), „Gelernt aus Zahlen“ (vom Menschen bestätigt, für den Agent verbindlich) und „Verworfen“ (damit abgelehnte Vorschläge nicht wiederkommen). Bei jeder neuen Auswertung die Regeln gegen die neuen Zahlen prüfen und Streichen vorschlagen. Gleiches Muster wie „Gelernt aus Korrekturen“. (exion-workspace, 09.11.2026)
- **Datenschutz & AI Act:** Wer veröffentlicht, trägt die redaktionelle Verantwortung → menschliche Freigabe als Pflichtschritt einbauen; keine Daten Dritter ohne Zustimmung.
