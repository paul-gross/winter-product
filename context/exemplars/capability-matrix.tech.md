# Exemplar — Tech Approach with Verification Capability Matrix

A real `.tech.md`, preserved as the reference example for authoring a verification capability matrix. It is the tech approach for the change that introduced the matrix convention itself, so its matrix rows are live: the `ok` evals pass against this repo today. The format spec is [../capability-matrix.md](../capability-matrix.md); the surrounding conventions are [../tech-approach.md](../tech-approach.md).

The work was a documentation-only change to this extension. No code; the structural changes are new and amended convention surfaces.

## Structural Changes

Documentation-only change — no code, API endpoints, or schema deltas. All structural changes are new and amended convention documents.

**Documentation changes:**

| Module | Document | Change | Verifies via |
|--------|----------|--------|-------------|
| winter-product | `context/capability-matrix.md` | New — canonical matrix format, ID scheme, verb-with-object rule, eval-before-status rule, `ok`/`wanted` statuses, row ownership, lifecycle. Routed from `context/index.md`. | `obs.index`, `obs.xref` |
| winter-product | `context/tech-approach.md` | Amended — matrix joins "What to Include"; testing exclusion narrows from all testing strategies to free-text test plans only. | `obs.xref` |
| winter-product | `context/workflow.md` | Amended — refine-flow steps gain matrix authoring and capability-ID acceptance criteria. | `obs.xref` |
| winter-product | `agents/product-engineer.md` | Amended — instructed to author the matrix with every `.tech.md` and add `wanted` rows when implementation surfaces new verification needs. | `obs.index` |
| winter-product | `skills/refine/SKILL.md` | Amended — tech-approach step orchestrates matrix authoring; user-review step walks rows (human-gated); phase-documents step requires capability-ID references. | `obs.xref` |

## Verification Capability Matrix

### Module: winter-product

| ID | Capability | Eval | Status |
|----|------------|------|--------|
| `run.docs-lint` | Run the workspace convention lint over this extension's docs | `winter lint winter-product` exits 0 | ok |
| `obs.xref` | Observe that every relative doc link under `context/` resolves to an existing file | `cd context && grep -hoE '\(\./[a-z-]+\.md\)' *.md \| tr -d '()' \| sort -u \| xargs -r -I{} test -e {}` exits 0 | ok |
| `obs.index` | Observe that every `context/` document is routed from `context/index.md` | `for f in context/*.md; do grep -q "$(basename "$f")" context/index.md \|\| exit 1; done` exits 0 | ok |
| `seed.backlog-item` | Seed a disposable backlog work item to exercise the `refine` flow end-to-end | `tools/seed-backlog-item refine-fixture` creates `backlog/10-future/refine-fixture.work.md` and exits 0 | wanted |

The `wanted` row is the declared gap this work surfaced: exercising `refine` end-to-end today requires hand-writing a backlog item; a fixture seeder would make that repeatable.
