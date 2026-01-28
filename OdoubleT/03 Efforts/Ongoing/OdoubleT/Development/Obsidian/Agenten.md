Overall

|   |   |   |
|---|---|---|
|**Agent**|**Fokus**|**Aufgabe**|
|**The Librarian**|Obsidian Archivist|Analysiert bestehende Notizen, findet Anforderungen/Ziele in deinem "Atlas" oder "Efforts" Bereich.|
|**The Obsidian Writer**||Schreibt ins Obsidian|
|**The Scout**|Web Researcher|Durchsucht das Web/Stellenausschreibungen und aggregiert externe Infos.|
|**The Refactorer**||Spezialisiert darauf, zu lange Notizen aufzuspalten oder Metadaten (Properties) zu bereinigen.|
|**The Linker**||Findet ungenutzte Verbindungen (unrequited links) zwischen deinen Zielen und neuen Job-Infos.<br><br>- **Aufgabe:** Er liest die erzeugten Inhalte und setzt automatisch [[Wiki-Links]] um alle Begriffe, die bereits in deiner Vault existieren.<br>- **Ergebnis:** Deine Graph-Ansicht wächst organisch, ohne dass du manuell jedes Wort verknüpfen musst.|
|The Janitor||- **Aufgabe:** Er scannt neu erstellte Notizen auf Inkonsistenzen, Duplikate oder fehlende Metadaten.<br>- **Funktion:** Er korrigiert Tippfehler, vereinheitlicht Datumsformate und verschiebt "AI-Logs" in dafür vorgesehene Archiv-Ordner, um deinen Haupt-Workspace sauber zu halten.|
|Metadata/Property||Dieser Agent ist dafür verantwortlich, dass jede neue Information maschinenlesbar bleibt.<br><br>- **Aufgabe:** Er fügt standardisierte YAML-Frontmatter (Properties) zu neuen Notizen hinzu (z.B. status: aktiv, quelle: agent_scout, datum: YYYY-MM-DD).<br>- **Nutzen:** Er stellt sicher, dass Plugins wie **Dataview** oder die neuen **Obsidian Bases** die Daten korrekt filtern und anzeigen können.|
|Refiner||Oft sind erste KI-Entwürfe zu generisch oder in der falschen Sprache.<br><br>- **Aufgabe:** Er überarbeitet erzeugte Entwürfe (z.B. das Anschreiben), um sie an deinen persönlichen Stil ("Your Voice") anzupassen.<br>- **Funktion:** Du kannst ihm Befehle geben wie: _"Verfeinere dieses Anschreiben, mach es prägnanter und beziehe dich auf meine Werte aus Werte.md"_.|
||||
|**The Orchestrator**|Task Manager|Steuert den gesamten Workflow und aktualisiert die Übersichtsseiten (Dashboards).|
 
Specific

|   |   |   |
|---|---|---|
|**Agent**|**Fokus**|**Aufgabe**|
|**The Strategist**|Career Advisor|Analysiert den "Fit" und entwickelt Strategien, um die Stelle zu erhalten.|
|**The Ghostwriter**|Content Creator|Erstellt Anschreiben basierend auf deinem persönlichen Schreibstil ("Your Voice").|
|The Janitor||Archiviert abgelaufene Bewerbungen in den "Sleeping" Ordner deines Efforts-Systems.|
||||
   

MCP:

|   |   |
|---|---|
|Name|Aufgabe|
|Linter MCP|Überprüft automatisch, ob die Markdown-Syntax korrekt ist (z.B. Tabellen-Formatierung).|
|Chrome Dev tools oder Brave Search / Google Search MCP|Sammeln von Infos im Web|
|||

**1. Das Organisations-Fundament: Das ACE-Framework**  
Struktur muss in Obsidian "verdient" werden; lege niemals Ordner im Voraus an, ohne dass ein konkreter Bedarf besteht. Wir nutzen das ACE-Framework zur Orientierung in drei primären "Headspaces":

- **Atlas (Wissen):** Der Ort für Karten von Inhalten (MOCs), Themen und dauerhaftes Wissen.
- **Calendar (Zeit):** Alle zeitgebundenen Notizen, tägliche Logs und Rückblicke.
- **Efforts (Aktion):** Aktive Projekte und Bemühungen, unterteilt nach Intensität (On, Ongoing, Simmering, Sleeping).
 
**Regel für Agenten:** Verschiebe neue Notizen aus dem + Inbox (Add) Ordner erst in den Atlas oder die Efforts, wenn sie eine klare Relevanz für ein Thema oder Projekt haben.  
**2. Note-making statt Note-taking**  
Das Ziel ist nicht das mechanische Sammeln von Informationen, sondern das Erzeugen von Wert durch eigenes Denken.

- **Noma-Methode:** Nutze Prompts wie „Es ist ähnlich wie...“, „Es ist anders als...“ und „Es ist wichtig, weil...“, um Verbindungen herzustellen.
- **Eigene Worte:** KI-Agenten sollen keine langen Texte kopieren. Informationen müssen synthetisiert und in die "eigene Stimme" des Nutzers übersetzt werden.
- **Verlinkung:** Nutze [[Links]], um Beziehungen zwischen Ideen herzustellen, anstatt sich nur auf Ordner zu verlassen.

**3. KI-Integrations-Richtlinien (Claude Code)**  
KI ist ein Denkpartner, kein Ersatz für das eigene Gehirn.

- **KI-Zone:** Erstelle einen dedizierten Bereich (oder eine separate Vault) für KI-generierte Analysen. Dies schafft eine "Wall of Good Friction" zwischen KI-Inhalten und deinem heiligen Denkraum.
- **IDI-Framework:** Folge dem Prozess: _Imagine_ (Was ist möglich?), _Discern_ (Was davon ist wahr/wertvoll?), _Integrate_ (Verbinde das Wertvolle mit deinem Wissen).
- **Vermeidung von Übergenerierung:** Generiere niemals Textmassen, die deine eigenen Notizen überwuchern.

**4. Technische Standards & Syntax**  
Agenten müssen strikt die Markdown-Standards einhalten:

- **Properties (YAML Frontmatter):** Jede Notiz sollte Metadaten enthalten (z. B. type, tags, up). Diese sind essenziell für die Nutzung von Obsidian Bases.
- **Verlinkung:** Aktiviere in den Einstellungen "Automatically update internal links", um Brüche bei Umbenennungen zu vermeiden.
- **Header:** Verwende # für Titel und ### für Unterüberschriften, um die Lesbarkeit und das Falten (Folding) zu ermöglichen.

**5. Workflow für Agenten bei der Verwaltung**  
Wenn Claude Code beauftragt wird, die Vault zu restrukturieren, gilt:

1. **Backup zuerst:** Erstelle immer ein Backup, bevor hunderte Notizen automatisiert bearbeitet werden.
2. **MOC-Pflege:** Wenn ein Thema mehr als 10–20 Notizen umfasst, erstelle oder aktualisiere eine "Map of Content" (MOC), um die Übersicht zu wahren.
3. **Refactoring:** Nutze das Prinzip des Refactorings, um zu lange Notizen in kleinere, atomare Notizen aufzuteilen und diese zu verlinken.