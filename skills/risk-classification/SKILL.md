---
name: risk-classification
description: Defines how Attest classifies the risk level of AI-generated outputs. Used during /attest:review to determine question depth and escalation prompts. Four levels from Critical to Low, based on output type, intended use, and domain impact.
user-invocable: false
---

# Risk Classification

## Purpose

Risk classification determines how many questions Attest surfaces and how deeply it probes. Higher risk outputs receive more questions across more categories. The classification is always presented as a suggestion the reviewer can override.

## Risk Levels

### Critical

Outputs that directly affect legal rights, financial commitments, regulatory compliance, or safety.

**Examples:**
- Contract terms, legal opinions, or regulatory filings
- Data processing agreements (DPAs), service level agreements (SLAs), or any binding agreement
- Financial commitments, pricing models, or investment analyses
- Compliance assessments or audit responses
- Health, safety, or environmental impact assessments
- Data protection impact assessments or privacy notices with legal force
- Any output that will be submitted to a regulator or court
- Any output that creates binding legal or financial obligations

**Review depth:** 12-16 questions (including 5 mandatory baseline questions). Deep scrutiny across all applicable categories. Always prompt the reviewer to consider whether any items warrant escalation to a specialist.

**Escalation prompt:** At the end of question presentation, include:
> Given the critical nature of this output, consider whether any items require review by a specialist before this output is used.

### High

Outputs that inform significant decisions, face external audiences, or affect service delivery.

**Examples:**
- Policy drafts or strategy recommendations
- Client-facing communications or proposals
- Procurement specifications or vendor assessments
- Board papers or executive briefings
- Public-facing content on regulated topics
- Outputs that will be relied upon by others to make decisions

**Review depth:** 8-12 questions (including 5 mandatory baseline questions). Thorough coverage of key categories. Prompt the reviewer to consider whether escalation is warranted for any items.

**Escalation prompt:** At the end of question presentation, include:
> Consider whether any items in this review warrant input from a colleague with specialist knowledge before this output is used.

### Medium

Outputs that inform internal decisions or serve as inputs to further work.

**Examples:**
- Internal briefing notes or research summaries
- Draft documents that will undergo further review
- Analysis that informs but does not constitute the final decision
- Process documentation or internal procedures
- Training materials or knowledge base articles

**Review depth:** 6-10 questions (including 5 mandatory baseline questions). Focused on key assumptions, accuracy of specific claims, and fitness for the intended purpose.

**Escalation prompt:** None by default. Escalation available if the reviewer flags items.

### Low

Outputs used for reference, informal communication, or internal convenience.

**Examples:**
- Meeting summaries or note formatting
- Email drafts for routine correspondence
- Internal Q&A or information retrieval
- Data formatting or reorganisation
- Brainstorming or ideation outputs

**Review depth:** 5-7 questions (including 5 mandatory baseline questions). Focused on basic accuracy and whether the output is fit for its intended use.

**Escalation prompt:** None by default. Escalation available if the reviewer flags items.

## Classification Method

To classify an output, assess the following in order:

1. **What will this output be used for?** Direct use in high-stakes decisions pushes toward Critical/High. Use as input to further work pushes toward Medium. Reference or convenience pushes toward Low.

2. **Who will see or rely on this output?** External audiences, regulators, or clients push toward Critical/High. Internal audiences push toward Medium/Low.

3. **What happens if this output is wrong?** Legal liability, financial loss, or regulatory consequence pushes toward Critical. Reputational damage or poor decisions push toward High. Rework or correction pushes toward Medium. Minimal consequence pushes toward Low.

4. **What domain does this output operate in?** Contracts, DPAs, legal agreements, regulatory filings, and compliance documents are Critical by default. Other legal, financial, regulatory, and safety domain outputs default to at least High. Policy and strategy default to at least Medium. General knowledge work starts at Low and adjusts based on use.

**Important:** Any output that creates binding obligations (contracts, agreements, terms, DPAs) or will be submitted to a regulator is Critical, not High. The test is: "Could this document be relied upon in a legal or regulatory proceeding?" If yes, it is Critical.

## Presentation to Reviewer

Present the classification clearly and invite override:

> **Risk classification: [Level]**
>
> This output has been classified as [level] risk because [one-sentence rationale]. You can adjust this classification if it does not reflect your assessment of the risk.

If the reviewer overrides the classification, adjust the question depth accordingly and note the override in the decision log.

## Recording

The decision log records:
- The suggested risk classification
- Whether the reviewer accepted or overrode it
- If overridden, the reviewer's chosen level
- The rationale for the classification (whether suggested or overridden)
