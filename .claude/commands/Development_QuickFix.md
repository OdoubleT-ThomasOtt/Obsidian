# Development_QuickFix

## Purpose & Scope
This command implements custom user requirements based on provided text input. It is designed for quick fixes and small changes that don't require full DEVPLAN/TESTPLAN implementation cycles.

---

## Core Requirements

### Prerequisites
- Valid requirement text must be provided in the request
- Requirement should be suitable for quick implementation

### Validation Rules
- **MUST** have requirement text in request
- **MUST NOT** proceed without valid requirement

### Orchestration Rules
- Act as pure orchestrator - never implement directly
- Follow orchestration conventions without exception
- Delegate all implementation to specialized agents

---

## Configuration
- **Model**: Default (Orchestrator)
- **Timeout**: Standard agent timeout
- **Parallel Execution**: Not applicable (single agent)

---

## Conventions & Standards
- **Orchestration**: @.claude/conventions/AgentOrchestrationConventions.md
- **Error Handling**: @.claude/conventions/ErrorHandlingConventions.md

---

## Execution Flow

### Step 1: Validate Input
- Check for requirement text in request
- Validate requirement is suitable for quick fix
- Stop with error if no requirement provided

### Step 2: Execute Quick Fix
- **Agent**: development_quickfix_implementation
- **Purpose**: Implement the provided requirement
- **Input**: Raw requirement text
- **Expected Output**: Implemented changes
- **Error Handling**: Retry once on failure

### Step 3: Finalize
- Report results to user

---

## Agent Specifications

### Required Agents
| Agent | Purpose | When Used |
|-------|---------|-----------|
| development_quickfix_implementation | Quick implementation of requirements | Step 2    |

### Excluded Agents
| Agent | Reason for Exclusion |
|-------|---------------------|
| development_basic_implementation | For DEVPLAN implementations only |
| planning_devplan_creation | Not needed for quick fixes |
| planning_testplan_creation | Not needed for quick fixes |
| testing_epics_and_userstories | Overkill for quick fixes |

### Agent Dependencies
- None - single agent execution

---

## Usage Guidelines

### When to Use
- Small bug fixes
- Minor feature adjustments
- Configuration changes
- Quick refactoring tasks
- Emergency hotfixes

### When NOT to Use
- Full User Story implementation
- Complex features requiring planning
- Changes requiring extensive testing
- Multi-component modifications

### Command Syntax
```
Development_QuickFix: [requirement description]
```

---

## Quality Assurance

### Success Criteria
- [ ] Requirement text validated
- [ ] development_quickfix_implementation executed successfully
- [ ] Changes implemented as requested
- [ ] Todo list updated
- [ ] Results reported to user

### Validation Checklist
- [ ] No direct implementation in orchestrator
- [ ] All conventions followed
- [ ] Error handling implemented

---

## Examples

### Example 1: Fix Typo
```
Command: Development_QuickFix: Fix typo in login button text "Sigin" should be "Sign in"
Result: Quick fix applied to login component
```

### Example 2: Adjust Styling
```
Command: Development_QuickFix: Increase font size of header from 14px to 16px
Result: CSS updated with new font size
```

### Example 3: Configuration Update
```
Command: Development_QuickFix: Update API timeout from 30s to 60s in config
Result: Configuration file updated
```

---

## Notes & Special Considerations

### Limitations
- Not suitable for architectural changes
- No automated test generation
- No documentation updates
- Limited to single-file or small multi-file changes

### Best Practices
- Use for changes under 50 lines of code
- Ensure change is well-defined and unambiguous
- Consider full implementation flow for complex changes
- Always verify changes don't break existing functionality

### Error Recovery
- If quick fix fails, consider using full Development_Implement_US flow
- Log failures for analysis
- Provide clear error messages to user

---

End of Development_QuickFix Command