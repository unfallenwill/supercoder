# Phase 3: Clarify

> Load this reference at the start of Phase 3.

Use codebase context to ask targeted clarifying questions. Turn "what the user said" into "what the user means."

## What to Communicate

After getting the user's answers, present:

- **Refined scope** — updated in/implicit/out boundaries
- **Refined acceptance criteria** — updated based on answers
- **Key decisions** — each decision, the user's answer, and how it changes the approach

## Context to Preserve

Before finishing, make sure the conversation retains: the refined intent, what changed from Phase 1, the updated acceptance criteria count, and the top decisions with their impact.

## Principle

Good clarification questions are specific and grounded in the codebase. Compare:

- Weak: "What payment methods do you want?" (generic, no context)
- Strong: "The codebase has WechatPay and AliPay adapters in `src/payments/adapters/`. Should new methods follow this adapter pattern, or refactor to a plugin architecture?" (specific, references actual code, offers concrete options)

## Steps

1. TaskUpdate — set Phase 3 to `in_progress`.
2. Generate up to 8 prioritized questions. For each question, state the ambiguity clearly, reference specific code or files that create it, and offer 2–3 concrete options where possible.

   Prioritize questions that:
   1. Block architectural decisions (highest priority)
   2. Affect the scope of work significantly
   3. Resolve conflicting interpretations
   4. Clarify edge cases in acceptance criteria

3. Present to user — use AskUserQuestion, up to 4 questions per batch. Each question gets a clear header, the context, and 2–3 options with descriptions.
4. Incorporate answers — present updated scope and acceptance criteria.
5. Preserve context for downstream phases.
6. TaskUpdate — set Phase 3 to `completed`.

## Rollback

If clarification reveals insufficient exploration (e.g., the user mentions a module not found in Phase 2): set Phase 2 back to `pending`, re-run exploration with the additional focus area (carrying forward prior findings), then return to Clarify with updated context.

## Transition

Proceed to Phase 4 (Design). Read `design-phase.md`.
