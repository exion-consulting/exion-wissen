# Playbook: Datenschutz und Recht (Praxis-Checkliste)

Stand: 17.11.2026 · Keine Rechtsberatung – Orientierung aus den bisherigen Projekten. Bei Unsicherheit Fachanwalt / Steuerberater einbeziehen.

**Grundsatz (seit 28.10.2026):** Jedes Projekt wird von Anfang an DSGVO- und EU-AI-Act-konform geplant und gebaut. Jedes Konzept enthält einen Abschnitt „Datenschutz & AI Act“ (Pflichtpunkte siehe `Projekte\CLAUDE.md`). Diese Datei ist die Checkliste dafür.

## AVV (Auftragsverarbeitungsvertrag)

- Für **jeden** Dienst, der personenbezogene Daten verarbeitet: Hosting (Hetzner, in konsoleH), Google Workspace (CDPA in der Admin-Konsole), n8n (Settings → DPA), KI-Anbieter, Newsletter-Tools.
- Ablage: Google Drive → Verwaltung/Datenschutz/AVV. Bei neuen Diensten AVV **vor** dem Start abschließen und in der Datenschutzerklärung nennen.
- Bei Kundenprojekten: Ist EXION selbst Auftragsverarbeiter (z. B. Hosting/Betreuung), braucht der Kunde einen AVV mit EXION.

- **KI-Dienste mit Sitz/Servern in den USA:** Der EU-US-Datenschutzrahmen (Angemessenheitsbeschluss (EU) 2023/1795) gilt derzeit, ist aber angefochten (Rechtsmittel C-703/25 P beim EuGH; Brief des EDSA vom 31.07.2026 mit Bitte um Neubewertung nach dem US-Urteil Trump v. Slaughter). Mit zertifiziertem Anbieter und AVV „kann das derzeit ein Weg sein“ – in Texten nie „erlaubt“ oder „verboten“, Einzelfall vom Fachanwalt/DSB prüfen lassen. (Geprüft 16.11.2026 durch Faktenprüfer: Kommissionsseite, EDSA-PDF, Sekundärquellen; jüngste Bestätigung Mitte Sept. 2026)
- **ChatGPT im Geschäftskonto (Business/Team-Workspace):** Laut Einstellungen → Datenkontrollen verwendet OpenAI Daten aus dem Workspace standardmäßig nicht zum Training, eine Zustimmung ist dort gar nicht möglich (Screenshot JJ, 16.11.2026). AVV/DPA für den Workspace trotzdem prüfen bzw. abschließen. Für die API gilt eine eigene Checkliste (DPA, EU-Speicherung, Aufbewahrung, `store: false`) – siehe `exion-workspace	oolssparringREADME.md`. Ins Sparring nur Inhalte, die ohnehin veröffentlicht werden.

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

## Social-Media-Auftritt (z. B. LinkedIn-Firmenseite, geschäftlich genutztes Profil)

- **Impressumspflicht** gilt auch für geschäftliche Social-Media-Auftritte. LinkedIn hat kein Impressum-Feld → Link `…/impressum` (und `…/datenschutz`) ans Ende des Info-/Übersichtstexts, nicht entfernen.
- **Datenschutzerklärung der Website** um einen Abschnitt zum Auftritt ergänzen: Anbieter (LinkedIn Ireland Unlimited Company, Dublin), nur zusammengefasste Statistiken (Page Insights), **gemeinsame Verantwortung nach Art. 26 DSGVO** mit Link auf LinkedIns „Page Insights Joint Controller Addendum“ (legal.linkedin.com/pages-joint-controller-addendum), Rechtsgrundlage Art. 6 Abs. 1 lit. f, Hinweis auf mögliche USA-Übermittlung + Link auf LinkedIns Datenschutzrichtlinie, Klarstellung „keine LinkedIn-Plugins/-Tracking auf der Website“. Vorlage: `exion-website/src/data/datenschutz.html` Abschnitt 6 (eigene Ergänzung, mit e-recht24-Modul „Social Media“ gegenprüfen).
- Website nur **verlinken**, keine Plugins oder „Folgen“-Buttons von LinkedIn einbinden (sonst Einwilligung nötig).
- Keine Personen ohne Zustimmung markieren oder namentlich nennen (Kunden, Teilnehmende).

## Direkte Ansprache von Firmen (§ 7 UWG, Gesetz gegen unlauteren Wettbewerb)

