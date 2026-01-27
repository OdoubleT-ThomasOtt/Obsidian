# Obsidian Vault Rules - ACE Framework

## Overview
The ACE framework organizes vaults around three mental headspaces: **Knowledge**, **Time**, and **Action**. Folders and links mirror each other to enable deliberate context switching.

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

## Agent Rules

### Structure Management
- **Earn Your Structure:** Do NOT create subfolders until a category has 10+ notes
- Start with beginner-level structure (Atlas/Calendar/Efforts)

### Context Switching
- Facilitate moves between headspaces when appropriate
- Example: Calendar meeting note → Effort project (if actionable outcomes emerge)

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

## Example Decision

**Scenario:** Note "Project X - Research" in `+ Add` folder

**Agent Action:**
1. Move to `03 Efforts/On/Project X` (contains actionable steps)
2. Create link to `01 Atlas/Notes/Technology` (connect to long-term knowledge)
