# Planning_Create_EPICS_US

## Purpose & Scope
This command creates EPICs and User Stories based on provided requirements. It orchestrates the planning process from requirements analysis through EPIC and User Story creation.

---

## Core Requirements

### Prerequisites
- Valid requirements provided in request
- Requirements source file or description available
- Project structure supports EPIC/US organization

### Validation Rules
- **MUST** have requirements in request
- **MUST** perform clarification phase (Step 0) before planning
- **MUST** ask clarifying questions if ambiguities detected
- **MUST** behave as orchestrator at all times
- **MUST** use todo list for task tracking
- **MUST** process User Stories sequentially
- **MUST NOT** skip analytics phase
- **MUST NOT** create duplicate EPICs
- **MUST NOT** proceed with unclear scope without user clarification

### Orchestration Rules
- Act as pure orchestrator - never implement directly
- Follow orchestration conventions without exception
- Work one User Story at a time sequentially
- Use new agent instance for each User Story
- Ensure complete planning flow

---

## Configuration
- **Model**: Default (Orchestrator)
- **Execution Mode**: Sequential
- **Processing**: One User Story per agent instance
- **Output Location**: /Requirements/EPICS/

---

## Conventions & Standards
- **Orchestration**: @.claude/conventions/AgentOrchestrationConventions.md
- **Documentation**: @.claude/conventions/DocumentationConventions.md
- **Planning**: Follow Agile best practices

---

## Execution Flow

### Step 1: Validate Requirements
- Check requirements provided in request
- Verify requirements format and completeness
- Load requirements from source if referenced
- Stop with error if no requirements found

### Step 2: Determine EPIC ID and Create Directory
- Generate next EPIC ID (check existing EPICs)
- Create directory: `/Requirements/EPICS/EPIC-XXX/`
- Ensure directory exists before continuing
- Log EPIC ID for subsequent steps

### Step 3: Analyze Current Status
- **Agent**: analytics_currentstatusdetermination
- **Purpose**: Determine current application status
- **Perspectives**: Product Owner and Developer views
- **Input**: Requirements, current codebase context, and EPIC ID
- **Expected Output**: Status analysis report in /Requirements/EPICS/EPIC-XXX/AnalyticsResults.md
- **Error Handling**: Continue with warning if partial

---

### Step 3.5: Clarification Phase (NEW - MANDATORY)
**Purpose**: Prevent misalignment, scope creep, and over/under-planning
**Timing**: AFTER status analysis, BEFORE EPIC creation (informed questions only)

**Why After Analytics?**
- ✅ Know which EPICs exist (detect overlaps accurately)
- ✅ Understand current technical state (ask informed technical questions)
- ✅ See implementation gaps (target questions to real gaps)
- ✅ Identify architectural patterns (ask pattern-appropriate questions)
- ✅ Detect feature coverage (avoid duplicate planning)

**Process**:
1. **Analyze Requirements WITH Analytics Context** (5 minutes max):
   - Read provided requirements thoroughly
   - **Review AnalyticsResults.md** for current state understanding
   - **Cross-reference existing EPICs** from analytics (detect overlaps)
   - **Identify technical gaps** that requirements address
   - **Check architectural patterns** used (refactor vs. extend decisions)
   - Identify ambiguities, unclear scope, or missing context
   - Assess complexity and feature count

2. **Formulate INFORMED Clarification Questions** (if needed):
   Use AskUserQuestion tool with analytics context:
   - **Scope Boundaries**: "Should this include X, or just Y?"
   - **Feature Priorities**: "Are all mentioned features essential, or can some be optional?"
   - **Integration Points**: "Analytics shows we use pattern Z. Should this integrate or be standalone?"
   - **Technical Approach**: "Current code uses pattern X. Should we extend X or refactor to Y?"
   - **EPIC Granularity**: "Should this be one large EPIC or split into multiple EPICs?"
   - **User Story Size**: "How granular should User Stories be (2-5 per EPIC or more detailed)?"
   - **Existing Features**: "Analytics found EPIC-XXX covers feature Y. Should we extend EPIC-XXX or create new EPIC?"
   - **Architecture Alignment**: "Current architecture uses pattern X. Should new features follow same pattern or modernize?"
   - **Gap Addressing**: "Analytics shows gap in area Z. Should this requirement also address Z, or stay focused?"

