# Phase 1: Discover — 需求理解

> Load this reference at the start of Phase 1.

Parse the requirement and build a structured understanding of what the user wants.
This phase is about making sense of raw input, not about the codebase yet.

## Input
- Requirement content from user (already fetched/resolved by SKILL.md Input Parsing)

## Output
Structured understanding presented in conversation:

```
### Requirement: [Title]

**Core Intent:** [one sentence]

**Scope:**
- In: [items]
- Implicit: [items]
- Out: [items]

**Acceptance Criteria:**
1. [criterion]
2. [criterion]

**Constraints:** [list]

**Key Terms:** [term: definition pairs]

**Preliminary Questions:** [list for Phase 3]
```

## Carry-Forward Summary

Before completing this phase, output a compact summary (under 100 words) for
downstream phases:

```
## Carry-Forward
- **Intent:** [core intent in one line]
- **Scope:** [key in/out items]
- **Criteria count:** [N acceptance criteria]
- **Key constraints:** [top 1-2 constraints]
- **Open questions:** [count] preliminary questions for Phase 3
```

## Steps

1. **TaskUpdate** — set Phase 1 status to `in_progress`.

2. **Extract structured understanding** — Analyze the requirement across five
   dimensions: Core Intent, Scope (in/implicit/out), Acceptance Criteria (numbered,
   testable), Constraints (technical/business/compat/performance), Key Terms
   (definitions). Present using the Output template above.

3. **Produce carry-forward summary** using the template above.

4. **TaskUpdate** — set Phase 1 status to `completed`.

## Transition

Proceed to Phase 2 (Explore). Read `explore-phase.md`.
