# Product Delivery Workbench

A skill-based workspace for managing business knowledge, requirements analysis, and delivery execution with coding agents.

## What This Does

`Product Delivery Workbench` is a domain-based workspace for end-to-end product delivery execution:
from business knowledge management, to requirement analysis, to delivery-ready outputs.

It currently includes the `biz-knowledge-base` domain based on the Karpathy-style LLM Wiki pattern:

- `ingest`: turn daily work outputs (notes, Jira stories, meeting summaries) into structured wiki knowledge
- `lint`: detect business-rule conflicts and consistency issues
- `query`: answer from validated business knowledge, not only raw retrieval

It also prepares a `requirements` domain for product/requirement analysis workflows, including requirement breakdown, user story drafting, and delivery card writing.

This gives teams a continuous path:
capture business knowledge -> keep it consistent -> analyze requirements -> produce implementation-ready outputs.

Result: product delivery work becomes clearer, more traceable, and easier to scale across projects.

The default workspace shape is:

- `skills/`: domain-based product delivery skills (for example biz-knowledge-base, requirements, and future delivery domains)
- `raw/`: source materials before ingestion
- `wiki/`: validated business knowledge

## Installation

Users do not need to manually clone this repository.

1. Copy the GitHub repository URL.
2. Open a coding agent (Cursor, Claude, OpenCode, etc.).
3. Paste the URL and ask the agent to use this repository as a skill source.
```https://github.com/Siping-Liu/product-delivery-workbench```
4. The agent should:
  - Acquire repository files in runtime context (clone/fetch)
  - Read `README.md` and root `SKILL.md`
  - Select a domain and load that domain `SKILL.md`
  - Run workflows defined by the selected domain

## Repository Layout

- `SKILL.md`: project overview and project-level global rules
- `skills/biz-knowledge-base/SKILL.md`: biz-knowledge-base domain rules and workflow routing
- `skills/requirements/`: requirements-domain skill area (planned; for analysis and story/card workflows)
- `skills/biz-knowledge-base/`: domain folder containing global rules and core workflows (`ingest`, `lint`, `query`)

## Requirements

- A coding agent with filesystem access
- GitHub access from the agent runtime

## Publish Safety

- Pre-publish checklist: `docs/pre-publish-review-checklist.md`
- Custom sensitive keyword list: `docs/sensitive-keywords.txt`

## License

MIT