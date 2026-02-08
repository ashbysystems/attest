---
description: Start a structured review of an AI-generated output. Surfaces contextual questions based on the output content, captures your decisions, and produces an auditable decision log. Run this after any AI plugin or Claude generates an output you need to review.
argument-hint: [output-type or file-path]
---

# /attest:review

The primary Attest command. Initiates a structured human review of an AI-generated output.

## Prerequisites

There must be AI-generated output in the current session context, or the reviewer must specify a file to review.

## Full Workflow

Follow every step in order. Do not skip or reorder steps. Refer to the review-methodology skill as the governing document throughout.

### Step 1: First-run check

Check whether `${CLAUDE_PLUGIN_ROOT}/.config.json` exists and contains a save location.

If no configuration exists, prompt:

> **First-time setup:** Where should Attest save decision logs and escalation records?
> Enter a path to a folder (e.g., a shared drive, compliance folder, or document management directory).
> This can be changed later with `/attest:config`.

If the reviewer provides a path, save it via the config mechanism. If they skip or dismiss, proceed using the current working directory. Only prompt on first use.

### Step 2: Disclaimer

Display the Attest disclaimer before any review content:

> **Attest by Ashby**
>
> Attest by Ashby surfaces questions for human consideration. It does not provide legal, financial, or compliance advice. It does not assess the quality or correctness of AI outputs. All review decisions are made by you, the reviewer.

Proceed after displaying.

### Step 3: Output identification

Identify what is being reviewed:

- If the reviewer provided a file path as an argument, read that file as the review target
- If the reviewer specified an output type (e.g., "contract review"), note it
- Otherwise, identify the most recent AI-generated output in the session context
- Determine the output type (contract review, policy draft, financial analysis, compliance assessment, code review, general knowledge work)
- Identify the source plugin if detectable (legal, finance, data, etc.)

If the output or type is ambiguous, ask:

> What type of output is this? For example: contract review, policy draft, financial analysis, compliance assessment, or general knowledge work.

### Step 4: Output fingerprint

Capture the output fingerprint for audit traceability:

- **SHA-256 hash** of the full output content (use `echo -n "[content]" | shasum -a 256` or equivalent)
- **First 200 characters** of the output content (preserving formatting)
- **Total word count** of the output
- **Review timestamp** (current date and time, YYYY-MM-DD HH:MM)

The hash provides forensic-grade identification of the exact content that was reviewed. Store all fingerprint data for inclusion in the decision log. Present briefly to the reviewer:

> **Output fingerprint captured**
> Type: [output type] | Words: [count] | SHA-256: [first 16 chars of hash]... | Source: [plugin/Claude]

### Step 5: Risk classification

Using the risk-classification skill, classify the output's risk level based on:
- Output type
- Intended use (if known)
- Domain

Present the classification as a suggestion:

> **Risk classification: [Level]**
>
> [One-sentence rationale for why this level was assigned.]
>
> You can adjust this classification if it does not reflect your assessment of the risk. Respond with Critical, High, Medium, or Low to override, or confirm to proceed.

If the reviewer overrides, note the override and adjust question depth accordingly.

### Step 6: Assumption analysis

Read the full output and identify:
- **Stated assumptions** — things the output explicitly says it assumes
- **Unstated assumptions** — things the output proceeds as if true without stating
- **Jurisdiction or regulatory references** — legal, policy, or regulatory frameworks referenced
- **Specific claims or figures** — numbers, dates, citations, named standards
- **Areas of confident specificity** — definitive statements without hedging
- **Organisational context** — what the output assumes about the reviewer's organisation

This analysis informs question generation. Do not present the raw analysis to the reviewer.

### Step 7: Question generation

Using the question-frameworks skill, generate contextual review questions:

1. Select applicable question categories based on the output content
2. Generate questions specific to this output (never generic)
3. **You MUST include all 5 baseline organisational context questions exactly as written below.** These are mandatory in every review, in addition to the category-specific questions:
   - "Does this output reflect how your organisation actually operates, or how organisations operate generically?"
   - "Are there internal policies, standards, or precedents this output should align with?"
   - "Who in your organisation would normally be responsible for this type of work, and have they been consulted?"
   - "If this output were wrong, what would the consequences be and who would be affected?"
   - "Is this output going to be used as-is, or as input to further work?"
4. Scale the total number of questions (including the 5 baseline questions) to the risk level:
   - Critical: 12-16 questions
   - High: 8-12 questions
   - Medium: 6-10 questions
   - Low: 5-7 questions
5. Prioritise questions per the framework's prioritisation rules

Every question must reference something specific in the output and briefly explain why it matters.

### Step 8: Structured presentation

