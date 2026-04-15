# Phase 3: Clarify — 澄清歧义

> Load this reference at the start of Phase 3.
> Read `context.md` and `understanding.md` before following these steps.

Use codebase context to ask targeted clarifying questions. Turn "what the user said"
into "what the user means."

## Principle

Good clarification questions are specific and grounded in the codebase. Compare:

- **Weak**: "What payment methods do you want?" (generic, no context)
- **Strong**: "The codebase has WechatPay and AliPay adapters in
  `src/payments/adapters/`. Should new methods follow this adapter pattern, or
  refactor to a plugin architecture?" (specific, references actual code, offers
  concrete options)

## Steps

1. **Load context** — Read `context.md` and `understanding.md`.

2. **Generate 3-5 targeted questions**
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

3. **Present to user** — Use AskUserQuestion to present questions. Max 4 questions
   per batch. If you have more than 4, batch them.

   For each question, provide:
   - Clear header (short label)
   - The question with codebase context
   - 2-3 options with descriptions
   - "Other" is available automatically for custom answers

4. **Incorporate answers** — Write `clarified.md`:
   ```markdown
   # Clarified Requirement: <name>

   ## Original Intent
   <from understanding.md>

   ## Clarifications

   ### Q: <question text>
   **A:** <user's answer>
   **Impact:** <how this changes the approach>

   (repeat for each question)

   ## Refined Scope
   Updated scope incorporating all clarifications.

   ## Refined Acceptance Criteria
   Updated criteria incorporating all clarifications.
   1. [updated criterion 1]
   2. [updated criterion 2]
   ```

5. **Update context.md** — Add a "Clarifications" section with a concise summary
   of key decisions. Update status to "CLARIFY → DESIGN".

## Rollback

If clarification reveals that the codebase exploration was insufficient
(e.g., the user mentions a module not found during Phase 2):

1. Note the gap in context.md
2. Roll back to EXPLORE phase
3. Re-run exploration with the additional focus area
4. Then return to CLARIFY with updated context

## Transition

Proceed to Phase 4 (Design). Read `design-phase.md`.
