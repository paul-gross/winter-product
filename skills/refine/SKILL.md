---
description: Refine a backlog item — evaluate quality, fill gaps interactively with the user, promote to active work, and create a technical approach
model: opus
allowed-tools: Bash, Read, Write, Edit, Glob, Grep, Task, AskUserQuestion
---

Refine a backlog item into work-ready quality and promote it to active work.

## Argument Parsing

Parse `$ARGUMENTS` for an **item name** (required): a kebab-case name matching a file under `winter-product:/backlog/`. Examples:
- `/refine user-notifications`
- `/refine dependency-upgrade`
- `/refine project-restructure`

## Step 0: Find the Item

Look up the name by searching `winter-product:/backlog/**/<name>.*.md`. If no match is found, list available backlog items and ask the user which one they meant.

Read the file. Note the item type (`.idea.md`, `.todo.md`, or `.work.md`) and priority bucket.

## Step 1: Evaluate the Work Item

Assess the item against the quality standards defined in `winter-product:/ai/overview-format.md` and `winter-product:/ai/writing-style.md`. The goal is a **business-facing work item** that clearly communicates what, why, and how — without technical implementation details.

### Evaluation Criteria

Rate each of the following as present/strong, weak/incomplete, or missing:

1. **Business Objective** — Is there a clear 1-2 sentence problem statement or opportunity?
2. **Success Criteria** — Are there measurable, concrete outcomes?
3. **High-Level Approach** — Is there a general strategy explained without technical jargon?
4. **Phases** — Is the work broken into logical, deliverable phases, if applicable?
5. **Dependencies** — Are prerequisites and related work identified?
6. **Risks & Considerations** — Are known challenges or open decisions called out?

Also check for:
- **Open questions or uncertainties** — Anything left vague or unresolved that would block implementation
- **Gaps** — Missing sections, incomplete reasoning, or hand-waved details
- **Scope clarity** — Is it clear what is in scope and what is not?

### Present the Evaluation

Give the user a structured evaluation:

1. **Overall assessment** — One sentence: is this ready, close, or needs significant work?
2. **What's strong** — Call out the parts that are well-defined
3. **What's missing or weak** — Specific gaps, with concrete suggestions for what to add
4. **Open questions** — List any uncertainties that need resolution before work begins

### Refine Interactively

If the item needs work:
- Propose specific improvements or additions for the weakest areas
- Ask the user targeted questions to fill gaps (don't ask open-ended "what do you think?" — be specific: "Should preferences be per-user or per-workspace?")
- After discussion, update the file with the refined content
- If the item started as an `.idea.md`, it will likely need to be rewritten as a proper `.work.md` format

If the item is already solid, tell the user so and proceed to Step 2.

**Do not proceed to Step 2 until the user confirms the work item content is good.**

## Step 2: Promote to Work

Once the work item is solid, promote it from the backlog into active work.

1. Create `winter-product:/work/<name>/`
2. Copy the backlog file into the work directory as `00-overview.md` (the canonical overview filename per `winter-product:/ai/overview-format.md`)
3. Remove the original backlog file
4. Commit: `product(<name>): promote from backlog`

## Step 3: Technical Approach

Create the technical approach. This bridges the product plan and implementation.

### Create the Technical Approach

Spawn a `product-engineer` agent to explore the codebase and write the technical approach. The agent should:

1. Read the work item at `winter-product:/work/<name>/00-overview.md`
2. Read the tech approach conventions at `winter-product:/ai/tech-approach.md`
3. Explore the project worktrees (from the workspace root) to understand existing patterns
4. Write the tech approach file(s) per the conventions in that document

### Review with User

Present the technical approach to the user for review. If changes are needed, iterate until approved.

### Create Phase Documents (if applicable)

If the work item defines phases and they don't already have detailed phase documents:
- Create numbered phase files (`01-<phase-name>.md`, `02-<phase-name>.md`, etc.) in the work directory
- Each phase document should contain technical specificity and actionable implementation steps per `winter-product:/ai/overview-format.md`

### Commit

Commit all tech approach and phase files:
```
product(<name>): add technical approach
```

## Step 4: Report

Summarize what was done:
- The work item location: `winter-product:/work/<name>/`
- Files created (overview, tech approach, phases)

$ARGUMENTS
