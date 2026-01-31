# Obsidian_Modify

## Purpose & Scope
This command is the central orchestrator for all Obsidian vault modifications. It analyzes user instructions, determines which agents are needed, provisions them with appropriate data, and coordinates their execution. The workflow supports parallel data collection followed by sequential content processing, with status file tracking for recovery and inter-agent communication.

---

## Core Requirements

### Prerequisites
- The_Obsidian_Reader agent available in .claude/agents/
- The_Web_Researcher agent available in .claude/agents/
- The_Obsidian_Mentor agent available in .claude/agents/
- The_Obsidian_Writer agent available in .claude/agents/
- The_Obsidian_Curator agent available in .claude/agents/

### Validation Rules
- **MUST** verify required agents exist before execution
- **MUST** initialize status files before agent execution
- **MUST** read only Status_Orchestration.md for orchestration decisions
- **MUST** analyze instructions to determine agent selection
- **MUST** delegate all vault operations to appropriate agents via Task tool
- **MUST NOT** perform vault operations directly
- **MUST NOT** read agent file content

### Orchestration Rules
- Initialize status files at workflow start
- Analyze user instructions to determine operation type
- Select appropriate agent(s) based on operation requirements
- **Run data collection agents (Reader, Web Researcher) in parallel when both needed**
- **Run Mentor agent to process collected context into expert-level content**
- Pass STATUS.md path to all agents for data sharing
- Coordinate sequential execution for processing agents (Mentor, Writer, Curator)
- Update Status_Orchestration.md after each phase
- Report consolidated results from all agent executions

---

## Status File System

### Overview
Two status files enable workflow recovery and inter-agent communication:

| File | Purpose | Written By | Read By |
|------|---------|------------|---------|
| Status_Orchestration.md | Phase tracking, recovery | Orchestrator only | Orchestrator only |
| STATUS.md | Data sharing, findings | All agents | All agents |

### File Locations
Status files are created in the project's .claude/status directory:
```
.claude/status/[session-id]/
├── Status_Orchestration.md   # Orchestration log
└── STATUS.md                  # Agent communication
```

**Note**: The `[session-id]` is a unique identifier for each workflow execution, preventing conflicts between parallel or sequential runs.

### Status_Orchestration.md Structure (Minimal, Orchestrator Only)
```markdown
# Obsidian Modify Orchestration

## Meta
- **Task**: [Brief task description]
- **Status**: InProgress | Completed | Failed
- **Start**: [ISO timestamp]
- **Current Phase**: [Phase name]

## Phase Log
| Time | Phase | Status | Duration |
|------|-------|--------|----------|
| HH:MM:SS | Initialize | ✅ Done | 0ms |
| HH:MM:SS | Data Collection | ⏳ Running | - |
| - | Mentor | ⏳ Pending | - |
| - | Writer | ⏳ Pending | - |
| - | Curator | ⏳ Pending | - |

## Blockers
None

## Next Action
[What to do next]
```

