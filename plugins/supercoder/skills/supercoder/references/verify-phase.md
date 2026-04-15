# Phase 6: Verify — 验证交付

> Load this reference at the start of Phase 6.

Confirm that the implementation actually works and meets the acceptance criteria.
This is the final quality gate before delivery.

## Input
- Refined Acceptance Criteria from Phase 3
- Design plan from Phase 4 (what was intended)
- Implementation Summary from Phase 5 (files changed, deviations)
- Carry-Forward summaries from Phase 3, 4, and 5

## Output

```
## Verification Results

### Test Results
- Suite: [ran / not available]
- Status: [all pass / N failures]
- Pre-existing failures: [none / listed]

### Acceptance Criteria Status
1. PASS — [criterion] — satisfied by `file:line`
2. PASS — [criterion] — satisfied by `file:line`
3. FAIL — [criterion] — reason: [explanation]

### Edge Case Scan
- **Error handling:** [covered / needs attention: details]
- **Boundary conditions:** [covered / needs attention: details]
- **Security:** [covered / needs attention: details]
- **Performance:** [covered / needs attention: details]

### Known Limitations
- [limitation and why]

### PR Description
**Summary:**
- [bullet 1]
- [bullet 2]

**Test plan:**
- [ ] [test 1]
- [ ] [test 2]

### Reviewer Notes
- [area]: [why it needs careful review]
```

## Steps

1. **TaskUpdate** — set Phase 6 status to `in_progress`.

2. **Run full test suite**
   Use Bash to run the project's full test suite.

   If tests fail:
   - **Related to new changes**: Fix and re-run. Re-run only the failing tests
     first, then the full suite.
   - **Pre-existing failures**: Note them and proceed. Do not fix unrelated failures.
   - **No test suite exists**: Note this explicitly. Recommend test coverage as
     a follow-up task.

3. **Verify acceptance criteria**
   For each criterion from Phase 3's refined acceptance criteria:
   - Check if it's met by the implementation
   - Identify the specific code that satisfies it (file + line reference)
   - Mark as PASS or FAIL with explanation

   If any criterion FAILS:
   - Minor: fix directly, re-verify
   - Major: roll back to IMPLEMENT or DESIGN

4. **Edge case scan**

   **Error Handling** — Are error paths covered? Invalid input? Network/API failures?

   **Boundary Conditions** — Empty inputs, maximum size, null/undefined, concurrent
   access (if applicable).

   **Security** — Input validation, authentication/authorization checks, injection
   risks (SQL, XSS, CSRF), sensitive data handling.

   **Performance** — N+1 queries, unnecessary loops, memory leaks (event listeners,
   subscriptions), large payload handling.

5. **Present delivery summary** — Show the user the full Output above.

6. **Ask user to confirm** — Use AskUserQuestion for final approval or adjustments.

7. **TaskUpdate** — set Phase 6 status to `completed`.

## Issue Severity Guide

| Severity | Examples | Response |
|----------|---------|----------|
| Minor | Typos, missing edge case | Fix directly, re-verify |
| Moderate | Incomplete error handling | New increment, implement, re-verify |
| Major | Core functionality broken | Roll back to IMPLEMENT or DESIGN |

## Rollback

For major issues found during verification:
1. Report the issue with specific details
2. TaskUpdate Phase 5 (or Phase 4) back to `pending`
3. Re-enter the appropriate phase with explanation (carry forward prior findings)

## Done

After user confirms delivery, the workflow is complete.
