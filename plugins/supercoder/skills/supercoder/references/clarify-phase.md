# Phase 3: Clarify — 澄清歧义

> Load this reference at the start of Phase 3.

Use codebase context to ask targeted clarifying questions. Turn "what the user said"
into "what the user means."

## Input
- Structured understanding from Phase 1 (Core Intent, Scope, Acceptance Criteria, Key Terms)
- Codebase findings from Phase 2 (relevant files, patterns, constraints)
- Carry-Forward summaries from Phase 1 and Phase 2

## Output

```
## Clarified Requirement

### Refined Scope
- In: [updated items]
- Implicit: [updated items]
- Out: [updated items]

### Refined Acceptance Criteria
1. [updated criterion]
2. [updated criterion]

### Key Decisions
- **[Decision 1]:** [user's answer] — Impact: [how this changes the approach]
- **[Decision 2]:** [user's answer] — Impact: [how this changes the approach]
```

## Carry-Forward Summary

Before completing this phase, output a compact summary (under 100 words):

```
## Carry-Forward
- **Refined intent:** [one line]
- **Scope changes:** [what changed from Phase 1]
- **Criteria count:** [N updated acceptance criteria]
- **Key decisions:** [top 1-2 decisions and their impact]
```

## Principle

Good clarification questions are specific and grounded in the codebase. Compare:

- **Weak**: "What payment methods do you want?" (generic, no context)
- **Strong**: "The codebase has WechatPay and AliPay adapters in
  `src/payments/adapters/`. Should new methods follow this adapter pattern, or
  refactor to a plugin architecture?" (specific, references actual code, offers
  concrete options)

## Steps

1. **TaskUpdate** — set Phase 3 status to `in_progress`.

2. **Generate 3-5 targeted questions** (if more than 8 exist, prioritize the
   top 8 and note the rest for potential follow-up).
   Based on the requirement AND codebase findings, identify the most critical
   ambiguities. For each question:
   - State the ambiguity clearly
   - Reference specific code/files that create the ambiguity
   - Offer 2-3 concrete options where possible (using AskUserQuestion options)

   Prioritize questions that:
   1. Block architectural decisions (highest priority)
   2. Affect the scope of work significantly
   3. Resolve conflicting interpretations
   4. Clarify edge cases in acceptance criteria

3. **Present to user** — Use AskUserQuestion. Max 4 questions per batch.
   If more than 4, batch them. For each question, provide:
   - Clear header (short label)
   - The question with codebase context
   - 2-3 options with descriptions

4. **Incorporate answers** — Present updated scope and acceptance criteria
   using the Output template above.

5. **Produce carry-forward summary** using the template above.

6. **TaskUpdate** — set Phase 3 status to `completed`.

## Rollback

If clarification reveals insufficient exploration (e.g., user mentions a module
not found during Phase 2):
1. TaskUpdate Phase 2 back to `pending`
2. Re-run exploration with the additional focus area (carry forward prior findings)
3. Return to CLARIFY with updated context

## Transition

Proceed to Phase 4 (Design). Read `design-phase.md`.
