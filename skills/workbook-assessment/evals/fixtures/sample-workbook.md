# Evaluation Workbook — Workflow Automation Platform (FIXTURE)

> Eval fixture: a completed workbook for testing `workbook-assessment`.
> Vendors are fictional. Vendor A is the over-claimer (Case 2); requirement
> TEC-06 carries the contradiction (Case 3).

## Overview

- **Project:** Customer-onboarding overhaul — automate handoffs between CRM, billing, and provisioning
- **Scale:** ~200 onboarding cases/week today, target 600/week within 18 months
- **Stakeholders:** platform engineering (technical), security lead (security), onboarding ops manager (UX), finance (commercial)
- **Vendors:** FlowMatic, Conductor
- **Decision:** platform team recommendation due end of quarter

## Requirements — Technical dimension

| ID | Requirement | Criticality | Acceptance signal |
|---|---|---|---|
| TEC-01 | REST API covering all workflow CRUD operations | must-have | Build/modify/delete a workflow entirely via API |
| TEC-02 | OAuth2 client-credentials auth for service integrations | must-have | Service account completes auth flow without user context |
| TEC-03 | Webhook triggers with delivery guarantees | must-have | Documented retry policy on failed delivery |
| TEC-04 | Idempotent workflow execution (safe retries) | must-have | Duplicate trigger does not double-execute side effects |
| TEC-05 | Rate limits ≥ 100 req/s sustained on management API | nice-to-have | Published limits or load-test evidence |
| TEC-06 | Webhook replay for missed events | must-have | Operator can replay a 24h window from the UI or API |
| TEC-07 | Sandbox environment with production parity | must-have | Same connector versions and limits as production |
| TEC-08 | Bulk export of workflow definitions (portable format) | must-have | Full export in documented JSON/YAML schema |
| TEC-09 | SDKs for TypeScript and Python | nice-to-have | Official SDKs, released within last 12 months |
| TEC-10 | Event ordering guarantees within a workflow run | nice-to-have | Documented ordering semantics |

## Vendor responses — FlowMatic

| ID | Support | Vendor narrative | Evidence |
|---|---|---|---|
| TEC-01 | Fully | "Complete API coverage." | — |
| TEC-02 | Fully | "All modern auth supported." | — |
| TEC-03 | Fully | "Webhooks are fully reliable." | — |
| TEC-04 | Fully | "Retries are never a problem." | — |
| TEC-05 | Fully | "No practical limits." | — |
| TEC-06 | Fully | "Full replay support." | — |
| TEC-07 | Fully | "Sandbox identical to prod." | — |
| TEC-08 | Fully | "Export anything, anytime." | — |
| TEC-09 | Fully | "SDKs for every language." | — |
| TEC-10 | Fully | "Ordering fully guaranteed." | — |

**Public docs excerpt (FlowMatic, retrieved for the evaluation):**
> "Webhook delivery is fire-and-forget. FlowMatic does not currently retry
> failed deliveries or store events for replay. We recommend customers
> implement their own event persistence." — docs.flowmatic.example/webhooks

## Vendor responses — Conductor

| ID | Support | Vendor narrative | Evidence |
|---|---|---|---|
| TEC-01 | Fully | "Full CRUD via REST API v3." | docs.conductor.example/api/workflows |
| TEC-02 | Fully | "Client-credentials and authorization-code flows." | docs.conductor.example/auth |
| TEC-03 | Fully | "At-least-once delivery, exponential backoff, 72h retry window." | docs.conductor.example/webhooks#retries |
| TEC-04 | Partially | "Idempotency keys supported on triggers; connector side effects depend on the downstream system." | docs.conductor.example/api/idempotency |
| TEC-05 | Partially | "100 req/s on Enterprise tier; 25 req/s on Growth." | docs.conductor.example/limits |
| TEC-06 | Fully | "Replay any event window up to 7 days, UI and API." | docs.conductor.example/webhooks#replay |
| TEC-07 | Partially | "Sandbox matches connector versions; rate limits are lower than production." | docs.conductor.example/sandbox |
| TEC-08 | Fully | "Full workflow export as versioned YAML." | docs.conductor.example/export |
| TEC-09 | Roadmap | "TypeScript SDK GA; Python SDK in public beta, GA next quarter." | github.example/conductor/sdk-python |
| TEC-10 | Not supported | "Ordering is best-effort across parallel branches; strict ordering is on the long-term roadmap." | — |

## Commercial summary (both vendors, for context)

| | FlowMatic | Conductor |
|---|---|---|
| Pricing model | Flat per-workspace | Per-task usage tiers |
| Quoted at stated scale | "Contact sales" | $48k/yr Growth, $96k/yr Enterprise |
| Implementation | "Free white-glove" | Partner-led, est. $15–25k |
