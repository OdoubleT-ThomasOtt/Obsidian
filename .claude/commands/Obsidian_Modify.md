# Obsidian_Modify

## Purpose & Scope
This command is the central orchestrator for all Obsidian vault modifications. It analyzes user instructions, determines which agents are needed (The_Obsidian_Writer, The_Obsidian_Curator, or both), provisions them with appropriate data, and coordinates their execution.

---

## Core Requirements

### Prerequisites
- The_Obsidian_Writer agent available in .claude/agents/
- The_Obsidian_Curator agent available in .claude/agents/

### Validation Rules
- **MUST** verify required agents exist before execution
- **MUST** analyze instructions to determine agent selection
- **MUST** delegate all vault operations to appropriate agents via Task tool
- **MUST NOT** perform vault operations directly
- **MUST NOT** read agent file content

### Orchestration Rules
- Analyze user instructions to determine operation type
- Select appropriate agent(s) based on operation requirements
- Pass relevant context and data to selected agents
- Coordinate sequential execution when both agents needed
- Report consolidated results from all agent executions

---

## Configuration
- **Agents**: The_Obsidian_Writer, The_Obsidian_Curator
- **Execution Mode**: Full delegation via Task tool
- **Agent Models**: Sonnet (both agents)
- **Error Handling**: Report and guide

---

## Conventions & Standards
- **Vault Rules**: Agents follow @.claude/conventions/ObsidianRules.md
- **Status Reporting**: Consolidated reports from all agents
- **Error Handling**: Report agent failures with context
- **No Content Reading**: Never read agent file content

---

## Agent Selection Logic

### Operation Analysis
Analyze user instructions to identify:
1. **Content Operations** - Creating, writing, updating, or modifying note content
2. **Curation Operations** - Metadata updates, linking, frontmatter, folder index maintenance
3. **Combined Operations** - Content changes that require subsequent curation

### Selection Matrix

| User Intent | Writer | Curator | Execution Order |
|-------------|--------|---------|-----------------|
| Create new note | Yes | Yes | Writer → Curator |
| Update note content | Yes | Yes | Writer → Curator |
| Add content to note | Yes | Yes | Writer → Curator |
| Fix/update metadata only | No | Yes | Curator only |
| Add links to note | No | Yes | Curator only |
| Update frontmatter | No | Yes | Curator only |
| Organize/curate existing note | No | Yes | Curator only |
| Delete note | Yes | No | Writer only |
| Move note to different location | Yes | Yes | Writer → Curator |

### Decision Keywords

**Writer-triggering keywords:**
- erstellen, create, new, write, schreiben
- hinzufügen, add, append, einfügen
- ändern, change, modify, update (content)
- löschen, delete, remove, entfernen
- verschieben, move

**Curator-triggering keywords:**
- verlinken, link, verbinden
- metadaten, metadata, frontmatter, properties
- kuratieren, curate, organize
- tags, kategorisieren, categorize
- related, verwandt, up-link

---

## Execution Flow

### Step 1: Validate Agents
- Check for .claude/agents/The_Obsidian_Writer.md existence
- Check for .claude/agents/The_Obsidian_Curator.md existence
- Abort if required agent(s) not available

### Step 2: Analyze Instructions
- Parse user instructions for operation type
- Identify target note(s) or location(s)
- Determine required agent(s) using selection matrix
- Prepare context data for each agent

### Step 3: Execute Writer (if needed)
- Call The_Obsidian_Writer agent with:
  - Operation type (create, update, append, patch, delete)
  - Target location/file
  - Content to write
  - Any specific formatting requirements
- Wait for completion before proceeding to Curator

### Step 4: Execute Curator (if needed)
- Call The_Obsidian_Curator agent with:
  - Target note path (from Writer output or user instruction)
  - Curation scope (full curation or specific tasks)
  - Any specific metadata requirements
- Curator handles: frontmatter, semantic links, backlinks, folder index

### Step 5: Report Results
- Consolidate outputs from all executed agents
- Report:
  - Files created/modified
  - Links established
  - Metadata updates
  - Any warnings or issues
- Suggest follow-up actions if needed

---

## Agent Specifications

### Required Agents
| Agent | Purpose | Model | When Used |
|-------|---------|-------|-----------|
| The_Obsidian_Writer | Execute write operations (create, update, patch, delete) | Sonnet | Content changes |
| The_Obsidian_Curator | Maintain metadata, links, frontmatter, folder index | Sonnet | After edits, metadata tasks |