- **E-Mail:** Werbung braucht auch an Firmen die vorherige ausdrückliche Einwilligung (Abs. 2 Nr. 2). Ausnahme nur für eigene Kunden, wenn alle Voraussetzungen von Abs. 3 erfüllt sind (Adresse aus einem Verkauf, eigene ähnliche Leistungen, kein Widerspruch, Hinweis auf das Widerspruchsrecht). Für bloße Interessenten gilt sie nicht.
- **Telefon:** Bei Firmen genügt eine zumindest mutmaßliche Einwilligung (Abs. 2 Nr. 1), bei Verbrauchern nie. Es muss also im Einzelfall ein konkreter Grund für das Interesse des Betriebs erkennbar sein.
- **Brief:** Kein eigener Erlaubnisvorbehalt im Gesetz. Unzulässig wird er, wenn erkennbar ist, dass der Empfänger keine Werbung wünscht (Abs. 1), etwa nach Widerspruch oder bei einem Aufkleber am Briefkasten. Absender muss erkennbar sein, die DSGVO gilt für Adressen weiter. Praktische Folgerung aus dem Wortlaut, nicht anwaltlich geprüft.
- Geprüft 03.11.2026 am Wortlaut auf gesetze-im-internet.de. (exion-workspace, 03.11.2026)

## AI Act (EU-KI-Verordnung)

- **Art. 4 – KI-Kompetenz (gilt seit 02.02.2025):** Seit 27.07.2026 neu gefasst durch den „Digital Omnibus“ (VO (EU) 2026/1744): Unternehmen, die KI einsetzen, müssen **Maßnahmen** zur KI-Kompetenz ihrer Leute ergreifen – ein bestimmtes Niveau müssen sie nicht garantieren (vorher: „ausreichendes Maß sicherstellen“). Kein Zertifikat vorgeschrieben; Dokumentation (wer, wann, welche Inhalte) empfohlen. Aufsicht durch nationale Marktaufsichtsbehörden. Grundlage der EXION-Schulung. (Geprüft 28.10.2026 – Sekundärquellen + EUR-Lex-Eintrag; Wortlaut vor Rechtsaussagen auf EUR-Lex prüfen)
- **Art. 5 – Verbote (seit 02.02.2025):** u. a. Social Scoring, manipulative KI, **Emotionserkennung am Arbeitsplatz und in Bildungseinrichtungen** (aus Gesicht/Stimme/biometrischen Daten). Laut Leitlinien der EU-Kommission (Feb. 2025) **auch im Bewerbungsverfahren**. Ausnahmen nur medizinisch/Sicherheit; reine Textauswertung fällt nicht unter das Verbot. (Geprüft 27.10.2026)
- **Anhang III – Hochrisiko:** u. a. KI für Bewerberauswahl/-bewertung, Beförderung, Kündigung → strenge Pflichten; KMU-Kunden davon abraten.
- **Art. 2 Abs. 10 – rein private Nutzung:** Natürliche Personen, die KI rein privat und nicht beruflich nutzen, fallen nicht unter die Betreiberpflichten. Das endet bei beruflicher Nutzung oder Nutzung über eine Firma. (Geprüft 31.10.2026 über Sekundärquellen und den AI Act Service Desk; Grenzfälle nicht geklärt)
- **Art. 50 – Transparenz:** Chatbots/Voice Agents müssen sich als KI zu erkennen geben; KI-erzeugte, echt wirkende Inhalte kennzeichnen. Art. 50 Abs. 4 (täuschend echte Inhalte, Pflicht der Betreiber) gilt seit 02.08.2026; der Digital Omnibus verschiebt nur die technische Markierung (Abs. 2) für bestehende KI-Systeme bis 02.12.2026. (Geprüft 02.11.2026 über Sekundärquellen, Originaltext gegenlesen)
- **KI-Bilder in der Werbung:** Echt wirkende KI-Bilder von Hallen, Produkten oder Ergebnissen vorsorglich im Bild kennzeichnen („Symbolbild, mit KI erstellt“), weil sie sonst wie echte Referenzen wirken (auch Thema irreführende Werbung). Ob solche Bilder unter die Pflicht fallen, ist nicht abschließend geklärt. Klar erkennbare Sinnbilder sind weniger heikel, ein Hinweis im ersten Kommentar kostet aber nichts. (exion-workspace, 02.11.2026)
- **Nach einer Gesetzesänderung alle Unterlagen durchsuchen, auch fertige Office-Dateien:** Nach der Neufassung von Art. 4 waren Skripte und Website aktuell, aber Leistungsmappe, Handzettel und Angebot (PPTX/DOCX) enthielten noch alten Wortlaut → Text in Office-Dateien durchsuchen mit `unzip -p datei.pptx | grep -c "Suchwort"`, danach neu erzeugen. Der Prüf-Agent hatte die Änderung gefunden – Faktencheck bei Rechtsthemen ernst nehmen. (exion-workspace, 28.10.)
- **Feste Regeln sind in der Regel kein KI-System:** Automatisierungen, deren Regeln Menschen festgelegt haben (Pflichtfelder, Bestellvorschlag nach Formel, Tastenmenü), fallen nach unserem Verständnis nicht unter den Begriff KI-System (Art. 3 Nr. 1, Erwägungsgrund 12) und damit nicht allein deshalb unter AI-Act-Pflichten; die DSGVO gilt trotzdem, sobald Personendaten verarbeitet werden. *Merkposten (16.11.2026, aus GPT-Sparring und Kampagnenplan) – Wortlaut vor öffentlicher Verwendung an EUR-Lex prüfen.*
- **Rechtliche Aussagen in Vorträgen** vor dem Einsatz an der Quelle prüfen und die Quelle in die Sprechernotiz schreiben. (Vortrag 3, 27.10.)
- **DSGVO Art. 22:** Entscheidungen über Menschen (z. B. Bewerbungen) trifft ein Mensch, nicht die KI. AGG: Benachteiligung kann Entschädigung auslösen.

