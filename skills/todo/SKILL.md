---
description: Create a lightweight TODO for deferred work items — small refactors, quick enhancements, things to do after the current feature merges
allowed-tools: Bash, Read, Write, Edit, Glob, Grep, AskUserQuestion
---

Create a TODO for deferred work.

Read `winter-product:/ai/todos.md` for the file format, naming rules, and archive conventions before writing.

## Argument Parsing

Parse `$ARGUMENTS` as a freeform description of the work to be done. Examples:
- `todo Refactor UserService to use the new DTO pattern`
- `todo Add input validation to the billing endpoints`
- `todo Clean up unused imports in the API controllers`

## Step 1: Derive a Name

Convert the description into a kebab-case name suitable for a filename. Keep it concise (3-6 words). Examples:
- "Refactor UserService to use the new DTO pattern" → `refactor-user-service-dto-pattern`
- "Add input validation to the billing endpoints" → `billing-input-validation`

Present the derived name to the user with `AskUserQuestion` and offer to adjust it. Options:
- "Use `<derived-name>`" (Recommended)
- "Let me specify a different name"

## Step 2: Choose a Priority Bucket

TODOs are deferred work by default, so they should land in `02-next` unless there's a reason to elevate or defer them further. Pick the bucket via:

1. **List the actual buckets** — `ls winter-product:/backlog/` to confirm the directories currently in use (don't assume from this skill).
2. **Ask the user** via `AskUserQuestion`, presenting the buckets discovered in step 1 with `02-next` first as the recommended default. Typical buckets and their meaning:
   - `01-now` — pick up as soon as the current branch merges
   - `02-next` *(default for deferred TODOs)* — work on after the current item, but no rush
   - `05-near` — relevant in the next few weeks
   - `10-future` — someday/maybe; keep it captured but don't schedule
3. **Validate** the user's choice against the directories from step 1 before proceeding. If it doesn't match, re-prompt.

## Step 3: Write the TODO File

Create `winter-product:/backlog/<bucket>/<name>.todo.md` using the bucket chosen in step 2 and the TODO file format defined in `winter-product:/ai/todos.md`. Fill in each section using:
- The freeform description from `$ARGUMENTS`
- Current conversation context (what the user has been working on, why this came up)
- Codebase knowledge if available (file paths, service names)

Be specific in "Where" and "Done When" — these guide the agent that implements the TODO later.

## Step 4: Commit

Commit the new file from `winter-product:/` with message `todo(<name>): <short description>`. The short description should be a concise summary (under 70 chars) of the TODO.

## Step 5: Report

Tell the user the TODO was created and where.

$ARGUMENTS
