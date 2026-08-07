# Backlog & Work Conventions

Conventions for managing the product backlog, active work, and the lifecycle between them. See [`index.md`](../index.md) at the extension root for the directory layout and the runtime surface (skills and agents). Each document governs the artifacts its row names, for authoring and review alike: a plan review's conformance gate applies the governing specs as its criteria, read fresh each review.

| Document | Governs |
|----------|---------|
| [Overview & Phase Format](./overview-format.md) | `.work.md` items, `00-overview.md`, and phase documents (`01-*.md` …): required sections, business-facing voice (no technical details), phase structure, file naming and layout |
| [Technical Approach](./tech-approach.md) | `*.tech.md`: change skeleton tables, include/exclude lists |
| [Verification Capability Matrix](./capability-matrix.md) | the matrix in a `*.tech.md`: row rules, runnable evals, `ok`/`wanted` lifecycle, capability IDs cited from phase documents |
| [Capability Matrix Exemplar](./exemplars/capability-matrix.tech.md) | nothing — a real `.tech.md` matrix with passing evals to model new ones on |
| [TODOs](./todos.md) | `.todo.md` items: creating, formatting, archiving |
| [Writing Style](./writing-style.md) | prose in every artifact: pseudocode, domain models, when to show actual code |
| [Workflow](./workflow.md) | the lifecycle around the artifacts: backlog → work → archive, promotion, phase acceptance criteria referencing capability IDs |
