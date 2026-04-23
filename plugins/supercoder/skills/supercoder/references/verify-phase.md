# Phase 6: Verify

Confirm the implementation meets acceptance criteria. Final quality gate.

## Output

- **Test results** — suite status, pass/fail
- **Acceptance criteria** — each marked pass/fail with specific code location
- **Edge cases** — error handling, boundaries, security, performance
- **Known limitations** — what's not covered
- **Reviewer notes** — areas needing human review

## Steps

1. Run the full test suite. Related failures: fix and re-run. Pre-existing: note and proceed.
2. Verify each acceptance criterion — identify satisfying code (file + line).
3. Scan edge cases: invalid input, boundary conditions, auth checks, injection risks, N+1 queries.
4. Present delivery summary. Ask for final confirmation via AskUserQuestion.
