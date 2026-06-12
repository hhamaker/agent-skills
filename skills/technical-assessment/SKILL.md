---
name: technical-assessment
description: Use for deep technical due-diligence on a vendor, tool, or platform before adoption — API quality, auth, data handling, scalability, lock-in — ending in an adopt/trial/hold/avoid recommendation with a risk register.
---

# Technical Assessment

Produce an engineering-grade assessment of a vendor, tool, or platform. Where the vendor workbook answers "what does this vendor offer," the technical assessment answers "what will this actually be like to build on, operate, and eventually leave."

## Inputs

Required:
- The vendor/tool/platform under assessment
- The intended use ("what are we going to build on this")

Optional (use when provided):
- API documentation links, sandbox credentials note (never request real credentials)
- Expected scale (requests/day, records, growth)
- Existing architecture context (what it must integrate with)
- Team constraints (languages, hosting, compliance regimes)

## Process

1. **Frame the decision.** State the intended use, the scale it must serve, and what "failure" would look like in production. The assessment evaluates fitness for THIS use, not general quality.
2. **Assess each dimension** (below) from primary sources — API reference, changelogs, status history, engineering blog, community issue trackers. Real-world failure reports outweigh marketing claims.
3. **Build the risk register.** Each risk gets: severity, likelihood, blast radius, and the cheapest experiment that would retire it (a sandbox test, a vendor question, a load probe).
4. **Recommend.** One of: **adopt** / **trial** (with the specific trial design) / **hold** (with what would change the answer) / **avoid** (with the disqualifier). Never end on "it depends."

## Assessment dimensions

1. **API quality** — consistency, versioning policy, error model, idempotency support, pagination, bulk operations, documented vs actual behavior
2. **Authentication & authorization** — supported flows (OAuth2 grants, API keys, mTLS), secret rotation story, scope granularity, service-account support
3. **Data handling** — residency options, encryption, retention/deletion guarantees, export paths and formats, PII handling, subprocessors
4. **Scalability & limits** — rate limits and their negotiability, throughput ceilings, queue/backpressure behavior, documented incident history at scale
5. **Reliability & operations** — SLA, status-page history, degradation modes, observability hooks (request IDs, event logs, metrics export), webhook delivery guarantees and replay
6. **Integration patterns** — event-driven vs polling, ordering guarantees, exactly/at-least-once semantics, sandbox fidelity to production
7. **Lock-in & exit** — proprietary surface area, data egress cost and format, migration paths competitors actually support, contract terms that punish leaving
8. **Ecosystem health** — release cadence, deprecation track record, community size, hiring pool familiarity

## Output format

- **Verdict line first**: recommendation + one sentence why
- **Decision frame**: intended use, scale, failure definition
- **Dimension findings**: one section each, facts sourced, gaps marked `UNKNOWN`
- **Risk register**: table — risk, severity, likelihood, blast radius, retiring experiment
- **Trial design** (when verdict is "trial"): what to build, success criteria, time box

## Guardrails

- **Fitness over quality.** A great platform can be the wrong answer for this use; say so.
- **Primary sources and dated claims.** Same rule as all diligence work: no invented facts, `UNKNOWN` is an acceptable cell value, marketing pages are claims rather than evidence.
- **Never request or handle production credentials.** Sandbox only, and say so when a finding requires hands-on verification.
- **Exit analysis is mandatory.** An assessment without a lock-in section is incomplete — the cost of leaving is part of the cost of adopting.
