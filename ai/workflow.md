# Plan Workflow

The end-to-end lifecycle for creating, reviewing, and archiving plans.

## Why plans exist

- Define clear business objectives before technical work begins
- Break complex work into manageable phases
- Enable review and approval before implementation
- Document decision rationale for future reference
- Track progress across multi-phase initiatives

## Review Process

1. **Create Overview First** — Start with the business-focused overview
2. **User Review** — User reviews and approves the business objective and phases
3. **Technical Approach** — The `product-engineer` agent explores the codebase and writes `.tech.md` files describing the architectural approach
4. **User Review of Tech Approach** — User reviews the structural changes before implementation begins
5. **Create Phase Plans** — Break the approved approach into implementable phases with technical detail
6. **Implementation** — Agent executes the plan in the designated worktree

## Creating New Plans

When a user requests a new feature or improvement:

1. **Create Directory**
   - Always create a directory, even for single-document plans
   - Use kebab-case-lowercase
   - Be descriptive but concise
   - Avoid acronyms unless widely known

2. **Write Overview First**
   - Multi-phase plans: `00-overview.md`
   - Single-document plans: `00-{plan-name}.md`
   - Focus on business value
   - Keep technical details out
   - Get user approval before proceeding

3. **Add Phase Details**
   - Break into logical implementation chunks
   - Number phases sequentially (01, 02, 03...)
   - Include all technical details needed for implementation

4. **Commit**
   - Use `plan(<plan-name>)` as the commit type

5. **Request Review**
   - Present overview for business approval
   - Review technical phases before implementation

## Archiving Completed Plans

When a plan's work is complete (all phases merged to the main branch):

1. Identify the date of the last feature commit on the main branch for that plan
2. Move the plan directory from `winter-product:/plans/` to `winter-product:/archive/` with a date prefix:
   ```
   winter-product:/plans/user-notifications/  →  winter-product:/archive/2026-01-28-user-notifications/
   ```
3. The date format is `yyyy-MM-dd`
4. Use `feat(<plan-name>)` as the commit type
5. The archive serves as a historical record of completed work and can be referenced for similar future efforts

## Maintenance

Update a plan when:
- Requirements change during review
- New phases are needed
- Phases are completed (mark as done or archive)
- Technical approach changes significantly
