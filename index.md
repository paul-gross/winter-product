# Product workflow

A prioritized backlog, an active work area, and an archive — with the conventions, agents, and skills that move items through them. The `product-specialist` agent shapes work items; the `/refine` skill turns them into work-ready items; the `product-engineer` agent writes `.tech.md` approach docs. The `/todo` skill captures small deferred work.

## Path notation

Files in this extension are addressed with the `winter-product:` prefix — for example, `winter-product:/backlog/01-now/user-notifications.work.md`. Resolve to the on-disk path via the `# Winter Extensions` block in workspace `CLAUDE.md`; the local directory name varies (`./winter-product/`, `./product/`, `./backlog/`, etc.).

## Layout

| Path | Contents |
|------|----------|
| `winter-product:/backlog/` | Prioritized queue. Subdirectories `01-now/`, `02-next/`, `05-near/`, `10-future/` |
| `winter-product:/work/` | Active work — items promoted from the backlog (one directory per item) |
| `winter-product:/archive/` | Completed work and TODOs, date-prefixed |
| `winter-product:/ai/` | Planning conventions (item formats, lifecycle, writing style) |

## Backlog item types

Each backlog item is a single file named `<name>.<type>.md` (kebab-case-lowercase):

| Extension | Purpose |
|-----------|---------|
| `.idea.md` | Rough concept, not flushed out |
| `.todo.md` | Small, concrete, already well-defined |
| `.work.md` | Product-level plan, potentially multi-phase |

## Lifecycle

Items flow `backlog/ → work/ → archive/`:

1. **Backlog** — single file under `backlog/<bucket>/<name>.<type>.md`.
2. **Work** — promoted to `work/<name>/` as a directory. `.work.md` items get fleshed out with `00-overview.md`, optional `.tech.md` files, and numbered phase documents. `.todo.md` items typically stay a single file inside the directory.
3. **Archive** — moved to `archive/yyyy-MM-dd-<name>/` (or `archive/yyyy-MM-dd-todo-<name>.md` for a flat TODO) when the work merges to the main branch.

The `/refine` skill is the primary way to move an item from backlog to work-ready, including writing the technical approach. The `/todo` skill is the fast path for dropping new TODOs into the backlog.

Full conventions in [ai/index.md](./ai/index.md).
