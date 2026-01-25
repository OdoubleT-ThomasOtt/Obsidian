|   |   |
|---|---|
|[Datenschutzaspekte bei der Nutzung der ChatGPT-API \| Simpliant Insights](https://simpliant.eu/de/insights/GDPR-requirements-when-using-chatgpt-api)|DSGVO in Bezug auf OpenAI chatgpt API|
|[EU-Nutzungsbedingungen \| OpenAI](https://openai.com/de-DE/policies/eu-terms-of-use/)|OpenAI Nutzungsbedingungen|
 
**Relevante Schritte beim Kunden:**

1. **Data Processing Addendum, DPA)** [Data processing addendum | OpenAI](https://openai.com/policies/data-processing-addendum/) zwischen Kunden und OpenAi unterzeichnen durch click am Ende der Seite. Dieser muss den Anforderungen des Art. 28 DSGVO standhalten.
2. Datenschutzerklärung um Nutzung der GPT-API ergänzen
    1. Wie und zu welchen Zweck werden die Daten verarbeitet?
    2. Wie und zu welchen Zweck werden die Daten gespeichert?
    3. Wann werden die Daten gelöscht?
    
    --\> [Muster Datenschutzhinweis](Muster%20Datenschutzhinweis)
    
    5. Informieren Sie darüber, welche Rechte (Auskunft, Löschung, Berichtigung etc.) Betroffene haben.
3. Datenschutzfolgenabschätzung (DSFA) und Datensicherheit
    1. Prüfen ob eine DSFA laut [EU-Datenschutz-Grundverordnung (DSGVO): Datenschutz-Folgenabschätzung und vorherige Konsultation - WKO](https://www.wko.at/datenschutz/eu-dsgvo-datenschutz-folgenabschaetzung-konsultation) durchgeführt werden muss und gff. durchführen.
4. Verfahrensverzeichnisses
    1. Anlage oder Aktualisierung laut [Verfahrensverzeichnis](https://www.bitkom.org/sites/default/files/file/import/2016-03-22-Leitfaden-Verfahrensverzeichnis.pdf)

Der Prozess zum Abschluss des Datenverarbeitungszusatzes (DPA) umfasst folgende Schritte:  
1. Online-Formular ausfüllen: Unternehmen füllen ein Online-Formular aus, in dem sie unter anderem ihren vollständigen rechtlichen Firmennamen und die Organisations-ID angeben müssen. Für Unternehmen im Europäischen Wirtschaftsraum (EWR) oder in der Schweiz ist zusätzlich die Angabe des Standorts erforderlich.  
2. OpenAI-Entität auswählen: Unternehmen in der EU sollten OpenAI Ireland Ltd. als Vertragspartner auswählen.  
3. Kontaktdaten für die Unterzeichnung angeben: Die E-Mail-Adresse und die Position der Person, die den DPA im Namen des Unternehmens unterzeichnet, müssen bereitgestellt werden.  
4. DPA überprüfen und akzeptieren: Nach dem Einreichen des Formulars erhalten die beteiligten Parteien eine Aufforderung per E-Mail, den Vertrag zu überprüfen und elektronisch zu akzeptieren. Diese E-Mail enthält einen Link zur digitalen Plattform, auf der der Vertrag eingesehen und unterzeichnet werden kann. Nach der elektronischen Unterzeichnung erhalten beide Parteien eine Bestätigung und Zugriff auf eine gespeicherte, digital signierte PDF-Kopie des DPA. Das DPA wird rechtsverbindlich, sobald es von dem Unternehmen akzeptiert ist. Das per E-Mail erhaltene DPA sollte dann an geeigneter Stelle abgespeichert werden, um die Einhaltung der Datenschutzanforderungen nachweisen zu können (Art. 5, 28 DSGVO).
   

**Relevante Schritte bei der Umsetzung:**

1. Datenschutzfolgenabschätzung mit Hilfe von AI anlegen oder erweitern
2. Datenschutzerklärung mit Hilfe von AI anlegen oder erweitern
3. Verfahrensverzeichnis mit Hilfe von AI anlegen oder erweitern
4. Verarbeitung gezielt protokollieren.
    - Loggen Sie Anfragen an die ChatGPT API inkl. Zeitstempel, Statuscodes und (sofern datenschutzkonform) Input-/Output-Daten zur Fehlerdiagnose und Performanceüberwachung
    - Erfassen Sie Workflow-Logs: Ausführungszeiten, Erfolg/Misserfolg, Fehlerdetails und benutzte Nodes, um den Ablauf nachvollziehen zu können.
    - Protokollieren Sie alle CRUD-Operationen (Create, Read, Update, Delete) inkl. Zeitstempel und (falls möglich) Benutzer-IDs, um einen Audit-Trail zu gewährleisten.
    - Dokumentieren Sie Verbindungsdetails, Authentifizierungsversuche und eventuelle Fehlermeldungen – wichtig für das Monitoring von Sicherheitsvorfällen.
    - Achten Sie darauf, dass personenbezogene Daten nur pseudonymisiert oder anonymisiert geloggt werden und die DSGVO-Vorgaben einhalten.
5. Automatisches Löschen der Daten im definierten Zeitraum
 
**Allgemein:**

- **Emailverarbeitung:**
    - der Verweis auf die Datenschutzerklärung beim Absenden auf der Internetseite sollte gut sichtbar sein (Für die Verarbeitung unbekannter E-Mails eignet sich in der Regel das berechtigte Interesse (§ 6 Abs. 1 lit. f DSGVO)).
    - Bei Klassifizierung nur Betreff und Email zuerst verarbeiten. Dann könnte man daraus schließen dass es sich um einen Kunden handelt mit dem man einen Vertrag abgeschlossen hat der es erlaubt die Emails voll zu verarbeiten. Alternativ kann auch die E-Mail anonymisiert werden aber für diesen Schritt wird ein lokales Hosting benötigt.
- **Falls Daten von unbekannten Entitäten verarbeitet werden sollen empfiehlt sich folgende Infrastruktur:**
    - Selbst gehostetes Llama 3 Model um eingehende Daten zu anonymisieren
    - Selbst gehostetes n8n, um die Daten zu verarbeiten ([N8N fully managed open source service | Elest.io](https://elest.io/open-source/n8n) oder [n8n Hosting | peaknetworks](https://www.peaknetworks.at/server-cloud/apps/n8n))
    - Selbst gehostete Datenbank um die Daten zu speichern
    - OpenAI business Account oder Copilot Studio account, um komplexere KI Anfragen mit anonymisierten Daten zu verarbeiten
- **Falls Daten von bekannten Entitäten verarbeitet werden sollen empfiehlt sich folgende Infrastruktur:**
    - Cloud n8n, um Daten zu verarbeiten
    - Airtable um Daten zu speichern bzw. Eingaben oder Darstellung der Daten zu ermöglichen
    - OpenAI business Account oder Copilot Studio account, um komplexere KI Anfragen zu verarbeiten (ggf anonymisiert)