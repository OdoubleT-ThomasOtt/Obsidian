# Development_Implement_US_Extended

## Purpose & Scope
This command implements a single User Story based on a provided US-ID with extended planning phases. It orchestrates the complete implementation cycle including analytics, development planning, design planning, implementation, testing, and documentation for one User Story.

---

## Core Requirements

### Prerequisites
- Valid US-ID must be provided
- User Story must exist in /Requirements/EPICS/
- User Story should have requirements defined
- Project should be in implementable state
- MCP servers must be available (verified by analytics_setup_check agent)

### Validation Rules
- **MUST** strictly follow the Execution Flow and never ever skip any step
- **MUST** have valid US-ID in request
- **MUST** verify User Story exists before proceeding
- **MUST** initialize status files and verify MCP servers via development_initialization agent
- **MUST** read only Status_Orchestration.md for orchestration decisions (not STATUS.md)
- **MUST** use todo list for task tracking
- **MUST** ensure all implementation steps are executed
- **MUST NOT** skip any planning phase
- **MUST NOT** leave fragments (missing tests/docs)

### Orchestration Rules
- Act as pure orchestrator - never implement directly
- Follow orchestration conventions without exception
- Run testing loops until acceptance confirmed
- Include analytics phase before planning
- Include design planning after dev planning
- Ensure complete implementation flow
- Never commit code to github

---

## Configuration
- **Execution Mode**: Sequential with loops
- **Retry Policy**: Max 3 attempts for failed agents
- **Loop Limit**: Max 5 iterations for testing loops
- **Planning Mode**: Extended (analytics + design)

---

## Conventions & Standards
- **Error Handling**: @.claude/conventions/ErrorHandlingConventions.md
- **Testing**: @.claude/conventions/TestingConventions.md
- **Design**: @.claude/conventions/DesignConventions.md

### Timestamp Implementation Requirements
- **MUST** use actual system time, not simulated times
- **MUST** record timestamps in ISO 8601 format
- **MUST** calculate duration from actual start/end times
- **NEVER** use placeholder times like "14:23:45"
- **NEVER** estimate or hallucinate execution times

---

## Execution Flow

### Step 1: Validate User Story
- Verify US-ID provided in request
- Check User Story exists in filesystem
- Review existing requirements
- Stop with error if prerequisites not met

### Step 2: Initialize Implementation & Verify MCP Servers
- **Record**: Start time BEFORE calling agent
- **Agent**: development_initialization
- **Purpose**: Initialize STATUS.md and Status_Orchestration.md files, verify all MCP servers are operational
- **Input**: User Story ID and path
- **Expected Output**: Initialized status files + MCP verification report with pass/fail status
- **Error Handling**: Abort if verification fails
- **Record**: End time AFTER agent completes
- **Calculate**: Duration in milliseconds

### Step 3: Analytics Phase
- **Record**: Start time BEFORE calling agent
- **Agent**: analytics_currentstatusdetermination
- **Purpose**: Determine current status from PO and developer perspectives
- **Input**: User Story context and requirements
- **Expected Output**: Status analysis report
- **Error Handling**: Continue with warning if partial analysis
- **Record**: End time AFTER agent completes
- **Calculate**: Duration in milliseconds

### Step 5: Development Planning
- **Record**: Start time BEFORE calling agent
- **Agent**: planning_devplan_creation
- **Purpose**: Create or update DEVPLAN.md
- **Input**: User Story requirements and analytics
- **Expected Output**: DEVPLAN.md file
- **Error Handling**: Retry on failure, critical step
- **Record**: End time AFTER agent completes
- **Calculate**: Duration in milliseconds

### Step 6: Design Planning
- **Record**: Start time BEFORE calling agent
- **Agent**: planning_uidesign_creation
- **Purpose**: Extend DEVPLAN with design specifications
- **Input**: DEVPLAN.md and User Story context
- **Expected Output**: Enhanced DEVPLAN with UI/UX details
- **Error Handling**: Continue with warning if not applicable
- **Record**: End time AFTER agent completes
- **Calculate**: Duration in milliseconds

### Step 7: Implementation Loop
- **Record**: Start time for EACH iteration
- **Initial Agent**: development_basic_implementation
- **Purpose**: Implement DEVPLAN steps (code only, no tests)
- **Loop Structure**:
  1. Run development_basic_implementation
  2. Run testing_codingconventions
  3. If conventions fail: Fix and repeat
  4. Run testing_designconventions
  5. If conventions fail: Fix and repeat
  6. Run testing_epics_and_userstories (includes mobile/responsive testing for applicable User Stories)
  7. If acceptance fails: Return to Step 6 (planning)