Present questions grouped by category, with risk-relevant categories first.

For each question:

> **Q[n]: [Question text]**
> *[One sentence explaining why this was surfaced for the reviewer's consideration]*

After presenting all category-specific questions, present the organisational context questions under their own heading.

For Critical risk outputs, end with:
> Given the critical nature of this output, consider whether any items require review by a specialist before this output is used.

For High risk outputs, end with:
> Consider whether any items in this review warrant input from a colleague with specialist knowledge before this output is used.

### Step 9: Response capture

Each question has a response type (defined in the question-frameworks skill). Use the correct response mechanism for each type.

**For verification questions** (confirm, verify, check):

Ask the reviewer for their assessment using these options:

- **Confirmed** — You agree or have verified this
- **Flagged** — You have concerns or cannot verify this
- **Escalated** — This needs someone with more authority or expertise
- **Not applicable** — Not relevant to your context

After each response, ask if they want to add notes. Notes are optional but encouraged for Flagged and Escalated items.

**For information questions** (who, what, describe, explain):

Ask the reviewer to provide their answer as free text. Do NOT present Confirmed/Flagged/Escalated/Not applicable as options — these do not make sense for questions asking for a name, description, or explanation.

Instead, prompt for a text response:

> **Q[n]: [Question text]**
> Please type your answer:

Record the reviewer's text response as the answer. After they respond, ask if they want to add any additional notes.

If the reviewer indicates the question is not relevant, record "Not applicable" with their explanation.

**For all questions:**

If a reviewer selects or indicates **Escalated**, offer to create an escalation record immediately via `/attest:escalate`, or note it for later.

Present all questions first so the reviewer can see the full scope. Then collect responses one question at a time, using the appropriate response mechanism for each question's type.

### Step 10: Rubber-stamp detection

After all questions have been answered, check: are all items marked Confirmed with no free-text notes on any item?

If yes, display:

> **Review completeness check**
>
> All items have been confirmed without additional notes. Please confirm this reflects a genuine review of each item.

The reviewer must explicitly acknowledge this. Record whether this prompt was triggered and acknowledged.

If no (the reviewer used other response types or added notes), skip this step.

### Step 11: Completion and decision log

When all questions have been addressed, present the summary:

> **Review complete**
>
> - [n] items confirmed
> - [n] items flagged
> - [n] items escalated
> - [n] items marked not applicable

Then ask whether the reviewer wants to generate the decision log. If yes, you MUST complete all of the following steps before writing the file. Do not skip any.

**11a. Prompt for reviewer identity (MANDATORY)**

Ask the reviewer for their full name and their job title or role. Do not use placeholder text like "Session reviewer". The log is an audit artefact and must name the actual reviewer.

**11b. Prompt for overall decision (MANDATORY)**

Ask the reviewer to select one:
- **Approved for use** — The output can be used as-is
- **Approved with modifications** — The output can be used with specified changes
- **Rejected** — The output should not be used
- **Escalated** — The overall determination requires higher authority

**11c. Prompt for sign-off statement (MANDATORY)**

Ask the reviewer for a brief free-text statement summarising their overall assessment. This is their professional sign-off on the review.

**11d. Generate and save the decision log**

Use the template at `${CLAUDE_PLUGIN_ROOT}/templates/decision-log.md`. Populate ALL fields. The filename MUST follow this exact format:

```
attest-review-YYYY-MM-DD-HH-MM-[output-type].md
```

Where `[output-type]` is kebab-case (e.g., `data-processing-agreement`, `contract-review`, `policy-draft`). Example: `attest-review-2026-02-15-14-30-data-processing-agreement.md`

Do NOT use formats like `LOG-2026-02-08-001.md` or any other naming scheme.

**11e. Include the exact disclaimer footer**

The decision log MUST end with this exact text:

> ---
>
> *This decision log was generated by Attest (Ashby). Attest surfaced questions for the reviewer's consideration. All review decisions, assessments, and the final determination were made by the human reviewer named above. Attest does not provide legal, financial, or compliance advice and has made no quality judgment about the reviewed output.*
>
> *Learn more: ashby.systems/attest*

If the reviewer declines to generate the log, inform them they can generate it later with `/attest:log` while the review is still in session context.

## Language rules

Throughout this entire workflow, follow the language rules in the review-methodology skill:
- Use only permitted language
- Never use prohibited language
- Attribute all decisions to the reviewer
- Frame all questions as considerations, not conclusions
- Never imply the AI output is correct or incorrect

## Output type handling

If the argument is a recognised output type keyword, use it directly. If it is a file path, read the file and determine the output type from its content. If no argument is provided, identify the output from session context.
