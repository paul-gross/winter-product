# Product workflow

A prioritized backlog, an active work area, and an archive — with the conventions, agents, and skills that move items through them. The `product-specialist` agent shapes work items; the `refine` skill turns them into work-ready items; the `product-engineer` agent writes `.tech.md` approach docs. The `todo` skill captures small deferred work. The `plan-review` skill spawns a cold `plan-reviewer` agent to check a plan against the planning specs before implementation begins.

## Path notation

Files in this extension are addressed with the `winter-product:` prefix — for example, `winter-product:/backlog/01-now/user-notifications.work.md`. Resolve to the on-disk path via the `# Winter Extensions` block in workspace `CLAUDE.md`; the local directory name varies (`./winter-product/`, `./product/`, `./backlog/`, etc.).

## Layout

| Path | Contents |
|------|----------|
| `winter-product:/backlog/` | Prioritized queue. Subdirectories `01-now/`, `02-next/`, `05-near/`, `10-future/` |
| `winter-product:/work/` | Active work — items promoted from the backlog (one directory per item) |
| `winter-product:/archive/` | Completed work and TODOs, date-prefixed |
| `winter-product:/ai/` | Planning conventions (item formats, lifecycle, writing style) |

## Conventions

The item-type formats (`.idea.md` / `.todo.md` / `.work.md`) and the `backlog/ → work/ → archive/` lifecycle are documented under [ai/](./ai/index.md) — start there before adding, refining, or archiving an item. The `refine` skill moves an item from backlog to work-ready (including the technical approach); the `todo` skill is the fast path for dropping new TODOs into the backlog.
