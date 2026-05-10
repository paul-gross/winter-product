---
description: Create a lightweight TODO for deferred work items — small refactors, quick enhancements, things to do after the current feature merges
model: sonnet
allowed-tools: Bash, Read, Write, Edit, Glob, Grep, AskUserQuestion
---

Create a TODO for deferred work.

Read `winter-product:/ai/todos.md` for the file format, naming rules, and archive conventions before writing.

## Argument Parsing

Parse `$ARGUMENTS` as a freeform description of the work to be done. Examples:
- `/todo Refactor UserService to use the new DTO pattern`
- `/todo Add input validation to the billing endpoints`
- `/todo Clean up unused imports in the API controllers`

## Step 1: Derive a Name

Convert the description into a kebab-case name suitable for a filename. Keep it concise (3-6 words). Examples:
- "Refactor UserService to use the new DTO pattern" → `refactor-user-service-dto-pattern`
- "Add input validation to the billing endpoints" → `billing-input-validation`

Present the derived name to the user with `AskUserQuestion` and offer to adjust it. Options:
- "Use `<derived-name>`" (Recommended)
- "Let me specify a different name"

## Step 2: Write the TODO File

Create `winter-product:/backlog/01-now/<name>.todo.md` using the TODO file format defined in `winter-product:/ai/todos.md`. Fill in each section using:
- The freeform description from `$ARGUMENTS`
- Current conversation context (what the user has been working on, why this came up)
- Codebase knowledge if available (file paths, service names)

Be specific in "Where" and "Done When" — these guide the agent that implements the TODO later.

## Step 3: Commit

Commit the new file from `winter-product:/` with message `todo(<name>): <short description>`. The short description should be a concise summary (under 70 chars) of the TODO.

## Step 4: Report

Tell the user the TODO was created and where.

$ARGUMENTS
