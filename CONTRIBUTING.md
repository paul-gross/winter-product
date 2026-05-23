# Contributing

## Commit messages

Conventional Commits with a scope:

    <type>(<scope>): <description>

    [optional body]

- Types: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`, `perf`, `style`, `ai`, `product`, `todo`
- Scope: repo name or subsystem (e.g. `winter-product`, `agents`, `skills`)
- The `/wf-commit` skill from [winter-workflow](https://codeberg.org/pgross/winter-workflow) generates commits in this format

### Product-backlog types

This repo manages a product backlog, so two additional types are reserved for backlog content:

- `product(<name>)` — for `.idea.md` and `.work.md` items: creating, refining, promoting to work, or adding a technical approach. Scope is the kebab-case item name.
- `todo(<name>)` — for `.todo.md` items: creating a deferred work TODO. Scope is the kebab-case TODO name.

Use the standard types (`feat`, `fix`, etc.) for everything else — skills, agents, docs, archive moves of completed work.

## Pre-commit checks

None. No linters, formatters, or tests are wired in.

## Delivery

- Default branch: `master`
- **Primary contributors** push directly to `master` whenever — no PR or review required. Allowed to rewrite history.
- **Outside contributors** are welcome — open a PR against `master` and I'll review and merge.
