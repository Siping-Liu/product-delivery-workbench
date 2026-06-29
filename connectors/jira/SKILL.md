---
name: jira-connector
description: Unified Jira connector skill for read/write operations via MCP, CLI, or REST, with review-first safety gates.
disable-model-invocation: true
---

# Jira Connector - SKILL

## Purpose

Provide one stable Jira access entry for all product-delivery workflows.

This skill supports:
- Ingest-related Jira reads
- Requirements workflows (draft from existing cards, create/update cards)
- Direct Jira card operations with review-before-write safety

## Scope

Read operations:
- Fetch one issue by key
- Search issues by JQL
- Fetch all stories under one Epic

Write operations:
- Create issue (especially Story)
- Update existing issue fields (summary, description, acceptance details)
- Assign issue
- Transition issue
- Add comment

## Capability

Always detect backend first.

Priority order:
1. MCP
2. Jira CLI
3. Jira REST API
4. Fallback (manual input for read flows)

Capability checks:
- MCP: Jira tools are available and callable.
- CLI: `jira` command exists and user is authenticated (`jira me` succeeds).
- REST: base URL and token/user credentials are configured and request succeeds.

When reporting capability state, include:
- `available_backends`
- `selected_backend`
- `availability_reason`
- `next_action_for_user` (when blocked)

## Read

### A) Fetch a single issue

Input:
- Issue key (for example `PROJ-123`) or Jira issue URL

Output:
- Key fields needed for downstream workflows:
  - issue key, title, description/body, issue type, status, assignee, labels, links, updated time

### B) Search issues by JQL

Input:
- JQL string
- Optional page limit

Output:
- Matching issue list with key metadata for triage and ingest

### C) Fetch all stories under one Epic (required scenario)

Input:
- Epic key (for example `EPIC-88`)

Behavior:
1. Validate Epic key format.
2. Run an Epic-child query by backend:
   - MCP/REST: use JQL with Epic-link style fields configured by the Jira project.
   - CLI: run JQL query through the CLI query flag supported by the installed version (commonly `-q` or `--jql`).
3. Return all child stories (or paginated list when needed).
4. If project uses a custom Epic-link field, include that field in query adaptation notes.

Recommended JQL patterns:
- `"Epic Link" = EPIC-88`
- `parent = EPIC-88` (team-managed project style)
- `issuekey in childIssuesOf(EPIC-88)` (instance-dependent function availability)

For ingest usage:
- After story list retrieval, pass the issue keys/content into the ingest pipeline as source inputs.

## Write

All write operations must run through Safety rules in this file.

### A) Create Story

Required input:
- Project key
- Issue type (`Story` unless user asks otherwise)
- Summary
- Description/body

Optional input:
- Acceptance criteria
- Labels/components
- Assignee
- Parent Epic

Flow:
1. Build draft payload.
2. Show review block to user.
3. Wait for explicit confirmation.
4. Execute create via selected backend.
5. Verify by fetching created issue.

### B) Update existing Story

Required input:
- Target issue key
- Requested changes

Flow:
1. Fetch current issue first.
2. Build proposed change patch (current vs proposed).
3. Show review block.
4. Wait for explicit confirmation.
5. Execute update.
6. Verify by re-fetching issue and summarizing applied changes.

### C) Assign / Transition / Comment

Assign:
- Resolve target user identity (account id where required).

Transition:
- Fetch available transitions first.
- Never assume transition names are universal.

Comment:
- Add comment body exactly as reviewed with user.

## Safety (Review-First Policy)

Before any write operation:
1. Read current state (or show create draft for new issue).
2. Present a review block:
   - Operation
   - Target issue/project
   - Current state (if applicable)
   - Proposed changes
   - Potential side effects (notifications/status changes)
3. Ask for explicit user confirmation.

Do not execute writes without explicit confirmation.

After write:
1. Verify with a follow-up read.
2. Return concise execution summary:
   - backend used
   - operation status
   - key resulting fields
   - warnings/next steps

## Fallback

If no backend is available:
- For read flows:
  - Ask for minimum manual input (issue URL/key + pasted core fields/content)
  - Continue workflows using manual input
- For write flows:
  - Do not execute
  - Return exact setup instructions for one backend path (MCP, CLI, or REST)

If auth/permission fails:
- Report exact failure reason
- Provide next action (re-auth, permission request, correct project/key)
- Do not silently retry destructive writes

## Guardrails (Never)

- Never transition an issue without fetching current status and available transitions first.
- Never assign by display name where account id is required.
- Never update description/summary without showing current vs proposed content.
- Never execute bulk or repeated writes without explicit user approval.
- Never hide auth/permission errors.
