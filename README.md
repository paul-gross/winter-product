# ❄️ winter-product

A [winter](https://github.com/paul-gross/winter) extension that adds product-workflow tooling to a winter workspace: a prioritized backlog, planning conventions, product agents, and skills for refining and capturing work — plus the actual `backlog/`, `work/`, and `archive/` directories where items live.

## ✨ Features

- **Prioritized backlog** — `backlog/01-now/`, `02-next/`, `05-near/`, `10-future/` give every item an explicit priority. Three lightweight types — `.idea.md`, `.todo.md`, `.work.md` — capture concepts at the right level of detail.
- **Backlog → work → archive lifecycle** — items promote from `backlog/` into `work/<name>/` when they're ready, and archive into `archive/yyyy-MM-dd-<name>/` when complete. History stays in the workspace.
- **Voice-of-the-user planning** — the `product-specialist` agent thinks in user terms and writes the work items; it doesn't dive into code unless the plan calls for it.
- **Code-aware technical approaches** — the `product-engineer` agent bridges product and code, exploring the repos and writing `.tech.md` approach docs against approved work items.
- **Refine-to-ready workflow** — the `/refine` skill evaluates a backlog item against the quality bar, fills gaps interactively, promotes it to `work/`, and orchestrates the technical approach.
- **Lightweight TODO capture** — the `/todo` skill drops deferred work into `backlog/01-now/<name>.todo.md` so small follow-ups don't get lost when the current feature is the priority.

## 🚀 Installation

Add to the workspace's `.winter/config.toml`:

```toml
[[standalone_repository]]
name = "winter-product"
url = "git@github.com:paul-gross/winter-product.git"
```

Then run `winter ws init`. The extension's agents become available as `product-engineer` and `product-specialist`, and the `/todo` and `/refine` skills install under the workspace's configured prefix — by default `prefix = "wp"` in `winter-ext.toml`, so winter-cli wires them up as `/wp-todo` and `/wp-refine` in this configuration.

> **Note:** This repository is intended to be **forked**. The `backlog/`, `work/`, and `archive/` directories are your project's product backlog and belong under version control in your fork. Point your workspace's `.winter/config.toml` at your fork's URL so items created during development are tracked alongside the rest of your project history.

See [`index.md`](./index.md) for the full layout — that file is auto-loaded into every Claude session that runs in a winter workspace with this extension installed.

## License

MIT.
