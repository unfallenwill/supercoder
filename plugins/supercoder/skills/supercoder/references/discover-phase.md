# Phase 1: Discover — 发现需求

> Load this reference at the start of Phase 1.
> This is the first phase — no prior context file exists yet.

Parse the requirement and build a structured understanding of what the user wants.
This phase is about making sense of raw input, not about the codebase yet.

## Steps

1. **Derive working directory name**
   Extract 2-4 kebab-case words from the requirement's:
   - Title or first heading (preferred)
   - Core topic if no clear title exists
   - Most specific noun phrase

   Examples:
   - "User Authentication Module" → `user-auth-module`
   - "Export data to CSV" → `export-csv`
   - "Refactor payment processing" → `refactor-payment`
   - "Fix the bug where users can't login on mobile" → `mobile-login-fix`

2. **Create working directory**
   - Create `.supercoder/<name>/`
   - If it exists, append numeric suffix: `.supercoder/<name>-2/`, `.supercoder/<name>-3/`
   - Never overwrite an existing directory

3. **Save raw input**
   Write the raw requirement text verbatim to `.supercoder/<name>/input.md`.
   Do not modify, summarize, or interpret — save exactly what the user provided.

4. **Extract structured understanding**
   Analyze the requirement and extract five dimensions:

   **Core Intent** — What is the user actually asking for? One clear, declarative
   sentence. If the requirement has multiple intents, list each but identify the
   primary one.

   **Scope** — What is explicitly in scope (mentioned directly), implicitly in scope
   (necessary to achieve the stated goal), and explicitly out of scope.

   **Acceptance Criteria** — Extract explicit criteria ("must support X", "should
   handle Y") and infer implicit ones from the core intent. Make each criterion
   testable (specific, measurable). Number them for traceability.

   **Constraints** — Technical (language, framework, platform), business (deadline,
   budget, compliance), backwards compatibility, performance requirements.

   **Key Terms** — Domain-specific terms needing precise definition, ambiguous words
   with multiple interpretations, acronyms needing expansion.

5. **Write understanding.md**
   ```markdown
   # Understanding: <name>

   ## Core Intent
   <one sentence>

   ## Scope
   ### In Scope
   - ...

   ### Out of Scope
   - ...

   ## Acceptance Criteria
   1. ...
   2. ...

   ## Constraints
   - ...

   ## Key Terms
   - **term**: definition

   ## Preliminary Questions
   (to be refined in Phase 3 after codebase exploration)
   - ...
   ```

6. **Initialize context.md** — Use the full 7-section template:
   ```markdown
   # Context: <name>

   ## Status: DISCOVER → EXPLORE

   ## Requirement Summary
   <core intent from understanding.md>

   ## Codebase Findings
   (to be filled in Phase 2)

   ## Clarifications
   (to be filled in Phase 3)

   ## Design Decision
   (to be filled in Phase 4)

   ## Implementation Progress
   (to be filled in Phase 5)

   ## Decisions
   (accumulated across phases)
   ```

## Transition

Update context.md status to "DISCOVER → EXPLORE" and proceed to Phase 2.
Read `explore-phase.md`.
