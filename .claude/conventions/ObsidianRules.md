# Obsidian Vault Rules - ACE Framework

## Overview
The ACE framework organizes vaults around three mental headspaces: **Knowledge**, **Time**, and **Action**. Folders and links mirror each other to enable deliberate context switching.

---

## Philosophie & Grundprinzipien (The Ideaverse Mindset)

Dieser Vault ist ein **Ideaverse** – ein lebendiges Ökosystem für Gedanken.

### Link Your Thinking (LYT)
- Verbindungen zwischen Ideen sind wertvoller als isolierte Notizen in strikten Hierarchien
- Ordner dienen nur als Container, die wahre Struktur entsteht durch Verlinkung

### Note Making statt Note Taking
- Ziel ist es, **eigene Gedanken zu entwickeln**, nicht Informationen anderer zu sammeln
- Notizen sollten in eigenen Worten formuliert sein
- Mehrwert entsteht durch eigene Perspektiven und Reflexionen

### Struktur schafft Verständnis
- **Erstelle proaktiv Ordnerstrukturen** um Übersicht und Verständnis zu schaffen
- Strukturen entstehen "Top-down" basierend auf logischen Themenbereichen
- Jeder Ordner sollte eine **Index-Datei** enthalten (gleichnamig wie der Ordner)
- Tiefe Verschachtelung ist erlaubt wenn sie die Navigation verbessert

---

## Folder Structure

### `+ Add` (Inbox)
- Landing zone for new sparks and captured thoughts
- **Agent Rule:** Suggest moving notes to appropriate ACE folder based on content analysis

### `01 Atlas` (Knowledge)
Focus: **Understanding** - timeless ideas, research, MOCs

| Subfolder | Purpose |
|-----------|---------|
| `Maps` | High-level MOCs organizing other notes |
| `Notes` | Individual atomic ideas ("Dots") |
| `Sources` | Notes from external media (books, articles, movies) |
| `People` | Relationships and influential figures |

### `02 Calendar` (Time)
Focus: **Focus & Reflection** - linear tracking of life

| Subfolder | Purpose |
|-----------|---------|
| `Daily Notes` | Sparks and daily game plans |
| `Logs` | Specific tracking (Idea Logs, Meeting Logs) |
| `Compass` | Long-term planning and reflection |

### `03 Efforts` (Action)
Focus: **Acting & Outcomes** - managed by **intensity**, not deadlines

| Subfolder | Purpose |
|-----------|---------|
| `On` | Active projects, high bandwidth |
| `Ongoing` | Continuous efforts, no clear end date |
| `Simmering` | Back-burner projects |
| `Sleeping` | Completed/archived efforts |

### `90 Extras` (Utilities)
Non-note files organized by function to prevent a "junk drawer":

| Subfolder | Purpose | Agent Rule |
|-----------|---------|------------|
| `91 Attachments` | Media files (images, PDFs, audio, video) | Set as Obsidian's default attachment location |
| `92 Templates` | Note blueprints and JSON snippets | Include mandatory properties: `created:`, `updated:`, `type:` |
| `93 Scripts` | Dataview, Templater, CLI instructions | Store automated workflows and agent instructions here |
| `94 Styles` | CSS snippets for visual customization | - |
| `95 Archive` | Inactive non-text data for preservation | - |

**File Management Rules:**
- **Zero-Conflict Naming:** Never name an image exactly like a note title (prevents ambiguous links)
- **Orphan Cleanup:** Periodically check `91 Attachments` for unlinked files → suggest deletion/archiving
- **Extras vs Atlas:** PDFs live in `91 Attachments`, but notes *about* them live in `01 Atlas/Sources`
- **Path Awareness:** Always use relative paths for attachments (e.g., `[[91 Attachments/image.png]]`)

---

## Linking & Navigation

### Wiki-Links beim Schreiben
- Nutze **`[[Wiki-Links]]`** um Konzepte sofort zu verbinden
- Verlinke proaktiv während des Schreibens, nicht erst nachträglich
- Jede Idee, die an anderer Stelle existiert oder existieren könnte, sollte verlinkt werden

### Top-of-Note Links
Füge am Anfang jeder Notiz kontextuelle Links hinzu:

```markdown
---
up: "[[Übergeordnete MOC]]"
related: ["[[Verwandte Notiz 1]]", "[[Verwandte Notiz 2]]"]
---
```

| Link-Typ | Zweck |
|----------|-------|
| `up` | Link zur direkten Eltern-MOC (vertikale Navigation) |
| `related` | Links zu thematisch verwandten Notizen |

---

