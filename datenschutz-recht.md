# Playbook: Datenschutz und Recht (Praxis-Checkliste)

Stand: 28.10.2026 · Keine Rechtsberatung – Orientierung aus den bisherigen Projekten. Bei Unsicherheit Fachanwalt / Steuerberater einbeziehen.

**Grundsatz (seit 28.10.2026):** Jedes Projekt wird von Anfang an DSGVO- und EU-AI-Act-konform geplant und gebaut. Jedes Konzept enthält einen Abschnitt „Datenschutz & AI Act“ (Pflichtpunkte siehe `Projekte\CLAUDE.md`). Diese Datei ist die Checkliste dafür.

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

- **Art. 4 – KI-Kompetenz (gilt seit 02.02.2025):** Seit 27.07.2026 neu gefasst durch den „Digital Omnibus“ (VO (EU) 2026/1744): Unternehmen, die KI einsetzen, müssen **Maßnahmen** zur KI-Kompetenz ihrer Leute ergreifen – ein bestimmtes Niveau müssen sie nicht garantieren (vorher: „ausreichendes Maß sicherstellen“). Kein Zertifikat vorgeschrieben; Dokumentation (wer, wann, welche Inhalte) empfohlen. Aufsicht durch nationale Marktaufsichtsbehörden. Grundlage der EXION-Schulung. (Geprüft 28.10.2026 – Sekundärquellen + EUR-Lex-Eintrag; Wortlaut vor Rechtsaussagen auf EUR-Lex prüfen)
- **Art. 5 – Verbote (seit 02.02.2025):** u. a. Social Scoring, manipulative KI, **Emotionserkennung am Arbeitsplatz und in Bildungseinrichtungen** (aus Gesicht/Stimme/biometrischen Daten). Laut Leitlinien der EU-Kommission (Feb. 2025) **auch im Bewerbungsverfahren**. Ausnahmen nur medizinisch/Sicherheit; reine Textauswertung fällt nicht unter das Verbot. (Geprüft 27.10.2026)
- **Anhang III – Hochrisiko:** u. a. KI für Bewerberauswahl/-bewertung, Beförderung, Kündigung → strenge Pflichten; KMU-Kunden davon abraten.
- **Art. 50 – Transparenz:** Chatbots/Voice Agents müssen sich als KI zu erkennen geben; KI-erzeugte, echt wirkende Inhalte kennzeichnen.
- **DSGVO Art. 22:** Entscheidungen über Menschen (z. B. Bewerbungen) trifft ein Mensch, nicht die KI. AGG: Benachteiligung kann Entschädigung auslösen.

## Chatbots / Voice Agents für Kunden (EXION als Anbieter)

- Hinweis „Sie sprechen mit einer KI“ (Art. 50), AVV je Baustein (Telefonie, KI-Modell, Speicherung), **Einwilligung vor Aufzeichnung** von Gesprächen.

## Beschäftigtendaten in Software (Vorgehen, keine geprüfte Rechtsaussage)

- Auswertungen je Mitarbeiter (Umsatz je Vertriebler, Ziele, Abschlussquoten) sind Leistungsdaten über Beschäftigte. Bewährt: nur die Leitung sieht sie (eigenes Recht), jeder sieht seine eigenen Werte; im Abschnitt „Datenschutz & AI Act“ der Spezifikation nennen und Mitarbeitende informieren.
- Gibt es einen Betriebsrat, ihn früh einbeziehen – Systeme, die Leistung auswerten können, sind dort typischerweise Thema.
- Rechtsgrundlage und Mitbestimmung vom Datenschutzbeauftragten bzw. Fachanwalt bestätigen lassen; Stand vor Verwendung prüfen. Beispiel: `justluxx-ERP/docs/technik/entscheidungen-etappe-1d.md` (R11, Abschnitt Datenschutz). (justluxx-ERP, 28.10.2026)

## GoBD (bei Software mit Belegen/Rechnungen)

- Belege nach Freigabe unveränderbar, archiviertes PDF nie neu erzeugen, Änderungsprotokoll nur anhängbar, Stammdaten archivieren statt löschen, externe Datensicherung des Archivs.
- E-Rechnung (XRechnung/ZUGFeRD) ist im B2B-Bereich Pflicht (Empfang seit 2025, Versand stufenweise).
