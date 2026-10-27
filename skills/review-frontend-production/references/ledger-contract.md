# Audit ledger and coverage contract

`audit.json` stores machine-checkable declarations; Markdown explains them. Keep conclusions consistent, update incrementally, and regenerate the coverage index. The validator cannot establish that a declaration is true in the real world.

## 1. Entities and coverage units

| Entity | ID example | Meaning |
|---|---|---|
| Project | PRJ-001 | Agreed target, access, baseline |
| Page | PAGE-001 | Route template, sub-app, or independent task view |
| Definition | DEF-001 | An actual shared implementation |
| Instance | CMP-001 | Logical UI unit at a particular page position/context |
| Scenario | SCN-001 | Verification with identity, data, environment, event order |
| Check | CHK-001 | Answerable question for a target and dimension |
| Evidence | EV-001 | Located record actually read, executed, or observed |
| Finding | FND-001 | Actual/expected difference, impact, evidence, cause |
| Blueprint | BP-001 | Current and target contract for a definition |
| Task | TASK-001 | Independently implementable/verifiable/recoverable action |
| Gate | GATE-001 | Release condition appropriate to product goals |

IDs are stable and globally unique, except component plans are keyed by instance ID. Split same-named but different implementations into different definitions.

Register units with independent semantic, behavior, state, layout, or data responsibility, including shells, regions, information, icons, controls, errors, and conditional content. Decorative wrappers belong to the nearest responsible instance's `layout_content` check; explain ownership in notes.

For repeated rows, register templates and distinct props/permission/state/layout contracts. Explain equivalence groups and representative data. Expand the denominator when new pages, branches, or parameter classes appear; do not enumerate infinite records or skip different contexts because they share a component.

## 2. JSON structure

Use UTF-8 and `schema_version: "1.0"`. Retain list fields even when empty. Extension fields are allowed. All explanation/reference arrays contain nonempty strings. Required `reason` fields are strings: empty where allowed, meaningful and nonempty when required; never `null` or an object.

### `project`

- `id`, `name`, `target`, `scope`: actual identifiers and path/URL/scope, or an explicit pending description.
- `mode`: `audit_plan` or `implement`, selected from authority given.
- `review_depth`: `quick` or `full`; omitted in legacy ledgers means `full`. Quick reviews cannot pass full coverage, full plan, or readiness gates.
- `access_mode`: `source_runtime`, `source_only`, `runtime_only`, `screenshots_only`.
- `baseline`: nonempty `source_ref`, `runtime_ref`, `observed_at`. Do not invent revisions. Manually reconcile evidence baselines with source, builds, runtime, and historical retests; equal strings do not prove identical builds, and different strings may refer to the same build.
- `inventory_status`: `discovering`, `reconciled`, `limited`. Use reconciled only after checking available discovery channels and resolving discrepancies.
- `inventory_sources`: objects with nonempty `kind`, `locator`, and an `evidence_ids` array. Reconciled inventories need evidence for each source. One channel requires a limitation explanation.
- `out_of_scope`: objects with nonempty `surface`, `reason`, `authority`; do not silently exclude hard pages.
- `production_profile`: object describing tasks, roles, data/operation risk, scale, supported environments, performance/accessibility, and release/recovery targets.
- `assumptions`: string array; preserve uncertainty.

### `pages`, `definitions`, `instances`

**Page fields:** `id`, `route`, `title`, `source_locator`, `entry_conditions`, `variants`, `scope_status`, `evidence_ids`. Entry conditions and variants are string arrays. `scope_status` is `in_scope` or `excluded`; exclusions also require `exclusion_reason` and `exclusion_authority`.

**Definition fields:** `id`, `name`, `kind`, `source_locator`, `source_status`. Source status is `located`, `unavailable`, or `inferred`. Unavailable source does not justify invented signatures.

**Instance fields:** `id`, `page_id`, `definition_id`, `label`, `locator`, `variant`, `criticality` (`high` or `normal`). Optional: `parent_instance_id`, `data_source`, `equivalence_group`, `notes`. Parents must exist on the same page and form an acyclic tree. Provide observable and available source locations rather than “the button.” Separate top and bottom save buttons as instances even if their definition is shared.

### `scenarios`

Required: `id`, `title`, `page_ids`, `instance_ids`, `preconditions`, `steps`, `expected`, `context`, `risk`, `status`, `evidence_ids`, `finding_ids`, `reason`.

- `context` contains `role`, `data`, `network`, `viewport`, `input`, `lifecycle`. Each is a nonempty string or nonempty string array with concrete conditions; explain non-applicability rather than writing bare N/A.
- `risk`: `high` or `normal`.
- `status`: `planned`, `passed`, `failed`, `blocked`, `not_applicable`.
- `steps` and `expected` are nonempty string arrays with concrete actions/assertions. Preconditions are a string array.
- Passed/failed scenarios require actual `runtime` or `test` evidence. Failed scenarios also need confirmed findings. Express source-confirmed defects through failed checks; an unexecuted scenario remains unexecuted.
- Blocked means a specific missing capability/evidence and a next action. Preserve failure and pre-fix evidence with timestamps/baselines when retesting.
- Include every affected instance's page in `page_ids`.

