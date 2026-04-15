# Phase 4: Design — 方案设计

> Load this reference at the start of Phase 4.

Propose concrete architectural approaches and let the user choose. This phase
uses a two-step process: first generate brief approach cards in parallel, then
detail only the chosen approach.

## Input
- Structured understanding from Phase 1 (Core Intent, Scope, Constraints)
- Codebase findings from Phase 2 (Architecture, Patterns, Relevant Files)
- Refined Scope, Refined Acceptance Criteria, Key Decisions from Phase 3
- Carry-Forward summaries from Phase 1, 2, and 3

## Output (Step One: Approach Cards)

Each subagent returns a brief card:

```
## Approach [X]: [Name]

**Summary:** [one sentence]

**Strategy:** [what changes and how — the core mechanism]

**Files affected:** [specific file paths]

**Complexity:** Low / Medium / High

**Risk:** [what could go wrong]

**Consistency:** [how well it fits existing patterns — High / Medium / Low]
```

## Output (Step Two: Chosen Design)

```
## Design: [Chosen Approach Name]

**Rationale:** [why this approach was chosen]

### Implementation Plan

#### Step 1: [title]
- **Files:** [paths to create or modify]
- **Changes:** [what to do]
- **Verification:** [how to confirm it works]

#### Step 2: [title]
- **Files:** [paths]
- **Changes:** [what to do]
- **Verification:** [how to confirm it works]

### Data Model Changes
(if applicable) Schema changes, new types, migrations.

### API Changes
(if applicable) New endpoints, modified contracts, breaking changes.

### Testing Strategy
- Unit: [what to test]
- Integration: [what to verify]
- Manual: [how to verify end-to-end]

### Migration / Rollout
(if applicable) Deployment steps, feature flags, rollback plan.
```

## Carry-Forward Summary

Before completing this phase, output a compact summary (under 100 words):

```
## Carry-Forward
- **Chosen approach:** [name and one-line rationale]
- **Steps:** [N implementation steps]
- **Files affected:** [count]
- **Key trade-off:** [what we gain vs. what we give up]
- **Testing:** [unit + integration + manual summary]
```

## Steps

1. **TaskUpdate** — set Phase 4 status to `in_progress`.

2. **Step One: Generate 3 approach cards in parallel** — Use the Agent tool to
   spawn 3 subagents simultaneously. Include the carry-forward summaries from
   Phase 1, 2, and 3 in each Agent tool's prompt.

   The 3 subagents should vary along these dimensions:
   - **Approach A: Minimal Change** — extend existing patterns, smallest scope,
     lowest risk
   - **Approach B: Balanced** — moderate refactoring, good extensibility,
     reasonable risk
   - **Approach C: Architectural** — introduce new abstraction, most extensible,
     highest complexity

   Each subagent returns a card using the Step One Output template above.

3. **Present to user** — Show all 3 approach cards. Use AskUserQuestion to let
   the user select one. Include trade-offs in the option descriptions.

4. **Step Two: Detail the chosen design** — After user selection, expand the
   chosen approach into a full plan using the Step Two Output template above.

5. **Produce carry-forward summary** using the template above.

6. **TaskUpdate** — set Phase 4 status to `completed`.

## Rollback

If detailing the chosen approach reveals ambiguities not caught in Phase 3:
1. TaskUpdate Phase 3 back to `pending`
2. Return to CLARIFY with specific new questions
3. Carry forward all previously established findings

## Transition

Proceed to Phase 5 (Implement). Read `implement-phase.md`.
