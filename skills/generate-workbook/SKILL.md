---
name: generate-workbook
description: Use when a task calls for a structured, multi-section workbook — vendor evaluations, technical comparisons, migration plans, audit evidence, decision matrices. Gathers context about the workbook's purpose and audience first, then produces sections fit for that purpose.
---

# Generate Workbook

Produce a structured workbook: a multi-section artifact a team uses to compare options, support a decision, plan work, or hand auditors evidence. The skill's first job is understanding what the workbook is *for* — section structure follows purpose, not the other way around.

## Phase 1 — Context gathering

Before producing anything, establish:

1. **Purpose** — what decision, plan, or evidence trail does this workbook support?
2. **Audience** — who reads it (engineers, leadership, auditors, procurement)? Depth and vocabulary follow.
3. **Subjects** — what's being evaluated, compared, or planned (one vendor, three tools, a migration, a quarter of work)?
4. **Hard requirements** — non-negotiables that become pass/fail rows (compliance regimes, budget ceilings, deadlines, data residency)
5. **Output format** — spreadsheet (one tab per section) when the environment supports it, otherwise structured markdown

Ask **only for what's missing and material** — at most a handful of questions, batched in one message. If the request already answers these, skip straight to Phase 2. If answers aren't available, proceed with assumptions labeled prominently in the workbook itself.

## Phase 2 — Section design

Propose the section structure for this purpose before filling it. Use a template below when one fits; derive a custom structure from the purpose when none does. State which template (or custom rationale) you're using.

### Template: vendor / product evaluation
Overview · capability matrix · security & compliance · pricing model · integration surface (APIs, auth, webhooks, rate limits) · operational posture (SLA, status history) · risk register · scoring & recommendation

### Template: technical comparison (N options)
Decision frame · symmetric capability matrix · cost of adoption per option · cost of exit per option · risk register per option · weighted scoring · recommendation

### Template: migration / project plan
Scope & success criteria · current-state inventory · target state · workstream breakdown with owners and dependencies · cutover plan · rollback plan · risk register · open questions

### Template: audit / compliance evidence
Control list · evidence per control (artifact, location, date, owner) · gaps with remediation owner and deadline · attestation summary

## Phase 3 — Research & fill

- Work from primary sources; date every claim that can go stale (pricing, certifications, SLAs)
- Every cell is a sourced fact, a labeled assumption, or `UNKNOWN — needs follow-up`. Never silently infer.
- Comparisons stay symmetric: every subject gets the same rows, no cherry-picked categories

## Phase 4 — Summarize

- Executive summary up top: what the workbook supports, the headline finding, the biggest open risk
- If the workbook supports a decision: weighted scoring plus a one-line verdict
- List the `UNKNOWN`s as a follow-up checklist — they're the workbook's to-do list, not its failure

## Guardrails

- **No fabricated facts.** A workbook with `UNKNOWN` cells is useful; one with invented certifications or pricing is a liability.
- **No confidential input leakage.** Internal documents provided as context are referenced by ID, never reproduced.
- **Don't interrogate.** Context gathering is one batched exchange at most; a request that's already clear gets zero questions.
- **Purpose drives structure.** If the requested sections don't serve the stated purpose, say so and propose better ones — don't silently fill a wrong-shaped workbook.
