# Research Summarisation Workflow — Prompt System

## Use Case
A two-stage prompt chain that converts long-form research (reports, papers, 
articles) into structured summaries calibrated for a target audience.

Designed for: Consultants, newsletter writers, business analysts, executives.

---

## The Prompt Chain

### STAGE 1 — Extraction
```
You are a research analyst. You will receive a block of text from a 
report, paper, or article. Extract the following — nothing else:

1. Core thesis or main argument (1 sentence)
2. Key supporting data points (bullet list, max 5)
3. Conclusions or recommendations stated by the author
4. Any caveats, limitations, or uncertainties the author flags
5. Methodology (if stated — if not, write "Not stated")

Do not add your own interpretation. Extract only what the text states.
```

### STAGE 2 — Audience-Calibrated Summary
```
You are a business writer. Using the extracted research notes provided, 
write a summary calibrated for this audience: {{AUDIENCE}}

Format options (choose based on audience):
- EXECUTIVE: 3 bullet points + 1 action implication. Max 100 words.
- ANALYST: structured 3-paragraph summary with data citations. Max 300 words.  
- GENERAL PUBLIC: plain English explainer, no jargon. Max 200 words.
- SOCIAL MEDIA: Twitter-style thread (5 tweets max, each under 280 chars)

Audience selected: {{EXECUTIVE / ANALYST / GENERAL / SOCIAL}}
```

---

## Sample Output (Social Media format)

**Source:** IMF World Economic Outlook excerpt on Sub-Saharan Africa growth

```
1/ The IMF projects Sub-Saharan Africa will grow at 3.8% in 2025 — 
faster than the global average. But the headline hides big differences 
between countries. 🧵

2/ Resource-rich nations like Nigeria and Angola are being held back 
by oil dependency and currency pressures. Non-resource economies 
are actually outperforming.

3/ The real growth story is East Africa — Kenya, Ethiopia, and Rwanda 
are pulling ahead with services and manufacturing diversification.

4/ Key risk: global interest rate levels are keeping dollar debt 
expensive for African governments. Debt service is eating into 
public investment budgets.

5/ Bottom line: Africa's growth potential is real, but uneven. 
Investors and policymakers need country-level data, not continental 
averages. Don't sleep on the non-resource economies.
```

---

## Why It's Structured This Way

**Two-stage extraction before synthesis:** Forcing extraction first 
prevents the model from hallucinating or interpolating. 
Stage 2 works only with what Stage 1 actually found.

**Audience calibration options:** The same research serves different people 
differently. A CFO needs 3 bullets. A journalist needs a thread. 
This one prompt system serves all four use cases.

**Explicit format constraints (word counts, tweet limits):** Vague 
instructions produce vague outputs. Hard constraints produce 
professional-grade deliverables every time.
