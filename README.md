# Supercoder

Supercoder is a Claude Code plugin that turns a requirement into an implementation workflow. It guides an agent through discovery, codebase exploration, clarification, design, implementation, and verification.

The project is intentionally small: the core behavior lives in one skill definition, with each workflow phase documented in a focused reference file.

## What It Does

Supercoder is designed for requests such as:

- "Analyze this PRD and implement it."
- "Build this feature in the current codebase."
- "Review this spec and turn it into working code."
- "Assess feasibility, plan the implementation, then deliver it."

The workflow is:

```text
DISCOVER -> EXPLORE -> CLARIFY -> DESIGN -> IMPLEMENT -> VERIFY
```

Each phase has a specific job:

- **Discover**: parse the requirement, define scope, acceptance criteria, constraints, and key terms.
- **Explore**: inspect the target codebase, identify relevant files, patterns, constraints, and precedent.
- **Clarify**: ask targeted technical questions only when decisions are blocked.
- **Design**: compare implementation approaches and expand the selected one into a concrete plan.
- **Implement**: make incremental, verifiable code changes.
- **Verify**: run tests, check acceptance criteria, scan edge cases, and summarize delivery status.

## Repository Layout

```text
.
├── .claude-plugin/
│   └── marketplace.json
├── plugins/
│   └── supercoder/
│       ├── .claude-plugin/
│       │   └── plugin.json
│       └── skills/
│           └── supercoder/
│               ├── SKILL.md
│               └── references/
│                   ├── discover-phase.md
│                   ├── explore-phase.md
│                   ├── clarify-phase.md
│                   ├── design-phase.md
│                   ├── implement-phase.md
│                   └── verify-phase.md
└── CLAUDE.md
```

Important files:

- `plugins/supercoder/.claude-plugin/plugin.json`: plugin metadata.
- `.claude-plugin/marketplace.json`: marketplace metadata for publishing/discovery.
- `plugins/supercoder/skills/supercoder/SKILL.md`: skill entry point and phase orchestration.
- `plugins/supercoder/skills/supercoder/references/*.md`: detailed instructions for each phase.
- `CLAUDE.md`: repository-level contributor instructions.

## Installation

Install the plugin from this repository using the Claude Code plugin flow.

The marketplace metadata points to:

```text
https://github.com/unfallenwill/supercoder.git
```

After installation, the `supercoder` skill is available when a user provides a requirement, PRD, spec, feature request, or implementation request.

## Usage

Invoke the skill with requirement content, a requirement file path, or a URL:

```text
Use supercoder to implement the feature described in docs/checkout-refactor.md
```

```text
Use supercoder:

Add CRUD endpoints for todo items. Todos need a title, optional description,
completed flag, created_at, updated_at, pagination, validation, and tests.
```

Supercoder will parse the input as:

- URL: fetched with the available web fetch tool.
- File path: read from the current workspace.
- Raw text: treated as the requirement directly.

## Workflow Details

Supercoder uses task tracking for the six phases. Each phase is marked in progress when it starts and completed when it finishes.

Rollback paths are allowed when later work reveals a gap:

- Clarification may return to exploration.
- Design may return to clarification.
- Implementation may return to design.
- Verification may return to implementation.

State is carried in the conversation, not in generated project files. Each phase preserves only the conclusions needed by later phases: decisions, constraints, accepted scope, and verification status.

## Development

This repository currently contains plugin documentation and metadata only. There is no runtime package, dependency manager, or test suite yet.

Useful local checks:

```sh
jq empty plugins/supercoder/.claude-plugin/plugin.json .claude-plugin/marketplace.json
```

```sh
find plugins/supercoder/skills/supercoder -type f -name '*.md' -print
```

When editing the skill:

- Keep phase files focused on their own responsibilities.
- Avoid duplicating instructions across phases.
- Reference actual project paths only.
- Keep the workflow executable by an agent, not just readable by humans.

## Commit Convention

Every commit must include this trailer:

```text
Co-Authored-By: GLM 5.1 <noreply@z.ai>
```

## Status

Current maturity: early but usable.

The next quality improvements should be:

- Add example runs that show expected outputs.
- Add evals or fixtures to validate workflow behavior.
- Add release checks for plugin metadata and documentation consistency.
