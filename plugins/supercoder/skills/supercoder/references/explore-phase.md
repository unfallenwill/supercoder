# Phase 2: Explore — 代码库探索

> Load this reference at the start of Phase 2.

Deeply analyze the codebase to understand how the project works and how the
requirement relates to existing code. This phase delegates exploration to 3
parallel subagents for efficiency.

## Input
- Structured understanding from Phase 1 (in conversation)
- Carry-Forward summary from Phase 1

## Output
Merged codebase exploration findings (target: under 500 words):

```
## Explore Findings

### Architecture
<how the project is organized>

### Relevant Files
- `path/to/file` — <role and why it's relevant>

### Existing Patterns
- <pattern>: <description and where it's used>

### Similar Implementations
- <feature>: <how it was done, files involved>

### Impact Radius
<N> files across <M> modules would be affected.

### Constraints Discovered
- <constraint>: <where it comes from>
```

## Carry-Forward Summary

Before completing this phase, output a compact summary (under 100 words):

```
## Carry-Forward
- **Architecture:** [style in one line]
- **Key files:** [top 3-5 relevant paths]
- **Pattern to follow:** [primary pattern name]
- **Impact:** [N files, M modules]
- **Constraint:** [top 1-2 discovered constraints]
```

## Steps

1. **TaskUpdate** — set Phase 2 status to `in_progress`.

2. **Launch 3 parallel subagents** — Use the Agent tool to spawn 3 agents
   simultaneously. Include the Phase 1 carry-forward summary in each Agent
   tool's prompt so they know what to explore.

3. **Collect and synthesize** — After all 3 agents return, merge their findings
   into a unified summary using the Output template. Discard redundant findings
   between subagents to stay under 500 words.

4. **Produce carry-forward summary** using the template above.

5. **TaskUpdate** — set Phase 2 status to `completed`.

### Subagent Assignments

**Explorer-1: Structure & Pattern**
- Directory organization (src/, lib/, tests/, config/)
- Module boundaries and responsibilities
- Entry points (main, index, app)
- Build system and dependency management
- Architecture style (MVC, layered, hexagonal, event-driven)
- Naming patterns (files, classes, functions)
- Import/dependency patterns

**Explorer-2: Impact & Convention**
- Files and modules directly related to the requirement
- Files that import or depend on those modules
- Shared utilities or services that would be used
- Database models or schemas involved
- Error handling approach (exceptions, results, null checks)
- Logging, test structure, and configuration conventions

**Explorer-3: Precedent**
- Similar features previously implemented
- Patterns to follow for consistency
- Anti-patterns to avoid
- Reusable components or utilities

### Subagent Output Format

Each subagent must return findings in this format for easy merging:

```
## [Subagent Name]

### Architecture
<how the project is organized — only Explorer-1 fills this>

### Relevant Files
- `path/to/file` — <role and why it's relevant>

### Existing Patterns
- <pattern>: <description and where it's used>

### Similar Implementations
- <feature>: <how it was done, files involved>

### Impact Radius
<N> files across <M> modules would be affected.

### Constraints Discovered
- <constraint>: <where it comes from>
```

### Key Principles for All Subagents

- Reference specific file paths, not vague descriptions
- Note patterns the implementation should follow for consistency
- Identify potential conflicts or constraints early
- If no relevant code is found, note this explicitly — the feature may be novel
- LSP tools (go to definition, find references) can improve exploration depth

## Transition

Proceed to Phase 3 (Clarify). Read `clarify-phase.md`.