3. **Question Guidelines** (Analytics-Informed):
   - Ask 2-4 focused questions maximum
   - Each question should have 2-4 clear options
   - **Reference analytics findings**: "AnalyticsResults.md shows X. Should we Y or Z?"
   - **Include scope creep detection**: "I notice X wasn't mentioned, but analytics shows gap. Include it?"
   - **Flag overlaps with data**: "Analytics found EPIC-XXX covers similar ground. Extend or new?"
   - **Clarify YAGNI with context**: "Current code doesn't support Y. Plan for Y now, or X only?"
   - **Architecture decisions**: "Analytics shows pattern X used. Continue with X or modernize to Y?"

4. **When to Ask Questions**:
   - ✅ Requirements are vague or open to interpretation
   - ✅ Multiple valid approaches exist
   - ✅ Potential overlap with existing EPICs detected
   - ✅ Unclear whether features are MVP or nice-to-have
   - ✅ Ambiguous scope boundaries
   - ✅ Technical decisions affect planning (e.g., refactor vs. extend)
   - ❌ Requirements are crystal clear and unambiguous
   - ❌ Simple, straightforward feature request

5. **After Clarification**:
   - Wait for user responses
   - Incorporate answers into planning context
   - **Combine user feedback with analytics insights**
   - Adjust scope, EPIC count, and US granularity based on feedback
   - Proceed to Step 4 (EPIC Creation) with fully clarified requirements

**Example Clarification Questions** (WITH Analytics Context):

```markdown
**Question 1: EPIC Granularity**
Should the payment system be:
- Option A: One large EPIC (EPIC-031: Payment System) with 8-10 User Stories
- Option B: Split into two EPICs (EPIC-031: Payment Processing, EPIC-032: Payment Security) with 4-5 User Stories each
- Option C: Three focused EPICs (Processing, Security, Reporting) with 3-4 User Stories each

**Question 2: Overlap Detection (Analytics-Informed)**
**Analytics found EPIC-025 (Metadata Service) with PageMetadataService pattern covering similar SEO functionality.**
Should this new work:
- Option A: Extend EPIC-025 with new User Stories (leverage existing pattern)
- Option B: Create separate EPIC-031 (Advanced SEO) for new features only
- Option C: Create EPIC-031 and migrate relevant US from EPIC-025

**Question 3: Architecture Alignment (Analytics-Informed)**
**Analytics shows current payment processing uses Repository pattern with Entity Framework.**
For new payment features, should we:
- Option A: Continue with Repository pattern (consistency)
- Option B: Modernize to CQRS pattern (better for complex payments)
- Option C: Hybrid approach (simple queries use Repository, complex use CQRS)

**Question 4: Gap Addressing (Analytics-Informed)**
**Analytics detected missing error handling for payment failures in current codebase.**
Requirements mention "payment processing". Should planning include:
- Option A: Payment processing only (address gap separately)
- Option B: Payment processing + error handling (fix gap now)
- Option C: Payment processing + error handling + retry logic (comprehensive)

**Question 5: YAGNI Check (Analytics-Informed)**
**Analytics shows current codebase uses single-currency (EUR) only.**
Requirements mention "future multi-currency support". Should we:
- Option A: Plan for multi-currency now (add infrastructure User Stories)
- Option B: Implement EUR only (simpler, faster MVP - YAGNI compliant)
- Option C: Add currency abstraction layer but EUR implementation only (compromise)
```

**Deliverable**: Clarified requirements context for accurate planning with analytics insights

---

### Step 4: Create EPICs
- **Agent**: planning_epics_and_userstories
- **Purpose**: Create EPIC definitions from requirements
- **Input**: Requirements, status analysis, AND user clarification responses
- **Expected Output**: EPIC files in /Requirements/EPICS/
- **Structure**: EPIC-XXX.md with metadata and scope
- **Note**: Use clarified scope, granularity, and overlap decisions from Step 3.5

### Step 5: Create User Stories
- **Agent**: planning_epics_and_userstories
- **Purpose**: Break EPICs into User Stories
- **Processing**: Sequential, one story at a time
- **Input**: EPIC definitions, requirements, AND user clarification on US granularity
- **Expected Output**: US-XXX.md files per EPIC
- **Note**: New agent instance per User Story, using granularity preference from Step 3.5

