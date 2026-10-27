# Discovery and page-by-page review

## 1. Inputs and goals

Read inputs from the session and project. Do not ask again for information already supplied. Without a project, explain a method rather than inventing an actual inventory.

| Access | What it supports | Gaps to preserve |
|---|---|---|
| Source + runtime | Static, executed, and cross-boundary checks | Missing services, devices, deployment configuration |
| Source only | Routes, implementation, definite static defects, proposed design | Live interaction, real APIs, task accessibility, measured performance |
| Runtime only | Observed pages, states, network, behavior | Hidden routes, architecture, server controls, build/release |
| Screenshots/designs | Layout, content, hierarchy in shown states | Unshown states, timing, performance, data/security implementation |

Record audience, tasks, reversibility, data risk, identity/tenancy, supported environments/inputs, scale, SEO/SSR needs, accessibility, and recovery in `production_profile`. Do not invent concurrency, latency, memory, compliance, or SLA promises. Continue checks independent of unknown conditions.

Separate current implementation, design intent, API guarantees, and proposed rules. Show conflicts instead of silently selecting a standard and declaring the other wrong.

## 2. Discover pages

**Static channels:** framework version; file/table routes; dynamic paths; lazy imports; redirects/fallbacks; layouts; nested/parallel/intercepting routes; 404/error/loading boundaries; login return paths; menus, links, button navigation, notifications and deep links; query/hash views, wizards, drawers, modals and tabs with independent tasks; roles, tenants, subscriptions, flags, experiments and server configuration; in-scope iframes, sub-apps, admin areas, subdomains and mobile variants.

For dynamic IDs, cover valid, missing, expired, deleted, unauthorized, and materially different business types as equivalence classes.

**Runtime channels:** traverse authorized navigation and in-page transitions; open deep links and refresh/back/forward; compare available roles; open reachable overlays, tabs, disclosures, menus, retries, and secondary settings. Inspect controls appearing only after scrolling, hover/focus, selection, or bulk actions. Record URL, title, state, version, and `EV`. Unavailable role branches remain blocked. Do not claim runtime traversal without execution.

**Reconciliation:** distinguish source-only routes, runtime surfaces not yet located in source, and documented surfaces not found in implementation. Resolve differences as undeployed, flagged, permission-restricted, obsolete, or still unknown.

Use `reconciled` only after available discovery channels and discrepancies have been addressed, with limitations disclosed. Use `limited` if undiscovered role pages may remain. Record promised-but-unimplemented prototype features as product gaps; do not invent pages and pretend they exist.

## 3. Split components

Use page → task region → composite → leaf responsibility, not file count. Include shells/navigation/toolbars/headings, fields/help/errors/submit/cancel, tables/cell types/row actions/selection/pagination, search/filter/sort, overlays, feedback, files/editors/media/charts, AI messages/citations/tools/jobs.

Use `DEF` for shared implementations and `CMP` for logical page instances, including inline controls. Locate inline units in their parent file and symbol. For every shared instance inspect:

1. Props, callbacks, and contract.
2. Object, role, and tenant identity.
3. Names, labels, descriptions, IDs, and error relationships.
4. Parent clipping, size, scrolling, stacking, theme, and focus return.
5. Identity after unmount/remount, cache reuse, and route changes.
6. Instance-specific effects and trust boundaries.

Include wrapper styles, DOM order, and bubbling in the responsible parent instance. Group repeated records only with justified equivalence; different permission, layout, data, or behavior contracts remain distinct.

## 4. Construct scenarios

Define expectations before execution. Do not derive correctness solely from current behavior. Create page/instance scenarios and separate cross-page scenarios.

| Axis | Relevant classes |
|---|---|
| Identity | Anonymous, self, another user, another tenant, admin, expired session |
| Data | Not loaded, empty, one item, typical, agreed limit, over limit, long/missing/zero/unknown values |
| Network | Normal, delayed, failed, offline/recovered, reordered, partial success, unknown timeout outcome |
| Ordering | Single, repeated, reversed, interrupted, concurrent, leave/return, refresh, multiple tabs |
| Input | Mouse, keyboard, touch, IME, paste, autofill, assistive technology |
| Environment | Supported browsers/devices, narrow containers, zoom, themes, reduced motion |
| Lifecycle | Initial entry, background resume, long sessions, old clients and new APIs |

Avoid a meaningless full Cartesian product. Cover actual branches and single-axis boundaries, adding high-impact combinations such as expired session + repeated writes, tenant switch + late response, or nested modal + keyboard + deleted trigger. Explain selection and uncovered combinations; do not silently sample different pages/contracts.

A scenario states identity/version/environment, ordered actions and responses, observable outcomes, prohibited side effects, recovery, and actual evidence. Unexecuted scenarios stay `planned` or `blocked`.

## 5. Review order

Walk the main task first, then every instance:

1. Visual/content: hierarchy, density, truncation, themes, reference differences.
2. Behavior: actions, reversal, cancellation, interruption, repetition, fake/inert controls.
3. Semantics: native elements, names, reading order, focus, keyboard, feedback.
4. Data: real contract, loading/failure, identity, cache, concurrent effects.
5. Implementation: ownership, identity, duplication, dependencies, errors, cleanup.
6. Stress: realistic content scale, layout combinations, performance, duration.
7. Boundaries: privacy, permissions, third parties, build/release dependencies.
8. Save the page's `CHK/FND/BP`, decisions, and `SCN`.

Scans supplement task observation, source tracing, and business assertions. Link recordings or stage screenshots to page/instance/scenario and baseline when available.

## 6. Verify evidence

Find minimum safe reproduction conditions. Static control flow may prove a definite defect without proving its browser impact. Performance needs build mode, device, network, scale, operation, and metrics; bundle size and render counts alone are not defects.

Establish actual security boundaries and existing framework/platform protections. Missing backend visibility does not prove missing authorization. Prioritize high-consequence unknowns for evidence gathering.

Separate design violations, usability barriers, and subjective preferences. Recheck original and affected scenarios after fixes. Record source changes, static checks, tests, and deployment separately.

## 7. Coverage and continuation

Maintain one authoritative `audit.json`. If delegation is authorized, assign page/domain work and stable ID ranges; collect evidence records and let one owner merge, deduplicate, preserve instance differences, and validate. Do not have multiple agents write the same ledger.

Inventory the full known denominator before batches. Save new discoveries, completed pages/instances, actual blockers, and next actions. Before delivery, account for every page and instance, eight dimensions, scenarios, evidence-backed findings, concrete blueprints/tasks, dependencies, and recovery. Judge review coverage, plan coverage, and release conditions separately.
