# Ingest

## Purpose

Compile new business knowledge into the latest wiki.

The wiki should evolve as the project evolves.

A new source may:
- add new business context
- add a new feature
- update old business logic
- clarify existing rules
- replace previous behavior
- introduce a new edge case
- reveal a conflict
- add a new UI behavior
- add or change an integration rule

## Key Principle

`raw` = evidence  
`jira` = signals  
`confluence` = documentation  
`wiki` = final business truth model

Do not mirror source structures into wiki structure.  
Always abstract into business domains.

## Inputs

### 1) Raw Files

Located under `raw/`.

Rules:
- Do not modify `raw/`.
- Check the ingestion log before processing.
- Skip already ingested files unless re-ingestion is explicitly requested.

### 2) Jira Sources (Remote)

If the user provides a Jira issue key or Jira link, fetch the Jira content and ingest it.

Rules:
- Use `connectors/jira/SKILL.md` as the single Jira access contract.
- Detect backend using Jira connector capability order: `MCP -> CLI -> REST -> fallback`.
- Treat Jira items as structured business requirements.
- Multiple stories may map to one business feature.
- Normalize into business concepts (not Jira-native structure).
- Jira is input, wiki is output.

Supported Jira ingest requests include:
- ingest one Jira issue by key/link
- ingest a JQL result set
- ingest all stories under one Epic key (retrieve story list first, then ingest)

### 3) Confluence Sources (Remote)

If the user provides a Confluence link, fetch the page content and ingest it.

Rules:
- Treat Confluence as semi-structured knowledge.
- Extract business rules, flows, roles, and integrations.
- Ignore formatting noise.
- Convert into a wiki-centric structure.

### 4) Direct User Instruction

If the source is not a file or remote system, treat user instruction as input.

Rules:
- Treat input as a confirmed or proposed change.
- Save a raw snapshot of the instruction as source trace and mark it as `Source Trace: User instruction`.
- Reference that source trace in the resulting wiki update.
- Ask clarification when instructions are ambiguous.

### 5) Fallback Rule

If remote retrieval fails (authentication, network, or tooling), report the failure reason clearly, then request the minimum manual input needed (export file, page markdown, or link plus pasted content).
For Jira specifically, follow fallback behavior from `connectors/jira/SKILL.md`.

## Ingestion Log

Location: `wiki/log.md`

Rules:
- Must check before ingest.
- Skip duplicates unless re-ingestion is requested.

Recommended format:

| Date | Source | Type | Status | Wiki Pages Updated | Notes |
|---|---|---|---|---|---|

## Ingestion Behavior

1. Understand source.
2. Extract business knowledge.
3. Normalize into business concepts.
4. Identify impacted wiki areas.
5. Detect conflicts.
6. Propose update plan.
7. Wait for confirmation if needed.
8. Update wiki (English only).
9. Add source trace.
10. Update ingestion log.

## Ingestion Plan (Always Required)

Use this plan template before applying updates:

### Sources Detected
| Source | Type | Action |
|---|---|---|

### Already Ingested (Skipped)
| Source | Reason |
|---|---|

### Business Summary

### Knowledge Extracted

### Wiki Updates Required

### Conflicts / Questions

### Files to Create / Update

### Conflict Handling

Classify:
- Clarification
- Update
- Conflict
- Unclear

Never silently override.
Ask user before resolving conflicts.

### Source Trace

Add to updated wiki pages:

| Source | Update | Date |
|---|---|---|

If date is unknown, use `Unknown`.

## Outputs

- New or updated knowledge pages under `wiki/`
- A short ingestion summary (what changed, why, and source references)

## Failure Handling

Report the failure reason clearly, then request the minimum manual input needed.

