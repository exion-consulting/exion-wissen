# Playbook: Automatisierung mit n8n

Stand: 27.10.2026 · Quellen: `exion-website/n8n/` (Kontaktformular, Download per Mail), `justluxx-ERP` (API + Webhooks als Anschluss für n8n), `exion-workspace/tools/folien-generator/build-n8n-demo.js` (Demo „Anfragen sortieren“ für Vortrag 2).

## Grundaufbau

- **n8n Cloud, Region EU / Frankfurt.** AVV unter Settings → Data Processing Agreement abschließen (Pflicht, sobald personenbezogene Daten fließen) und ablegen (Google Drive → Verwaltung/Datenschutz/AVV).
- Workflows als **JSON-Datei im Projekt-Git** ablegen (`n8n/<name>.workflow.json`) plus `n8n/README.md` mit Ablauf, Einrichtung, Test. Zugangsdaten **nie** im JSON – sie werden in n8n als Credential gewählt.
- ⚠️ **Testabo n8n läuft 14 Tage** – rechtzeitig Tarif wählen, sonst fallen alle Formulare still aus.

## Muster: Website-Formular → E-Mail

1. **Webhook** empfängt die Felder (`/webhook/<name>`), „Allowed Origins“ auf die Domain begrenzen (lokal `localhost:4321` nur zum Testen).
2. **Code-Knoten „Formular prüfen“:** Texte kürzen und bereinigen, Pflichtfelder und E-Mail prüfen, Honeypot `website` gefüllt → Spam.
3. **Switch:** ok / Spam / ungültig.
   - ok → Gmail-Knoten
   - Spam → keine Mail, aber trotzdem „ok“ antworten (Bot merkt nichts)
   - ungültig → Fehler 400
4. **Antwort:** mit `?js=1` kurzes `{"ok": true}`, sonst Weiterleitung auf die Danke-Seite.
5. **Workflow-Einstellungen:** `saveDataSuccessExecution: none` – erfolgreiche Ausführungen nicht speichern (keine Daten bleiben in n8n liegen); nur Fehler speichern.

## Stolpersteine

- **Gmail und Aliase:** Mail vom eigenen Konto an den eigenen Alias landet nur unter „Gesendet“ → immer an die Hauptadresse schicken.
- **Gmail-Zugang mit minimalen Rechten** (nur „Entwürfe verwalten und E-Mails senden“), nicht Vollzugriff.
- **Keine Werbung in automatischen Mails** an Interessenten ohne Werbe-Einwilligung – auch kein „Buchen Sie ein Erstgespräch“.
- Webhooks aus eigenen Anwendungen an n8n brauchen eine **öffentliche https-Adresse** (interne Adressen werden aus Sicherheitsgründen abgelehnt).

## Muster: eigene Anwendung ↔ n8n

- Anwendung bietet eine **REST-API mit Token** (je Token ein technischer Benutzer mit eigenen Rechten, Rate-Limit) und **Webhooks** bei Ereignissen (z. B. `invoice.released`, `article.updated`).
- Webhooks: nur https, Wiederholung bei Fehlern, eigener Worker-Prozess; Inhalte sparsam (IDs und Art, keine Beträge/Personaldaten, die n8n nicht braucht – n8n holt Details per API).
- Vorlage: `justluxx-ERP/docs/api/v1.md`.

## KI in Workflows

- KI-Anbieter mit EU-Verarbeitung bevorzugen (in der Demo: Mistral); Zugang in n8n wählen, nie im JSON.
- Ergebnisse der KI als Vorschlag behandeln (z. B. Kategorie, Entwurf), Entscheidung über Menschen trifft ein Mensch.

## Offen / Ideen

- Eigene Terminbuchung über n8n (freie Zeiten aus Google-Kalender) – als Referenzprojekt geplant (`exion-website`).
