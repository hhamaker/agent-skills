# Eval cases — generate-workbook

Run each case by invoking the skill with the case input. Grade the output against the rubric below.

## Cases

### Case 1 — well-specified vendor evaluation
**Input:** "Evaluate Postmark for transactional email. Hard requirements: SOC 2 Type II, EU data residency option, webhooks for delivery events. We send ~2M emails/month. Compare against our incumbent, SendGrid. Audience is our platform team plus procurement."

**Expects:** zero context questions (everything material was given); vendor-evaluation template named; both vendors in symmetric columns; residency answered with sourced evidence; cost-scaling row reflects 2M/month; depth fits a mixed engineer/procurement audience.

### Case 2 — underspecified request triggers context gathering
**Input:** "Can you put together a workbook for Workato?"

**Expects:** one batched message asking for purpose, audience, and hard requirements (not an interrogation, not a generic marketing summary, not a silently-assumed vendor evaluation).

### Case 3 — non-vendor purpose, template selection
**Input:** "I need a workbook for our Salesforce org migration — consolidating two orgs into one by Q3. Audience is the engineering leads running the workstreams."

**Expects:** migration/project-plan template (not vendor sections); workstreams with owners and dependencies; cutover and rollback sections present; no pricing/capability-matrix sections bolted on.

### Case 4 — wrong-shaped request gets pushback
**Input:** "Build me a vendor-evaluation workbook to plan our team's quarterly OKRs."

**Expects:** skill flags the mismatch and proposes a purpose-fit structure instead of silently filling vendor sections with OKR content.

### Case 5 — thin public information
**Input:** "Vendor evaluation workbook for AcmeComplianceBot (acmecompliancebot.example) for sanctions screening."

**Expects:** sparse workbook dominated by `UNKNOWN — needs follow-up` cells; the documentation gap itself appears in the risk register; no invented certifications or pricing.

### Case 6 — confidential input handling
**Input:** Case 1 plus an attached internal requirements doc marked confidential.

**Expects:** workbook references requirement IDs only; no verbatim reproduction of the confidential document's text.

## Rubric

**Must contain**
- [ ] Context gathering when material context is missing — batched in one message, skipped when context is sufficient
- [ ] Named template or stated custom-structure rationale before sections are filled
- [ ] Sections that fit the stated purpose and audience
- [ ] Every factual claim sourced, labeled assumption, or `UNKNOWN`
- [ ] Retrieval dates on claims that go stale (pricing, compliance, SLAs)
- [ ] Executive summary with headline finding and biggest open risk
- [ ] `UNKNOWN`s collected as a follow-up checklist

**Must never contain**
- [ ] Invented certifications, SLAs, pricing, or capabilities
- [ ] Unlabeled assumptions presented as facts
- [ ] Confidential input text reproduced in the output
- [ ] Asymmetric comparison rows across subjects
- [ ] A wrong-shaped template silently applied to a mismatched purpose

**Grading:** pass = all "must contain" boxes ticked, zero "must never" violations. A single must-never violation fails the case regardless of other quality.
