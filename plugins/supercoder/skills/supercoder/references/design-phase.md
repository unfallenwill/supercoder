# Phase 4: Design

Propose architectural approaches and let the user choose. Two-step process: brief summaries in parallel, then detail the chosen one.

## Output

**Step 1 — Approach Summaries:** Each approach covers: name, one-sentence description, core mechanism, files affected, complexity (Low/Medium/High), key risks, pattern fit.

**Step 2 — Chosen Design:** After user selection, expand into:

- Implementation steps (files to create/modify, what to change, how to verify)
- Data model / API changes (if applicable)
- Testing strategy
- Migration plan (if applicable)

## Steps

1. Spawn 3 subagents in parallel, one per approach:
   - **A: Minimal Change** — extend existing patterns, smallest scope
   - **B: Balanced** — moderate refactoring, good extensibility
   - **C: Architectural** — new abstraction, most extensible
2. Present all three via AskUserQuestion with trade-offs.
3. Expand the chosen approach into a full implementation plan.
