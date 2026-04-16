# Supercoder

A Claude Code plugin that turns a requirement into working code through an interactive six-phase workflow.

## Workflow

```text
DISCOVER → EXPLORE → CLARIFY → DESIGN → IMPLEMENT → VERIFY
```

Each phase has a specific job:

- **Discover** — parse the requirement, define scope, acceptance criteria, constraints
- **Explore** — inspect the codebase, identify relevant files, patterns, precedent
- **Clarify** — ask targeted technical questions when decisions are blocked
- **Design** — compare approaches, expand the chosen one into a concrete plan
- **Implement** — make incremental, verifiable code changes
- **Verify** — run tests, check acceptance criteria, scan edge cases

Rollback paths exist when later phases reveal gaps: Clarify → Explore, Design → Clarify, Implement → Design, Verify → Implement.

## Installation

```sh
npx skills add unfallenwill/supercoder -g -y
```

## Usage

Provide a requirement as text, a file path, or a URL:

```text
Use supercoder to implement the feature described in docs/checkout-refactor.md
```

```text
Use supercoder:
Add CRUD endpoints for todo items. Todos need a title, optional description,
completed flag, timestamps, pagination, validation, and tests.
```

Supercoder parses input automatically: URLs are fetched, file paths are read, everything else is treated as raw requirement text.

## Repository Layout

```text
plugins/supercoder/
├── .claude-plugin/plugin.json
└── skills/supercoder/
    ├── SKILL.md                  # Phase orchestration
    └── references/               # Per-phase instructions
        ├── discover-phase.md
        ├── explore-phase.md
        ├── clarify-phase.md
        ├── design-phase.md
        ├── implement-phase.md
        └── verify-phase.md
```