- **Exit Condition**: All tests pass
- **Max Iterations**: 5
- **Important**: Tests will be created later by a dedicated test agent
- **Note**: Mobile/responsive testing is performed by testing_epics_and_userstories agent for User Stories involving responsive layouts or mobile features
- **Record**: End time for EACH sub-step
- **Calculate**: Duration for each operation

### Step 8: Update Documentation
- **Record**: Start time BEFORE calling agent
- **Agent**: documentation_basic_creation
- **Purpose**: Create/update documentation
- **Input**: Implementation details and changes
- **Expected Output**: Updated documentation files
- **Record**: End time AFTER agent completes
- **Calculate**: Duration in milliseconds

### Step 9: Finalize
- **Record**: Start time
- Update STATUS.md for User Story (detailed completion notes)
- Update Status_Orchestration.md for User Story (completion status only)
- Generate implementation summary
- Report results to user
- **Record**: End time
- **Calculate**: Total implementation duration

### Step 10: Cleanup (MANDATORY)
- **Purpose**: Free resources and prevent zombie processes
- **Actions**:
  1. Stop app server: `pkill -f "dotnet run.*5288" 2>/dev/null || true`
  2. Update Status_Orchestration.md App Server section:
     - Status: Stopped
     - Started: -
  3. Verify no remaining Foxra processes: `pgrep -f "Foxra" || echo "Clean"`
- **Important**: This step prevents accumulation of background processes that waste context
- **Note**: Always execute this step, even if previous steps failed

---

## Agent Specifications

### Required Agents
| Agent                                | Purpose                              | When Used | Execution Mode |
|--------------------------------------|--------------------------------------|-----------|----------------|
| development_initialization           | Status file init + MCP verification  | Step 2    | Sequential |
| analytics_currentstatusdetermination | Status analysis                      | Step 3    | Sequential |
| planning_devplan_creation            | Dev planning                         | Step 4    | Sequential |
| planning_uidesign_creation           | Design planning                      | Step 5    | Sequential |
| development_basic_implementation     | Implementation                       | Step 6    | Loop |
| testing_codingconventions            | Coding Convention testing            | Step 6    | Loop |
| testing_designconventions            | Design Convention testing            | Step 6    | Loop |
| testing_epics_and_userstories        | Acceptance testing                   | Step 6    | Loop |
| documentation_basic_creation         | Documentation                        | Step 7    | Sequential |

### Excluded Agents
| Agent | Reason for Exclusion |
|-------|---------------------|
| development_quickfix_implementation | For quick fixes only, not planned implementations |
| planning_testplan_creation | Not included in this extended flow |
| development_test_implementation | Focus on implementation, not test automation |

### Agent Dependencies
```
    development_initialization
                ↓
analytics_currentstatusdetermination
                ↓
    planning_devplan_creation
                ↓
    planning_uidesign_creation
                ↓
    development_basic_implementation
                ↓
    testing_codingconventions ─> if fails planning_devplan_creation
                ↓
    testing_designconventions ─> if fails planning_devplan_creation
                ↓
    testing_epics_and_userstories ─> if fails planning_devplan_creation
                ↓
    documentation_basic_creation
```

---

### Command Syntax
```
Development_Implement_US_Extended: EPIC-123 US-133
```

---

## Quality Assurance

### Success Criteria
- [ ] STATUS.md and Status_Orchestration.md created by development_initialization agent
- [ ] MCP servers verified via development_initialization agent
- [ ] Analytics phase completed
- [ ] DEVPLAN created/updated (without test steps)
- [ ] Design planning integrated
- [ ] User Story code implemented
- [ ] Coding conventions passing
- [ ] Acceptance criteria verified (manual/existing tests)
- [ ] Mobile/responsive layouts verified by testing_epics_and_userstories agent (if applicable)
- [ ] Documentation updated
- [ ] Both status files updated throughout
- [ ] No implementation fragments
- [ ] Note: Automated tests deferred to dedicated test agent

### Validation Checklist
- [ ] US-ID validated
- [ ] Status files initialized via development_initialization
- [ ] MCP servers verified via development_initialization
- [ ] Analytics performed
- [ ] Planning phases completed
- [ ] Implementation loop successful
- [ ] All testing phases passed
- [ ] No agents skipped
- [ ] Error handling implemented

### Implementation Quality
- [ ] Code follows conventions
- [ ] Design specifications met
- [ ] Documentation complete
- [ ] Build successful
- [ ] No linting errors
- [ ] Test creation deferred to test agent

---

## Examples

### Example 1: Standard Extended Implementation
```
Command: Development_Implement_US_Extended: EPIC-123 US-140
Flow:
  1. User Story Validation → US-140 exists
  2. Initialization → development_initialization agent → Status files created + All MCP servers operational
  3. Analytics → Current state analyzed
  4. Dev Planning → DEVPLAN created
  5. Design Planning → UI specs added
  6. Implementation → Success
  7. Convention Testing → Pass
  8. Acceptance Testing → Pass (includes mobile/responsive testing if applicable)
  9. Documentation → Updated
Result: US-140 fully implemented with design
```

