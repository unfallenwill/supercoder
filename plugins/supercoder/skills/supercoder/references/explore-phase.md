# Phase 2: Explore

Analyze the codebase to understand how the project works and how the requirement relates to existing code.

## Output

After merging subagent results, present a unified picture (under 500 words):

- **Architecture** — project organization
- **Relevant files** — each file's role and relevance
- **Existing patterns** — conventions to follow
- **Similar implementations** — precedent features
- **Impact radius** — files and modules affected
- **Constraints discovered** — from code structure or tech stack

## Steps

1. Launch three parallel subagents via Agent tool. Include the requirement context in each prompt:

   **Explorer-1: Structure** — directory layout, module boundaries, architecture style, naming conventions, build system.

   **Explorer-2: Impact** — files related to the requirement, their dependents, shared utilities, database schemas, test structure, error handling patterns.

   **Explorer-3: Precedent** — similar features previously implemented, reusable components, patterns to follow.

2. Merge findings, deduplicate across subagents.