### `evidence`

Required: `id`, `kind`, `locator`, `observed_at`, `baseline_ref`, `summary`.

| Kind | Meaning and limits |
|---|---|
| `source` | File/symbol/lines actually read, with relevant control flow |
| `runtime` | URL, actions, and results actually observed; optional screenshot/network references |
| `test` | Executed command, environment, exit status, located output |
| `measurement` | Device/browser/build, sampling conditions, metric/result |
| `artifact` | Sourced screenshot/recording/design; cannot prove async/backend/authorization behavior |
| `specification` | Agreed rule, contract, or standard; establishes expectation, not implementation |

Keep tokens, personal data, and full sensitive responses out of records. Use redacted summaries and controlled original locations.

### `checks`

Required: `id`, `scope`, `target_id`, `dimension`, `question`, `status`, `evidence_ids`, `scenario_ids`, `finding_ids`, `reason`.

| Scope | Required dimensions |
|---|---|
| `project` | `reproducibility`, `architecture`, `security_boundaries`, `delivery_observability` |
| `page` | `routing_history`, `state_coverage`, `responsive_content`, `journey_integration` |
| `component` | `behavior`, `states`, `semantics_accessibility`, `layout_content`, `data_effects`, `security_privacy`, `performance_lifecycle`, `maintainability_integration` |

`target_id` references the corresponding entity. Multiple atomic questions may share a dimension. `sync` creates minimum placeholders; refine them and add linked scenarios. Split static and runtime assertions so unverified runtime behavior cannot hide inside a broadly passed row.

| Status | Use |
|---|---|
| `not_checked` | Discovered but not examined |
| `passed` | Sufficient evidence supports every stated expectation |
| `failed` | Evidence shows violation of an explicit expectation; link confirmed FND |
| `blocked` | Missing environment/account/tool/data/source/contract; explain |
| `not_applicable` | Explain why the target is outside this check's applicability, with traceable scope/implementation basis |

Passed/failed checks require evidence; failed checks require a confirmed finding. Blocked/not-applicable need reasons. Behavioral, state, keyboard, async, routing, and journey assertions require actual execution. Source can prove missing handling without proving all live behavior correct. Screenshots support only shown visual states. Performance requires measurement conditions.

Every in-scope page and instance needs a scenario; high-risk instances need high-risk scenarios. Prefer business outcomes over class names, loading flags, or toast visibility.

## 3. Findings, blueprints, and tasks

### `findings`

Required strings: `id`, `title`, `category`, `severity`, `confidence`, `status`, `owner`, `actual`, `expected`, `impact`, `root_cause`, `root_cause_confidence`, `remediation`, `regression_test`.

Required reference arrays: `page_ids`, `instance_ids`, `definition_ids`, `check_ids`, `scenario_ids`, `evidence_ids`, `resolution_evidence_ids`. Required `reproduction` object: string arrays `preconditions` and nonempty `steps`.

- `severity`: `P0/P1/P2/P3`, justified by consequence, reachability, scope, and recoverability.
- `confidence`: `confirmed/probable/needs_validation`. Static certainty may support confirmed while browser impact remains unexecuted. Failed checks/scenarios can link only confirmed findings.
- `status`: `open/in_progress/fixed_unverified/resolved/accepted_risk/dismissed`.
- Confirmed findings require evidence. Resolved findings require resolution evidence including `source/runtime/test/measurement`; artifacts/specifications alone are insufficient. Static fixes may use source evidence without forced browser execution.
- A resolved finding's current linked checks/scenarios must be passed or justified not-applicable. Forward references and reverse `finding_ids` must agree with resolution. Preserve historic failure evidence; update current verdicts without deleting history.
- Accepted risk/dismissal requires `decision.reason` and `decision.authority`. The reviewer does not accept risk on the user's behalf.
- Deduplicate shared causes while preserving every affected page/instance and its symptoms.

### `component_blueprints`

Required: `id`, `definition_id`, `current_contract`, `target_contract`, nonempty string-array `change_locations`. Every registered definition needs a blueprint, even if no current instance references it.

`target_contract` contains nonempty strings for:

1. `responsibility`: duties/boundaries.
2. `interface`: props/events/slots/outputs and compatibility.
3. `states`: valid combinations, transitions, reversals, interruptions.
4. `data_effects`: authority, cache, requests, cancellation, cleanup.
5. `semantics_accessibility`: names, semantics, focus, keyboard, feedback.
6. `styling_layout`: tokens, size, content, responsive/stacking/motion rules.
7. `performance_lifecycle`: resources, rendering, lifetime, budgets.
8. `security_privacy`: trust, authorization dependencies, minimization.
9. `observability`: needed errors/events, correlation, redaction.
10. `integration`: parent/child, page, and service contracts.

