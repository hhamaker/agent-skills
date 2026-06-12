---
name: workbook-assessment
description: Use to render a verdict from a vendor-evaluation workbook — pick the dimension (technical, security, user experience, commercial), grade the vendor's answers by evidence quality, and end with an adopt/trial/hold/avoid recommendation. Works standalone from desk research at reduced confidence.
---

# Workbook Assessment

Render a verdict from the evidence a vendor evaluation has gathered. This skill is the downstream half of the pipeline that starts with `generate-workbook`: that skill produces the evidence base — requirements with stable IDs, vendor answers keyed to them — and this one turns a chosen slice of that evidence into a scored, defensible recommendation.

One workbook supports many assessments. The dimension being assessed is decided at intake, not baked into the skill.

## Phase 1 — Intake

Establish, in one batched exchange (skip anything already clear):

1. **The workbook** — vendor responses, requirements, criticality weights. No workbook? See *Standalone mode*.
2. **The dimension under assessment** — technical, security, user experience, commercial, or a custom lens. One dimension per assessment run; multiple dimensions are multiple runs that can share an executive roll-up.
3. **The consumer of the verdict** — who acts on it (engineering leads, CISO, procurement) and what decision it feeds.
4. **Scale and failure definition** — what load/usage must this survive, and what does failure look like in production? Fitness is judged against THIS, not general quality.

## Phase 2 — Dimension lens

Apply the matching lens to the vendor's answers. Each lens lists what "look hard at" means for that dimension:

### Technical
API quality (consistency, versioning, error model, idempotency, pagination, bulk) · auth (flows, rotation, scopes, service accounts) · scalability and limits (rate limits, ceilings, backpressure) · reliability (SLA, status history, degradation modes, observability hooks) · integration patterns (events vs polling, ordering, delivery semantics, sandbox fidelity) · lock-in and exit (proprietary surface, egress, migration paths)

### Security
Authentication and authorization depth · data handling (residency, encryption, retention, deletion, PII flows, subprocessors) · compliance posture (SOC 2 type and scope, ISO, DPAs) · vulnerability management (disclosure policy, patch cadence, pen-test evidence) · incident history and breach disclosures · tenant isolation model

### User experience
Fit to the actual users' workflows (from the workbook's UX requirements) · learning curve and training burden · admin and configuration experience · accessibility · performance as perceived at the user's scale · quality of error states and recoverability

### Commercial
Total cost at stated scale (license, usage, implementation, support) · cost-scaling behavior at 10× · contract terms (minimums, lock-ins, renewal cliffs) · exit costs (egress, migration, parallel-run) · vendor viability (funding, market position, deprecation track record)

### Custom
Derive the lens from the dimension's requirements in the workbook; state the lens explicitly before grading.

## Phase 3 — Evidence grading

The core discipline. Vendors over-claim; the assessment's job is to weigh claims by their backing. Every vendor answer in the assessed dimension gets a grade:

| Grade | Meaning |
|---|---|
| `VERIFIED` | Tested hands-on, demoed live against our scenario, or confirmed by a reference customer |
| `DOCUMENTED` | Vendor's public docs or auditable artifacts support the claim |
| `ASSERTED` | Vendor says so; no evidence offered |
| `CONTRADICTED` | Available evidence cuts against the claim |

Rules:
- A "fully supported" checkbox with no evidence is `ASSERTED` and scores accordingly — enthusiasm is not evidence
- Every **must-have** requirement sitting on `ASSERTED` gets a line in the **verification plan**: the cheapest experiment that would move it to `VERIFIED` (sandbox test, scripted demo — "show us X live, against our data shape" — or a reference-customer question)
- `CONTRADICTED` on a must-have is a headline finding, never a footnote

## Phase 4 — Verdict

- **Verdict line first**: **adopt / trial / hold / avoid** for this dimension, one sentence why. Never "it depends."
- **Per-requirement findings**: requirement ID · vendor claim · evidence grade · finding
- **Risk register**: keyed to requirement IDs — severity, likelihood, blast radius, retiring experiment
- **Trial design** (when the verdict is trial): what to build, success criteria mapped to must-have IDs, time box
- **Comparative mode**: multiple vendors in the workbook → same lens applied symmetrically, ranked verdict, per-requirement diff on must-haves

A dimension verdict is scoped: a technical **adopt** is not a recommendation to buy — it means this dimension raises no blocking objection. The buying decision belongs to the roll-up across dimensions.

## Standalone mode

No workbook available? The assessment can run from desk research (vendor docs, status history, community evidence) — but every finding is capped at `DOCUMENTED` by construction, the report states this confidence cap up front, and the verification plan is correspondingly longer. Recommend running `generate-workbook` when the decision warrants stakeholder-owned requirements.

## Guardrails

- **Evidence over claims.** No finding rests on vendor enthusiasm. The grading ladder is applied to every answer, no exceptions for impressive demos of *other* features.
- **Fitness over quality.** A great product can be the wrong answer at this scale or for this failure definition; say so.
- **Never request or handle production credentials.** Sandbox only; findings requiring hands-on access go to the verification plan instead.
- **Stay in your dimension.** Findings outside the assessed dimension get a one-line pointer ("security concern observed — assess separately"), not a verdict.
- **No invented facts.** Same rule as the whole pipeline: `UNKNOWN` is an acceptable grade input; invention is not.
