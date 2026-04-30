# Overview & Phase Format

## Plan Types

The plan type informs how you frame the overview's "why".

- **Feature** — new user-facing functionality. Example: `user-notifications`.
- **Tech Debt** — improvements that don't add features (maintainability, performance, dependency upgrades). Example: `dependency-upgrade`.
- **Architectural** — major structural changes to codebase organization. Example: `project-restructure`.

## Directory Layout

Active plans live in `winter-product:/plans/`; completed ones in `winter-product:/archive/`. Every plan is a directory — even single-phase plans — so phases can be added later without reorganization.

```
winter-product:/plans/
└── feature-name/
    ├── 00-overview.md               # Business-focused overview (required)
    ├── 00-overview.tech.md          # Technical approach (optional, after overview approval)
    ├── 01-phase-one.md              # First implementation phase
    ├── 01-phase-one.tech.md         # Technical approach for phase one (optional)
    ├── 02-phase-two.md
    └── ...
```

For a single-document plan (no phases), put one file inside the directory as `00-{plan-name}.md`:

```
winter-product:/plans/
└── feature-name/
    └── 00-feature-name.md
```

## Naming

Plan directories use **kebab-case-lowercase**: `user-notifications`, `dependency-upgrade`, `project-restructure`.

File numbering:
- `00-overview.md` (or `00-{plan-name}.md` for single-doc plans) — always the primary document
- `01-*.md` through `99-*.md` — implementation phases in order

Archive directories add a `yyyy-MM-dd` date prefix reflecting when the last feature commit landed on the main branch (e.g., `2026-01-28-user-notifications`).

## Overview Structure (00-overview.md)

The overview is the **business-facing** document. It should be:

### Concise
Keep it brief - 1-2 pages maximum. Focus on the "why" and "what", not the "how".

### Business-Oriented
Written for non-technical stakeholders who need to understand:
- What problem this solves
- What value it delivers
- What success looks like
- High-level approach (without technical jargon)

### No Technical Details
Avoid implementation specifics like:
- Class names, file structures, or code patterns
- Specific libraries or framework details
- Database schemas or API endpoints
- Technical architecture decisions

### Example Overview Structure
```markdown
# Feature Name - Overview

## Business Objective
[1-2 sentences describing the business problem or opportunity]

## Success Criteria
- [Measurable outcome 1]
- [Measurable outcome 2]
- [Measurable outcome 3]

## High-Level Approach
[2-3 paragraphs explaining the general strategy without technical details]

## Phases
1. **Phase Name** - Brief description of what this phase delivers
2. **Phase Name** - Brief description of what this phase delivers
3. **Phase Name** - Brief description of what this phase delivers

## Dependencies
[Any prerequisites or related work that must be completed first]

## Risks & Considerations
[Known challenges or decisions that need to be made]
```

## Phase Structure (01-*.md, 02-*.md, etc.)

Phase documents contain **technical details** for implementation:

### Technical Specificity
Include implementation details like:
- File structures and component architecture
- Database schemas and migrations
- API endpoints and contracts
- Libraries, frameworks, and tools to use
- Code patterns and design decisions
- Testing strategies

### Actionable Steps
Break work into clear, implementable tasks that an agent can execute.

### Context for Decisions
Explain technical choices and trade-offs so future agents understand the rationale.