## Metadaten & Properties (STIR)

Vermeide "Over-Engineering" bei Metadaten. Konzentriere dich auf das Wesentliche.

### Empfohlene Properties

| Property | Zweck | Beispiel |
|----------|-------|----------|
| `created` | Erstellungsdatum | `2024-01-15` |
| `updated` | Letzte Änderung | `2024-01-20` |
| `up` | Eltern-MOC | `"[[Hauptthema MOC]]"` |
| `related` | Verwandte Notizen | `["[[Notiz A]]", "[[Notiz B]]"]` |
| `status` | Für Efforts | `On`, `Ongoing`, `Simmering`, `Sleeping` |
| `type` | Notiz-Typ | `note`, `moc`, `source`, `person` |

### Tags sparsam verwenden
- Tags (`#`) nur für **Status oder Typ** einer Notiz verwenden
- Beispiele: `#person`, `#source/book`, `#status/draft`
- **Nicht für thematische Organisation** – dafür sind Links da
- Tags ergänzen Links, ersetzen sie aber nicht

---

## Workflows & Prozesse

### ARC-Framework (Ideenentwicklung)

Wenn Ideen verarbeitet oder zusammengefasst werden:

| Phase | Aktion | Beschreibung |
|-------|--------|--------------|
| **A** - Add | Hinzufügen | Neue Ideen landen in `+ Add` oder Daily Notes |
| **R** - Relate | Verbinden | Verbinde mit bestehendem Wissen (Known Ideas) |
| **C** - Communicate | Kommunizieren | Aufbereiten für "Future You" oder Publikum |

**Agent-Regel:** Bei neuen Notizen immer fragen: "Womit hängt das zusammen?"

### Maps of Content (MOCs) erstellen

Wenn eine Sammlung von Notizen zu einem Thema unübersichtlich wird ("Mental Squeeze Point"):

1. **Erstelle** eine neue Notiz (z.B. `[[Thema MOC]]`)
2. **Sammle** Links zu allen relevanten Notizen
3. **Gruppiere** und strukturiere diese Links
4. **Kommentiere** die Gruppierungen um Zusammenhänge sichtbar zu machen

```markdown
# Thema MOC

## Grundlagen
- [[Konzept A]] - Basis für alles Weitere
- [[Konzept B]] - Wichtige Ergänzung

## Fortgeschritten
- [[Konzept C]] - Baut auf A und B auf

## Offene Fragen
- Wie hängt X mit Y zusammen?
```

### Refactoring (Notizen aufteilen)

Wenn eine Notiz zu lang wird oder mehrere Ideen enthält:

1. **Identifiziere** eigenständige Konzepte innerhalb der Notiz
2. **Extrahiere** diese in eigene, neue Notizen ("Atomic Notes")
3. **Verlinke** die neue Notiz an der ursprünglichen Stelle
4. **Prüfe** ob die neue Notiz weitere Verlinkungen benötigt

**Ziel:** Wiederverwendbare, atomare Ideen-Bausteine

---

## Agent Rules

### Structure Management
- **Struktur schafft Verständnis:** Erstelle proaktiv sinnvolle Ordnerstrukturen
- Jeder thematische Bereich erhält einen eigenen Ordner
- Jeder Ordner enthält eine **Index-Datei** (gleicher Name wie Ordner, z.B. `Kauf/Kauf.md`)
- Spezifische Objekte/Projekte als Unterordner (z.B. `Bestand/Rapfstraße 3/`)
- Status-Ordner für Workflow-Phasen (z.B. `Suche/`, `Abgebrochen/`)

### Context Switching
- Facilitate moves between headspaces when appropriate
- Example: Calendar meeting note → Effort project (if actionable outcomes emerge)

### Ordnerstruktur-Prinzipien

**Granulare Struktur ist erwünscht:**

```
Projekt X/
├── Projekt X.md           ← Index-Datei (Übersicht)
├── Recherche/
│   ├── Recherche.md       ← Index-Datei
│   ├── Quelle A.md
│   └── Quelle B.md
├── Umsetzung/
│   ├── Umsetzung.md
│   ├── Phase 1/
│   │   └── Details.md
│   └── Phase 2/
├── Kontakte/
└── Abgeschlossen/
```

**Ordner-Typen:**

| Typ | Beschreibung | Beispiel |
|-----|--------------|----------|
| **Thematisch** | Logische Themenbereiche | `Kauf/`, `Vermietung/` |
| **Objekt-spezifisch** | Konkrete Instanzen | `Rapfstraße 3/`, `Kunde A/` |
| **Status-basiert** | Workflow-Phasen | `Suche/`, `Abgebrochen/`, `Archiv/` |
| **Zeitlich** | Chronologische Gruppierung | `2024/`, `Q1/` |

