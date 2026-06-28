# Product workflow

A prioritized backlog, an active work area, and an archive — with the conventions, agents, and skills that move items through them.

## Path notation

Files in this extension are addressed with the `winter-product:` prefix — for example, `winter-product:/backlog/01-now/user-notifications.work.md`. Resolve to the on-disk path via the `# Winter Extensions` block in workspace `CLAUDE.md`; the local directory name varies (`./winter-product/`, `./product/`, `./backlog/`, etc.).

## Layout

| Path | Contents |
|------|----------|
| `winter-product:/backlog/` | Prioritized queue. Subdirectories `01-now/`, `02-next/`, `05-near/`, `10-future/` |
| `winter-product:/work/` | Active work — items promoted from the backlog (one directory per item) |
| `winter-product:/archive/` | Completed work and TODOs, date-prefixed |
| `winter-product:/context/` | Planning conventions (item formats, lifecycle, writing style) |

## Agents and skills

| Component | Use when |
|-----------|----------|
| [`product-specialist`](./agents/product-specialist.md) | shaping a backlog item, defining a feature, or reasoning about user value and priorities |
| [`product-engineer`](./agents/product-engineer.md) | discovering what the code does in product terms, or writing a `.tech.md` technical approach |
| [`plan-reviewer`](./agents/plan-reviewer.md) | cold-reviewing a plan against the planning specs (spawned by `plan-review`) |
| [`refine`](./skills/refine/SKILL.md) | taking a backlog item to work-ready quality and promoting it to active work |
| [`todo`](./skills/todo/SKILL.md) | capturing small deferred work as a `.todo.md` in the backlog |
| [`plan-review`](./skills/plan-review/SKILL.md) | checking a plan is implementation-ready before work begins |

## Conventions

The item-type formats (`.idea.md` / `.todo.md` / `.work.md`) and the `backlog/ → work/ → archive/` lifecycle are documented under [context/](./context/index.md) — start there before adding, refining, or archiving an item.
