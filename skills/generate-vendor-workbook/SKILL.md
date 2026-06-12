---
name: generate-vendor-workbook
description: Use when evaluating a third-party vendor, SaaS product, or API provider — compiles research into a structured evaluation workbook covering capabilities, security posture, pricing, and integration surface, so vendors can be compared side by side.
---

# Generate Vendor Workbook

Produce a structured evaluation workbook for a third-party vendor. The workbook is the artifact a platform team uses to compare vendors, justify a selection, and hand auditors evidence that diligence happened.

## Inputs

Required:
- Vendor name and product under evaluation
- The business capability being evaluated (e.g. "transactional email", "sanctions screening", "workflow automation")

Optional (use when provided, request if missing and material):
- Vendor documentation links (API docs, security/trust page, pricing page)
- Compliance artifacts (SOC 2 report, ISO certs, DPA)
- Internal requirements list or scoring criteria
- Incumbent/alternative vendors for comparison columns

## Process

1. **Scope check.** Confirm the capability being evaluated and any hard requirements (compliance regimes, data residency, budget ceiling). If hard requirements are unknown, list assumptions explicitly in the workbook rather than guessing silently.
2. **Research.** Work from the vendor's primary sources first (docs, trust center, pricing page, changelog, status page history). Note the retrieval date on every claim — vendor facts go stale.
3. **Fill the workbook sections** (below). Every cell is either a sourced fact, a clearly-marked assumption, or `UNKNOWN — needs vendor call`. Never present an inference as a documented fact.
4. **Score.** Apply the scoring criteria if provided; otherwise use the default weights in the scoring section and say so.
5. **Summarize.** One-paragraph executive summary: what the vendor does well, the biggest risk, and what must be verified before contract.

## Workbook sections

Produce as a spreadsheet when the environment supports it (one tab per section); otherwise as a single markdown document with one heading per section.

1. **Overview** — vendor, product, evaluation date, evaluator, capability under evaluation, hard requirements
2. **Capability matrix** — rows: required capabilities; columns: supported (yes/partial/no), evidence link, notes. Partial support gets a note explaining the gap, never a bare "partial"
3. **Security & compliance** — certifications (SOC 2 type, ISO 27001, etc.), data encryption at rest/in transit, data residency options, subprocessor list link, breach history (public record), DPA availability
4. **Pricing model** — pricing axis (seats, usage, flat), published tiers, overage behavior, contract minimums if published, cost-scaling risk (what happens at 10× usage)
5. **Integration surface** — API style (REST/GraphQL/SOAP), auth methods (OAuth2, API key, mTLS), webhooks/events, rate limits, sandbox availability, SDK languages, bulk/export paths
6. **Operational posture** — published SLA, status page history (last 12 months), support tiers, deprecation policy
7. **Risk register** — top 3–5 risks with severity and the question that would retire each one
8. **Scoring & recommendation** — weighted score per section and a one-line verdict

## Guardrails

- **No fabricated facts.** A workbook with `UNKNOWN` cells is useful; a workbook with invented certifications is a liability. When the vendor's own sources don't answer a question, mark it for the vendor call.
- **No confidential input leakage.** If internal requirements documents are provided, the workbook references requirement IDs, not the documents' contents.
- **Date everything.** Pricing and compliance claims carry the date they were checked.
- **Comparisons stay symmetric.** If comparing multiple vendors, every vendor gets the same rows — no cherry-picked categories.