## Chatbots / Voice Agents für Kunden (EXION als Anbieter)

- Hinweis „Sie sprechen mit einer KI“ (Art. 50), AVV je Baustein (Telefonie, KI-Modell, Speicherung), **Einwilligung vor Aufzeichnung** von Gesprächen.

## Beschäftigtendaten in Software (Vorgehen, keine geprüfte Rechtsaussage)

- Auswertungen je Mitarbeiter (Umsatz je Vertriebler, Ziele, Abschlussquoten) sind Leistungsdaten über Beschäftigte. Bewährt: nur die Leitung sieht sie (eigenes Recht), jeder sieht seine eigenen Werte; im Abschnitt „Datenschutz & AI Act“ der Spezifikation nennen und Mitarbeitende informieren.
- Gibt es einen Betriebsrat, ihn früh einbeziehen – Systeme, die Leistung auswerten können, sind dort typischerweise Thema.
- Ziele vorgeben und Umsatz je Vertriebler anzeigen ist im Vertrieb übliche Steuerung und grundsätzlich zulässig. Voraussetzungen: Mitarbeitende vor dem Echtbetrieb informieren (welche Zahlen, wer sieht sie), Zugriff begrenzen (eigene Zahlen bzw. Leitung), keine Verhaltensprotokolle (Klicks, Bildschirmzeiten, heimliche Ranglisten). *Nach Kenntnisstand, nicht im Netz geprüft (30.10.2026):* Die bisher übliche Grundlage § 26 BDSG ist seit einem EuGH-Urteil von 2023 umstritten; man stützt sich eher direkt auf die DSGVO („für das Arbeitsverhältnis nötig“). Vor Verwendung aktuellen Stand prüfen. Beispiel: `justluxx-ERP/docs/superpowers/specs/2026-10-29-design-stufe-2a-mein-tag-design.md` Abschnitt 11.
- Rechtsgrundlage und Mitbestimmung vom Datenschutzbeauftragten bzw. Fachanwalt bestätigen lassen; Stand vor Verwendung prüfen. Beispiel: `justluxx-ERP/docs/technik/entscheidungen-etappe-1d.md` (R11, Abschnitt Datenschutz). (justluxx-ERP, 28.10.2026)

## Haftung, Urheberrecht, Deepfakes (Recherche 17.11.2026, keine Rechtsberatung)

