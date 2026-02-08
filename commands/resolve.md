---
description: Close an open escalation with a resolution record. Appends the resolution to the original escalation file, preserving the audit trail.
argument-hint: <escalation-filename>
---

# /attest:resolve

Close an open escalation by recording its resolution.

## Prerequisites

An escalation record file must exist. The reviewer provides the filename or path as an argument.

## Behaviour

### 1. Identify the escalation

If an argument is provided, treat it as the escalation filename or path. Look for the file in:
1. The configured save location (from `${CLAUDE_PLUGIN_ROOT}/.config.json`)
2. The current working directory
3. The exact path provided

If the file is not found, inform the reviewer:

> Escalation record not found: [filename]. Check the filename and try again. Run `/attest:status` to see open escalations.

If no argument is provided, check the configured save location for any open escalation records (files containing "**Status:** Open") and present them:

> **Open escalations:**
> 1. [filename] — [brief item description] (escalated [date])
> 2. [filename] — [brief item description] (escalated [date])
>
> Which escalation would you like to resolve?

### 2. Verify the escalation is open

Read the file. If the Status field shows "Resolved", inform the reviewer:

> This escalation was already resolved on [date] by [name]. No action needed.

### 3. Capture resolution details

Ask the reviewer for:

- **Resolved by:** Name and role of the person who resolved the escalation
- **Decision:** What was decided (free text)
- **Conditions or follow-up actions:** Any conditions, caveats, or required follow-up (free text, or "None")
- **Resolution notes:** Any additional notes (free text, or "None")

### 4. Update the escalation record

Read the escalation record file. Update the following:

1. Change the Status field from "Open" to "Resolved"
2. Populate the Resolution section with:
   - Resolved by (name and role)
   - Resolution date and time
   - Decision
   - Conditions or follow-up actions
   - Resolution notes

Preserve all existing content in the file. The resolution is appended to the existing record. Never modify the original escalation content.

### 5. Save and confirm

Write the updated file back to the same location. Confirm:

> Escalation resolved: [filename]
> Resolved by [name] on [date].
>
> This resolution is now recorded in the escalation file. Run `/attest:status` to view updated escalation status.
