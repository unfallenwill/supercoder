# Phase 5: Implement — 增量实现

> Load this reference at the start of Phase 5.

Write working code, one increment at a time. Each increment is independently
verifiable and produces a tangible step forward.

## Input
- Design plan from Phase 4 (chosen approach, implementation steps, testing strategy)
- Codebase patterns and conventions from Phase 2
- Carry-Forward summaries from Phase 2 and Phase 4

## Output
- Working code (files created/modified)
- Implementation Summary (template below)

```
## Implementation Summary

**Files Changed:**
- `path/to/file` — <what changed and why>

**Design Approach Implemented:** <which approach was chosen in Phase 4>

**Deviations from Design:** <any deviations and why, or "None">

**Verification Status:** <tests run, manual checks performed>
```

## Carry-Forward Summary

Before completing this phase, output a compact summary (under 100 words):

```
## Carry-Forward
- **Files changed:** [count and key paths]
- **Design approach:** [name]
- **Deviations:** [any, or "None"]
- **Test status:** [passing / failing / manual]
```

## Increment Principles

1. **Independently verifiable** — Each increment can be tested on its own
2. **Small scope** — 1-3 files changed per increment
3. **Sequential by dependency** — Earlier increments don't depend on later ones
4. **High value first** — Core path before edge cases
5. **Single responsibility** — Each increment addresses one concern

## Steps

1. **TaskUpdate** — set Phase 5 status to `in_progress`.

2. **Plan increments** — Break the design's implementation plan into small
   increments. Use TaskCreate for each increment as a sub-task.

3. **Execute each increment**:

   a. **TaskUpdate** the increment task to `in_progress`.

   b. **Implement** — Use Edit/Write tools to make code changes. Follow the
      patterns and conventions identified in Phase 2.

   c. **Verify** — Run relevant tests with Bash. If no tests exist for this
      area, verify manually and note that manual verification was used.

   d. **Handle failures**:
      - Test failure → Analyze error output, fix the code, re-test
      - Max 2 retries per increment
      - On 3rd failure: pause, report to user with error details
      - Ask whether to adjust the approach or roll back to DESIGN

   e. **TaskUpdate** the increment task to `completed`.

4. **First increment checkpoint** — After the FIRST increment is complete and
   verified, always pause for user confirmation via AskUserQuestion. Present
   the changes made and the direction for next increments. This ensures the
   implementation is on track before investing in more work.

5. **Implementation Summary** — After ALL increments are complete, present a
   consolidated summary using the Output template above.

6. **Produce carry-forward summary** using the Carry-Forward template above.

7. **TaskUpdate** — set Phase 5 status to `completed`.

## Error Recovery

| Error Type | Response |
|-----------|----------|
| Compile/type error | Fix immediately, no need to ask user |
| Test failure | Retry up to 2 times, then escalate |
| Persistent failure | Escalate to user with error details |
| Design doesn't fit | Roll back to DESIGN with explanation |
| Scope creep | Stop, ask user. Do not gold-plate |

## Anti-Patterns to Avoid

- **Gold-plating**: Adding features not in the design
- **Preemptive refactoring**: Cleaning up unrelated code
- **Over-engineering**: Adding abstractions for hypothetical future needs
- **Skipping verification**: Moving on without confirming the increment works

## Rollback to DESIGN

If implementation reveals fundamental design issues:
1. Report what was found in conversation
2. Explain why the design doesn't work
3. TaskUpdate Phase 4 back to `pending`
4. Propose an adjusted design (carry forward prior findings)

## Transition

Proceed to Phase 6 (Verify). Read `verify-phase.md`.
