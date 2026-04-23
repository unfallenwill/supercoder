---
name: supercoder
description: >
  Trigger when the user provides a requirement, PRD, specification, or feature request
  and wants it analyzed and implemented against the codebase. Use when the user asks to
  "implement a feature," "build this," "review a spec," "analyze requirements," "plan
  implementation," "assess feasibility," or provides a PRD/spec and expects end-to-end
  delivery. DO NOT TRIGGER for bug fixes, refactoring, code explanation, single-file
  edits, or questions about existing code.
argument-hint: <requirement content, URL, or file path>
allowed-tools:
  - Agent
  - AskUserQuestion
  - TaskCreate
  - TaskUpdate
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
  - LSP
  - WebFetch
---

# Supercoder

Given a requirement, deliver working code. Six phases with user checkpoints at critical decision points.

## Input Parsing

- URL (starts with `http`): fetch with WebFetch
- File path (ends in `.md`, `.txt`, `.pdf`, or contains `/`): read with Read
- Otherwise: treat as raw requirement text

## Workflow

```
DISCOVER → EXPLORE → CLARIFY → DESIGN → IMPLEMENT → VERIFY → DONE
```

Rollback paths:

- EXPLORE ← CLARIFY
- CLARIFY ← DESIGN
- DESIGN ← IMPLEMENT
- IMPLEMENT ← VERIFY

No rollback to Discover. On rollback, carry forward all prior findings and re-enter the target phase focused on the gap that triggered it.

## Per-Phase Protocol

Applies to every phase:

1. **Task lifecycle** — on skill start, create six tasks (one per phase). Set current phase to `in_progress` at start, `completed` when done. On rollback, set target phase back to `pending`.
2. **Context carry-forward** — ensure key conclusions remain in conversation for downstream phases. Preserve: decisions made, constraints discovered, key terms defined. Do not repeat full phase output. Merge subagent results to under 500 words.
3. **Read the reference** — at phase start, read the corresponding file under `${CLAUDE_SKILL_DIR}/references/`:

| Phase | Reference |
|-------|-----------|
| 1. Discover | `discover-phase.md` |
| 2. Explore | `explore-phase.md` |
| 3. Clarify | `clarify-phase.md` |
| 4. Design | `design-phase.md` |
| 5. Implement | `implement-phase.md` |
| 6. Verify | `verify-phase.md` |

## Error Handling

- Phase failure: report what was attempted and what went wrong.
- No relevant code found: note it and proceed.

## Constraints

Every file path in outputs must reference actual files in the project.
