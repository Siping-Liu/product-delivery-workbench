# User Story Generation Workflow

## Purpose

Generate, refine, or update user stories using wiki-grounded context, then perform Jira changes only after user approval.

## When to Use

Use this workflow when user asks to:

- create a story
- refine a story
- add or update acceptance criteria
- convert scope into Jira-ready story content
- create or update a Jira story after review

## Mandatory Steps

### Step 1 - Understand Story Scope

- Parse the user request into:
  - target business behavior
  - target user role
  - required outcome
  - constraints or exclusions

If scope is unclear, ask only the minimum clarification needed.

### Step 2 - Wiki Context Retrieval (Required)

Before drafting, search `wiki/` for relevant pages based on the requested scope.

Retrieval rules:

1. Start from `wiki/index.md` to identify candidate domain pages.
2. Read related pages that map to scope.
3. Extract applicable business rules, constraints, and terms.
4. If conflicts appear, flag them explicitly in the draft.
5. Do not invent business rules not supported by wiki context.

### Step 3 - Draft Story for Review

Create a concise Jira-ready draft in English using this default structure:

```md
# User Story: <Title>

## Business Context

## Business Value

As a <role>,
I want <capability>,
so that <business outcome>.

## Scope

1. ...

## Out of Scope

- ...

## Acceptance Criteria

### AC1 - <Name>
Given ...
When ...
Then ...

## Open Questions

- ...
```

Also include:

- `Wiki Context Used` section listing source wiki pages
- `Assumptions` only when needed

### Step 4 - Review Gate (Required)

After drafting:

1. Present story draft to user for review.
2. Ask for explicit confirmation:
   - approve as-is
   - request edits
   - approve and proceed with Jira action

Do not run Jira create/update before explicit approval.

### Step 5 - Jira Action (Only After Approval)

When user requests creation or update after review:

1. Load and follow `connectors/jira/SKILL.md`.
2. For create:
   - show final payload summary
   - request explicit write confirmation
   - create issue
   - return issue key and URL
3. For update:
   - fetch existing issue first
   - show current vs proposed change summary
   - request explicit write confirmation
   - apply update
   - return issue key and URL

## Safety Rules

- No Jira bulk writes unless user explicitly asks.
- No status transition, assignment, or unrelated field edits unless requested.
- No wiki updates during story drafting unless user explicitly requests ingest.
- Keep story content and ACs testable and scope-aligned.

## Output Contract

Each response should include:

- Story scope understanding
- Wiki context used
- Story draft or revision
- Open questions
- Next action prompt (`review` or `proceed to Jira`)
