---
description: Refine a backlog item — evaluate quality, fill gaps interactively with the user, promote to active work, and create a technical approach
allowed-tools: Bash, Read, Write, Edit, Glob, Grep, Task, AskUserQuestion
argument-hint: <item-name>
---

Refine a backlog item into work-ready quality and promote it to active work. The skill branches by item type — work items (`.work.md`), TODOs (`.todo.md`), and ideas (`.idea.md`) each have their own rubric and promotion shape.

## Argument Parsing

Parse `$ARGUMENTS` for an **item name** (required): a kebab-case name matching a file under `winter-product:/backlog/`. Examples:
- `refine user-notifications`
- `refine dependency-upgrade`
- `refine project-restructure`

## Step 0: Find the Item

Look up the name by searching `winter-product:/backlog/**/<name>.*.md`. If no match is found, list available backlog items and ask the user which one they meant.

Read the file. **Note the item type** — the type drives which rubric Step 1 uses and which promotion shape Step 2 produces:

| Type | Format spec | Step 1 rubric | Step 2 shape |
|------|-------------|----------------|---------------|
| `.idea.md` | free-form concept (no spec) | rewrite-as-work-item or TODO (1c) | if converted to `.work.md` → 2a (Step 3 runs); if converted to `.todo.md` → 2b (Step 3 skipped) |
| `.todo.md` | `winter-product:/context/todos.md` | TODO rubric (below) | promote as flat `work/<name>/` (Step 3 skipped) |
| `.work.md` | `winter-product:/context/overview-format.md` | work-item rubric (below) | promote as `00-overview.md` + phases (Step 3 runs) |

## Step 1: Evaluate

Branch by item type. In all branches the goal is the same — **rate each criterion as present/strong, weak/incomplete, or missing, then refine interactively** — but the criteria differ.

### 1a. Work item (`.work.md`)

Assess against the quality standards in `winter-product:/context/overview-format.md` and `winter-product:/context/writing-style.md`. The goal is a **business-facing work item** that clearly communicates what, why, and how — without technical implementation details.

Criteria:

1. **Business Objective** — Is there a clear 1-2 sentence problem statement or opportunity?
2. **Success Criteria** — Are there measurable, concrete outcomes?
3. **High-Level Approach** — Is there a general strategy explained without technical jargon?
4. **Phases** — Is the work broken into logical, deliverable phases, if applicable?
5. **Dependencies** — Are prerequisites and related work identified?
6. **Risks & Considerations** — Are known challenges or open decisions called out?

### 1b. TODO (`.todo.md`)

Assess against `winter-product:/context/todos.md`. TODOs are deliberately lightweight — a good TODO is short, scoped, and self-contained, not a stripped-down work item.

Criteria:

1. **What** — 1-3 sentences naming the concrete change. Vague or open-ended? Refine.
2. **Why** — 1-2 sentences explaining why this was deferred or why it matters. Missing rationale → refine.
3. **Where** — File paths or areas of the codebase affected. Missing or "tbd" → refine.
4. **Done When** — 1-3 concrete acceptance bullets. Each bullet should be checkable by another agent. Fuzzy ("looks better") → refine to "X function returns Y".
5. **Scope** — TODOs are *single-session*, no architectural decisions, no multi-phase. If the item smells multi-session or design-heavy, propose **converting to a `.work.md`** instead of refining as a TODO.

### 1c. Idea (`.idea.md`)

Ideas are pre-format — no rubric to grade against. The refine step here is **a rewrite, not a polish**. Ask the user enough targeted questions to determine whether this should become a TODO or a work item, then rewrite into the chosen format and **rename the file** (`.idea.md` → `.todo.md` or `.work.md`). Then re-enter 1a or 1b for the rewritten content.

### Present the Evaluation

For 1a and 1b, give the user a structured evaluation:

1. **Overall assessment** — One sentence: is this ready, close, or needs significant work?
2. **What's strong** — Call out the parts that are well-defined
3. **What's missing or weak** — Specific gaps, with concrete suggestions for what to add
4. **Open questions** — List any uncertainties that need resolution before work begins

### Refine Interactively

If the item needs work:
- Propose specific improvements or additions for the weakest areas
- Ask the user targeted questions to fill gaps (don't ask open-ended "what do you think?" — be specific: "Should preferences be per-user or per-workspace?")
- After discussion, update the file with the refined content

If the item is already solid, tell the user so and proceed to Step 2.

**Do not proceed to Step 2 until the user confirms the content is good.**

## Step 2: Promote to Work

Once the item is solid, promote it from the backlog into active work. The shape differs by type:

### 2a. Work item (`.work.md`)

1. Create `winter-product:/work/<name>/`
2. Copy the backlog file into the work directory as `00-overview.md` (the canonical overview filename per `winter-product:/context/overview-format.md`)
3. Remove the original backlog file
4. Commit: `product(<name>): promote from backlog`
5. Proceed to Step 3 (Technical Approach).

### 2b. TODO (`.todo.md`)

Per `winter-product:/context/todos.md`, TODOs in active work stay as a single file inside a thin directory — no overview, no phases, no tech approach.

1. Create `winter-product:/work/<name>/`
2. Move the backlog `<name>.todo.md` into the work directory as `<name>.todo.md` (keep the `.todo.md` suffix; the directory is the only structural change)
3. Commit: `product(<name>): promote from backlog`
4. **Skip Step 3** — TODOs don't get a technical approach. Jump to Step 4 (Report).

## Step 3: Technical Approach (work items only)

Create the technical approach. This bridges the product plan and implementation. **This step does not run for TODOs.**

### Create the Technical Approach

Spawn a `product-engineer` agent to explore the codebase and write the technical approach. The agent should:

1. Read the work item at `winter-product:/work/<name>/00-overview.md` (or `00-{name}.md` for single-document items — see `winter-product:/context/overview-format.md` naming conventions)
2. Read the tech approach conventions at `winter-product:/context/tech-approach.md` and the matrix format at `winter-product:/context/capability-matrix.md`
3. Explore the project worktrees (from the workspace root) to understand existing patterns
4. Write the tech approach file(s) per the conventions in that document, including the verification capability matrix — the capabilities the work needs to verify, with missing tooling marked `wanted`

### Review with User

Present the technical approach to the user for review. Walk through the capability matrix rows explicitly — rows are human-gated, so the user must confirm what the work promises to verify and which gaps are declared `wanted`. If changes are needed, iterate until approved.

### Create Phase Documents (if applicable)

If the work item defines phases and they don't already have detailed phase documents:
- Create numbered phase files (`01-<phase-name>.md`, `02-<phase-name>.md`, etc.) in the work directory
- Each phase document should contain technical specificity and actionable implementation steps per `winter-product:/context/overview-format.md`
- Acceptance criteria reference capability IDs from the tech approach's matrix; a phase that references a `wanted` row schedules that tooling work before the dependent feature work

### Commit

Commit all tech approach and phase files:
```
product(<name>): add technical approach
```

## Step 4: Report

Summarize what was done:
- The work item location: `winter-product:/work/<name>/`
- Files created (overview/TODO + tech approach + phases, as applicable)

$ARGUMENTS
