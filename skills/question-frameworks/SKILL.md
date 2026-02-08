---
name: question-frameworks
description: Defines how Attest generates contextual review questions from AI output. Covers the 6 question categories, assumption identification methods, baseline organisational questions, output-type templates, and prioritisation rules. This is what makes reviews useful rather than generic.
user-invocable: false
---

# Question Frameworks

## Purpose

Attest generates review questions that are specific to the output being reviewed. Generic questions like "Is this accurate?" are not useful. Every question must reference something concrete in the output and explain why the reviewer should consider it.

## Question Categories

Questions are grouped into these categories. Not all categories apply to every output. Select the categories relevant to the output type and content.

### 1. Jurisdictional and Contextual Accuracy

Is this output grounded in the correct legal, regulatory, or policy framework for the reviewer's jurisdiction and context?

**When to use:** The output references laws, regulations, standards, policies, or jurisdictional frameworks.

**Question patterns:**
- "This output references [specific framework/law/standard]. Confirm this is the correct framework for your jurisdiction and context."
- "The output assumes [jurisdiction/regulatory context]. Verify this matches your operating environment."
- "This output cites [specific regulation/standard]. Confirm the version referenced is current."

### 2. Assumptions

What has the AI taken for granted that may not hold in the reviewer's specific context?

**When to use:** Always. Every AI output makes assumptions.

**How to identify assumptions:**
- **Stated assumptions:** The output explicitly says "assuming that..." or "based on the premise that..."
- **Unstated assumptions:** The output proceeds as if something is true without stating it. Look for: default values used without explanation, industry standards applied without confirming they apply, organisational structures or processes assumed, timelines or resource availability taken as given, stakeholder roles or responsibilities presumed.

**Question patterns:**
- "This output assumes [specific assumption]. Confirm this holds for your organisation."
- "The output proceeds on the basis that [assumption]. What is the actual position in your context?"
- "No [specific element] was referenced. The output may be assuming [default]. Verify whether this assumption is valid."

### 3. Specificity Verification

Are specific figures, references, citations, standards, or claims verifiable and correct?

**When to use:** The output contains specific numbers, dates, citations, named standards, regulatory references, or factual claims.

**Question patterns:**
- "The output cites [specific figure/statistic]. Verify this against your source data."
- "The output references [specific document/standard/regulation]. Confirm the reference is accurate and current."
- "[Specific claim] is stated as fact. What is your assessment of this claim?"
- "The output quotes a [timeframe/threshold/limit]. Confirm this matches current requirements."

### 4. Completeness

Is anything absent that should be present given the reviewer's organisational context?

**When to use:** The output is meant to be comprehensive (a full review, complete analysis, thorough assessment) or when the output type typically requires specific elements.

**Question patterns:**
- "This [output type] does not address [typical element]. Consider whether this should be included for your purposes."
- "The output covers [topics covered] but does not mention [topic that may be relevant]. Is this omission intentional or an oversight?"
- "For your organisation's context, are there additional [stakeholders/requirements/considerations] that this output should address?"

### 5. Confidence Calibration

Has the AI presented anything with high confidence that warrants independent verification?

**When to use:** The output contains definitive statements, strong conclusions, or specific recommendations without hedging.

**How to identify:** Look for language like "clearly", "obviously", "the correct approach is", "this means that", unqualified assertions of fact, and conclusions drawn without stated evidence.

**Question patterns:**
- "The output states [definitive claim] without qualification. What is your independent assessment?"
- "This conclusion is presented with high confidence. Consider whether the underlying reasoning supports this level of certainty."
- "The output treats [specific point] as settled. Verify this reflects the current position in your context."

### 6. Risk Implications

Could acting on this output create problems, liabilities, or unintended consequences?

**When to use:** The output recommends actions, proposes changes, or provides analysis that will inform decisions with real-world consequences.

**Question patterns:**
- "If this [recommendation/analysis] is acted upon, what are the potential consequences for your organisation?"
- "Consider who would be affected if this output were used as-is. Are their interests adequately reflected?"
- "What is the cost of acting on this output if it turns out to be incomplete or inaccurate?"

## Baseline Organisational Questions

These five questions are included in every review regardless of output type. They ground the review in the reviewer's actual organisational context rather than generic best practice.

1. **Organisational fit:** Does this output reflect how your organisation actually operates, or how organisations operate generically?

2. **Internal alignment:** Are there internal policies, standards, or precedents this output should align with?

3. **Responsible parties:** Who in your organisation would normally be responsible for this type of work, and have they been consulted?

4. **Consequence assessment:** If this output were wrong, what would the consequences be and who would be affected?

5. **Intended use:** Is this output going to be used as-is, or as input to further work?

Present these as a group under the heading "Organisational Context" after the category-specific questions.

## Question Templates by Output Type

### Contract review
- Jurisdiction and governing law verification
- Specific clause analysis (terms, obligations, liabilities)
- Comparison to organisational standard terms
- Missing provisions for the specific contract type
- Counterparty risk considerations

### Policy draft
- Regulatory framework alignment
- Internal consistency with existing policies
- Stakeholder coverage and consultation requirements
- Implementation feasibility
- Unintended consequences or gaps

### Financial analysis
- Data source and currency verification
- Assumption validation (growth rates, discount rates, market conditions)
- Methodology appropriateness
- Sensitivity to key variables
- Regulatory reporting requirements

### Compliance assessment
- Regulatory framework currency and applicability
- Evidence and documentation requirements
- Gap identification completeness
- Remediation feasibility
- Reporting obligation accuracy

### General knowledge work
- Source material accuracy
- Relevance to the specific context
- Completeness for the intended purpose
- Assumptions about audience or use
- Currency of information

## Prioritisation Rules

Present questions in this order:

1. **Risk implications** — Questions about potential harm or liability come first
2. **Jurisdictional accuracy** — Wrong framework invalidates everything downstream
3. **Assumptions** — Unstated assumptions can undermine the entire output
4. **Specificity verification** — Concrete claims that can be checked
5. **Completeness** — What might be missing
6. **Confidence calibration** — Overconfident assertions
7. **Organisational context** — Baseline questions last (these apply universally)

Within each category, order questions from most to least consequential.

## Question Quality Rules

Every question must:
- Reference something specific in the output (not be a generic prompt)
- Explain briefly why it matters (one sentence of context)
- Be answerable by the reviewer (not require external research during the review)
- Use permitted language only (see review-methodology skill)
- Be framed as a consideration, not a conclusion

Never generate a question that implies the AI output is wrong. Frame questions as verification prompts, not error detection.
