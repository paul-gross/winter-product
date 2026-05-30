# Technical Approach Files (*.tech.md)

Technical approach files sit alongside their corresponding work documents and describe the *structural changes* to the codebase at an architectural level — what new projects, classes, and interfaces will exist and where they fit. Phase documents then provide step-by-step implementation instructions for those structures. Tech approach files are created **after** the work item has been promoted from the backlog and the overview has been approved.

## Purpose

The tech approach bridges product plans and implementation. It answers: what new projects, classes, interfaces, and methods will be created? How do they fit into the existing architecture? The reader should be able to review the approach and understand the structural changes without reading code.

## Naming Convention

Tech approach files mirror the document they accompany, with a `.tech.md` suffix:

```
00-overview.md          →  00-overview.tech.md
01-phase-one.md         →  01-phase-one.tech.md
```

Not every work item needs a tech approach. Use them when the work involves structural changes to the codebase (new classes, interfaces, projects, API endpoints). Simple work that modifies existing code within well-understood patterns may not need one.

## Content Guidelines

Tech approach files should be:

- **Concise** — Enough to review and understand the structural changes, not a full design document
- **Architectural** — Focus on new classes, interfaces, methods, and where they live in the project structure
- **Connected to the codebase** — Reference existing patterns, projects, and conventions so the approach fits naturally
- **No implementation code** — Describe what will exist, not how it will be coded line-by-line

## What to Include

- New projects, classes, or interfaces being introduced
- Which existing files or patterns are being extended
- New API endpoints or controller actions
- Database schema changes (if any)
- Key method signatures and their purpose
- Dependencies between new components
- Which existing patterns or conventions the new code follows

## What to Exclude

- Full method implementations or pseudocode (that belongs in phase documents)
- Business justification (that belongs in the overview)
- Testing strategies (that belongs in phase documents)
- Detailed error handling or edge cases

## Creation Process

Tech approach files are created by the `product-engineer` agent. This agent explores the codebase to understand existing patterns and writes the approach alongside the work item. The workflow:

1. Work item is promoted from backlog to `winter-product:/work/<name>/` and reviewed by the user
2. User requests a technical approach (or the `/refine` skill orchestrates it automatically)
3. The `product-engineer` agent explores the codebase and writes the `.tech.md` file
4. User reviews the technical approach before implementation begins
