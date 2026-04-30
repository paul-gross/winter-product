# Product workflow

Plans, TODOs, and the conventions that govern them. The product-specialist agent writes plans; the product-engineer agent writes `.tech.md` approach docs. The todo skill captures deferred work.

## Path notation

Files in this extension are addressed with the `winter-product:` prefix — for example, `winter-product:/plans/user-notifications/00-overview.md`. Resolve to the on-disk path via the `# Winter Extensions` block in workspace `CLAUDE.md`; the local directory name varies (`./winter-product/`, `./product/`, `./backlog/`, etc.).

## Layout

| Path | Contents |
|------|----------|
| `winter-product:/plans/` | Active plan directories (one per plan, kebab-case-lowercase) |
| `winter-product:/todos/` | Active TODO files (`<name>.md`) |
| `winter-product:/archive/` | Completed plans and TODOs, date-prefixed |
| `winter-product:/ai/` | Planning conventions (plan format, TODO format, lifecycle, writing style) |

## When to create a plan vs a TODO

- **Plan** — multi-phase work, needs design review, business context. Lives in `winter-product:/plans/<name>/`.
- **TODO** — single small change, no architectural decisions, 1–3 sentence description. Lives in `winter-product:/todos/<name>.md`.

Full conventions in [ai/index.md](./ai/index.md).
