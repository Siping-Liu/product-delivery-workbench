# Lint

Use this skill when the user asks to check the health, quality, or consistency of the wiki.

## Purpose

Review `/wiki/` and identify issues that may reduce the quality or reliability of the business knowledge base.

Do not update files during lint unless the user confirms.

## What to Check

Review `/wiki/` for:

- possible business conflicts
- inconsistent terminology
- inconsistent status names
- inconsistent field names
- duplicate or overlapping pages
- missing source trace
- outdated rules
- unclear open questions
- unresolved assumptions
- pages that are too large and should be split
- pages that are too small and should be merged
- broken or missing Obsidian links
- wiki pages that still look like raw notes instead of compiled knowledge
- repeated content copied from sources instead of normalized knowledge
- missing relationship links between important concepts
- missing index or navigation pages
- unclear page ownership or purpose

## Lint Output Format

Use this output format:

```md
# Wiki Health Check

## Summary

## Findings

| Severity | Finding | Affected Pages | Recommendation |
|---|---|---|---|

## Potential Business Conflicts

## Suggested Next Actions

## Items Requiring User Decision
```

Severity can be:

- High
- Medium
- Low

## Conflict Handling

If lint finds a potential conflict:

1. Explain the conflicting knowledge.
2. Identify the affected pages.
3. Explain why it may be a conflict.
4. Recommend how to resolve it.
5. Do not resolve it automatically unless the user confirms.

## Structure Improvement

The wiki structure can evolve.

During lint, the agent may propose:

- splitting large pages
- merging overlapping pages
- creating index pages
- creating glossary or concept pages
- renaming pages for clarity
- adding missing source trace sections
- adding related links

But do not perform major restructuring without user confirmation.

## No Updates by Default

Lint is a review skill.

Do not edit files unless the user says to proceed.

If the user confirms, make small targeted updates first.
