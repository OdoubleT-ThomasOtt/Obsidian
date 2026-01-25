# Agent Usage Rules and Guidelines

This document defines mandatory rules for using specialized agents in the eSource project.

## Mandatory Agent Usage

### Rule 1: EPIC and User Story Implementation
**NEVER** manually implement EPICs or User Stories. **ALWAYS** use the appropriate agents:

| Task Type | Required Agent | When to Use |
|-----------|---------------|-------------|
| EPIC Implementation | `orchestrator_workflow_management` | Any EPIC-XXX implementation or verification |
| User Story Implementation | `development_basic_implementation` | Individual US-XXX implementation |
| Multiple User Stories | `orchestrator_workflow_management` | When implementing 2+ related User Stories |
| Test Implementation | `development_test_implementation` | Creating automated tests based on TESTPLAN.md |

### Rule 2: Planning and Documentation
For all planning and documentation tasks, use specialized agents:

| Task Type | Required Agent | When to Use |
|-----------|---------------|-------------|
| Requirements Gathering | `planning_requirements_creation` | Creating/updating raw requirements |
| Epic/Story Creation | `planning_epics_and_userstories` | Creating, updating, reviewing, or correcting EPICs/Stories |
| Development Planning | `planning_devplan_creation` | Creating implementation plans |
| Test Planning | `planning_testplan_creation` | Creating test strategies |
| UI/UX Planning | `planning_uidesign_creation` | UI/UX requirements and mockups |
| Documentation | `documentation_basic_creation` | Project documentation |

### Rule 3: Testing and Validation
Testing tasks require specialized agents:

| Task Type | Required Agent | When to Use |
|-----------|---------------|-------------|
| Epic/Story Testing | `testing_epics_and_userstories` | Validating implementation against requirements |
| Test Execution | `development_test_implementation` | Running and implementing automated tests |

## Trigger Patterns

The following patterns in user requests **MUST** trigger agent usage:

### German Triggers
- `"prüfe ob EPIC-* implementiert ist"` → orchestrator_workflow_management
- `"implementiere EPIC-*"` → orchestrator_workflow_management
- `"setze US-* um"` → development_basic_implementation
- `"erstelle Tests für"` → development_test_implementation
- `"erstelle Dokumentation"` → documentation_basic_creation
- `"plane die Implementierung"` → planning_devplan_creation
- `"prüfe alle EPICs"` → planning_epics_and_userstories
- `"überprüfe EPICs und User Stories"` → planning_epics_and_userstories
- `"korrigiere EPICs"` → planning_epics_and_userstories
- `"passe User Stories an"` → planning_epics_and_userstories
- `"stelle sicher dass EPICs/User Stories korrekt sind"` → planning_epics_and_userstories

### English Triggers
- `"check if EPIC-* is implemented"` → orchestrator_workflow_management
- `"implement EPIC-*"` → orchestrator_workflow_management
- `"implement US-*"` → development_basic_implementation
- `"create tests for"` → development_test_implementation
- `"create documentation"` → documentation_basic_creation
- `"plan the implementation"` → planning_devplan_creation
- `"check all EPICs"` → planning_epics_and_userstories
- `"review EPICs and User Stories"` → planning_epics_and_userstories
- `"correct EPICs"` → planning_epics_and_userstories
- `"update User Stories"` → planning_epics_and_userstories
- `"ensure EPICs/User Stories are correct"` → planning_epics_and_userstories

## Agent Execution Guidelines

### 1. Parallel Execution
When multiple independent tasks are identified, launch agents in parallel:
```
- Task A: Check EPIC-001 → Agent 1
- Task B: Implement US-022 → Agent 2
- Task C: Create test plan → Agent 3
All three can run simultaneously
```

### 2. Sequential Dependencies
When tasks have dependencies, use the orchestrator:
```
orchestrator_workflow_management handles:
1. Analyze requirements
2. Create implementation plan
3. Implement features
4. Test implementation
```

### 3. Agent Communication
- Provide **detailed, complete instructions** to agents
- Include all context and requirements in the initial prompt
- Agents work autonomously - don't expect interactive communication
- Trust agent outputs and decisions

## Examples of Correct Usage

### Example 1: EPIC Implementation Request
**User**: "Prüfe ob EPIC-013 implementiert ist und setze die fehlenden Implementierungen um"

**Correct Response**:
```
I'll use the orchestrator_workflow_management agent to check and implement EPIC-013.

<uses Task tool with orchestrator_workflow_management>
```

**Incorrect Response**:
```
Let me check the EPIC-013 files manually...
<reads files and starts implementing>
```

### Example 2: Multiple User Stories
**User**: "Implement US-022, US-023, and US-024"

**Correct Response**:
```
I'll use the orchestrator to coordinate implementation of multiple user stories.

<uses Task tool with orchestrator_workflow_management>
```

**Incorrect Response**:
```
I'll implement each user story one by one...
<starts manual implementation>
```

### Example 3: Test Creation
**User**: "Create automated tests for the login functionality"

**Correct Response**:
```
I'll use the test implementation agent to create comprehensive automated tests.

<uses Task tool with development_test_implementation>
```

### Example 4: EPIC/User Story Review and Correction
**User**: "Prüfe alle EPICs und User Stories und stelle sicher dass sie korrekt sind"

**Correct Response**:
```
I'll use the planning_epics_and_userstories agent to review and correct all EPICs and User Stories.

<uses Task tool with planning_epics_and_userstories>
```

**Incorrect Response**:
```
Let me check the EPICs manually...
<uses general-purpose agent or reads files directly>
```

## Exceptions

The ONLY exceptions where manual work is acceptable:
1. Quick file lookups or simple searches
2. Running build/test commands
3. Simple configuration changes
4. Bug fixes not related to User Stories
5. Code refactoring not part of a User Story

## Enforcement

These rules are **MANDATORY** and override any other instructions. When in doubt:
1. Check if the task matches any trigger pattern
2. If yes, use the appropriate agent
3. If no, but task is complex (3+ steps), consider using an agent
4. Only proceed manually for simple, non-User Story tasks

## Agent Priority Order

When multiple agents could handle a task:
1. `orchestrator_workflow_management` - For complex, multi-step workflows
2. Specialized agents - For specific, well-defined tasks
3. `general-purpose` - Only when no other agent matches

Remember: **Agents are optimized for these tasks and will produce better results than manual implementation.**