### Agent Capabilities

**The_Obsidian_Writer handles:**
- Creating new notes in correct ACE framework locations
- Updating existing note content
- Appending content to notes
- Patching specific sections (headings, blocks)
- Deleting notes
- Managing attachments placement

**The_Obsidian_Curator handles:**
- Frontmatter validation and updates
- Semantic link discovery and creation
- Bidirectional backlink management
- Folder index (MOC) maintenance
- Property consistency (created, updated, type, up, related)

---

## Data Provisioning

### For Writer Agent
```
Operation: [create|update|append|patch|delete]
Target: [file path or location description]
Content: [markdown content to write]
Note Type: [note|moc|person|source]
ACE Location: [Atlas|Calendar|Efforts subfolder]
```

### For Curator Agent
```
Target Note: [file path of note to curate]
Scope: [full|metadata-only|links-only|index-only]
Specific Tasks: [list of specific curation tasks if not full]
```

---

## Quality Assurance

### Success Criteria
- [ ] Required agents found and available
- [ ] Instructions correctly analyzed
- [ ] Appropriate agent(s) selected
- [ ] Agent(s) executed successfully
- [ ] Results consolidated and reported

### Validation Points
- Agents exist in .claude/agents/
- Operation type correctly identified
- Target location/file clearly defined
- Agent execution completed without errors
- All changes reported to user

---

## Examples

### Example 1: Create New Note
```
User: Erstelle eine neue Notiz über "Machine Learning Grundlagen" im Atlas/Notes Bereich

Analysis:
- Operation: Create new note
- Agents needed: Writer + Curator

Execution:
1. Writer: Create note at correct ACE location with content
2. Curator: Add frontmatter, find related notes, update folder index
```

### Example 2: Update Existing Note
```
User: Füge einen neuen Abschnitt über "Backpropagation" zur ML-Notiz hinzu

Analysis:
- Operation: Append content to existing note
- Agents needed: Writer + Curator

Execution:
1. Writer: Append new section to note
2. Curator: Update `updated` date, find new related links
```

### Example 3: Curate Only
```
User: Aktualisiere die Links und Metadaten für die Projektübersicht

Analysis:
- Operation: Metadata and link update only
- Agents needed: Curator only

Execution:
1. Curator: Update frontmatter, semantic links, backlinks, folder index
```

### Example 4: Delete Note
```
User: Lösche die veraltete Notiz XYZ

Analysis:
- Operation: Delete
- Agents needed: Writer only

Execution:
1. Writer: Delete the note (Curator not needed for deletion)
```

### Example 5: Full Note Reorganization
```
User: Verschiebe die Notiz von Inbox nach Atlas/Investment und kuratiere sie

Analysis:
- Operation: Move + full curation
- Agents needed: Writer + Curator

Execution:
1. Writer: Move note to new location
2. Curator: Full curation (metadata, links, new folder index entry)
```

---

## Error Handling

### Error Types & Responses
| Error | Response |
|-------|----------|
| Agent not found | Abort, report missing agent |
| Ambiguous instructions | Ask user for clarification before proceeding |
| Writer fails | Report error, do not proceed to Curator |
| Curator fails | Report partial success (Writer completed) |
| Target not found | Report error, suggest alternatives |
| Invalid ACE location | Ask user for correct location |

### Recovery & Escalation
- **Recovery**: Report detailed error context
- **Partial Success**: Report what completed and what failed
- **Escalation**: Guide user to fix issues manually if agents fail

---

## Notes & Special Considerations

### Important Notes
- This command is a pure orchestrator
- All vault operations delegated to specialized agents
- Command only analyzes, selects, coordinates, and reports
- Both agents follow ACE framework and ObsidianRules.md
- Writer always executes before Curator when both needed

### Workflow Patterns
- **Create/Update** → Always Writer then Curator
- **Curate/Link/Metadata** → Curator only
- **Delete** → Writer only (nothing to curate)
- **Move** → Writer (move) then Curator (re-link)

### ACE Framework Awareness
- Atlas = Knowledge (MOCs, Notes, Sources, People)
- Calendar = Time (Daily Notes, Logs, Compass)
- Efforts = Action (On, Ongoing, Simmering, Sleeping)
- Extras = Utilities (Attachments, Templates, Scripts)

---

End of Obsidian_Modify Command
