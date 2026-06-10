# Verification Capability Matrix

Every technical approach carries a **verification capability matrix**: a per-module table where each row declares one verification capability the work needs — something the verifier must be able to do, with a runnable check proving it can. The planner and the verifier share the row vocabulary: phase documents reference rows by ID instead of carrying free-text test plans, and missing tooling becomes a scheduled `wanted` row instead of mid-task improvisation.

One table per module the work touches. Single-module work gets a single table.

A real matrix to model on: [exemplars/capability-matrix.tech.md](./exemplars/capability-matrix.tech.md).

## Columns

| Column | Meaning |
|--------|---------|
| `ID` | Stable reference key, e.g. `seed.user`, `err.smtp`, `obs.audit` — see [ID scheme](#id-scheme) |
| Capability | A verb with an object ("seed a report >50MB"), never a vague property ("good test data") |
| Eval | A runnable check with a binary outcome proving the capability exists — a command that exits 0, an endpoint that answers, a test suite that passes |
| Status | `ok` (the eval passes) or `wanted` (a declared gap) |

## ID scheme

IDs are `<verb-class>.<object>`: a short verb-class prefix, a dot, and a kebab-case object. IDs are stable reference keys — once a phase document cites a row, the ID never changes, even if the capability wording is sharpened.

Common verb classes:

| Prefix | Capability shape |
|--------|------------------|
| `build` | build it |
| `run` | run it |
| `seed` | seed state |
| `mock` | mock a dependency |
| `err` | force an error |
| `obs` | observe an effect |
| `reset` | reset to clean |

The list is open — add a verb class when none of these fit — but prefer an existing prefix so IDs stay greppable across work items.

## Row rules

- **Verb with an object.** Each capability is an action on a concrete target ("force an SMTP send failure"), never a quality ("good error coverage"). If you can't phrase it as something an agent *does*, it isn't a capability row.
- **Eval before status.** Every row needs a runnable proof before it can carry a status. The test: another agent must be able to run the eval from the row text alone and get an unambiguous pass/fail. That is all "deterministic" demands — a coarse check like a whole e2e suite passing qualifies; an eval that names no concrete invocation ("a seeder command…") or needs human judgment ("looks right") is underspecified: sharpen the capability until a runnable proof exists. Evals run from the module's repo root unless the row states otherwise.
- **Two statuses only.** `ok` means the eval passes today. `wanted` means the capability is declared but the tooling doesn't exist yet. There is no "partial" — split the row instead.

## Ownership

**Rows are human-gated; cells belong to agents.** Adding or removing a row changes what the work promises to verify, so new rows are proposed for user review. Filling cells — building the tooling, making the eval pass, flipping `wanted` to `ok` — is agent work and needs no gate.

## Lifecycle

1. **Authored with the tech approach.** The `product-engineer` agent enumerates the verification capabilities the work needs while writing the `.tech.md` (see [tech-approach.md](./tech-approach.md)), marking missing tooling as `wanted`.
2. **Referenced by phases.** Phase-document acceptance criteria cite capability IDs ("verify via `err.smtp` + `obs.audit`"). A phase that references a `wanted` row schedules that tooling work before the dependent feature work (see [workflow.md](./workflow.md)).
3. **Fed by implementation.** When an implementing agent discovers a verification need not in the matrix — test-data tooling, an error to force, an effect to observe — it adds the need as a new `wanted` row (verb + object + eval) for user review, rather than improvising one-off tooling.
