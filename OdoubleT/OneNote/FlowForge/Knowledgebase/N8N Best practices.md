[10 n8n Tips in 10 Minutes to 10x Your AI Automations](https://www.youtube.com/watch?si=Mp-URrh0tbfuzAEw&v=Nsu9BzQv5C4&feature=youtu.be):

- Chat-Historie/RAG-Speicherung

Vermeide In-Memory-Optionen; nicht skalierbar.  
Empfehlung: Supabase für SQL- und PG-Vector-Datenbanken.
 
- Auswahl von LLMs

Empfehlung je nach Use Case:  
Leistungsstark: Anthropic Claude 3.5.  
Schnell: Llama.  
Preiswert: OpenAI GPT-4 Mini.
 
- Text Embedding: OpenAI Text-Embedding-3 Small.

RAG mit verschiedenen Dateiformaten  
Unterschiedliche Nodes für Extraktion aus PDF, Text- und Excel-Dateien erforderlich.
 
- Dynamische Werte von vorherigen Nodes

JSON-Dot-Ausdruck nur für vorherige Node; für ältere Nodes explizite Referenz notwendig.
 
- Webhook + Chat-Trigger

Kombination aus Webhook- und Chat-Trigger für flexibles Testen und API-Integration.
 
- Umgang mit mehreren Node-Ausgaben

Automatische Schleifenverarbeitung bei Mehrfachausgaben.  
Beispiel: Text aus mehreren Dateien extrahieren und zusammenführen.
 
- Daten-Pinning

Testdaten nach Hard-Reload durch "Pin Data"-Feature sichern.
 
- Fehler-Workflows

Fehler-Trigger für Monitoring einrichten; z. B. Slack-Benachrichtigungen bei Fehlern.
 
- Schedule-Trigger

Regelmäßige Workflows auf Basis von Zeitplänen; ideal für Berichte oder Aufgabenüberwachung.
 
- n8n Workflow-Bibliothek

Über 1000 Vorlagen verfügbar, nützlich als Startpunkt.

[Why 97% of n8n Workflows Fail in Production (And How to Fix It)](https://www.youtube.com/watch?v=ASnwt2ilg28)

- **Sicherheit (Authentication)**
    - Webhooks nur per POST und mit API-Key absichern (Header “x-appi-key”)
    - Credentials als vordefinierte Typen nutzen (z. B. OpenAI) oder Variablen über einen Set-Node injizieren
    - So verhinderst du ungewollten Zugriff und stellst den ersten Schutzwall auf
- **Retry-Mechanismen**
    - Für jeden API- oder AI-Step “Retry on fail” aktivieren
    - Angepasste Wartezeiten (z. B. 5 s) und max. Wiederholungen einstellen
    - Fallback-Provider (z. B. Anthropic statt OpenAI) über Error-Output einbinden
- **Fehlerbehandlung & Logging**
    - Zentralen Error-Trigger-Workflow einrichten
    - “Stop and Error”-Nodes mit aussagekräftigen Meldungen (z. B. “Error at agent step”) verbinden
    - Automatisches Loggen (z. B. in Google Sheets) aller Fehlermeldungen und Ausführungs-URLs
- **Bonus-Tipp: Versionierung**
    - Workflows nach “production-ready-v1”, “-v2” etc. benennen
    - Per Download/Import alte Versionen schnell wiederherstellen
    - So behältst du jederzeit den Überblick und vermeidest ungewollte Änderungen