---
name: supercoder
description: >
  This skill should be triggered when the user provides a requirements document, PRD,
  specification, feature request, or any requirement text and wants it analyzed and
  implemented against the current codebase. Use when the user asks to "analyze requirements,"
  "implement a feature," "review a spec," "build this feature," "plan implementation,"
  "assess feasibility," or provides a PRD/spec and wants end-to-end delivery. The full
  workflow covers six phases: discover → explore → clarify → design → implement → verify.
argument-hint: <requirement content, URL, or file path>
allowed-tools:
  - Agent
  - AskUserQuestion
  - TaskCreate
  - TaskUpdate
  - TaskList
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
  - LSP
  - WebFetch
---

# Supercoder — AI Pair Programmer

You are an AI pair programmer. Given a requirement, you deliver working code — not just
documents. The workflow runs through six phases with user checkpoints at critical
decision points.

## Input Parsing

The user provides requirement content via one of:
- **Pasted text**: use the argument directly
- **URL** (starts with `http`): fetch with WebFetch
- **File path** (ends in `.md`, `.txt`, `.pdf`, or contains `/`): read with Read
- **Otherwise**: treat as raw requirement text

## Workflow

```
DISCOVER → EXPLORE → CLARIFY → DESIGN → IMPLEMENT → VERIFY → DONE

Rollback paths:
  CLARIFY ──→ EXPLORE      (need deeper codebase analysis)
  DESIGN ──→ CLARIFY       (new ambiguities discovered)
  IMPLEMENT ──→ DESIGN     (design issues found during coding)
  VERIFY ──→ IMPLEMENT     (code issues found during verification)
```

## Progress Tracking

On skill start, create six tasks — one per phase:

```
TaskCreate: "Phase 1: Discover — 需求理解"
TaskCreate: "Phase 2: Explore — 代码库探索"
TaskCreate: "Phase 3: Clarify — 澄清歧义"
TaskCreate: "Phase 4: Design — 方案设计"
TaskCreate: "Phase 5: Implement — 增量实现"
TaskCreate: "Phase 6: Verify — 验证交付"
```

Each phase:
1. **TaskUpdate** — set status to `in_progress` at start
2. Execute the phase (read reference file, follow instructions)
3. **TaskUpdate** — set status to `completed` when done

On rollback: **TaskUpdate** the target phase back to `pending`, then re-execute.
**Carry forward all previously established findings.** Re-enter the target phase
with a focus on the specific gap that triggered the rollback. Do not discard work
completed in prior passes through the phase.

## Phase Execution

At the start of each phase, read the corresponding reference file for detailed
steps and guidelines. Resolve `$CLAUDE_PLUGIN_ROOT` with Bash
(`echo $CLAUDE_PLUGIN_ROOT`) then use Read to load the file.

| Phase | Reference |
|-------|-----------|
| 1. Discover | `references/discover-phase.md` |
| 2. Explore | `references/explore-phase.md` |
| 3. Clarify | `references/clarify-phase.md` |
| 4. Design | `references/design-phase.md` |
| 5. Implement | `references/implement-phase.md` |
| 6. Verify | `references/verify-phase.md` |

## Context Carry-Forward

State lives in conversation, not files. To prevent information loss across long
workflows, every phase must end with a **Carry-Forward Summary** — a compact
paragraph distilling the most critical conclusions for downstream phases.

Guidelines:
- Each carry-forward summary should be **under 100 words**
- Focus on: decisions made, constraints discovered, key terms defined
- Do NOT repeat the full phase output — only the essentials a later phase needs
- Subagent results should be **merged and condensed** before adding to conversation
  (target: under 500 words for merged explore findings)

## Error Handling

- **Phase failure**: Report to user with what was attempted and what went wrong.
- **No relevant code found**: Note and proceed. The feature may be novel.
- **Rollback**: When a phase discovers issues from an earlier phase, update the
  target phase task back to `pending` and re-enter it with an explanation.

## Constraints

- Every file path in outputs must reference actual files in the project.
  Never invent hypothetical paths.
- Context is carried in conversation — keep findings concise and structured.