### Example 2: With Testing Loops
```
Command: Development_Implement_US_Extended: US-141
Flow:
  1. User Story Validation → US-141 exists
  2. Initialization → development_initialization agent → Status files created + All MCP servers operational
  3. Analytics → Complexity identified
  4. Dev Planning → DEVPLAN created
  5. Design Planning → Complex UI defined
  6. Implementation → Success
  7. Convention Testing → Fail (naming)
  8. Fix Implementation → Success
  9. Convention Testing → Pass
  10. Acceptance Testing → Fail (missing feature)
  11. Update Planning → DEVPLAN refined
  12. Implementation → Success
  13. All Tests → Pass
  14. Documentation → Complete
Result: US-141 implemented after planning refinement
```

### Example 3: MCP Server Failure
```
Command: Development_Implement_US_Extended: US-142
Flow:
  1. User Story Validation → US-142 exists
  2. Initialization → development_initialization agent → FAILED
     - Status files created
     - serena: OK
     - context7: OK
     - chrome-devtools: FAILED
  3. Abort → "MCP server 'chrome-devtools' is not available"
Result: Implementation aborted, user notified to check MCP configuration
```
---

## Notes & Special Considerations

### Initialization & MCP Server Verification
- **Delegated to Agent**: All initialization and MCP verification is handled by development_initialization agent
- **Agent Responsibilities**:
  - Create STATUS.md (detailed, for agents)
  - Create Status_Orchestration.md (minimal, for orchestration)
  - Test serena, context7, and chrome-devtools MCP servers
  - Provide detailed pass/fail status for each server
  - Generate troubleshooting guidance for failures
- **Verification Method**: Agent performs simple test operations on each server
- **Failure Handling**: Agent reports failures, orchestrator aborts implementation
- **Error Message**: Agent provides clear indication of which server failed with troubleshooting steps

### Status File Templates (Reference - Agent Creates These)

#### STATUS.md Initialization Template (Detailed, for Agents)
```markdown
# US-[ID] Implementation Status

## Overview
- **User Story**: [US-ID]
- **Title**: [Title from US file]
- **Status**: In Progress
- **Start Date**: [Current timestamp]
- **Implementation Type**: Extended (with analytics and design)

## Progress Tracking
- [ ] MCP Servers Verified
- [ ] Analytics Completed
- [ ] DEVPLAN Created
- [ ] Design Planning Done
- [ ] Implementation Started
- [ ] Convention Testing Passed
- [ ] Acceptance Testing Passed
- [ ] Documentation Updated

## Implementation Notes
[To be updated during implementation]
```

### Status_Orchestration.md Initialization Template (Minimal, for Orchestration)
```markdown
# US-[ID] Orchestration Status

## Meta
- **US**: [US-ID]
- **Title**: [Title from US file]
- **Status**: InProgress
- **Start**: [ISO timestamp]
- **Current Phase**: MCP Verification

## Phase Status
- MCP Verification: ⏳ In Progress
- Analytics: ⏳ Pending
- DevPlan: ⏳ Pending
- DesignPlan: ⏳ Pending
- Implementation: ⏳ Pending (0/0 steps)
- CodingConventions: ⏳ Pending
- DesignConventions: ⏳ Pending
- Acceptance: ⏳ Pending
- Documentation: ⏳ Pending

## Blockers
None

## Next Action
Execute analytics_setup_check agent
```

### Planning Integration
- Analytics informs development planning
- Design planning extends technical planning
- Both planning phases can trigger re-planning in loops
- Planning documents preserved for future reference

### Loop Management
- Convention testing before acceptance testing
- Failed acceptance can trigger re-planning
- Limit iterations to prevent infinite loops

### Error Recovery
- MCP failure: Abort immediately with clear message
- Analytics failure: Continue with warning
- Planning failure: Critical, must retry
- Design planning failure: Continue if not UI-focused
- Implementation failure: Enter fix loop
- Test failure: Re-plan if needed

### Best Practices
- Always initialize with development_initialization agent first (creates status files + verifies MCP servers)
- Read only Status_Orchestration.md for orchestration decisions (keep context lean)
- Agents update both files: STATUS.md with details, Status_Orchestration.md with phase status only
- Run analytics even for "simple" stories
- Ensure design planning for UI changes
- Update Status_Orchestration.md file after each major phase

### Common Issues
- MCP server timeout: Check server configuration
- STATUS.md conflicts: Check if already exists
- Missing requirements: Use analytics to discover
- Design conflicts: Resolve in design planning
- Convention failures: Usually naming or structure
- Acceptance failures: Often missing requirements
- Timeout in analytics: Increase scope gradually

---

End of Development_Implement_US_Extended Command