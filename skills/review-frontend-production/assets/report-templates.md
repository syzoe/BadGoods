# Report templates

Replace placeholders with real records. Split large reports while preserving an index of every page and instance. Reuse shared blueprints; never treat templates, examples, or planned checks as results.

## 1. Overview — `review.md`

State project, source/runtime locations, revisions, observation time, audience, core tasks, production goals, access, discovery channels, reconciliation, exclusions, and authority.

Answer separately: Was scope discovered and reconciled? Which pages/instances/scenarios were verified? Does the plan cover all instances/findings? Which release conditions are satisfied?

Give PAGE/DEF/CMP/SCN/CHK/FND/TASK denominators and status counts. Finding count is not proof of coverage.

| Finding/root cause | All affected pages/instances | User/data impact | Priority/confidence | Repair mechanism | Dependencies |
|---|---|---|---|---|---|
| <FND/group> | <PAGE/CMP> | <consequence> | <level and reason> | <specific mechanism> | <TASK/contract> |

List critical blockers, unverified risks, product decisions, backend/platform dependencies, and a complete file index.

## 2. Page report — `pages/PAGE-001.md`

Identify route/entry, variants, source/runtime evidence, tasks, data, roles, upstream/downstream dependencies, baseline, design/API references. Show the actual component tree using a list or suitable Mermaid diagram.

| CMP | Parent | DEF | Observable/source location | Role/data/layout variant | CHK/SCN | FND | Decision | BP/TASK |
|---|---|---|---|---|---|---|---|---|
| <every instance> | <parent> | <definition> | <precise locator> | <conditions> | <all links> | <or none> | <disposition> | <IDs> |

For each instance, report all eight dimensions, evidence, findings, and blocked/not-applicable reasons. Ledger references are acceptable if each instance is discoverable. Do not omit “other similar components.”

| SCN | Preconditions | Action/response order | Expected outcomes/invariants | Actual result | EV | Status |
|---|---|---|---|---|---|---|
| <scenario> | <identity/data/environment> | <ordered steps> | <business assertions> | <observed or unexecuted> | <evidence> | <status> |

Explain shared prerequisites, local changes, preserved/changed behavior, dependencies, affected journeys, and missing evidence.

## 3. Finding — `findings.md` or one file per FND

For each finding include:

- **Location:** PAGE/CMP/DEF, file/symbol/lines, URL/state.
- **Priority/confidence:** P0–P3 and confirmed/probable/needs_validation, with consequences and reachability.
- **Preconditions and steps:** identity, data, revision, network/device, starting state; safe reproduction or checkable static control flow.
- **Actual/expected:** observed behavior and the applicable user/API/component/standard requirement; name unexecuted portions.
- **Impact:** blocked task, affected users/data/resources, recoverability.
- **Evidence:** EV, command/screenshot/source/network locations, baseline.
- **Cause and repair:** separate certainty from inference; name the mechanism and smallest owning boundary, including parent/service changes.
- **Verification:** scenarios and observable pass criteria.
- **Ownership/links:** every affected instance, tasks, backend/platform prerequisites.
- **Disposition:** current status, authorized risk/dismissal decision, resolution evidence. Preserve pre-fix evidence.

## 4. Blueprint and instance decisions — `components/BP-001.md`

Describe the current responsibility, implementation, callers, interface, branches, and evidence before the target contract.

| Target dimension | Concrete content |
|---|---|
| Responsibility | Boundaries and ownership |
| Interface | Props/events/slots/output, compatibility |
| States | Valid combinations, transitions, reversal, recovery |
| Data/effects | Authority, cache, requests, concurrency, cleanup |
| Semantics/accessibility | Names, roles, focus, keyboard, feedback |
| Styling/layout | Tokens, sizes, content, themes, stacking, motion |
| Performance/lifecycle | Applicable budgets, resources, verification |
| Security/privacy | Trust boundary and backend guarantees needed |
| Observability | Needed errors/events, correlation, redaction |
| Integration | Parent/child/page/service and migration contracts |

| CMP / PAGE | Disposition | Local changes | Preserved behavior | FND/TASK | Acceptance/regression SCN |
|---|---|---|---|---|---|
| <every instance> | <retain/configure/refactor/replace/remove/investigate> | <config/layout/callback/identity> | <requirements> | <IDs> | <observable criteria> |

Use investigate for evidence gaps; do not invent current signatures or backend guarantees. Retain still needs instance evidence and regression. Reference common rules without filling fields with generic prose. Keep target contracts internally consistent: a form-submit change must also address parent form ownership, submit handlers, cancel button types, and old callers. Static leaves need no invented requests or telemetry.

## 5. System plan — `refactor-plan.md`

Explain relevant shared boundaries, state ownership, request/cache, errors, authorization, and release structure. Keep reliable implementations and justify necessary replacement.

| TASK | Phase | PAGE/CMP/DEF | Files/config | Actions | Dependencies | Owner | Verification SCN | Recovery |
|---|---|---|---|---|---|---|---|---|
| <task> | <phase> | <IDs> | <real or locating step> | <executable> | <TASKs> | <role> | <scenario> | <mechanism> |

For complex tasks give prerequisite contracts, selected mechanism and relevant tradeoff, smallest complete slice, old-caller migration/removal, normal/failure/permission/order scenarios, and shared-instance regression. UI rollback cannot undo database writes or external effects. Estimates need ranges, assumptions, and confidence.

List every page's task order and shared prerequisites, including retained pages and their regression.

## 6. Verification and handoff — `verification-handoff.md`

| Check/SCN | Actual command/manual steps | Baseline/environment | Actual result | EV | Uncovered areas |
|---|---|---|---|---|---|
| <record> | <reproducible steps> | <conditions> | <passed/failed/blocked> | <evidence> | <gaps> |

Separate planned from executed checks. Every blocker needs its unlocking condition, owner, and next action. List gates, target, evidence, status, and risk; unresolved P0/P1, unknown business rules, backend/platform dependencies, and missing real-device checks remain explicit.

Provide run instructions, data/state/permission contracts, instance index, task order, regression commands, recovery conditions, known limits, and saved progress. Keep conclusions consistent with `audit.json` and `coverage.md`. Record validation is not production certification.