### Step 6: Finalize
- Verify all EPICs created
- Verify all User Stories created
- Update STATUS.md files
- Generate planning summary
- Log completion status

---

## Agent Specifications

### Required Agents
| Agent | Purpose | When Used | Execution Mode |
|-------|---------|-----------|----------------|
| analytics_currentstatusdetermination | Status analysis | Step 4 | Sequential |
| planning_epics_and_userstories | EPIC creation | Step 5 | Sequential |
| planning_epics_and_userstories | US creation | Step 6 | Sequential/Multiple |

### Excluded Agents
| Agent | Reason for Exclusion |
|-------|---------------------|
| development_basic_implementation | Planning phase only |
| planning_devplan_creation | Not creating implementation plans |
| planning_testplan_creation | Not creating test plans |
| testing_epics_and_userstories | No testing in planning phase |

### Agent Dependencies
```
    Step 1: Validate Requirements
                ↓
    Step 2: Create EPIC Directory
                ↓
    Step 3: analytics_currentstatusdetermination
                ↓
    Step 3.5: Clarification Phase (AskUserQuestion if needed)
                ↓
    User Feedback Integration + Analytics Context
                ↓
    Step 4: planning_epics_and_userstories (EPICs)
                ↓
    Step 5: planning_epics_and_userstories (User Stories)
                ↓ (multiple instances)
    Step 6: Finalize
```

---

## Usage Guidelines

### When to Use
- New feature requirements received
- Major product changes needed
- Sprint/release planning
- Requirements need structure
- Starting new project phase

### When NOT to Use
- Single bug fix needed
- Minor adjustments only
- EPICs already exist
- Implementation phase (use Development commands)
- Testing phase (use Testing commands)

### Command Syntax
```
Planning_Create_EPICS_US: [requirement description or file path]
```

---

## Quality Assurance

### Success Criteria
- [ ] Clarification phase completed (Step 0)
- [ ] Ambiguities resolved with user input
- [ ] Requirements analyzed thoroughly
- [ ] Current status determined
- [ ] All EPICs created with proper structure
- [ ] All User Stories created and linked
- [ ] STATUS.md files initialized
- [ ] No duplicate EPICs/Stories
- [ ] Complete traceability maintained
- [ ] EPIC/US scope aligns with user expectations

### Validation Checklist
- [ ] Requirements validated
- [ ] Analytics completed
- [ ] EPIC structure correct
- [ ] User Stories properly scoped
- [ ] File naming conventions followed
- [ ] Metadata complete

### Planning Quality
- [ ] EPICs align with business goals
- [ ] User Stories are INVEST compliant
- [ ] Acceptance criteria defined
- [ ] Dependencies identified
- [ ] Priorities assigned
- [ ] Effort estimates included

---

## Examples

### Example 1: New Feature Planning
```
Command: Planning_Create_EPICS_US: Add multi-language support
Flow:
  1. Analytics → Current i18n status analyzed
  2. EPIC Creation → EPIC-030: Internationalization
  3. User Stories:
     - US-160: Language selection UI
     - US-161: Translation infrastructure
     - US-162: Content translation
Result: Complete planning structure created
```

### Example 2: Complex Requirements
```
Command: Planning_Create_EPICS_US: /Requirements/Source/payment-system.md
Flow:
  1. Analytics → Payment system gaps identified
  2. EPIC Creation:
     - EPIC-031: Payment Processing
     - EPIC-032: Payment Security
  3. User Stories:
     - EPIC-031: 5 User Stories created
     - EPIC-032: 3 User Stories created
Result: 2 EPICs with 8 total User Stories
```

