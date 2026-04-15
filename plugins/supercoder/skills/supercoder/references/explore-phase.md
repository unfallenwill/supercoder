# Phase 2: Explore — 探索代码库

> Load this reference at the start of Phase 2.
> Read `context.md` and `input.md` before following these steps.

Deeply analyze the codebase to understand how the project works and how the
requirement relates to existing code. This is about exploration and mapping,
not about making design decisions.

## Exploration Method

Perform codebase analysis directly using Read, Grep, Glob, and LSP tools.
Work through the layers below systematically, reading key files and tracing
execution paths related to the requirement.

## What to Look For

### Structure Layer
- Directory organization (src/, lib/, tests/, config/)
- Module boundaries and responsibilities
- Entry points (main, index, app)
- Build system and dependency management

### Pattern Layer
- Architecture style (MVC, layered, hexagonal, event-driven)
- Code organization conventions
- Naming patterns (files, classes, functions)
- Import/dependency patterns

### Convention Layer
- Error handling approach (exceptions, results, null checks)
- Logging patterns
- Test structure and conventions
- Configuration management

### Impact Layer
- Files and modules directly related to the requirement
- Files that import or depend on those modules
- Shared utilities or services that would be used
- Database models or schemas involved

### Precedent Layer
- Similar features previously implemented
- Patterns to follow for consistency
- Anti-patterns to avoid

## Synthesize Findings

Update context.md under "Codebase Findings" with:

```markdown
## Codebase Findings

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

Keep the context.md entry concise — this file is read at the start of every
subsequent phase.

## Key Principles

- Reference specific file paths, not vague descriptions
- Note patterns the implementation should follow for consistency
- Identify potential conflicts or constraints early
- If no relevant code is found, note this explicitly — the project may be new
  or the feature genuinely novel

## Transition

Update context.md status to "EXPLORE → CLARIFY" and proceed to Phase 3.
Read `clarify-phase.md`.