### STATUS.md Structure (Detailed, Agent Communication)
```markdown
# Obsidian Modify Session

## Task
[User's original request]

## Configuration
- **Target**: [Target note/location]
- **Operation**: [create|update|append|patch|delete]
- **Agents**: [List of agents to run]

---

## Vault Context (Reader Findings)
**Status**: Pending | InProgress | Completed
**Timestamp**: [ISO timestamp]

### Related Notes Found
- [[Note 1]] - relevance description
- [[Note 2]] - relevance description

### Existing Content Summary
[Summary of relevant vault content]

### Suggested Links
- [[Link 1]]
- [[Link 2]]

---

## Web Research (Web Researcher Findings)
**Status**: Pending | InProgress | Completed
**Timestamp**: [ISO timestamp]

### Key Findings
- Finding 1 with source
- Finding 2 with source

### Summary
[Research summary]

### Sources
- [Source 1](URL)
- [Source 2](URL)

---

## Mentor Output (Processed Content)
**Status**: Pending | InProgress | Completed
**Timestamp**: [ISO timestamp]
**Expert Role**: [Assigned expert persona]

### Evaluation Matrix
| Category | Score |
|----------|-------|
| Accuracy | ?/4 |
| Depth | ?/4 |
| Clarity | ?/4 |
| Relevance | ?/4 |
| Actionability | ?/4 |
| Honesty | ?/4 |
| Example Quality | ?/4 |

### TL;DR
[Brief summary]

### Processed Content
[Expert-level content ready for vault]

### Example
[Concrete example from the response]

### Content Instructions for Writer
- Note Title: [Suggested title]
- Target Location: [ACE framework path]
- Note Type: [note|moc|source]
- Key Links: [[Link 1]], [[Link 2]]

---

## Writer Output
**Status**: Pending | InProgress | Completed
**Timestamp**: [ISO timestamp]

### Created/Modified Files
- file1.md - [action taken]

### Notes for Curator
[Any special curation instructions]

---

## Curator Output
**Status**: Pending | InProgress | Completed
**Timestamp**: [ISO timestamp]

### Metadata Updates
- [file] - frontmatter updated

### Links Created
- [[Link 1]] ↔ [[Link 2]]

### Index Updates
- [folder]/[folder].md updated
```

---

## Configuration
- **Data Collection Agents**: The_Obsidian_Reader, The_Web_Researcher
- **Content Processing Agent**: The_Obsidian_Mentor
- **Vault Operation Agents**: The_Obsidian_Writer, The_Obsidian_Curator
- **Execution Mode**: Full delegation via Task tool
- **Agent Models**: Sonnet (all agents)
- **Parallel Execution**: Data collection phase supports parallel execution
- **Status Tracking**: Via Status_Orchestration.md and STATUS.md
- **Error Handling**: Report and guide

---

## Conventions & Standards
- **Vault Rules**: Agents follow @.claude/conventions/ObsidianRules.md
- **Status Reporting**: Consolidated reports from all agents
- **Error Handling**: Report agent failures with context
- **No Content Reading**: Never read agent file content
- **Status Files**: Always pass STATUS.md path to agents

---

## Agent Overview

### Agent Categories

| Category | Agents | Execution Mode | STATUS.md Role |
|----------|--------|----------------|----------------|
| Data Collection | Reader, Web Researcher | **Parallel** | Write findings |
| Content Processing | Mentor | Sequential | Read findings, write processed content |
| Vault Operations | Writer | Sequential | Read mentor output, write to vault |
| Curation | Curator | Sequential | Read writer output, curate metadata |

### Agent Capabilities

**The_Obsidian_Reader handles:**
- Semantic search in vault (search_vault_smart)
- Text-based search (search_vault_simple)
- Reading existing note content
- Finding related notes
- **Writes to**: STATUS.md "Vault Context" section

**The_Web_Researcher handles:**
- Web searches for current information
- Fetching and processing web page content
- Extracting relevant data from URLs
- **Writes to**: STATUS.md "Web Research" section

**The_Obsidian_Mentor handles:**
- Processing user requests with collected context
- Expert-level analysis and synthesis
- Quality self-evaluation (must reach Level 3+ in all categories)
- Content structuring with examples
- **Reads from**: STATUS.md "Vault Context" + "Web Research" sections
- **Writes to**: STATUS.md "Mentor Output" section

**The_Obsidian_Writer handles:**
- Creating new notes in correct ACE framework locations
- Updating existing note content
- **Reads from**: STATUS.md "Mentor Output" section
- **Writes to**: STATUS.md "Writer Output" section

**The_Obsidian_Curator handles:**
- Frontmatter validation and updates
- Semantic link discovery and creation
- **Reads from**: STATUS.md "Writer Output" section
- **Writes to**: STATUS.md "Curator Output" section

---

## Execution Flow

### Phase 0: Initialize Status Files
- Create Status_Orchestration.md with initial state
- Create STATUS.md with task configuration
- Record start timestamp
- **Update Status_Orchestration.md**: Phase = Initialize ✅

