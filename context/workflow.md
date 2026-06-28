# Backlog → Work → Archive Lifecycle

The end-to-end lifecycle for adding to the backlog, promoting items to active work, and archiving completed work. See [`index.md`](./index.md) for the underlying purpose and ongoing maintenance guidance.

## Adding Backlog Items

When a user requests a new feature or improvement:

1. **Determine the item type**
   - `.idea.md` — rough concept, needs design thinking
   - `.todo.md` — small, concrete, well-defined (use the `todo` skill)
   - `.work.md` — product-level plan, potentially multi-phase

2. **Choose a priority bucket** — the `backlog/` subdirectories, ordered by urgency:
   - `01-now` — pick up as soon as the current branch merges
   - `02-next` — work on after the current item, but no rush
   - `05-near` — relevant in the next few weeks
   - `10-future` — someday/maybe; keep it captured but don't schedule

   The bucket list is discovered at runtime (`ls backlog/`), so adding or renaming a bucket on disk needs no skill or doc change beyond this list.

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

Use the `refine` skill to take a backlog item to work-ready quality and promote it — it performs evaluate → promote → technical approach → phases. See [`../skills/refine/SKILL.md`](../skills/refine/SKILL.md) for the full procedure.

After the tech approach lands — or whenever a plan changes significantly — the `plan-review` skill spawns a cold `plan-reviewer` agent that checks the work item against these specs and reports must-fix findings before implementation begins.

For a manual promotion (without `refine`):

1. Confirm the item is solid (clear business objective, success criteria, approach, phases)
2. Create `winter-product:/work/<name>/`
3. Move the backlog file in as `00-overview.md`
4. Commit as `product(<name>): promote from backlog`
5. Spawn the `product-engineer` agent to write the technical approach — `.tech.md` files per [tech-approach.md](./tech-approach.md) with the verification capability matrix per [capability-matrix.md](./capability-matrix.md), plus numbered phase documents (`01-<phase-name>.md`, …) for multi-phase work whose acceptance criteria reference the matrix's capability IDs. Commit as `product(<name>): add technical approach`.

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

