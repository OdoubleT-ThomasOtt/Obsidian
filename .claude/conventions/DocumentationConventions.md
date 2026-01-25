# DocumentationConventions

## Purpose & Scope
This document enforces **ULTRA-MINIMAL** documentation. The goal is to write the absolute least documentation possible while still enabling basic system understanding.

---

## Core Principles

### 🚨 CRITICAL: Lean Documentation Mandate
**Documentation MUST be kept as lean and minimal as possible!**
- **LESS IS MORE**: Every word must earn its place
- **NO BLOAT**: Remove all unnecessary content ruthlessly
- **BREVITY FIRST**: If it can be said in 5 words, don't use 10
- **CODE IS TRUTH**: Let the code speak for itself whenever possible
- **ESSENTIAL ONLY**: Document only what cannot be understood from code alone

### Fundamental Rules
- **Absolute Minimalism**: Documentation must be the bare minimum needed
- **No Redundancy**: Never repeat what's obvious from code
- **Terse Writing**: Use bullet points, avoid prose
- **Structure**: Use consistent file organization and naming patterns
- **AI-Optimized**: Format documentation for easy parsing by AI agents
- **Single Source of Truth**: Never duplicate, always reference
- **Just-In-Time**: Update only when absolutely necessary

### Documentation Philosophy
- **Code > Documentation**: Well-written code needs minimal docs
- **Clarity through brevity**: Shorter is always better
- **Diagrams sparingly**: Only when they replace 100+ words
- **Facts only**: No opinions, interpretations, or fluff
- **Version control**: Track changes, not history lessons

---

## Implementation Guidelines

### Directory Structure
```
/Documentation/
├── Overview.md         # MASTER TOC - Lists ALL documentation files
├── Architecture/       # System architecture documentation
│   └── Architecture.md
├── Database/          # Database schema and design
│   └── Database.md
└── Application/       # Feature and functionality docs
    ├── Overview.md    # Application-specific TOC
    ├── Topic_*.md     # Feature docs (max 100 words)
    └── Topic_*_mermaid.md  # Process diagrams (if essential)
```

### Documentation Categories

#### Master Overview (ROOT)
- **Location**: `/Documentation/Overview.md`
- **Purpose**: Master index for ALL documentation files
- **Format**: File path + ultra-brief description (MAX 5 words)
- **Used by**: Documentation agents to find/update docs
- **Template**:
```markdown
# Documentation Index

## Architecture
- Architecture/Architecture.md - System structure overview
- Architecture/ComponentX.md - Component X patterns

## Database  
- Database/Database.md - Schema and tables
- Database/Migration.md - Migration procedures

## Application
- Application/Overview.md - Feature list
- Application/Topic_Feature1.md - Feature 1 details
- Application/Topic_Feature2.md - Feature 2 workflow

## Development
- Development/Port-Management.md - Port configuration
[etc - ALL files with 5-word MAX descriptions]
```

#### Architecture Documentation
- **Location**: `/Documentation/Architecture/`
- **Filename**: `Architecture.md`
- **Required Sections** (MAX 75 words total):
  - Type: [2-3 words]
  - Components: [Bullet list]
  - External: [List integrations]

#### Database Documentation
- **Location**: `/Documentation/Database/`
- **Filename**: `Database.md`
- **Required Sections** (MAX 50 words total):
  - DB Type: [One word]
  - Tables: [List main ones]
  - Issues: [Critical only]

#### Application Documentation
- **Location**: `/Documentation/Application/`
- **File Types**:
  - `Overview.md`: TOC only (no summaries)
  - `Topic_[Feature].md`: Max 100 words per file
  - `Topic_[Feature]_mermaid.md`: Only if essential

---

## Standards & Specifications

### File Naming Conventions
| Type | Pattern | Example |
|------|---------|---------|
| Master Index | `Overview.md` (root) | `/Documentation/Overview.md` |
| Architecture | `Architecture.md` | `Architecture.md` |
| Database | `Database.md` | `Database.md` |
| Feature Topic | `Topic_[FeatureName].md` | `Topic_UserAuthentication.md` |
| Diagrams | `Topic_[FeatureName]_mermaid.md` | `Topic_OrderFlow_mermaid.md` |
| Section Overview | `Overview.md` (subdirs) | `Application/Overview.md` |

### Content Structure Template

