# Phase 4: Design — 方案设计

> Load this reference at the start of Phase 4.
> Read `context.md`, `understanding.md`, and `clarified.md` before following these steps.

Propose concrete architectural approaches and let the user choose. Then detail
the chosen approach into an implementable plan.

## Principle

Design is a creative act with no single right answer. Present trade-offs honestly
and let the human make the call. Focus on approaches that differ in fundamental
ways, not minor variations.

## Design Method

Design directly using the codebase context (context.md), clarifications
(clarified.md), and design patterns appropriate to the project's technology
stack. Reference actual files and patterns found during exploration.

## Steps

1. **Generate 2-3 approaches** (if more than 3 emerge during brainstorming,
   pick the top 3 most distinct ones). For each approach, document:
   - **Summary**: One-sentence description of the approach
   - **Strategy**: What changes and how — the core mechanism
   - **Files affected**: Specific file paths that would change
   - **Complexity**: Low / Medium / High — implementation effort
   - **Risk**: What could go wrong with this approach
   - **Consistency**: How well it fits existing code patterns (High / Medium / Low)

   Approaches should vary along these dimensions:
   - Scope of change (minimal vs. broad refactoring)
   - Architecture pattern (extend existing vs. introduce new abstraction)
   - Trade-off between speed and extensibility

2. **Present to user** — Use AskUserQuestion to present the approaches.
   Show trade-offs clearly. Ask the user to select one.

3. **Detail the chosen design** — Write `design.md`:
   ```markdown
   # Technical Design: <name>

   ## Chosen Approach: <approach name>
   <rationale for choosing this approach>

   ## Implementation Plan

   ### Step 1: <title>
   - **Files**: specific paths to create or modify
   - **Changes**: what to do in this step
   - **Verification**: how to confirm it works

   ### Step 2: <title>
   - **Files**: specific paths
   - **Changes**: what to do
   - **Verification**: how to confirm it works

   (continue for all steps — order by dependency)

   ## Data Model Changes
   (if applicable) Schema changes, new types, migrations.

   ## API Changes
   (if applicable) New endpoints, modified contracts, breaking changes.

   ## Testing Strategy
   - Unit tests: what to test
   - Integration tests: what to verify
   - Manual testing: how to verify end-to-end

   ## Migration / Rollout
   (if applicable) Deployment steps, feature flags, rollback plan.
   ```

4. **Define checkpoints** — Identify 2-3 points during implementation where the
   user should review progress. Write `checkpoints.md`:
   ```markdown
   # Implementation Checkpoints: <name>

   ## Checkpoint 1: After <step description>
   - What to review: <specific files or behavior>
   - What to verify: <test or manual check>

   ## Checkpoint 2: After <step description>
   - What to review: <specific files or behavior>
   - What to verify: <test or manual check>
   ```

5. **Update context.md** — Add a "Design Decision" section:
   ```markdown
   ## Design Decision
   - **Approach**: <chosen approach name>
   - **Rationale**: <why this approach>
   - **Key trade-off**: <what we gain vs. what we give up>
   ```
   Update status to "DESIGN → IMPLEMENT".

## Rollback

If detailing the chosen approach reveals ambiguities not caught in Phase 3,
roll back to CLARIFY with specific new questions.

## Transition

Proceed to Phase 5 (Implement). Read `implement-phase.md`.