### Phase 1: Validate & Analyze
- Verify required agents exist in .claude/agents/
- Parse user instructions for operation type
- Determine required agents using selection matrix
- Update STATUS.md "Configuration" section
- **Update Status_Orchestration.md**: Phase = Analyze ✅

### Phase 2: Data Collection (PARALLEL)
When both Reader and Web Researcher are needed, execute them **in parallel**:

```
┌─────────────────────────────────────────────────────────┐
│                   PARALLEL EXECUTION                     │
├─────────────────────────┬───────────────────────────────┤
│   The_Obsidian_Reader   │   The_Web_Researcher          │
│   ─────────────────────────────────────────────────────│
│   • Reads vault         │   • Searches web              │
│   • Writes to STATUS.md │   • Writes to STATUS.md       │
│     "Vault Context"     │     "Web Research"            │
└─────────────────────────┴───────────────────────────────┘
```

**Execution**:
- Pass STATUS.md path to both agents
- Launch both agents simultaneously (single message, multiple Task calls)
- Wait for both to complete
- **Update Status_Orchestration.md**: Phase = Data Collection ✅

### Phase 3: Execute Mentor (Content Processing)
- Pass STATUS.md path to Mentor agent
- Mentor reads "Vault Context" and "Web Research" sections
- Mentor processes request with expert-level analysis
- Mentor creates evaluation matrix and validates quality (Level 3+ required)
- Mentor writes processed content to "Mentor Output" section
- **Update Status_Orchestration.md**: Phase = Mentor ✅

### Phase 4: Execute Writer (if needed)
- Pass STATUS.md path to Writer agent
- Writer reads "Mentor Output" section for processed content
- Writer creates/updates vault content based on Mentor instructions
- Writer writes results to "Writer Output" section
- **Update Status_Orchestration.md**: Phase = Writer ✅

### Phase 5: Execute Curator (if needed)
- Pass STATUS.md path to Curator agent
- Curator reads "Writer Output" section
- Curator performs curation tasks
- Curator writes results to "Curator Output" section
- **Update Status_Orchestration.md**: Phase = Curator ✅

### Phase 6: Finalize & Report
- Read final state from STATUS.md
- Consolidate results from all agents
- **Update Status_Orchestration.md**: Status = Completed ✅
- Report to user

---

## Recovery from Interruption

If the workflow is interrupted, the orchestrator can:

1. **Read Status_Orchestration.md** to determine last completed phase
2. **Read STATUS.md** to get all collected data
3. **Resume from next pending phase**

### Recovery Decision Matrix

| Last Completed Phase | Recovery Action |
|---------------------|-----------------|
| Initialize | Start from Phase 1 (Analyze) |
| Analyze | Start from Phase 2 (Data Collection) |
| Data Collection | Start from Phase 3 (Mentor) |
| Mentor | Start from Phase 4 (Writer) |
| Writer | Start from Phase 5 (Curator) |
| Curator | Finalize and report |

---

## Agent Data Provisioning

### For Reader Agent
```
STATUS_FILE: [path to STATUS.md]

Search Request:
  Query: [topic or keywords]
  Search Type: [semantic|text|combined]
  Scope: [folders to search]
  Limit: [max results]

Instructions:
  Write findings to STATUS.md "Vault Context" section
  Update status to "Completed" when done
```

### For Web Researcher Agent
```
STATUS_FILE: [path to STATUS.md]

Research Request:
  Topic: [subject to research]
  Query: [specific search terms]
  Focus: [what aspects to prioritize]
  Language: [German|English|both]

Instructions:
  Write findings to STATUS.md "Web Research" section
  Update status to "Completed" when done
```

### For Mentor Agent
```
STATUS_FILE: [path to STATUS.md]

Processing Request:
  User Request: [original user request]
  Context Available: Vault Context + Web Research in STATUS.md

Instructions:
  1. Read STATUS.md "Vault Context" and "Web Research" sections
  2. Assign expert role relevant to topic
  3. Create evaluation matrix (5-7 categories)
  4. Process request with expert-level analysis
  5. Ensure all matrix categories reach Level 3+
  6. Include concrete example in response
  7. Write to STATUS.md "Mentor Output" section
  8. Provide content instructions for Writer
```

