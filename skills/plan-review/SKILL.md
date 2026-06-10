---
description: Review a product plan against the planning specs — spawns a fresh-context plan-reviewer agent over a work item's overview, tech approach, and phases (or a backlog item) and reports whether it's implementation-ready. Use after writing or refining a plan, or before starting implementation.
allowed-tools: Read, Glob, Grep, Task, AskUserQuestion
argument-hint: <item-name>
---

Review a product plan with a cold `plan-reviewer` agent and relay the findings. The review's value is the fresh context — do not review the plan in this session yourself.

## Argument Parsing

Parse `$ARGUMENTS` for an **item name** (required): a kebab-case name matching a directory under `winter-product:/work/` or a file under `winter-product:/backlog/`. Examples:
- `plan-review user-notifications`
- `plan-review verification-capability-matrix`

## Step 1: Resolve the Plan

Search in order:

1. `winter-product:/work/<name>/` — review every document in the directory (overview, `.tech.md` files, phase documents)
2. `winter-product:/backlog/**/<name>.*.md` — review the single backlog file

If no match is found, list the available work items and backlog items and ask the user which one they meant. If the name matches both a work directory and a backlog file, ask via `AskUserQuestion`.

## Step 2: Spawn the Reviewer

Spawn a `plan-reviewer` agent **from the workspace root**. The agent definition carries the review methodology; pass it the coordination it needs:

- The resolved plan path(s) from Step 1
- The instruction to return its structured report (verdict, must-fix, nice-to-have, open questions)

## Step 3: Report

Relay the reviewer's verdict and findings to the user, must-fix first. Do not apply fixes — plan content and capability-matrix rows are human-gated. If the user wants the gaps closed, route them: format and wording fixes can be edited directly on request; weak or missing content goes back through `refine`; tech-approach gaps go to a `product-engineer` agent.

$ARGUMENTS
