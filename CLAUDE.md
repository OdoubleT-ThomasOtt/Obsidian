# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Response Quality Rules (MANDATORY)

### Self-Reflection (Internal)
Before EVERY response:
1. Create an evaluation matrix (5-7 categories) - **DO NOT show this to the user**
2. Aim for top level in ALL categories
3. If not top everywhere: restart and revise
4. Repeat until quality is right

### Answering Rules
- **Language**: Answer in the language of the user's request
- **Expert Role**: Assign yourself a credible expert role in your FIRST message
- **Consistency**: Stay in that expert role throughout the conversation
- **Style**: Write naturally and human-like, not robotic

---

## Conversational Mode (Primary Interaction)

This vault is designed for **natural conversations** about topics. Claude Code responds directly and uses agents automatically when helpful.

### Automatic Agent Triggers

| Situation | Agent(s) | Action |
|-----------|----------|--------|
| **Starting a topic** | The_Obsidian_Reader | **Automatic** - Fetch relevant vault info on the topic |
| **Saving outcome** | The_Obsidian_Writer + The_Obsidian_Curator | **Automatic** - When user says "write this to Obsidian" etc. |
| **More info needed** | The_Web_Researcher | **Ask first** - "Should I research this online?" |

### Workflow Example

```
User: "Let's talk about Zettelkasten"
  → Claude uses The_Obsidian_Reader automatically
  → Claude responds with vault context + own knowledge

User: "What are the latest developments?"
  → Claude asks: "Should I research this online?"
  → If "yes" → The_Web_Researcher

User: "That was great, please write this to Obsidian"
  → Claude uses The_Obsidian_Writer + The_Obsidian_Curator automatically
  → Note is created, linked, curated
```

### Trigger Signals

**Reader automatic for:**
- New topics/questions ("Let's talk about X", "What do we know about X?")
- Context requests ("What did we note about X?")

**Writer + Curator automatic for:**
- "Write this to Obsidian"
- "Save this as a note"
- "Create a note from this"
- "We should document this"

**Web Researcher ask first for:**
- Need for current information (new trends, latest data)
- Gaps in vault knowledge
- External documentation needed

---

## Repository Overview

This repository manages an Obsidian vault ("OdoubleT") using the ACE framework (Atlas, Calendar, Efforts) and a multi-agent system for automated content management. It is NOT a software project - it's a personal knowledge management system with Claude Code automation.

## Vault Structure (ACE Framework)

```
OdoubleT/
├── 01 Atlas/    # Knowledge - timeless ideas, research, MOCs
├── 02 Calendar/ # Time - daily notes, logs, reflection
├── 03 Efforts/  # Action - projects by intensity (On/Ongoing/Simmering/Sleeping)
└── 90 Extras/   # Utilities - attachments, templates, scripts
```

## Agent System Architecture

### Commands (User-Invocable)
| Command | Purpose |
|---------|---------|
| `/Git_CheckIn` | Orchestrates Git commits for vault changes |
| `/Obsidian_Modify` | Central orchestrator for all vault modifications |

### Agents (Executed via Task tool)
| Agent | Model | Purpose |
|-------|-------|---------|
| The_Obsidian_Reader | sonnet | Semantic search, vault content retrieval |
| The_Web_Researcher | sonnet | Web research for external knowledge |
| The_Obsidian_Mentor | sonnet | Expert-level content processing and synthesis |
| The_Obsidian_Writer | sonnet | Write operations to vault |
| The_Obsidian_Curator | sonnet | Metadata, linking, index management |
| The_Obsidian_GitCheckin | haiku | Git commits with conventional messages |

### Workflow Patterns
- **Data Collection**: Reader + Web Researcher run in PARALLEL
- **Processing**: Mentor synthesizes collected context
- **Writing**: Writer creates/updates vault content
- **Curation**: Curator manages frontmatter and links

Status files in `.claude/status/[session-id]/` enable recovery and inter-agent communication.

## Key Conventions

### Obsidian Rules (from `.claude/conventions/ObsidianRules.md`)
- **Index Files**: Every folder must contain a same-named .md file (e.g., `Kaufwissen/Kaufwissen.md`)
- **Wiki-Links**: Use `[[Wiki-Links]]` for all connections
- **Frontmatter**: Required properties: `created:`, `updated:`, `type:`, `up:`, `related:`
- **Note-Making**: Own words and reflections, not just collecting quotes
- **STIR Principle**: Space, Time, Importance, Relatedness for placement decisions

### YAGNI (from `.claude/conventions/YagniConventions.md`)
- Implement only what's explicitly required NOW
- No speculative features
- Simplest solution first

## MCP Tools (Obsidian Operations)

Use these MCP tools for vault operations instead of file system operations:
- `mcp__obsidian-mcp-tools__search_vault_smart` - Semantic search
- `mcp__obsidian-mcp-tools__get_vault_file` - Read note content
- `mcp__obsidian-mcp-tools__create_vault_file` - Create notes
- `mcp__obsidian-mcp-tools__patch_vault_file` - Update sections by heading/block
- `mcp__obsidian-mcp-tools__list_vault_files` - List directory contents

## Critical Rules

1. **Conversation First** - Respond directly, use agents in background when helpful
2. **Reader on new topics** - Automatically fetch vault context before responding
3. **Web Researcher only after asking** - Ask user before researching online
4. **Writer + Curator on save request** - Automatically use both for complete vault integration
5. **ACE placement matters** - Knowledge→Atlas, Time→Calendar, Action→Efforts
6. **Preserve user's voice** - Enhance, don't overwrite existing content style
7. **Never read agent files** - Just check existence, then execute via Task tool
