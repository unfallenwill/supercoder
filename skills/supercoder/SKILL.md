---
name: supercoder
version: 1.0.0
description: >
  This skill should be used when the user provides a requirements document, PRD, specification,
  feature request, or any requirement text and wants it analyzed against the current codebase.
  Useful when the user asks to "analyze requirements," "review a spec," "break down tasks,"
  "create a design doc," "plan implementation," or "assess feasibility." Produces a structured
  review, task breakdown, and technical design in the .supercoder/ working directory.
argument-hint: <requirement content, URL, or file path>
allowed-tools:
  - Agent
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
  - AskUserQuestion
  - WebFetch
---

# Supercoder

You are a requirements analysis pipeline. Given a requirements document, produce a review, task
breakdown, and technical design — all grounded in the current project's actual codebase.

## Input

The user provides requirement content via one of:
- Pasted text (the argument itself)
- A URL — fetch it with WebFetch and extract the text content
- A local file path — read it with Read

If the argument looks like a URL (starts with http), fetch it. If it looks like a file path
(ends in .md, .txt, .pdf, or contains /), read it. Otherwise treat the argument as raw requirement
text.

## Pipeline

Execute these steps in order. Each step builds on the previous one. Write every output to disk
before proceeding.

### Step 1: Create Working Directory

1. Read the requirement content and extract a short descriptive name (2-4 kebab-case words)
   from the title, first heading, or core topic. Examples:
   - "User Authentication Module" → `user-auth-module`
   - "Export data to CSV" → `export-csv`
   - "Refactor payment processing" → `refactor-payment`
2. Create directory: `.supercoder/<name>/`
3. If the directory already exists, append a numeric suffix: `.supercoder/<name>-2/`
4. Write the raw requirement content to `.supercoder/<name>/input.md`

### Step 2: Requirements Review

Use the `feature-dev:code-explorer` agent (subagent_type: "feature-dev:code-explorer") to deeply
analyze the codebase areas relevant to the requirement. Pass it:

- The full requirement text
- The specific technical domains mentioned in the requirement
- Instructions to trace execution paths, map architecture layers, and identify existing patterns
  that relate to the requirement

If the agent is not available, perform the analysis directly using Read, Grep, and Glob tools.
Examine the project's directory structure, identify relevant modules, read key files, and note
the reduced analysis depth in the output.

After the agent returns (or direct analysis completes), synthesize findings into a structured review:

Write `.supercoder/<name>/analysis.md` with these sections:

```markdown
# Requirements Review: <name>

## Summary
One-paragraph summary of the requirement.

## Project Context
What existing code is relevant. Reference specific file paths and modules.

## Feasibility Assessment
Can this be built with the current architecture? What constraints exist?

## Risk Analysis
- Technical risks
- Dependency risks
- Scope risks

## Open Questions
Unresolved ambiguities that need clarification before implementation.
```

### Step 3: Task Breakdown

Use the `feature-dev:code-architect` agent (subagent_type: "feature-dev:code-architect") to design
a concrete implementation blueprint. Pass it:

- The requirement text
- The analysis from Step 2 (read `.supercoder/<name>/analysis.md`)
- Instructions to produce a build sequence with specific files to create/modify, component designs,
  and data flows

If the agent is not available, perform the breakdown directly by reading the project structure,
identifying files that need to change, and producing the task list based on the analysis.
Note the reduced architectural depth in the output.

After the agent returns (or direct analysis completes), synthesize into an actionable task list:

Write `.supercoder/<name>/tasks.md` with these sections:

```markdown
# Task Breakdown: <name>

## Overview
Brief description of the implementation approach.

## Tasks

### Task 1: <title>
- **Files**: specific paths to create or modify
- **What**: concrete description of changes
- **Dependencies**: none / depends on Task N

### Task 2: <title>
- **Files**: specific paths to create or modify
- **What**: concrete description of changes
- **Dependencies**: depends on Task N

(Continue for all tasks)
```

Order tasks by dependency — earlier tasks must be completable without later ones. Reference real
file paths from the project.

### Step 4: Technical Design

Use the `Plan` agent (subagent_type: "Plan") to create a step-by-step implementation plan.
Pass it:

- The requirement text
- The analysis from Step 2
- The task breakdown from Step 3
- Instructions to design the implementation strategy considering architectural trade-offs

If the agent is not available, produce the design directly by reading the analysis and tasks,
then writing a structured implementation plan based on the project's architecture and conventions.
Note the reduced planning depth in the output.

After the agent returns (or direct analysis completes), synthesize into a final design document:

Write `.supercoder/<name>/design.md` with these sections:

```markdown
# Technical Design: <name>

## Architecture Decision
Key architectural choices and rationale.

## Implementation Plan
Step-by-step plan with:
- What to implement in each step
- Which files change
- How to verify each step works

## Data Model Changes
(if applicable) Schema changes, new types, migrations needed.

## API Changes
(if applicable) New endpoints, modified contracts.

## Testing Strategy
How to test the implementation — unit, integration, manual.

## Migration / Rollout Plan
(if applicable) How to deploy safely.
```

### Step 5: Summary

After all steps complete, print a brief summary to the user. Replace `<name>` with the actual
directory name and `N` with the actual task count:

```
Analysis complete. Outputs in .supercoder/<name>/
- input.md     — original requirement
- analysis.md  — review and risk assessment
- tasks.md     — N tasks in dependency order
- design.md    — technical implementation plan
```

## Error Handling

- If code-explorer finds no relevant code, note this in analysis.md and proceed — the project
  may be new or the feature is genuinely novel.
- If a step fails, save whatever was produced so far and report the error to the user.
  Do not discard partial results.

## Important Notes

- Every file path in tasks.md and design.md must reference actual files in the project.
  Never invent hypothetical paths.
- The pipeline is sequential — each step depends on the previous step's output.
- Read the output files back before passing context to the next agent, to ensure continuity.
- Keep the working directory structure flat: no nesting beyond `.supercoder/<name>/`.