### For Writer Agent
```
STATUS_FILE: [path to STATUS.md]

Instructions:
  Read STATUS.md "Mentor Output" section for processed content
  Follow "Content Instructions for Writer" from Mentor
  Execute write operation to vault
  Write results to STATUS.md "Writer Output" section
  Include notes for Curator if needed
```

### For Curator Agent
```
STATUS_FILE: [path to STATUS.md]

Instructions:
  Read STATUS.md "Writer Output" section for context
  Execute curation tasks
  Write results to STATUS.md "Curator Output" section
```

---

## Agent Selection Logic

### Selection Matrix

| User Intent | Reader | Web | Mentor | Writer | Curator | Execution |
|-------------|--------|-----|--------|--------|---------|-----------|
| Create note with research | Yes | Optional | Yes | Yes | Yes | [R+W] → M → Wr → C |
| Create note from web info | No | Yes | Yes | Yes | Yes | W → M → Wr → C |
| Create note from vault info | Yes | No | Yes | Yes | Yes | R → M → Wr → C |
| Update with new research | Yes | Yes | Yes | Yes | Yes | [R+W] → M → Wr → C |
| Update content only | No | No | Yes | Yes | Yes | M → Wr → C |
| Fix/update metadata only | No | No | No | No | Yes | C only |
| Add links to note | No | No | No | No | Yes | C only |
| Delete note | No | No | No | Yes | No | Wr only |
| Search vault for topic | Yes | No | No | No | No | R only |
| Research topic from web | No | Yes | No | No | No | W only |

**Legend**: R=Reader, W=Web Researcher, M=Mentor, Wr=Writer, C=Curator

### Decision Keywords

**Reader-triggering keywords:**
- suchen, search, finden, find
- vorhandene, existing, vault
- kontext, context, related
- was wissen wir, what do we know

**Web-triggering keywords:**
- recherchieren, research, web
- aktuell, current, latest
- online, internet
- dokumentation (external)

**Writer-triggering keywords:**
- erstellen, create, new, write, schreiben
- hinzufügen, add, append, einfügen
- ändern, change, modify, update (content)
- löschen, delete, remove, entfernen

**Curator-triggering keywords:**
- verlinken, link, verbinden
- metadaten, metadata, frontmatter
- kuratieren, curate, organize

---

## Quality Assurance

### Success Criteria
- [ ] Status files created at workflow start
- [ ] Required agents found and available
- [ ] Instructions correctly analyzed
- [ ] Data collection agents ran in parallel (when both needed)
- [ ] STATUS.md sections populated by each agent
- [ ] Context properly merged before Writer
- [ ] Agent(s) executed successfully
- [ ] Status_Orchestration.md updated after each phase
- [ ] Results consolidated and reported

### Validation Points
- Status files exist in .claude/status/[session-id]/
- Phase log accurately reflects progress
- Agent findings written to correct STATUS.md sections
- No data loss between phases

---

## Error Handling

### Error Types & Responses
| Error | Response |
|-------|----------|
| Agent not found | Abort, report missing agent |
| Status file write fails | Retry once, then abort |
| Reader fails | Continue with Web Researcher results if available |
| Web Researcher fails | Continue with Reader results if available |
| Both collectors fail | Report error, ask user for manual input |
| Mentor fails quality check | Retry once, if still fails report with best output |
| Mentor fails completely | Report error, do not proceed to Writer |
| Writer fails | Report error, do not proceed to Curator |
| Curator fails | Report partial success (Writer completed) |

### Recovery & Escalation
- **Recovery**: Use status files to resume from last checkpoint
- **Partial Success**: Report what completed and what failed
- **Escalation**: Guide user to fix issues manually if agents fail

---

## Examples

