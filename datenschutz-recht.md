# Playbook: Datenschutz und Recht (Praxis-Checkliste)

Stand: 27.10.2026 · Keine Rechtsberatung – Orientierung aus den bisherigen Projekten. Bei Unsicherheit Fachanwalt / Steuerberater einbeziehen.

## AVV (Auftragsverarbeitungsvertrag)

- Für **jeden** Dienst, der personenbezogene Daten verarbeitet: Hosting (Hetzner, in konsoleH), Google Workspace (CDPA in der Admin-Konsole), n8n (Settings → DPA), KI-Anbieter, Newsletter-Tools.
- Ablage: Google Drive → Verwaltung/Datenschutz/AVV. Bei neuen Diensten AVV **vor** dem Start abschließen und in der Datenschutzerklärung nennen.
- Bei Kundenprojekten: Ist EXION selbst Auftragsverarbeiter (z. B. Hosting/Betreuung), braucht der Kunde einen AVV mit EXION.

## Website-Rechtstexte

- Impressum und Datenschutzerklärung über einen **Generator** erstellen (aktuell: e-recht24, kostenlose Version – Quellenangabe „Quelle: e-recht24.de“ ist Lizenzbedingung, nicht entfernen).
- Selbst ergänzte Abschnitte (Formulare, n8n, Google) als solche markieren (`<!-- EIGENE ERGÄNZUNG -->`) – kein geprüfter Rechtstext.
- Bei neuen Diensten den Generator neu durchlaufen. Inhalte (Anschrift, Rechtsform, USt-ID) nie erfinden, beim Kunden einfordern.
- Bildnachweis im Impressum: Stockfotos mit Quelle; KI-Bilder als KI-erstellt kennzeichnen.

## Formulare

- Nur das Nötigste abfragen (Datenminimierung), Rest „optional“.
- Hinweis am Formular + Link auf den passenden Abschnitt der Datenschutzerklärung (Anker, z. B. `/datenschutz#download`).
- Eigener Abschnitt in der Datenschutzerklärung: Daten, Zweck, Rechtsgrundlage (Anfrage → Art. 6 Abs. 1 lit. b DSGVO), Speicherdauer, Dienste.
- **Werbung nur mit eigener, nicht vorangekreuzter Einwilligung** und Double-Opt-in. Ohne Einwilligung: keine Werbung, auch nicht in Bestätigungsmails; Adressen nicht in Verteiler übernehmen.
- In Automatisierungen keine Daten länger speichern als nötig (n8n: erfolgreiche Ausführungen nicht speichern).

## Externe Inhalte auf Websites

- Keine Tracker, Analytics, eingebetteten Karten/Videos/Kalender ohne Einwilligung → stattdessen einfache Links.
- Schriften lokal einbinden (Google Fonts von Google-Servern = Abmahnrisiko).

## AI Act (EU-KI-Verordnung)

- **Art. 4 – KI-Kompetenz:** Unternehmen, die KI einsetzen, müssen ihre Leute schulen (Grundlage der EXION-Schulung).
- **Art. 5 – Verbote (seit 02.02.2025):** u. a. Social Scoring, manipulative KI, **Emotionserkennung am Arbeitsplatz und in Bildungseinrichtungen** (aus Gesicht/Stimme/biometrischen Daten). Laut Leitlinien der EU-Kommission (Feb. 2025) **auch im Bewerbungsverfahren**. Ausnahmen nur medizinisch/Sicherheit; reine Textauswertung fällt nicht unter das Verbot. (Geprüft 27.10.2026)
- **Anhang III – Hochrisiko:** u. a. KI für Bewerberauswahl/-bewertung, Beförderung, Kündigung → strenge Pflichten; KMU-Kunden davon abraten.
- **Art. 50 – Transparenz:** Chatbots/Voice Agents müssen sich als KI zu erkennen geben; KI-erzeugte, echt wirkende Inhalte kennzeichnen.
- **DSGVO Art. 22:** Entscheidungen über Menschen (z. B. Bewerbungen) trifft ein Mensch, nicht die KI. AGG: Benachteiligung kann Entschädigung auslösen.

## Chatbots / Voice Agents für Kunden (EXION als Anbieter)

- Hinweis „Sie sprechen mit einer KI“ (Art. 50), AVV je Baustein (Telefonie, KI-Modell, Speicherung), **Einwilligung vor Aufzeichnung** von Gesprächen.

## GoBD (bei Software mit Belegen/Rechnungen)

- Belege nach Freigabe unveränderbar, archiviertes PDF nie neu erzeugen, Änderungsprotokoll nur anhängbar, Stammdaten archivieren statt löschen, externe Datensicherung des Archivs.
- E-Rechnung (XRechnung/ZUGFeRD) ist im B2B-Bereich Pflicht (Empfang seit 2025, Versand stufenweise).
