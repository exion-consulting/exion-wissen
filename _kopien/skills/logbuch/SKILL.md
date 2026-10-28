---
name: logbuch
description: Wiederverwendbares Wissen aus der aktuellen Sitzung bzw. dem aktuellen Projekt in die zentrale Wissensablage C:\Users\SIWAIT\Projekte\_wissen\ übernehmen. Verwenden, wenn JJ /logbuch aufruft (Logbuch-Eintrag), eine Etappe oder ein Projekt abschließt oder sagt „merk dir das für alle Projekte“.
---

# Logbuch – Erkenntnisse in die Wissensablage übernehmen

Ziel: Was in einem Projekt gelernt wurde, soll in allen künftigen Projekten verfügbar sein – ohne dass alte Projekte neu gelesen werden müssen.

## Ablauf

1. **Sammeln:** Aus der laufenden Sitzung (und bei Bedarf `git log` der letzten Tage, Entscheidungsprotokolle in `docs/technik/`, offene Punkte der Projekt-`CLAUDE.md`) herausfiltern:
   - gelöste Probleme und Stolpersteine (Fehler → Ursache → Lösung)
   - bewährte Vorgehen, die sich wiederholen werden (Website, Automatisierung, Software, Datenschutz, Vertrieb …)
   - Entscheidungen mit allgemeinem Wert (Technikwahl, Dienste, Vorlagen)
2. **Filtern:** Nur übernehmen, was **in einem anderen Projekt nützlich** wäre. Nicht übernehmen: Kundendaten, Zugangsdaten, Preise/Interna eines Kunden, rein projektspezifische Details (die bleiben in der Projekt-`CLAUDE.md`/`docs`).
3. **Zuordnen:** Index steht in `C:\Users\SIWAIT\Projekte\CLAUDE.md`. Vorher die Zieldatei lesen, damit nichts doppelt steht.
   - Stolperstein, kurz → `_wissen\erkenntnisse.md` (neueste oben, mit Datum und Projekt)
   - bewährtes Vorgehen / Standard → passendes Playbook (`website.md`, `n8n-automatisierung.md`, `software-projekte.md`, `datenschutz-recht.md`)
   - neues Themengebiet → zunächst in `erkenntnisse.md` sammeln. Eine eigene Datei `_wissen\<thema>.md` erst anlegen, wenn sich zum Thema **mindestens 3 Einträge** angesammelt haben (keine Mini-Dateien mit zwei Zeilen); dann die Einträge dorthin verschieben **und** die Datei in die Tabelle in `Projekte\CLAUDE.md` eintragen
   - **ERP/Software (`software-projekte.md`):** Abläufe sind bewährte Vorschläge, keine festen Vorgaben – jeder Kunde hat eigene Vorstellungen. Beim Eintragen klar trennen: *allgemein bewährt* vs. *so beim Kunden X entschieden*. Kundenspezifische Entscheidungen nicht als Standard formulieren.
4. **Vorschlag zeigen:** JJ eine kurze Liste zeigen („Diese 4 Punkte trage ich ein: …, in Datei …“) und auf Bestätigung warten.
5. **Eintragen:** knapp, in einfachem Deutsch, mit Verweis auf die Quelle (Projekt + Datei), damit man das vollständige Beispiel findet. Veraltetes in den Playbooks korrigieren statt nur Neues anzuhängen; Stand-Datum oben aktualisieren.
6. **Aufräumen (bei jedem Logbuch-Aufruf kurz prüfen):** `erkenntnisse.md` ist der Eingangskorb, keine Dauerablage.
   - Hat sich ein Eintrag bewährt (mehrfach aufgetreten oder ist er zur festen Regel geworden), als Regel ins passende Playbook übernehmen und im Korb streichen oder auf einen Verweis kürzen.
   - Spätestens alle 5–10 Logbuch-Einträge, einmal im Monat oder ab ~40 Punkten: JJ ein Aufräumen vorschlagen (Liste „Diese Punkte verschiebe ich nach …“) und auf Bestätigung warten.
   - Gibt es zu einem Thema ohne eigene Datei inzwischen 3 oder mehr Einträge → neue Themendatei vorschlagen (siehe Schritt 3).
7. **Sichern:** `_wissen\` ist ein eigenes Git-Repo (Remote `exion-consulting/exion-wissen`, privat). Falls `Projekte\CLAUDE.md` oder diese SKILL.md geändert wurden, zuerst nach `_wissen\_kopien\` kopieren (siehe `_kopien\README.md`). Dann committen (englische Message, z. B. „Add lessons from <projekt> stage X“) und `git push` ausführen, falls ein Remote eingerichtet ist. **Immer in dieser Form als einzelne Befehle** (nur diese sind in den Einstellungen ohne Rückfrage erlaubt, kein `cd … &&`): `git -C C:/Users/SIWAIT/Projekte/_wissen add <dateien>`, `git -C C:/Users/SIWAIT/Projekte/_wissen commit -m "…"`, `git -C C:/Users/SIWAIT/Projekte/_wissen push`.
8. **Abschluss:** in 2–3 Zeilen melden, was wo eingetragen wurde. Falls sinnvoll auch `exion-workspace\context\current-data.md` (Stand, offene Punkte) aktualisieren.
