# Attest by Ashby

**Structured human review of AI outputs.** Attest works in any language. Claude conducts reviews in your language automatically. This README is in English; visit [ashby.systems/attest](https://ashby.systems/attest) for other languages.

Attest is a free, open-source plugin for Claude (Cowork and Claude Code) that ensures AI-generated outputs are reviewed by qualified humans before use. It surfaces contextual questions, captures reviewer decisions, and produces auditable decision logs.

Every AI vendor tells you to "review outputs with a qualified professional." None of them tell you how. Attest does.

## What Attest Does

1. Reads the AI output from your current session
2. Suggests a risk classification for you to confirm or adjust, and identifies assumptions
3. Surfaces contextual review questions specific to that output
4. Captures your decisions on each question (Confirmed, Flagged, Escalated, or Not applicable)
5. Produces an audit-ready decision log you can store, share, and reference

Attest does not judge, score, or rate AI outputs. It does not tell you whether an output is safe to use. Every decision belongs to you, the reviewer.

## Installation

### Claude Cowork (Desktop)

1. Download this repository (Code > Download ZIP, or clone it)
2. In Claude Cowork, go to Settings > Plugins > Upload Plugin
3. Select the `Attest` folder
4. Attest commands will appear in your command menu

### Claude Code (Terminal)

```bash
claude plugin install ashbysystems/attest
```

Or install from a local directory:

```bash
claude plugin install ./path/to/Attest
```

## Quick Start

1. Use any AI plugin or Claude to generate an output (contract review, policy draft, analysis, etc.)
2. Run `/attest:review`
3. Attest shows you a disclaimer, classifies the risk level, and presents review questions
4. Respond to each question: Confirmed, Flagged, Escalated, or Not applicable
5. Add notes where relevant
6. A decision log is generated and saved

That is the full workflow. Your first review takes a few minutes. Subsequent reviews are faster as you learn the process.

## Commands

| Command | What it does |
|---------|-------------|
| `/attest:review` | Start a structured review of an AI output |
| `/attest:log` | Generate or regenerate a decision log |
| `/attest:escalate` | Create an escalation record for items needing specialist input |
| `/attest:resolve` | Close an open escalation with a resolution record |
| `/attest:status` | View a summary of review activity and open escalations |
| `/attest:config` | Set where decision logs and escalation records are saved |
| `/attest:help` | Show command reference and disclaimer |

## What Attest Is Not

- **Not a quality checker.** It does not score or rate AI outputs.
- **Not a recommender.** It does not tell you whether to accept or reject an output.
- **Not a replacement for professional judgment.** Every decision belongs to the human reviewer.
- **Not an AI-to-AI verifier.** It uses AI to surface questions, not to draw conclusions.

## Decision Logs

Decision logs record what was reviewed, what questions were considered, and what the reviewer decided. Each log includes a SHA-256 hash of the reviewed output for traceability. Logs are saved as markdown files to your configured location and are designed to be readable by anyone, including auditors who have never used Attest.

**Limitations to be aware of:**

- Decision logs are plain markdown files. They are not tamper-proof. For integrity assurance, store logs in a version-controlled (git) or access-logged directory.
- Reviewer identity is self-declared. Attest does not authenticate reviewers. For higher assurance, combine with access-controlled storage.
- Approvals are point-in-time. A decision log records the reviewer's assessment at the time of review. It does not guarantee continued validity if circumstances change.

## Escalation

When a review item is outside your expertise or authority, mark it as Escalated. Attest creates a self-contained escalation record you can share with the right person. When the escalation is resolved, run `/attest:resolve` to close it with a resolution record.

## Configuration

Run `/attest:config [path]` to set where Attest saves files. This can be a shared drive, compliance folder, or document management directory. If not configured, files are saved to your current working directory.

## Data Handling

All processing runs locally. No data is transmitted externally. Decision logs and escalation records are stored in your configured save location. Apply your organisation's existing data handling and retention policies.

## Disclaimer

Attest by Ashby surfaces questions for human consideration. It does not provide legal, financial, or compliance advice. It does not assess the quality or correctness of AI outputs. All review decisions are made by the human reviewer.

## License

Apache 2.0. See [LICENSE](LICENSE).

## How Attest Was Built

Attest was designed by the Ashby team and built using Claude Code. The review methodology, risk classifications, and question frameworks are based on human experience and service design practice. Claude was used as a development tool, not as a domain expert. All design decisions were made by humans.

## About Ashby

Ashby builds structured human oversight for AI operations. Attest is our open-source review workflow plugin. Requisite is our Article 14 (EU AI Act) compliance assessment tool.

Learn more at [ashby.systems](https://ashby.systems).