Keep static leaves concise, explaining applicability. Do not add networking/telemetry to fill fields or invent source signatures.

### `component_plans`

Exactly one per in-scope instance. Required: `instance_id`, `blueprint_id`, `disposition`, `rationale`, `instance_changes`, `finding_ids`, `task_ids`, `acceptance_criteria`, `regression_scenario_ids`.

Disposition: `retain/configure/refactor/replace/remove/investigate`. The blueprint must describe that instance's current definition. Explain local differences instead of copying an entire contract. `retain` still needs instance evidence and regression; `investigate` records evidence gathering, not a certain implementation. All dispositions except retain require tasks. Acceptance criteria and regression scenario IDs are nonempty arrays; scenarios must include that instance.

### `tasks`

Required: `id`, `title`, `phase`, `owner`, `scope_ids`, `finding_ids`, `depends_on`, `change_locations`, `implementation_steps`, `acceptance_criteria`, `verification_scenario_ids`, `rollback`, `risk`, `status`, `evidence_ids`.

- `phase`: nonnegative integer. `scope_ids`: nonempty references to PRJ/PAGE/DEF/CMP, not scenarios or evidence. Dependencies reference tasks, are acyclic, and cannot occur in later phases.
- Locations, implementation steps, acceptance criteria, and verification scenario IDs are nonempty arrays. Use real files/symbols/configuration or explicit locating steps. Assign frontend/backend/platform/product roles separately.
- `status`: `planned/in_progress/implemented/verified/blocked/deferred`.
- Verified tasks require actual runtime/test/measurement evidence, all verification scenarios passed or justified not-applicable, at least one passed scenario, and all dependencies verified. Source/specification/artifact alone is insufficient. For document/decision tasks, use an actual inspection test.
- If a dependency becomes unnecessary, amend `depends_on` and retain the reason in implementation steps; do not fabricate completion.
- Every non-dismissed/non-accepted finding, including resolved findings, retains a responsible task for traceability. Do not invent historical execution.
- Estimates are optional, evidence-based ranges with assumptions and confidence.

### `release_gates`

Required: `id`, `name`, `required` (boolean), `status`, `evidence_ids`, `reason`. Status vocabulary matches checks. Required gates cannot be not-applicable; a nonrequired gate needs a reason.

Tailor gates to the production profile: core journeys/recovery, object/tenant authorization, accessibility, consistency, build, performance, observability, release/recovery. Explain non-applicability; never delete failing gates to manufacture readiness.

## 4. Distinct conclusions

Report separately:

1. Discovery channels reconciled and remaining unknown surfaces.
2. In-scope page denominator: visited, source-read, runtime-verified, blocked.
3. Definition/instance counts, minimum dimensions, scenario coverage.
4. Planned/passed/failed/blocked and high-risk scenarios.
5. Blueprint/instance-plan/finding-task coverage and valid dependencies.
6. Release gates and evidence baseline consistency.

`audit_coverage_closed` means declared inventory is reconciled and required checks/scenarios have verdicts; confirmed failures may remain. It does not mean releasable.

`definitions_without_blueprints`, `instances_without_plans`, and `findings_without_tasks` prevent `plan_complete` / `--require-plan`, independently of audit coverage.

`production_gates_satisfied` requires full coverage and plan, source+runtime access/evidence, a production profile, no failed checks/scenarios, no unresolved P0/P1 findings, and passed required gates. It validates only declared records, never product certification or absence of bugs. Not-applicable is not a pass; blocked is not complete.

## 5. Batching and commands

`progress` is an object with `current_page` (known PAGE ID or null), `completed_batches`, `next_actions`, `unresolved_access` (string arrays, empty allowed), and nonempty timestamp `last_updated`. Do not use null for arrays.

Persist the known inventory, minimum checks, and progress before batches. Save after every page/shared batch. Preserve all unchecked items across time/context limits. When delegation is authorized, use separate records and one ledger writer.

```sh
python3 <skill-dir>/scripts/audit_ledger.py init <output-dir>/audit.json --name "<project>"
python3 <skill-dir>/scripts/audit_ledger.py sync <output-dir>/audit.json
python3 <skill-dir>/scripts/audit_ledger.py check <output-dir>/audit.json --require-plan
python3 <skill-dir>/scripts/audit_ledger.py check <output-dir>/audit.json --require-complete
python3 <skill-dir>/scripts/audit_ledger.py render <output-dir>/audit.json --out <output-dir>/coverage.md
```

`init` refuses an existing ledger; `sync` updates it without changing decisions. `render` replaces its requested report, so choose a dedicated generated file. `check` only validates records and coverage; it does not discover pages, run the product, or authenticate evidence. Exit codes are `0` satisfied, `1` invalid/command failure, `2` requested gate unmet.
