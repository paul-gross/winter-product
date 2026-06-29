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

### Change skeleton

Emit structural changes as concise tables — one per change type present in the work. Descriptions are one-liners in cells; the table structure carries the detail. Omit a table if the work has no changes of that type.

**Code changes** — new or modified classes, interfaces, and methods:

| Module | Class / Method | Change | Verifies via |
|--------|----------------|--------|-------------|
| `module-name` | `dotted.package.ClassName.method_name(param: Type) → Return` | One-line description of the change | `capability-id` |

**API endpoints** — new or modified routes:

| Module | Method | Path | Description | Verifies via |
|--------|--------|------|-------------|-------------|
| `module-name` | `POST` | `/api/resource` | One-line description | `capability-id` |

**Schema deltas** — new tables, columns, or migrations:

| Module | Migration | Table | Change | Verifies via |
|--------|-----------|-------|--------|-------------|
| `module-name` | `migration_name` | `table_name` | One-line description of the change | `capability-id` |

The **Verifies via** cell names a capability ID from the tech approach's verification capability matrix (below). When the verification method that capability ID names is absent from the application's verifiability matrix, record a `wanted` row in the capability matrix and schedule that tooling work before the dependent change — see [capability-matrix.md](./capability-matrix.md).

Documentation-only changes follow the same pattern using a **Documentation changes** table with columns `Module | Document | Change | Verifies via`.

### Verification capability matrix

A per-module table of the verification capabilities the work needs, with missing tooling marked `wanted`. Format: [capability-matrix.md](./capability-matrix.md). Exemplar: [exemplars/capability-matrix.tech.md](./exemplars/capability-matrix.tech.md).

## What to Exclude

- Full method implementations or pseudocode (that belongs in phase documents)
- Business justification (that belongs in the overview)
- Free-text test plans (those belong in phase documents — the verification capability matrix above is the only testing content a `.tech.md` carries)
- Detailed error handling or edge cases

## Creation Process

Tech approach files are created by the `product-engineer` agent. This agent explores the codebase to understand existing patterns and writes the approach alongside the work item. The workflow:

1. Work item is promoted from backlog to `winter-product:/work/<name>/` and reviewed by the user
2. User requests a technical approach (or the `refine` skill orchestrates it automatically)
3. The `product-engineer` agent explores the codebase and writes the `.tech.md` file
4. User reviews the technical approach before implementation begins
