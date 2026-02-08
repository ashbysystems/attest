---
description: View a summary of Attest review activity. Scans the save location for decision logs and escalation records, showing counts, decisions, and open escalations.
argument-hint: [directory-path]
---

# /attest:status

Provide a summary of review activity.

## Behaviour

### 1. Determine the scan directory

In order of priority:
1. If an argument is provided, use it as the directory path
2. Read `${CLAUDE_PLUGIN_ROOT}/.config.json` for the configured save location
3. Fall back to the current working directory

### 2. Scan for Attest files

Search the directory for:
- `attest-review-*.md` files (decision logs)
- `attest-escalation-*.md` files (escalation records)

If no files are found:

> No Attest review or escalation files found in [directory].
> Run `/attest:review` to start your first review, or `/attest:config` to set a different save location.

### 3. Parse files

For each decision log, extract:
- Review date
- Output type
- Risk classification
- Overall decision (Approved for use / Approved with modifications / Rejected / Escalated)
- Count of flagged items
- Count of escalated items

For each escalation record, extract:
- Escalation date
- Item description (from the escalated question)
- Escalated by (name)
- Suggested target role
- Status (Open / Resolved)
- If resolved: resolved by (name), resolution date

### 4. Generate summary

Use the template at `${CLAUDE_PLUGIN_ROOT}/templates/review-summary.md` as the structure. Populate all sections:

- **Overview** — Total reviews, flagged items, escalated items, resolved/open counts
- **Review Decisions** — Counts by decision type
- **Risk Classification Breakdown** — Counts by risk level
- **Open Escalations** — Table of unresolved escalations with dates, items, targets, timeframes
- **Resolved Escalations** — Table of closed escalations with resolution dates
- **Recent Reviews** — Table of recent review logs with key details

### 5. Present the summary

Display the summary in the session. Do not save it as a file unless the reviewer asks.

If there are open escalations, draw attention to them:

> **[n] open escalation(s) require resolution.** Run `/attest:resolve [filename]` to close an escalation.

### Shared directories

This command works against any directory, including shared or mounted directories containing logs from multiple reviewers. This is useful for compliance leads wanting an overview of team review activity.
