---
name: erkenntnisse
description: Wiederverwendbares Wissen aus der aktuellen Sitzung bzw. dem aktuellen Projekt in die zentrale Wissensablage C:\Users\SIWAIT\Projekte\_wissen\ übernehmen. Verwenden, wenn JJ /erkenntnisse aufruft, eine Etappe oder ein Projekt abschließt oder sagt „merk dir das für alle Projekte“.
---

# Erkenntnisse in die Wissensablage übernehmen

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
   - neues Themengebiet → neue Datei `_wissen\<thema>.md` anlegen **und** in die Tabelle in `Projekte\CLAUDE.md` eintragen
4. **Vorschlag zeigen:** JJ eine kurze Liste zeigen („Diese 4 Punkte trage ich ein: …, in Datei …“) und auf Bestätigung warten.
5. **Eintragen:** knapp, in einfachem Deutsch, mit Verweis auf die Quelle (Projekt + Datei), damit man das vollständige Beispiel findet. Veraltetes in den Playbooks korrigieren statt nur Neues anzuhängen; Stand-Datum oben aktualisieren.
6. **Aufräumen:** Wenn `erkenntnisse.md` lang wird (> ~40 Punkte), wiederkehrende Punkte ins passende Playbook verschieben.
7. **Sichern:** `_wissen\` ist ein eigenes Git-Repo. Nach dem Eintragen dort committen (englische Message, z. B. „Add lessons from <projekt> stage X“) und `git push` ausführen, falls ein Remote eingerichtet ist.
8. **Abschluss:** in 2–3 Zeilen melden, was wo eingetragen wurde. Falls sinnvoll auch `exion-workspace\context\current-data.md` (Stand, offene Punkte) aktualisieren.