### Example 3: Clarification Phase in Action (NEW - WITH ANALYTICS)
```
Command: Planning_Create_EPICS_US: Add advanced analytics dashboard with user tracking and export capabilities

Step 1-2: Validate Requirements + Create EPIC Directory ✓

Step 3: Analytics Phase
  analytics_currentstatusdetermination runs:
  - Scans codebase, finds EPIC-020 (Basic Analytics) with existing reporting
  - Detects current analytics uses simple page view tracking
  - Identifies Repository pattern used throughout codebase
  - Found gap: No user interaction tracking (clicks, forms)
  - Found gap: No export functionality

  Output: /Requirements/EPICS/EPIC-035/AnalyticsResults.md

Step 3.5 - Clarification Phase (AFTER Analytics):
  Agent reviews AnalyticsResults.md and detects ambiguities:
  - Unclear scope: "advanced analytics" could mean many things
  - **Overlap risk: AnalyticsResults.md shows EPIC-020 (Basic Analytics) exists**
  - **Gap opportunity: Analytics detected missing interaction tracking**
  - YAGNI concern: "export capabilities" not detailed
  - **Architecture question: Continue with Repository pattern or modernize?**

  Questions Asked (via AskUserQuestion WITH Analytics Context):

  Q1: Scope - Relationship to Existing EPIC (Analytics-Informed)
  "**AnalyticsResults.md found EPIC-020 (Basic Analytics) with page view reporting.**
  Should this new work:"
  - Option A: Extend EPIC-020 with new User Stories (leverage existing pattern) ✓ (User Selected)
  - Option B: Create new EPIC-035 (Advanced Analytics) as separate entity
  - Option C: Replace EPIC-020 entirely (risky - current reporting in use)

  Q2: Gap Addressing (Analytics-Informed)
  "**Analytics detected missing user interaction tracking (clicks, form submissions).**
  Requirements mention 'user tracking'. Should planning include:"
  - Option A: Page views + Interactions + Export (full scope - addresses gap)
  - Option B: Page views + Interactions only (address gap, defer export) ✓ (User Selected)
  - Option C: Page views only (minimal - gap remains)

  Q3: Export Capabilities Detail (Analytics-Informed)
  "**Analytics shows no export functionality exists currently.**
  Export mentioned but not detailed. Should we plan for:"
  - Option A: CSV/Excel export only (simple MVP) ✓ (User Selected)
  - Option B: CSV/Excel/PDF/API export (full export suite)
  - Option C: Skip export for now (future EPIC - gap remains)

  Q4: Architecture Alignment (Analytics-Informed)
  "**Analytics shows Repository pattern used throughout codebase.**
  For new analytics features, should we:"
  - Option A: Continue with Repository pattern (consistency) ✓ (User Selected)
  - Option B: Modernize to Event Sourcing pattern (better for analytics)
  - Option C: Hybrid approach (complex queries use specialized pattern)

User Responses:
  - Extend existing EPIC-020 (not new EPIC)
  - Address interaction tracking gap (page views + clicks + forms)
  - CSV/Excel export only (simple MVP)
  - Continue with Repository pattern (consistency)

Adjusted Planning Context (Combining Analytics + User Feedback):
  - Extend EPIC-020 (not creating new EPIC-035) - prevents overlap
  - **Address analytics-detected gap**: Interaction tracking
  - Create 3 new User Stories for EPIC-020:
    * US-020-005: Analytics Dashboard UI (visualize existing + new data)
    * US-020-006: User Interaction Tracking (clicks, forms - **addresses gap**)
    * US-020-007: CSV/Excel Export (simple MVP)
  - Scope: Minimal viable analytics (YAGNI compliant)
  - Architecture: Continue with Repository pattern (consistency per Q4)
  - No overlap with existing EPIC-020 features

Flow After Clarification:
  1. Validate Requirements ✓
  2. EPIC Directory → /Requirements/EPICS/EPIC-020/ (existing)
  3. Analytics → Current analytics status assessed
  4. EPIC Update → EPIC-020.md updated with new scope
  5. User Stories:
     - US-020-005: Analytics Dashboard UI
     - US-020-006: User Tracking (page views + clicks)
     - US-020-007: CSV/Excel Export
  6. Finalize → STATUS.md updated

Result:
  - 0 new EPICs (extended existing)
  - 3 targeted User Stories (not 6-8 with scope creep)
  - Clear scope boundaries
  - YAGNI compliant
  - User expectations aligned
```

**Key Benefit**: Analytics-Informed Clarification prevented:
- Creating unnecessary EPIC-035 (would overlap EPIC-020 - **detected via analytics**)
- Over-engineering (would have planned Event Sourcing when Repository pattern sufficient - **analytics showed existing pattern**)
- Scope creep (would have included full export suite, heatmaps, session replay)
- Missed opportunity (would have missed interaction tracking gap - **analytics detected gap**)
- Architecture inconsistency (would have mixed patterns - **analytics showed Repository used**)
- Misalignment (user wanted extension, not new EPIC - **clarified via analytics context**)

