# Query

Use this skill when the user asks a business question about the project.

## Purpose

Answer business questions based on the current compiled wiki.

The wiki under `/wiki/` is the main source of current business knowledge.

The user may communicate in any language.

Reply in the same language as the user unless the user requests a different language.

Do not update wiki pages during query unless the user explicitly asks.

## Source Priority

When answering:

1. Use `/wiki/` as the main source of truth.
2. Use `/raw/` only when:
   - the wiki is incomplete
   - the wiki is unclear
   - the user asks for source-level evidence
   - the user asks to trace back to source material
3. Do not invent missing business rules.
4. If the wiki does not contain enough information, say so clearly.
5. If the answer may be outdated or incomplete, mention the uncertainty.
6. Suggest what source or wiki update may be needed.

## Query Behavior

When answering a business question:

1. Identify the business topic.
2. Find relevant wiki pages.
3. Synthesize the latest current understanding.
4. Call out exceptions, edge cases, and open questions if relevant.
5. Mention related wiki areas when useful.
6. Do not simply dump raw notes.
7. Keep the answer practical for BA, developer, QA, or stakeholder use.

## Example Questions

Examples:

```text
What is the latest Big Lot Order flow?
Premium Item 现在有哪些规则？
How is PO quantity calculated?
Which roles can approve Big Lot Orders?
What happens after payment success?
哪些地方可能影响 RMS integration？
```

## If Wiki Knowledge Is Missing

If the wiki does not contain enough information, respond clearly.

Example:

```text
I could not find a confirmed rule for this in the current wiki. The closest related pages are...
This may require ingesting the latest Jira story, meeting note, or manual update.
```

If appropriate, suggest an ingest action.

## No Wiki Updates by Default

A query should not update files.

If the query reveals missing or outdated knowledge, suggest:

```text
This looks like a wiki gap. Would you like me to ingest the related source or create an update plan?
```
