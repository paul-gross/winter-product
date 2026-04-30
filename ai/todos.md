# TODOs

TODOs are lightweight deferred work items — small refactors, quick enhancements, and cleanup tasks that should wait until the current feature work is merged. They are simpler than plans: no phases, no tech files, just a concise actionable description.

## When to Use a TODO vs a Plan

| Use a TODO when... | Use a Plan when... |
|---|---|
| The work is a single, small change | The work spans multiple phases |
| No architectural decisions needed | Requires design review or approval |
| Can be described in 1-3 sentences | Needs business context and technical specs |
| Takes less than a session to implement | Involves multiple agents or services |

## File Format

Each TODO is a single markdown file in `winter-product:/todos/<name>.md` (kebab-case):

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

Same as plans: **kebab-case-lowercase**. Examples: `refactor-auth-service`, `input-validation-cleanup`.

## Archiving Completed TODOs

Archived to `winter-product:/archive/yyyy-MM-dd-todo-<name>.md` (flat file, not a directory). The `todo-` prefix distinguishes them from plan archives. The date reflects when the TODO's implementation was merged to the main branch.

## Commit Conventions

- Creating a TODO: `todo(<name>): <short description>`
- Archiving a completed TODO: `feat(todo-<name>): archive completed TODO`
