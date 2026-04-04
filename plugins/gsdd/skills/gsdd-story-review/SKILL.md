---
name: gsdd-story-review
description: Use before implementing any feature when the user provides a rough idea, production story, example workflow, or incomplete requirements. Converts narrative intent into an approved engineering spec.
---

# GSDD Story Review

Announce at start:
"I'm using the GSDD story-review skill to turn this request into an implementable spec."

Core rule:
Do not write production code, implementation plans, or tests yet.

Read `references/spec-checklist.md` before finalizing the spec.

## Process

1. Explore the current project context if a codebase exists.
2. Ask one clarifying question at a time.
3. Distinguish examples from rules.
4. Propose 2-3 implementation-shaping approaches when there are meaningful product or architecture choices.
5. Present the spec in short sections and confirm each section with the human partner.
6. Save the approved spec to `docs/claude-specs/YYYY-MM-DD-{feature}.md`.
7. Self-review the spec for ambiguity, contradictions, missing permissions, unclear statuses, and open questions.
8. Ask the human partner to approve the written spec before moving to planning.

## Rules For Questions

- Prefer concrete choices over open-ended questions when possible.
- If money, permissions, external systems, destructive actions, or audit requirements are ambiguous, stop and resolve them explicitly.
- If the feature is too large, decompose it and spec only the first deliverable.

## What The Spec Must Cover

- problem statement
- business goal
- actors and permissions
- trigger conditions
- happy path
- alternate paths
- failure paths
- matching or lookup rules
- statuses and state transitions
- data model changes
- file, attachment, and revision behavior
- notifications and external integrations
- observability and audit requirements
- acceptance criteria
- non-goals
- rollout notes

## Story Handling

If the user gives an example story:
- extract the underlying rules
- explicitly confirm which parts are illustrative
- avoid encoding example-specific assumptions as product behavior

## Definition Of Done

The spec is detailed enough that another agent can write failing tests without inventing business rules.
