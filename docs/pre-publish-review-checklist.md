# Pre-Publish Review Checklist

Use this checklist before publishing local updates to GitHub.

## 1) Scope and Intent

- Confirm what changed and why.
- Confirm the change belongs to this repository and domain.
- Confirm no unfinished draft content is included by accident.

## 2) Knowledge Quality

- New or updated wiki content is structured and not raw-copy dumps.
- Related pages are cross-linked when needed.
- Conflicts are clearly marked and not silently overwritten.
- Open questions and ambiguities are explicitly labeled.

## 3) Sensitive Information Check

Run a keyword-based scan before publish.

### 3.1 Configure your keyword list

Edit:

- `docs/sensitive-keywords.txt`

Add project-specific sensitive terms, such as:

- customer names
- internal project codenames
- private endpoint names
- internal IDs
- credentials/tokens patterns

### 3.2 Run scan

From repo root:

```bash
rg -n -i -f docs/sensitive-keywords.txt .
```

If matches are found:

- verify each match is safe to publish
- mask or remove sensitive values when needed
- re-run scan until results are acceptable

## 4) Source Trace and Auditability

- Source trace is present where needed.
- Trace references are useful but do not expose unnecessary raw sensitive data.
- Ingestion log is updated for newly ingested sources.

## 5) Routing and Skill Integrity

- Paths in domain skill files are valid.
- `SKILL.md` (project-level) and domain `SKILL.md` files are consistent.
- No broken internal links or outdated domain names remain.

## 6) Final Publish Gate

- Confirm intended files to publish.
- Confirm no local-only notes/secrets are included.
- Publish only after all checks above pass.
