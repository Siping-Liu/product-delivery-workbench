---
name: product-delivery-requirements
description: Requirements domain routing and workflow for story drafting, review-first approval, and Jira execution.
disable-model-invocation: true
---

# Requirements Domain - SKILL

## Purpose

This skill governs requirements-domain work, especially user-story generation and Jira delivery workflow.

## Global Rules

1. Use `wiki/` as the latest trusted business context before drafting stories.
2. Generate draft story content in chat first by default.
3. Always request user review before any Jira write action.
4. Use `connectors/jira/SKILL.md` for Jira read/write behavior and safety.
5. Do not update `wiki/` while drafting stories unless user explicitly asks for ingest.

## Routing

Choose the workflow based on user intent:

- Story drafting or refinement -> `skills/requirements/user-story-generation.md`
- Jira read/write for story cards -> `connectors/jira/SKILL.md`

Default for requirement requests: `skills/requirements/user-story-generation.md`.

## Required End-to-End Sequence

For story generation requests, execute this sequence:

1. Identify requested story scope from user input.
2. Retrieve relevant context from `wiki/` (do not skip this step).
3. Draft user story content using the requirements workflow.
4. Present draft for user review.
5. Wait for explicit confirmation.
6. Only after confirmation, create or update Jira story via `connectors/jira/SKILL.md`.

## Output Contract

Each run should return:

- Scope understanding
- Wiki pages used as context
- Story draft (or story change proposal)
- Open questions or assumptions
- Jira action status (only when user requested and confirmed Jira write)