#### Feature Documentation (Topic_*.md)
```markdown
# [Feature Name]

## Purpose
[One sentence - what it does]

## Technical
- Components: [List key classes/services]
- Flow: [A→B→C notation]
- Config: [Key settings only]

## Issues
[Known problems - bullets only]
```

#### Mermaid Diagram Template
```markdown
# [Feature] Flow

\```mermaid
graph TD
    A --> B --> C
\```
[No descriptions - diagram must be self-explanatory]
```

---

## Best Practices

### Writing Guidelines
- **Maximum 1 sentence per point**
- **No paragraphs** - bullets only
- **No code examples** - reference file:line instead
- **No explanations** - state facts only
- **Diagrams rarely** - only for truly complex flows

### Maintenance Strategy
- **Update only when broken**
- **Delete before adding**
- **Question every word**
- **No archives** - delete outdated content
- **No automation** - keep it manual and minimal
- **Master Overview.md** - MUST be kept current for agents

### AI Agent Optimization
- **Terse headings** (2-3 words max)
- **No metadata** - waste of space
- **Simple structure** - flat is better
- **Plain text** - no fancy formatting
- **Direct language** - no hedging

---

## Quality Assurance

### Documentation Checklist
- [ ] **Under 100 words per topic**
- [ ] **No redundancy with code**
- [ ] **Bullet points only**
- [ ] **Essential info only**
- [ ] **Can it be shorter?**
- [ ] **Listed in /Documentation/Overview.md**

### Validation Criteria
- **Word count minimized**
- **Zero duplication**
- **Code speaks for itself**
- **Delete before adding**

---

## Examples

### Architecture.md Example (LEAN)
```markdown
# Architecture

## Type
Layered, Blazor Server

## Stack
- Frontend: Blazor
- Business: Services  
- Data: EF + SQLite

## External
- Payment API
- SMTP
- Azure AD
```

### Topic Documentation Example (LEAN)
```markdown
# OrderProcessing

## Purpose
Order lifecycle management

## Technical
- Components: OrderService, OrderRepository
- Flow: UI→ViewService→Business→DB
- Config: MaxItems=100, Timeout=30min

## Issues
- Batch limit: 500
- Inventory lag: 2s
```

---

## Notes & Exceptions

### Special Considerations
- **Security docs**: Separate file, minimal details
- **APIs**: OpenAPI/Swagger only if required
- **Legacy**: Don't document, refactor instead
- **Generated docs**: Avoid entirely
- **External**: Link only, never copy

### Tool Integration
- **NO GENERATORS** - all manual, all minimal
- **Mermaid**: Only if saves 200+ words
- **No wikis** - too much overhead
- **No automation** - encourages bloat

---

## Requirements Documentation Separation of Concerns

### User Stories vs. DEVPLAN
**CRITICAL SEPARATION**: Technical implementation details MUST be kept separate from User Stories.

#### User Stories (Product Owner Perspective)
- **Location**: `/Requirements/EPICS/EPIC-ID/US-ID/US-ID.md`
- **Purpose**: Define WHAT and WHY from business/user perspective
- **Content**:
  - User story format: "As a X, I want Y, so that Z"
  - Acceptance Criteria (Given-When-Then with testable outcomes)
  - High-level Implementation Tasks (3-7 one-sentence steps)
  - Dependencies and Definition of Done
- **MUST NOT contain**:
  - Code examples or snippets
  - Technical implementation details
  - Architecture decisions
  - Namespaces, file paths, or class structures
  - Step-by-step technical instructions

#### DEVPLAN (Developer Perspective)
- **Location**: `/Requirements/EPICS/EPIC-ID/US-ID/DEVPLAN.md`
- **Purpose**: Define HOW to implement technically
- **Created by**: `planning_devplan_creation` agent
- **Content**:
  - Detailed implementation steps with code examples
  - Technical architecture decisions
  - Specific file paths, namespaces, class structures
  - Convention checkpoints and validation steps
  - Edge cases and technical considerations

#### Rationale
- **Prevents Redundancy**: Technical details documented once in DEVPLAN
- **Proper Separation**: PO-focused docs vs. Dev-focused docs
- **Maintainability**: Coding convention changes only affect DEVPLAN, not all User Stories
- **Agile Best Practice**: User Stories focus on value, not implementation

#### Template Reference
- **User Story Template**: `/.claude/templates/UserStory-Template.md`
- **Note in Template**: Explicitly states technical details belong in DEVPLAN

---

End of DocumentationConventions