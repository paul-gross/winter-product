# TODOs (*.todo.md)

TODOs are lightweight deferred work items — small refactors, quick enhancements, and cleanup tasks that should wait until the current feature work is merged. They live in the backlog as `.todo.md` files. No phases, no tech files, just a concise actionable description.

## When to Use a TODO vs Other Types

| `.todo.md` | `.work.md` | `.idea.md` |
|---|---|---|
| Single, small change | Spans multiple phases | Not flushed out yet |
| No architectural decisions | Requires design review | Needs design thinking |
| Described in 1-3 sentences | Needs business context and technical specs | Conceptual only |
| Less than a session to implement | Involves multiple agents or services | Effort unknown |

## File Format

Each TODO is a single markdown file in `winter-product:/backlog/<bucket>/<name>.todo.md` (kebab-case):

```markdown
# <Title>

## What
<1-3 sentences: what needs to change>

## Why
<1-2 sentences: why this was deferred / why it matters>

## Where
<File paths or areas of the codebase affected>

## Done When
<Concrete acceptance criteria, 1-3 bullets>
```

No subdirectories, no phases, no tech files. One file = one TODO.

## Naming

**kebab-case-lowercase**. Examples: `refactor-auth-service.todo.md`, `input-validation-cleanup.todo.md`.

## Priority Bucket

TODOs are deferred work by definition, so the default bucket is `02-next` — "pick up after the current item, but no rush." Reserve `01-now` for TODOs that should be worked on as soon as the current branch merges; use `05-near` and `10-future` for items that are further out.

The `/todo` skill asks the user for the bucket (defaulting to `02-next`) and validates the choice against the actual `backlog/` directories at runtime, so adding or renaming a bucket on disk is enough — no skill update needed.

## Lifecycle

TODOs follow the standard lifecycle: `backlog/ → work/ → archive/`. When a TODO is worked on, it moves to `work/<name>/` as a directory (typically still a single file inside). When complete, it archives — usually as a flat file at `winter-product:/archive/yyyy-MM-dd-todo-<name>.md` since most TODOs don't grow into multi-file directories.

The `todo-` prefix in the archive filename distinguishes completed TODOs from completed work items.

## Commit Conventions

- Creating a TODO: `todo(<name>): <short description>`
- Promoting from backlog to work: `product(<name>): promote from backlog`
- Archiving a completed TODO: `feat(<name>): archive completed work`
