# Backlog → Work → Archive Lifecycle

The end-to-end lifecycle for adding to the backlog, promoting items to active work, and archiving completed work. See [`index.md`](./index.md) for the underlying purpose and ongoing maintenance guidance.

## Adding Backlog Items

When a user requests a new feature or improvement:

1. **Determine the item type**
   - `.idea.md` — rough concept, needs design thinking
   - `.todo.md` — small, concrete, well-defined (use the `/todo` skill)
   - `.work.md` — product-level plan, potentially multi-phase

2. **Choose a priority bucket**
   - `01-now`, `02-next`, `05-near`, or `10-future`

3. **Write the item**
   - Use kebab-case-lowercase for the filename
   - For `.work.md` items, focus on business value; keep technical details out (see [overview-format.md](./overview-format.md))
   - For `.todo.md` items, follow the format in [todos.md](./todos.md)
   - For `.idea.md` items, capture the concept freely

4. **Commit**
   - Use `product(<name>)` as the commit type for new `.idea.md` or `.work.md` items
   - Use `todo(<name>)` for new `.todo.md` items

5. **Request Review**
   - Present for approval before promoting to work

## Refining and Promoting to Work

Use the `/refine` skill to take a backlog item to work-ready quality and promote it.

The refine flow:

1. **Evaluate** — score the item against the quality bar in [overview-format.md](./overview-format.md) and [writing-style.md](./writing-style.md). Identify missing sections, unresolved questions, and weak reasoning.
2. **Interactive refinement** — fill gaps with targeted user questions until the item is solid.
3. **Promote** — move `backlog/<bucket>/<name>.<type>.md` → `work/<name>/00-overview.md` (the canonical overview filename per [overview-format.md](./overview-format.md)). Commit as `product(<name>): promote from backlog`.
4. **Technical approach** — spawn the `product-engineer` agent to explore the codebase and write `.tech.md` files per [tech-approach.md](./tech-approach.md), including the verification capability matrix per [capability-matrix.md](./capability-matrix.md).
5. **Phase documents** — for multi-phase work, create numbered `01-<phase-name>.md`, `02-<phase-name>.md`, etc. with the technical specificity needed for implementation. Acceptance criteria reference capability IDs from the tech approach's matrix ("verify via `err.smtp` + `obs.audit`"); a phase that references a `wanted` row schedules that tooling work before the dependent feature work.
6. **Commit** the tech approach and phases as `product(<name>): add technical approach`.

For a manual promotion (without `/refine`):

1. Confirm the item is solid (clear business objective, success criteria, approach, phases)
2. Create `winter-product:/work/<name>/`
3. Move the backlog file in as `00-overview.md`
4. Commit as `product(<name>): promote from backlog`
5. Follow steps 4–6 above for the technical approach

## Implementation

Implementation happens in feature worktrees, not in this extension. The agent executing the plan reads from `winter-product:/work/<name>/` for direction.

## Archiving Completed Work

When work is complete (all phases merged to the main branch):

1. Identify the date of the last feature commit on the main branch for that item
2. Move the work directory to `archive/` with a date prefix:
   ```
   winter-product:/work/user-notifications/  →  winter-product:/archive/2026-01-28-user-notifications/
   ```
3. The date format is `yyyy-MM-dd`
4. Use `feat(<name>)` as the commit type
5. The archive serves as a historical record of completed work and can be referenced for similar future efforts

For a completed TODO that didn't grow into a multi-file directory, archive as a flat file: `archive/yyyy-MM-dd-todo-<name>.md`.

## Maintenance

Update an item when:
- Requirements change during review
- New phases are needed
- Phases are completed (mark as done or archive)
- Technical approach changes significantly
- Priority changes (move between backlog buckets)

