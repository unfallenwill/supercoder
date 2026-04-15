# Phase 6: Verify — 验证交付

> Load this reference at the start of Phase 6.
> Read `context.md`, `understanding.md`, and `clarified.md` before following these steps.

Confirm that the implementation actually works and meets the acceptance criteria.
This is the final quality gate before delivery.

## Steps

1. **Run full test suite**
   Use Bash to run the project's full test suite.

   If tests fail:
   - **Related to new changes**: Fix and re-run. This is still part of Phase 5
     recovery. Re-run only the failing tests first, then the full suite.
   - **Pre-existing failures**: Note them and proceed. Do not fix unrelated failures.
   - **No test suite exists**: Note this explicitly. Recommend test coverage as
     a follow-up task.

2. **Verify acceptance criteria**
   For each criterion from the clarified requirement:
   - Check if it's met by the implementation
   - Identify the specific code that satisfies it (file + line reference)
   - Mark as PASS or FAIL with explanation

   If any criterion FAILS:
   - Minor: fix directly, re-verify
   - Major: roll back to IMPLEMENT or DESIGN

3. **Edge case scan**

   **Error Handling** — Are error paths covered? Invalid input? Network/API failures?

   **Boundary Conditions** — Empty inputs, maximum size, null/undefined, concurrent
   access (if applicable).

   **Security** — Input validation, authentication/authorization checks, injection
   risks (SQL, XSS, CSRF), sensitive data handling.

   **Performance** — N+1 queries, unnecessary loops, memory leaks (event listeners,
   subscriptions), large payload handling.

4. **Generate deliverables** — Write `changes.md`:
   ```markdown
   # Changes: <name>

   ## Summary
   <one paragraph describing what was built and why>

   ## Files Changed
   - `path/to/file1` — <what changed and why>
   - `path/to/file2` — <what changed and why>

   ## Acceptance Criteria Status
   1. PASS [criterion] — satisfied by [code reference]
   2. PASS [criterion] — satisfied by [code reference]
   3. WARN [criterion] — partially met: [explanation]

   ## Edge Cases Reviewed
   - [edge case]: [handled / needs attention / out of scope]

   ## Known Limitations
   - [limitation and why]

   ## PR Description

   ### Summary
   <2-3 bullet points>

   ### Test plan
   - [ ] [manual or automated test 1]
   - [ ] [manual or automated test 2]

   ## Reviewer Notes
   Specific areas that warrant extra human attention:
   - [area 1]: [why it needs careful review]
   ```

5. **Present to user** — Show the changes summary. Ask the user to confirm the
   delivery or request adjustments via AskUserQuestion.

6. **Update context.md** — Update status to "DONE". Add final summary.

## Issue Severity Guide

| Severity | Examples | Response |
|----------|---------|----------|
| Minor | Typos, missing edge case | Fix directly, re-verify |
| Moderate | Incomplete error handling | New increment, implement, re-verify |
| Major | Core functionality broken | Roll back to IMPLEMENT or DESIGN |

## Final Output

After user confirms delivery, print:

```
Supercoder complete. Outputs in .supercoder/<name>/
- input.md         — original requirement
- understanding.md — structured requirement analysis
- context.md       — accumulated project context
- clarified.md     — refined requirement after Q&A
- design.md        — chosen architectural design
- checkpoints.md   — implementation checkpoints
- changes.md       — change summary and PR description

N code changes implemented across M files.
```

The workflow is done.