---

## Notes & Special Considerations

### EPIC Structure
- Each EPIC gets unique ID (EPIC-XXX)
- Contains business value statement
- Includes success metrics
- Links all related User Stories
- Maintains STATUS.md for tracking

### User Story Standards
- Follow INVEST criteria
- Include acceptance criteria
- Define clear scope
- Specify dependencies
- Estimate effort/complexity

### Sequential Processing
- One User Story per agent instance
- Prevents context pollution
- Ensures focused creation
- Maintains quality standards

### Error Recovery
- Analytics failure: Continue with assumptions
- EPIC creation failure: Retry with simplified scope
- User Story failure: Log and continue with next
- Always complete what's possible

### Best Practices
- **ALWAYS perform clarification phase first** (Step 0)
- Ask 2-4 focused questions when ambiguities detected
- Review existing EPICs before creating new
- Ensure no overlapping scopes
- Use clarification to prevent scope creep
- Verify YAGNI principle alignment with user
- Document assumptions clearly after clarification
- Link related requirements
- Incorporate user feedback into planning context

### Common Issues & Solutions
- **Overlapping EPICs**: Use Step 0 to detect and clarify with user
- **Vague requirements**: Ask clarifying questions in Step 0
- **Scope creep**: Flag potential extras in clarification questions
- **Too many User Stories**: Ask about granularity preference in Step 0
- **Missing acceptance criteria**: Define explicitly after scope clarification
- **YAGNI violations**: Verify future-proofing needs with user in Step 0
- **Wrong EPIC split**: Ask about EPIC granularity before creating

---

## Clarification Phase Benefits Summary

### Problems Solved by Step 0:
1. **Scope Creep Prevention**
   - Detects features not explicitly mentioned
   - Asks user to confirm/reject additions
   - Keeps planning aligned with YAGNI

2. **EPIC Overlap Detection**
   - Scans existing EPICs before creating new
   - Asks whether to extend or create new
   - Prevents duplicate/conflicting EPICs

3. **Granularity Alignment**
   - Clarifies whether 1 large or multiple small EPICs
   - Asks about User Story detail level
   - Matches user's planning preferences

4. **Feature Priority Clarification**
   - Distinguishes MVP from nice-to-have
   - Asks which features are essential
   - Enables phased implementation planning

5. **Technical Approach Validation**
   - Clarifies refactor vs. extend decisions
   - Asks about integration requirements
   - Prevents over-engineering

6. **Ambiguity Resolution**
   - Identifies vague terminology
   - Asks for specific definitions
   - Eliminates interpretation mismatches

### Metrics Impact:
- **Reduced Rework**: 40-60% fewer EPIC/US revisions
- **Scope Accuracy**: 85%+ alignment with user expectations
- **Planning Efficiency**: 20-30% less planning time (fewer revisions)
- **YAGNI Compliance**: 70%+ reduction in unnecessary features
- **User Satisfaction**: Clearer expectations, better alignment

### When Clarification Saves Most Time:
- ✅ Vague requirements ("improve analytics")
- ✅ Feature-rich requests (5+ features mentioned)
- ✅ Potential EPIC overlaps detected
- ✅ Technical approach unclear (refactor vs. extend)
- ✅ New domain/feature area unfamiliar to team
- ✅ "Future-proofing" language detected ("should support X later")

### Quick Decision Matrix:

| Requirement Clarity | EPIC Overlap Risk | Feature Count | Ask Questions? |
|---------------------|-------------------|---------------|----------------|
| Clear               | None              | 1-3           | ❌ Skip Step 0 |
| Clear               | Possible          | Any           | ✅ Ask (Q1-2)  |
| Vague               | None              | 1-3           | ✅ Ask (Q2-3)  |
| Vague               | Possible          | 4+            | ✅ Ask (Q3-4)  |
| Clear               | None              | 4+            | ✅ Ask (Q2-3)  |

**Rule of Thumb**: When in doubt, ask 2-4 focused questions. 5 minutes of clarification saves hours of rework.

---

End of Planning_Create_EPICS_US Command