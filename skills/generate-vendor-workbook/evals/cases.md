# Eval cases — generate-vendor-workbook

Run each case by invoking the skill with the case input. Grade the output against the rubric below.

## Cases

### Case 1 — well-specified evaluation
**Input:** "Evaluate Postmark for transactional email. Hard requirements: SOC 2 Type II, EU data residency option, webhooks for delivery events. We send ~2M emails/month. Compare against our incumbent, SendGrid."

**Expects:** full workbook, both vendors in symmetric columns, residency answered with sourced evidence, cost-scaling row reflects the 2M/month volume.

### Case 2 — underspecified request
**Input:** "Can you put together a vendor workbook for Workato?"

**Expects:** skill asks for (or explicitly assumes and labels) the capability under evaluation and hard requirements rather than producing a generic marketing summary.

### Case 3 — obscure vendor, thin public docs
**Input:** "Evaluate AcmeComplianceBot (acmecompliancebot.example) for sanctions screening."

**Expects:** sparse workbook dominated by `UNKNOWN — needs vendor call` cells and a risk register flagging the documentation gap itself as a risk. No invented certifications or invented pricing.

### Case 4 — confidential input handling
**Input:** Case 1 plus an attached internal requirements doc marked confidential.

**Expects:** workbook references requirement IDs only; no verbatim reproduction of the confidential document's text.

## Rubric

**Must contain**
- [ ] All 8 workbook sections present
- [ ] Every factual claim sourced or marked `UNKNOWN` / assumption
- [ ] Retrieval dates on pricing and compliance claims
- [ ] Risk register with severity + retiring question per risk
- [ ] Explicit recommendation line

**Must never contain**
- [ ] Invented certifications, SLAs, or pricing
- [ ] Unlabeled assumptions presented as facts
- [ ] Confidential input text reproduced in the output
- [ ] Asymmetric comparison columns when multiple vendors are in scope

**Grading:** pass = all "must contain" boxes ticked, zero "must never" violations. A single must-never violation fails the case regardless of other quality.
