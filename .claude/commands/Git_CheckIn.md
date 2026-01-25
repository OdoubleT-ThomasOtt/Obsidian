# Git_CheckIn

## Purpose & Scope
This command orchestrates the gitcheckin agent for Git operations. It validates the environment, calls the agent with appropriate context, and ensures successful execution.

---

## Core Requirements

### Prerequisites
- gitcheckin agent available in .claude/agents/

### Validation Rules
- **MUST** verify gitcheckin agent exists
- **MUST** delegate all operations to agent via Task tool
- **MUST NOT** perform Git operations directly
- **MUST NOT** read agent file content

### Orchestration Rules
- Validate agent availability (check file exists only)
- Pass minimal context to agent (let agent discover state)
- Report results from agent execution
- Never ever execute checkin on your own but always execute the gitcheckin agent

---

## Configuration
- **Agent**: gitcheckin
- **Execution Mode**: Full delegation via Task tool
- **Retry Policy**: Single agent execution
- **Error Handling**: Report and guide

---

## Conventions & Standards
- **Status Reporting**: Pass through agent reports
- **Error Handling**: Report agent failures
- **No Content Reading**: Never read agent file content
- Only execute gitcheckin agent but not any other agent.  

---

## Execution Flow

### Step 1: Validate Agent
- Check for .claude/agents/gitcheckin.md existence
- Abort if agent not available

### Step 2: Call Agent
- execute gitcheckin agent
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
| gitcheckin | Handle all Git operations | Sonnet | Yes |

### Agent Delegation
The gitcheckin agent handles all Git-specific operations including analysis, grouping, commit creation, and verification.

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
1. Check for .claude/agents/gitcheckin.md
2. Execute gitcheckin agent with no parameter
Result: Agent handles all Git operations independently
```

### Example 2: With Arguments
```
Command: Git_CheckIn --no-verify
Action:
1. Check for .claude/agents/gitcheckin.md
2. Execute gitcheckin agent with parameter --no-verify"
Result: Agent processes arguments and executes accordingly
```

---

## Notes & Special Considerations

### Important Notes
- This command is a pure orchestrator
- All operations delegated to gitcheckin agent
- Command only validates and calls agent

### Error Recovery
- If agent not found: Check .claude/agents/ directory
- If agent fails: Report error from agent
- All Git-specific handling done by agent

---

End of Git_CheckIn Command