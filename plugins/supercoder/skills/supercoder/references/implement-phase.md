# Phase 5: Implement — 增量实现

> Load this reference at the start of Phase 5.
> Read `context.md`, `design.md`, and `checkpoints.md` before following these steps.

Write working code, one increment at a time. Each increment is independently
verifiable and produces a tangible step forward.

## Increment Principles

1. **Independently verifiable** — Each increment can be tested on its own
2. **Small scope** — 1-3 files changed per increment
3. **Sequential by dependency** — Earlier increments don't depend on later ones
4. **High value first** — Core path before edge cases
5. **Single responsibility** — Each increment addresses one concern

## Steps

1. **Plan increments**
   Break the design's implementation plan into small increments. Write the plan
   to context.md under "Implementation Progress":
   ```markdown
   ## Implementation Progress

   ### Plan
   1. <increment 1 description> — Status: pending
   2. <increment 2 description> — Status: pending
   3. <increment 3 description> — Status: pending

   ### Completed
   (none yet)
   ```

2. **Execute each increment**:

   a. **Implement** — Use Edit/Write tools to make code changes. Follow the
      patterns and conventions identified in Phase 2.

   b. **Verify** — Run relevant tests with Bash. If the project has no tests
      for this area, verify manually (run the code, check output). Note that
      manual verification was used.

   c. **Handle failures**:
      - Test failure → Analyze the error output, fix the code, re-test
      - Max 2 retries per increment
      - On 3rd failure: pause, report to user with error details
      - Ask whether to adjust the approach or roll back to DESIGN

   d. **Check checkpoint** — If this increment corresponds to a checkpoint in
      `checkpoints.md`, pause and ask the user to review via AskUserQuestion.

   e. **Update progress** — Mark increment as completed in context.md. Add to
      "Completed" section with files changed and verification result.

3. **First increment checkpoint**
   After the FIRST increment is complete and verified, always pause for user
   confirmation — even if not listed in checkpoints.md. Present the changes
   made and the direction for next increments. This ensures the AI understood
   the requirement correctly before investing in more implementation.

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
1. Document what was found in context.md
2. Explain why the design doesn't work
3. Roll back to DESIGN phase
4. Propose an adjusted design

## Transition

After all increments are complete, proceed to Phase 6 (Verify).
Read `verify-phase.md`.
