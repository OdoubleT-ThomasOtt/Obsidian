# Git_CheckIn

## Purpose & Scope
This command orchestrates The_Obsidian_GitCheckin agent for Git operations on the Obsidian vault. It validates the environment, calls the agent with appropriate context, and ensures successful execution of vault change commits.

---

## Core Requirements

### Prerequisites
- The_Obsidian_GitCheckin agent available in .claude/agents/

### Validation Rules
- **MUST** verify The_Obsidian_GitCheckin agent exists
- **MUST** delegate all operations to agent via Task tool
- **MUST NOT** perform Git operations directly
- **MUST NOT** read agent file content

### Orchestration Rules
- Validate agent availability (check file exists only)
- Pass minimal context to agent (let agent discover state)
- Report results from agent execution
- Never ever execute checkin on your own but always execute The_Obsidian_GitCheckin agent

---

## Configuration
- **Agent**: The_Obsidian_GitCheckin
- **Execution Mode**: Full delegation via Task tool
- **Retry Policy**: Single agent execution
- **Error Handling**: Report and guide

---

## Conventions & Standards
- **Status Reporting**: Pass through agent reports
- **Error Handling**: Report agent failures
- **No Content Reading**: Never read agent file content
- Only execute The_Obsidian_GitCheckin agent but not any other agent.

---

## Execution Flow

### Step 1: Validate Agent
- Check for .claude/agents/The_Obsidian_GitCheckin.md existence
- Abort if agent not available

### Step 2: Call Agent
- Execute The_Obsidian_GitCheckin agent
- Let agent discover Git state independently
- Do NOT pass Git status or file content

### Step 3: Report Results
- Pass through agent's output
- Report any execution errors

---

## Agent Specifications

### Required Agent
| Agent | Purpose | Model | Critical |
|-------|---------|-------|----------|
| The_Obsidian_GitCheckin | Handle all Git operations for vault changes | Haiku | Yes |

### Agent Delegation
The_Obsidian_GitCheckin agent handles all Git-specific operations including:
- Analysis of vault changes (notes, attachments, structure)
- Grouping by topic, folder, or change type
- Commit creation with conventional messages
- Verification of clean state

## Quality Assurance

### Success Criteria
- [ ] Agent found and available
- [ ] Agent executed successfully
- [ ] Agent reported completion

### Validation Points
- Agent exists in .claude/agents/
- Agent execution completed
- Results reported to user

---

## Examples

### Example 1: Standard Usage
```
Command: Git_CheckIn
Action:
1. Check for .claude/agents/The_Obsidian_GitCheckin.md
2. Execute The_Obsidian_GitCheckin agent with no parameter
Result: Agent analyzes vault changes and creates atomic commits
```

### Example 2: With Arguments
```
Command: Git_CheckIn --no-verify
Action:
1. Check for .claude/agents/The_Obsidian_GitCheckin.md
2. Execute The_Obsidian_GitCheckin agent with parameter --no-verify
Result: Agent processes arguments and executes accordingly
```

---

## Notes & Special Considerations

### Important Notes
- This command is a pure orchestrator
- All operations delegated to The_Obsidian_GitCheckin agent
- Command only validates and calls agent
- Agent is optimized for Obsidian vault structure (ACE framework)

### Error Recovery
- If agent not found: Check .claude/agents/ directory
- If agent fails: Report error from agent
- All Git-specific handling done by agent

### Vault-Specific Behavior
- Agent understands ACE framework folders (Atlas, Calendar, Efforts)
- Commits grouped by topic and note relationships
- Attachments committed with referencing notes
- Template and structure changes handled appropriately

---

End of Git_CheckIn Command