### Example 1: Full Pipeline with Mentor Processing
```
User: Erstelle eine Notiz über "Machine Learning in der Medizin" mit Recherche

1. Initialize:
   - Create Status_Orchestration.md (Status: InProgress)
   - Create STATUS.md (Task configured)

2. Data Collection [PARALLEL]:
   - Reader: Searches vault for ML, AI, Medical notes
   - Web Researcher: Searches for current ML in medicine info
   - Both write findings to STATUS.md
   - Status_Orchestration.md: Data Collection ✅

3. Mentor Processing:
   - Reads "Vault Context" + "Web Research" from STATUS.md
   - Assigns expert role: "Medical AI Researcher, PhD..."
   - Creates evaluation matrix, validates Level 3+ in all categories
   - Synthesizes expert-level content with example
   - Writes to STATUS.md "Mentor Output"
   - Status_Orchestration.md: Mentor ✅

4. Writer:
   - Reads STATUS.md "Mentor Output"
   - Creates note at specified ACE location
   - Writes to STATUS.md "Writer Output"
   - Status_Orchestration.md: Writer ✅

5. Curator:
   - Reads STATUS.md "Writer Output"
   - Adds frontmatter, finds related notes, updates index
   - Writes to STATUS.md "Curator Output"
   - Status_Orchestration.md: Curator ✅

6. Finalize:
   - Status_Orchestration.md: Status = Completed ✅
   - Report to user with Mentor's expert analysis
```

### Example 2: Recovery After Interruption
```
Scenario: Workflow interrupted after Mentor phase

1. Read Status_Orchestration.md:
   - Last Phase: Mentor ✅
   - Next Phase: Writer

2. Read STATUS.md:
   - Vault Context: Completed (data preserved)
   - Web Research: Completed (data preserved)
   - Mentor Output: Completed (processed content preserved)
   - Writer Output: Pending

3. Resume from Phase 4 (Writer):
   - Writer reads Mentor Output
   - Continue normal flow
```

### Example 3: Mentor Quality Loop
```
Scenario: Mentor initially fails quality check

1. Data Collection completes successfully

2. Mentor Processing (Attempt 1):
   - Evaluation Matrix: Accuracy 4/4, Depth 2/4, Clarity 4/4...
   - Depth at Level 2 → Below threshold
   - Mentor revises response

3. Mentor Processing (Attempt 2):
   - Evaluation Matrix: All categories 3/4 or 4/4 ✅
   - Writes to STATUS.md "Mentor Output"
   - Continues to Writer
```

---

## Workflow Patterns Summary

| Pattern | Agents | Execution Flow |
|---------|--------|----------------|
| Full Research + Create | R + W + M + Wr + C | [R+W parallel] → M → Wr → C |
| Vault Research + Create | R + M + Wr + C | R → M → Wr → C |
| Web Research + Create | W + M + Wr + C | W → M → Wr → C |
| Content Update | M + Wr + C | M → Wr → C |
| Curate/Link/Metadata | C | C only |
| Delete Note | Wr | Wr only |
| Vault Search Only | R | R only |
| Web Search Only | W | W only |

**Legend**: R=Reader, W=Web Researcher, M=Mentor, Wr=Writer, C=Curator

---

## Notes & Special Considerations

### Important Notes
- This command is a pure orchestrator
- All vault operations delegated to specialized agents
- **Orchestrator only reads Status_Orchestration.md for decisions**
- **Agents communicate via STATUS.md**
- **Mentor is the intellectual core** - processes all content with expert-level quality
- Status files enable recovery after interruption
- Data collection (Reader + Web) runs in PARALLEL when both needed
- Mentor must achieve Level 3+ in all evaluation categories before proceeding

### Status File Rules
- Status_Orchestration.md: Only orchestrator writes
- STATUS.md: All agents read/write their designated sections
- Always pass STATUS.md path when launching agents
- Update Status_Orchestration.md after each phase completes

### ACE Framework Awareness
- Atlas = Knowledge (MOCs, Notes, Sources, People)
- Calendar = Time (Daily Notes, Logs, Compass)
- Efforts = Action (On, Ongoing, Simmering, Sleeping)
- Extras = Utilities (Attachments, Templates, Scripts)

---

End of Obsidian_Modify Command
