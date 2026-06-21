# ❄️ winter-product

A [winter](https://github.com/paul-gross/winter) extension that adds product-workflow tooling to a winter workspace: a prioritized backlog, planning conventions, product agents, and skills for refining and capturing work — plus the actual `backlog/`, `work/`, and `archive/` directories where items live.

📚 **Documentation:** <https://paul-gross.github.io/winter-docs/>

## ✨ Features

- **Prioritized backlog** — `backlog/01-now/`, `02-next/`, `05-near/`, `10-future/` give every item an explicit priority. Three lightweight types — `.idea.md`, `.todo.md`, `.work.md` — capture concepts at the right level of detail.
- **Backlog → work → archive lifecycle** — items promote from `backlog/` into `work/<name>/` when they're ready, and archive into `archive/yyyy-MM-dd-<name>/` when complete. History stays in the workspace.
- **Voice-of-the-user planning** — the `product-specialist` agent thinks in user terms and writes the work items; it doesn't dive into code unless the plan calls for it.
- **Code-aware technical approaches** — the `product-engineer` agent bridges product and code, exploring the repos and writing `.tech.md` approach docs against approved work items.
- **Refine-to-ready workflow** — the `refine` skill evaluates a backlog item against the quality bar, fills gaps interactively, promotes it to `work/`, and orchestrates the technical approach.
- **Cold plan review** — the `plan-review` skill spawns a fresh-context `plan-reviewer` agent that checks a work item's overview, tech approach (including its verification capability matrix), and phases against the planning specs and reports must-fix findings.
- **Lightweight TODO capture** — the `todo` skill captures deferred work as a `.todo.md` in the backlog (prompts for priority bucket, defaulting to `02-next`) so small follow-ups don't get lost when the current feature is the priority.

## 🚀 Installation

Add to the workspace's `.winter/config.toml`:

```toml
[[standalone_repository]]
name = "winter-product"
url = "git@github.com:paul-gross/winter-product.git"
```

Then run `winter ws init`. The `wp-` prefix is the default — it is workspace-configurable, so your install may differ.

> **Note:** This repository is intended to be **forked**. The `backlog/`, `work/`, and `archive/` directories are your project's product backlog and belong under version control in your fork. Point your workspace's `.winter/config.toml` at your fork's URL so items created during development are tracked alongside the rest of your project history.

See [`index.md`](./index.md) for the agents, skills, and layout this extension makes available once installed.

## License

MIT.