- **Produkthaftung neu:** Gesetz zur Modernisierung des Produkthaftungsrechts vom 22.10.2026, BGBl. 2026 I Nr. 321 (verkündet 27.10.2026, Primärquelle gelesen). Neues ProdHaftG gilt ab **09.12.2026**; für Produkte, die bis 08.12.2026 in Verkehr gebracht wurden, gilt das alte Gesetz (§ 23). **Software inkl. KI ist Produkt** (§ 2; Ausnahme freie Open-Source-Software außerhalb einer Geschäftstätigkeit). Wer wesentlich verändert, wird Hersteller (§ 5); Importeur/Bevollmächtigter bei Herstellern außerhalb der EU (§ 10), Fulfilment-Dienstleister (§ 11), Händler nur subsidiär (§ 12). **Fehlende Sicherheitsupdates** können haften lassen (§§ 8, 9). Beweiserleichterungen für Geschädigte (§§ 19, 20). Ersetzt werden Schäden natürlicher Personen (Körper, private Sachen, private Daten), nicht rein beruflich genutzte Sachen. Kein vertraglicher Ausschluss gegenüber Geschädigten (§ 18). Selbstbeteiligung (500 €) und Höchstbetrag (85 Mio. €) entfallen (laut Fachbeiträgen, am BGBl gegenlesen). **In Schulungen:** kaum betroffen ist, wer gekaufte KI-Werkzeuge nur intern nutzt. **Achtung:** Hersteller ist auch, wer ein Produkt für den Eigenbedarf entwickelt oder herstellt (RL Art. 4 Nr. 10 c) – selbst gebaute Software oder Umrüstung von Maschinen kann erfasst sein. Nie pauschal „interne Nutzung = nicht betroffen“ schreiben (Faktenprüfung 17.11.2026).
- **KI-Haftungsrichtlinie (COM(2022) 496) zurückgezogen:** angekündigt Arbeitsprogramm 2025, Rücknahme im Amtsblatt C/2025/5423 vom 06.10.2025. Es gibt keine eigene EU-KI-Haftung – Produkthaftung, Vertrag, § 823 BGB.
- **Urheberrecht an KI-Ergebnissen:** rein KI-erzeugte Inhalte sind in der Regel nicht geschützt (§ 2 Abs. 2 UrhG). AG München 13.02.2026, Az. 142 C 9786/25: drei KI-Logos nicht geschützt (Rechtskraft nicht geprüft). OLG Düsseldorf 02.04.2026, Az. I-20 W 2/26 (sekundär): KI-Bild nach fremdem Foto verletzt kein Urheberrecht, wenn nur das ungeschützte Motiv übernommen wird; zur Schutzfähigkeit von KI-Bildern lesen Fachquellen den Beschluss widersprüchlich. Praxis: Marke statt Urheberrecht, eigene Arbeitsschritte dokumentieren.
- **KI-Training/Ausgaben:** § 44b UrhG (Text- und Data-Mining, Nutzungsvorbehalt nur maschinenlesbar wirksam). LAION: LG Hamburg 27.09.2024, OLG Hamburg 10.12.2025 – Klage abgewiesen; BGH I ZR 281/25, verhandelt 03.09.2026, Entscheidung offen (Verkündungstermin nicht belegt, **nachtragen**). GEMA gegen OpenAI: LG München I 11.11.2025, Az. 42 O 14139/24 – Liedtexte im Modell = Vervielfältigung, Haftung des Anbieters; **nicht rechtskräftig** (Berufung angekündigt). Wer eine Ausgabe mit erkennbar fremdem Werk veröffentlicht, kann selbst haften (§ 97 UrhG, Folgerung).
- **Deepfakes:** Kennzeichnung nach Art. 50 Abs. 4 AI Act seit 02.08.2026. **§ 201b StGB ist nur Regierungsentwurf** (BR-Drs. 590/26 vom 09.10.2026) – nicht als geltend darstellen; Stand im DIP prüfen. Recht am eigenen Bild (§§ 22, 23 KUG) gilt.
- Quellen und Rohtexte: Recherche-Bericht 17.11.2026 (exion-workspace, Brainstorming „Legal Day“); vor Verwendung in Unterlagen Datum prüfen. (exion-workspace, 17.11.2026)

## GoBD (bei Software mit Belegen/Rechnungen)

- Belege nach Freigabe unveränderbar, archiviertes PDF nie neu erzeugen, Änderungsprotokoll nur anhängbar, Stammdaten archivieren statt löschen, externe Datensicherung des Archivs.
- E-Rechnung (XRechnung/ZUGFeRD) ist im B2B-Bereich Pflicht (Empfang seit 2025, Versand stufenweise).
