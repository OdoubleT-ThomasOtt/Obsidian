Ich habe von [https://www.data.gv.at/api/hub/repo/](https://www.data.gv.at/api/hub/repo/) alle Catalogue (ca. 2300), Dataset (ca. 4000) und Distribution (ca. 13000) Informationen heruntergeladen. Ich habe also zu allen Entitäten den Title und Metadaten wie Description und Licence etc. Diese Daten sind in einer sqlite Datenbank gespeichert. Ich möchte nun aufgrund der Daten Business Cases entwickeln. Das heisst die KI soll mir helfen anhand der verfügbaren Daten sinnvolle Anwendungsfälle zu finden die ich in ein Produkt umwandeln kann. Ich arbeite soweit mit c#, blazor und claude code. Wie kann ich so grosse Datenmengen durch die KI verarbeiten lassen damit diese mir zusammenhänge findet. Als Beispiel möchte ich dir geben: Es gibt vielleicht Daten die aussagen dass in einem Wohnbereich eine erhöhte Lärmbelastung besteht und in einem anderen Datensatz kann man ableiten dass Baumaßnahmen zur Lärmberuhigung geplant sind. Dadurch wäre es sinnvoll in dem Bereich noch günstig in Wohnungen zu investieren weil diese derzeit aufgrund der Lärmbelastung günstig sind aber im Preis steigen werden und dies kann ich unter anderem in einem Immobilienbewertungstool verkaufen.
 ![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223802-0.png)  

**PHASE 1: Die Vorbereitung (Der "Ideen-Pool")**  
Das passiert im Hintergrund (z.B. einmal pro Woche, wenn neue Daten von data.gv.at kommen).

1. **SQLite Source:** Dein C# Backend liest die textlastigen Metadaten (Title, Description, Keywords) aus deiner Datenbank.
2. **Embedding:** Du schickst diese Texte an ein Embedding-Modell (über Semantic Kernel Konnektoren). Das Modell wandelt den _Inhalt_ des Textes in einen mathematischen Vektor (eine lange Liste von Zahlen) um.
    - _Warum?_ Ein Vektor für "Lärmbelastung" liegt im mathematischen Raum sehr nah an einem Vektor für "Schallschutzfenster Förderung", obwohl die Wörter unterschiedlich sind.
3. **Vektor-Speicher:** Du speicherst diese Vektoren. Jeder Vektor ist mit der ID des ursprünglichen Datensatzes verknüpft. Das ist dein durchsuchbares Gedächtnis.

**PHASE 2: Die intelligente Suche (Der Filter)**  
Hier interagiert der Nutzer live mit deinem Blazor Frontend.

1. **User Input:** Der Nutzer gibt ein abstraktes Ziel ein, z.B. "Investitions-Chancen bei Wohnraum".
2. **Semantische Suche (Semantic Kernel):**
    - Dein C# Code wandelt die Suchanfrage des Nutzers ebenfalls in einen Vektor um.
    - Er fragt den Vektor-Speicher: "Gib mir die 50 Vektoren, die diesem Such-Vektor am nächsten sind."
    - _Das Ergebnis:_ Statt 4000 Datensätzen hast du nun die 50 relevantesten Metadaten herausgefiltert, die sich thematisch um Wohnen, Investition oder verwandte Probleme drehen.

**PHASE 3: Das KI-Reasoning (Das Gehirn)**  
Jetzt kommt Claude ins Spiel, aber effizient.

1. **Kontext-Aufbau:** Du nimmst die _Text-Metadaten_ dieser 50 gefilterten Datensätze. Das sind nur wenige tausend Token, das passt perfekt und kostengünstig in das Kontextfenster.
2. **Der "Strategist Prompt":** Du sendest diese 50 Schnipsel an Claude mit einem sehr spezifischen Auftrag (Prompt Engineering ist hier entscheidend).
    - _Falscher Prompt:_ "Finde was."
    - _Richtiger Prompt (vereinfacht):_ "Du bist ein Data Strategist. Hier sind 50 Datensatz-Beschreibungen. Deine Aufgabe ist es, Paare zu finden, die einen Business Case bilden. Suche nach dem Muster: Dataset A beschreibt ein aktuelles Problem (z.B. Lärm, Hitzeinsel) UND Dataset B beschreibt eine zukünftige positive Veränderung in der gleichen Domäne (z.B. Bauprojekt, neue U-Bahn, Begrünungsplan). Erkläre die wirtschaftliche Logik dahinter."
3. **Output:** Claude liefert dir strukturierte JSON- oder Markdown-Vorschläge zurück, die du direkt in deinem Blazor-Dashboard als "Potenzielle Business Cases" anzeigen kannst.