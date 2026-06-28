---
name: product-delivery-workbench
description: Project-level global rules for the Product Delivery Workbench. Use this as the top-level contract, then delegate to domain skills.
disable-model-invocation: true
---

# Product Delivery Workbench - Global Rules

## Purpose

This file defines project-level global rules for the Product Delivery Workbench.
It applies across all domains, including `biz-knowledge-base` and `requirements`.

## Project Global Rules

1. Prefer validated business knowledge base content before generating new conclusions.
2. Keep outputs traceable to source artifacts or existing wiki pages.
3. Flag conflicts explicitly; do not silently merge contradictions.
4. Keep naming and path conventions stable for reliable routing.
5. Keep user-facing docs concise and English-only.
6. For Jira read/write access in any domain workflow, use `connectors/jira/SKILL.md` as the shared connector contract.

## Domain Delegation

- Biz knowledge base domain entry: `skills/biz-knowledge-base/SKILL.md`  
  Maintains skills for a continuously evolving business knowledge base (ingest, consistency linting, and knowledge-base query).
- Requirements domain entry: `skills/requirements/SKILL.md`  
  Maintains requirement analysis skills, including decomposition, user story drafting, and card-writing quality rules.

## Usage

When an agent loads this repository as a skill source:

1. Read this file first for project-level rules.
2. Route by user intent:
   - Biz knowledge maintenance or governance -> `skills/biz-knowledge-base/SKILL.md`
   - Requirement analysis or story/card work -> `skills/requirements/SKILL.md`
   - Jira access (ingest, read, create, update, transition, comment) -> `connectors/jira/SKILL.md`
3. If intent is unclear, ask the user before routing. Use this decision question:
   - "Do you want to maintain business knowledge, do requirements analysis, or just ask a general AI question?"
4. If the request is unrelated to project skills, answer as a normal AI assistant without forcing skill routing.
5. Execute domain workflows only after routing is clear.
