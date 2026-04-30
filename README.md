# winter-product

A [winter](https://codeberg.org/pgross/winter) extension that adds product-workflow tooling to a winter workspace: planning conventions, product agents, and the `todo` skill, plus the actual `plans/`, `todos/`, and `archive/` directories where work items live.

## Features

- **Plan-first product workflow** — multi-phase work lives in `plans/<name>/` with overview, phases, and a defined lifecycle from draft to archive. One convention across every project in the workspace.
- **Voice-of-the-user planning** — the `wp-product-specialist` agent thinks in user terms and writes the plan; it doesn't dive into code unless the plan calls for it.
- **Code-aware technical approaches** — the `wp-product-engineer` agent bridges product and code, exploring the repos and writing `.tech.md` approach docs against approved plans.
- **Lightweight TODO capture** — the `/wp-todo` skill drops deferred work into `todos/<name>.md` so small follow-ups don't get lost when the current feature is the priority.
- **Archive-by-default lifecycle** — completed plans and TODOs move into `archive/` with a date prefix instead of being deleted, so the history of what was built (and why) stays in the workspace.

## Installation

Add to the workspace's `.winter/config.toml`:

```toml
[[standalone_repository]]
name = "winter-product"
url = "git@codeberg.org:pgross/winter-product.git"
```

Then run `winter ws init`. The extension's agents become available as `wp-product-engineer` and `wp-product-specialist`, and the skill as `/wp-todo`.

> **Note:** This repository is intended to be **forked**. The `plans/`, `todos/`, and `archive/` directories are your project's product backlog and belong under version control in your fork. Point your workspace's `.winter/config.toml` at your fork's URL so plans and TODOs created during development are tracked alongside the rest of your project history.

See [`index.md`](./index.md) for the full layout — that file is auto-loaded into every Claude session that runs in a winter workspace with this extension installed.