**Index-Dateien:**
- Jeder Ordner enthält eine gleichnamige `.md`-Datei
- Dient als Übersicht und Einstiegspunkt
- Verlinkt zu allen Unterinhalten
- Enthält Kontext und Zusammenfassung

### STIR Principle
When organizing or retrieving notes, consider:
- **S**pace - where does it belong?
- **T**ime - when is it relevant?
- **I**mportance - how critical is it?
- **R**elatedness - what connects to it?

---

## Content Quality

Goal: Cultivate insights, not hoard information. Notes should "marinate" and collide to form **Idea Emergence**.

### Note-Taking vs Note-Making

| Note-Taking (avoid) | Note-Making (goal) |
|---------------------|-------------------|
| Mechanical capture, clipping articles | Active engagement, externalizing perspective |
| Leads to information anxiety | Improves recall and creativity |

### NOMA Method (Transformation Prompts)
Use these to convert raw data into insights:
- **Similar to...** - What does this remind you of?
- **Different from...** - How does this contrast with existing knowledge?
- **Important because...** - Why does this matter to your goals?

### Capture Techniques

| Technique | Description |
|-----------|-------------|
| **Freelining** | Simple bullet points without formatting concerns |
| **Freetalking** | Dictate in chunks/blocks, not long rambles |
| **Freewriting** | Type non-stop to bypass self-censorship |

### Agent Synthesis Rules
- **Rename Game:** Suggest descriptive titles as content evolves (titling = sense-making)
- **Identify Sparks:** Raw thoughts needing development
- **Identify Boats:** Lonely ideas needing links to other notes
- **Avoid Collector's Fallacy:** Prioritize user's original words over clipped content

### Claude Code Rules
- **No Mechanical Copying:** Never just summarize articles → Ask: "How does this relate to your current project?"
- **Highlight the Unique:** Point out where user made unique connections (e.g., linking Matrix to Adversity Paradox)
- **Prompt for Reflection:** If note is only quotes → add "Reflections" header to nudge note-making

---

## KI-Agenten Sicherheitsregeln

Um die Integrität des Vaults zu wahren, gelten folgende Sicherheitsregeln:

### Kontext wahren
- **Respektiere** den bestehenden Kontext und die Stimme des Nutzers
- **Ergänze** Inhalte, statt sie zu überschreiben
- **Bewahre** den persönlichen Stil und Ton der Notizen
- **Frage nach** bei Unsicherheit über Änderungen

### Privacy First
- Dieser Vault enthält **lokale, private Dateien**
- **Sende keine sensiblen persönlichen Daten** an externe Server
- Ausnahme: Explizit vom Nutzer autorisierte und für die Aufgabe erforderliche Übertragungen
- **Behandle** alle Inhalte als vertraulich

### Integrität der Verlinkungen
- **Prüfe** vor Umbenennungen ob Links aktualisiert werden
- **Erstelle keine verwaisten Links** (Links zu nicht-existierenden Notizen)
- **Informiere** den Nutzer über potentielle Link-Brüche

---

## Technische Wartung

### Dateiformat
- Alle Dateien müssen im **validen Markdown (`.md`) Format** bleiben
- UTF-8 Encoding verwenden
- Keine proprietären Formatierungen einfügen

### Link-Updates
- Bei Dateinamensänderungen müssen alle internen Links (`[[...]]`) aktualisiert werden
- Obsidian macht dies automatisch bei manuellen Änderungen
- Bei Batch-Operationen muss der Agent dies **simulieren/sicherstellen**

### Regelmäßige Prüfungen

| Prüfung | Häufigkeit | Aktion |
|---------|------------|--------|
| Verwaiste Dateien in `91 Attachments` | Monatlich | Löschen oder Archivieren vorschlagen |
| Unverlinkte Notizen ("Boats") | Wöchentlich | Verlinkungsmöglichkeiten aufzeigen |
| Leere Notizen | Bei Bedarf | Löschen oder Befüllen vorschlagen |
| Defekte Links | Bei Änderungen | Sofort reparieren |

---

## Example Decision

**Scenario:** Note "Project X - Research" in `+ Add` folder

**Agent Action:**
1. Move to `03 Efforts/On/Project X` (contains actionable steps)
2. Create link to `01 Atlas/Notes/Technology` (connect to long-term knowledge)
3. Add `up:` property linking to relevant MOC
4. Check for related notes to link via `related:` property
