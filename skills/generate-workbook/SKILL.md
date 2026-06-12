---
name: generate-workbook
description: Use when evaluating vendors or tools for a project — facilitates requirements gathering with stakeholders, generates the forms vendors answer, and assembles the workbook that makes downstream comparisons (technical, security, UX, cost) possible.
---

# Generate Workbook

Build the instrument that lets a structured vendor evaluation happen. The end goal is a workbook that gives the business three things:

1. **A clear understanding of what the vendor will solve** — stated as requirements the stakeholders own, with the vendor's answers against each one
2. **What it will cost** — captured from the vendor in a comparable structure
3. **The evidence base for separate comparisons** — technical, security, user experience, and any other dimension the project needs, each scoreable from the same workbook

The agent's job is **facilitation and instrument design, not omniscience**. Requirements come from stakeholders; answers come from vendors. The skill makes both conversations structured enough to score. The workbook never contains facts the agent invented — only facts the parties supplied.

## Phase 1 — Frame the project

Collaborative. Establish with the requester:

- What is project X, and what does success look like?
- Who are the stakeholders, and which dimensions do they own (business, technical, security, UX, finance)?
- Which vendors are in scope (or is identifying candidates part of the project)?
- Timeline and decision process — who signs off, by when?

Batch the questions; don't interrogate. Capture answers in the workbook's Overview tab.

## Phase 2 — Draft requirements

Produce a first-pass requirements list from the project framing. Every requirement gets:

- **Stable ID** (e.g. `TEC-04`, `SEC-02`) — IDs never change once issued; everything downstream references them
- **Category** — functional, technical, security, compliance, user experience, budget/commercial
- **Criticality** — must-have or nice-to-have
- **Acceptance signal** — how we'd know the requirement is met (one sentence)

Mark the entire list **DRAFT** — it has no authority until stakeholders have refined it.

## Phase 3 — Stakeholder refinement form

Generate a form for stakeholders to refine the draft: confirm, edit, re-weight, add, or strike each requirement, plus free-text for anything the draft missed. One form, sectioned by category so each stakeholder can answer the dimensions they own.

When responses come back:
- Consolidate into the workbook's Requirements tab — now the **source of truth**
- **Conflicts between stakeholders are flagged, never silently resolved** — list them with both positions and get a decision
- Keep the stakeholder input trail in its own tab; auditability is a feature

## Phase 4 — Vendor response form

From the finalized requirements, generate the vendor-facing instrument:

- Each requirement becomes a question: *how* does your product meet this?
- Structured response per question: **fully / partially / not supported / on roadmap**, plus narrative and **evidence requested** (docs link, demo, reference customer)
- A **commercial section**: pricing model, costs at the project's stated scale, implementation costs, contract terms
- Identical form for every vendor in scope — symmetry is what makes responses comparable

## Phase 5 — Assemble the workbook

Spreadsheet when the environment supports it (one tab per section), structured markdown otherwise:

1. **Overview** — project frame, stakeholders, vendors, timeline
2. **Requirements** — the source of truth, by ID
3. **Stakeholder input** — the refinement trail
4. **Vendor responses** — one tab per vendor, answers keyed to requirement IDs
5. **Cost summary** — vendors side by side at the stated scale
6. **Comparison sheets** — one per dimension (technical, security, UX, …), pre-wired: requirement IDs × vendor answers × criticality weighting, ready for scoring

The comparison sheets are deliberately empty of verdicts. Scoring and recommendation are downstream work (see the `technical-assessment` skill for the technical dimension) — this workbook is what makes that work possible.

## Guardrails

- **No invented facts.** Vendor cells contain vendor answers or `AWAITING RESPONSE`. Agent-drafted content is labeled DRAFT until a human confirms it.
- **IDs are stable.** Renumbering requirements after forms go out breaks the entire chain.
- **Conflicts surface, never disappear.** Stakeholder disagreement and vendor non-answers are findings, not noise to smooth over.
- **Symmetric instruments.** Every vendor gets the same form; every comparison sheet uses the same rows.
- **No confidential leakage.** Internal context goes to vendors only as requirement text, never as attached internal documents or verbatim strategy.
