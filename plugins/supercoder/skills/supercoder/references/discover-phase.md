# Phase 1: Discover

> Load this reference at the start of Phase 1.

Parse the requirement and build a structured understanding of what the user wants. This phase is about making sense of raw input — the codebase comes later.

## What to Communicate

After analyzing the requirement, present these points clearly:

- **Core intent** — what the user actually wants, in one sentence
- **Scope** — what's in, what's implicitly in, what's out
- **Acceptance criteria** — numbered, testable conditions for "done"
- **Constraints** — technical, business, compatibility, performance
- **Key terms** — definitions for any ambiguous or domain-specific terms
- **Open questions** — ambiguities to resolve in Phase 3

Write it naturally. The goal is clarity, not filling in a form.

## Context to Preserve

Before finishing, make sure the conversation retains: the core intent, key scope boundaries, how many acceptance criteria exist, the most important constraints, and how many open questions remain for Phase 3. A sentence or two is enough.

## Steps

1. TaskUpdate — set Phase 1 to `in_progress`.
2. Analyze the requirement across five dimensions: core intent, scope (in/implicit/out), acceptance criteria (numbered, testable), constraints (technical/business/compatibility/performance), key terms (definitions). Present the analysis clearly.
3. Preserve context for downstream phases.
4. TaskUpdate — set Phase 1 to `completed`.

## Transition

Proceed to Phase 2 (Explore). Read `explore-phase.md`.
