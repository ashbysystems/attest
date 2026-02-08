---
description: Display Attest command reference and disclaimer.
---

# /attest:help

Display the Attest command reference.

## Behaviour

Display the following content exactly:

---

**Attest by Ashby** — Structured human review of AI outputs

> Attest by Ashby surfaces questions for human consideration. It does not provide legal, financial, or compliance advice. It does not assess the quality or correctness of AI outputs. All review decisions are made by you, the reviewer.

### Commands

| Command | Purpose |
|---------|---------|
| `/attest:review` | Start a structured review of an AI-generated output. Surfaces contextual questions, captures your decisions, and offers to generate a decision log. |
| `/attest:log` | Generate or regenerate a decision log from a completed review. |
| `/attest:escalate` | Create an escalation record for a review item that needs higher authority or specialist input. |
| `/attest:resolve` | Close an open escalation with a resolution record. |
| `/attest:status` | View a summary of review activity (reviews completed, items flagged, open escalations). |
| `/attest:config` | Set the save location for decision logs and escalation records. |
| `/attest:help` | Show this reference. |

### Quick start

1. Use any AI plugin or Claude to generate an output
2. Run `/attest:review` to start a structured review
3. Respond to each question: Confirmed, Flagged, Escalated, or Not applicable
4. A decision log is generated and saved automatically

### What Attest does

Attest reads AI-generated output, surfaces contextual review questions derived from the content, guides you through a structured decision process, and produces an auditable decision log that evidences your review.

### What Attest does not do

- It does not score, rate, or judge AI outputs
- It does not recommend accepting or rejecting outputs
- It does not replace professional judgment
- It does not provide legal, financial, or compliance advice

### Data handling

All processing runs locally. Decision logs and escalation records are saved to your configured save location (set via `/attest:config`). No data is transmitted externally. Apply your organisation's existing data handling and retention policies.

### About

Attest is built by Ashby (ashby.systems). Apache 2.0 license.

---
