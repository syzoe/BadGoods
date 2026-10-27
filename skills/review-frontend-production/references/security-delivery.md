# Security and delivery review

Apply to real identities, data, APIs, third parties, builds, deployment, and operations as relevant. For each topic collect evidence, perform authorized verification, establish what it proves, propose the owning repair, and define regression. Match primary sources and project versions using [Source register](source-register.md).

## Authority, evidence, ownership

Record URLs/revisions/environment/roles/tenants/data and available server visibility. Reuse authority already given. Start with source/readonly observation and isolated local verification; inspect scripts and target configuration before execution. A test name does not establish a test environment.

Production orders, deletes, permission changes, paid jobs, messages/webhooks, external export, credential/session changes, and deployment may have real consequences. Continue authorized bounded tests; otherwise prepare a concrete safe test plan and identify the missing authority. HTTP method alone does not determine safety.

Missing source, policies, identity configuration, services, or controlled data means blocked with exact missing evidence and next steps. Absence from searched frontend source does not prove a gateway/database control is absent. Assign frontend, backend/identity, database, platform, security, and product responsibility separately. UI guards/validation/debounce are experience controls; trusted authorization, business rules, idempotency, and audit belong at an unbypassable boundary.

Preserve all affected pages and caller differences. Record necessary redacted file/request/status/role/result evidence, never full credentials, private documents, or unrelated personal data.

## 01 Object, field, tenant, and API authorization

- **Inspect:** permission matrix, UI guards, middleware, queries, serialization, tenant derivation, downloads/exports, GraphQL resolvers.
- **Verify:** authorized anonymous/self/non-owner/cross-tenant/admin fixtures, reads/writes, direct API paths as well as UI.
- **Interpret:** hidden buttons do not establish backend safety; inaccessible backend does not prove bypass. Establish that data is actually intended to be private.
- **Repair/recheck:** trusted subject/action/object/field/tenant checks, default deny, trusted tenant identity, minimal responses; test allowed and denied list/detail/search/bulk/export/attachment paths. Sources: OWASP-AUTH, SUPABASE-RLS.

## 02 Sessions and browser storage

Trace login/refresh/expiry/logout/account/tenant changes, cookie attributes, token lifetimes, local/session storage, IndexedDB, and query caches. In isolated accounts test refresh, tabs, expiry, A logout → B login, late requests and cached data. Device revocation requires specific authority.

Ordinary stored preferences are not secrets. Assess JS-readable long-lived credentials in the actual architecture; HttpOnly does not eliminate XSS/CSRF. Reuse the identity provider's supported flow, coordinate refresh/retry, partition/clear identity data, and require server support for cross-device revocation. Verify no old-account data, infinite retry, unsafe draft loss, or resurrected identity. Sources: OWASP-HTML5, OWASP-AUTH.

## 03 Database authorization and RLS

For Supabase-like platforms inspect schema/grants/RLS/policies per operation, views/functions/service roles/storage/migrations/tests. In isolated fixtures test anon/authenticated/owner/other/cross-tenant SELECT/INSERT/UPDATE/DELETE on the actual affected objects.

Protected direct client APIs can be intentional. Public anon/publishable keys differ from secret/service-role keys; enabled RLS does not prove correct policies. Align grants and operation-specific policies, inspect bypass-capable roles/views/functions, migrate configuration, and test allowed data plus denied reads/writes/ownership changes/bulk/attachments. Without policies/database access, request redacted policy/migration and results, and retain blocked. Sources: SUPABASE-RLS, OWASP-AUTH.

## 04 Public configuration versus secrets

Trace client dependency graph, variable injection, built output, requests, and server entry points. Record names/locations without dumping environments. Check provider-defined capabilities of model/payment/mail/storage keys and inspect production bundles.

`.env`, obfuscation, Base64, proxy names, and Git exclusion do not keep browser-delivered values secret. “Public” in a name is not proof either. Move private calls/keys to trusted runtime, minimize scope/quota, and propose rotation/impact review for confirmed exposure. Recheck old/new builds, maps, logs and a safe test call. Public source maps alone are a source-disclosure policy question, not proof of leaked credentials. Sources: VITE-ENV, OWASP-FE, GHA-SECURE.

## 05 Runtime boundaries and server guarantees

Map browser/SSR/server components/BFF/API/edge/database/queue/third party, identity, quota, input and execution. Check prices, limits, target URLs and task transitions at trusted boundaries using harmless fixtures.

Server filenames/SSR/edge do not automatically establish authorization. Disconnect does not prove cancellation; disabled does not prove idempotency; lost response does not prove failure. Specify server validation/authorization/resource limits, stored idempotency, unknown-outcome query, real cancellation protocol, and bounded fetch/tool/proxy capabilities. Verify duplicate/lost/partial/cancel/retry behavior and actual effect counts. Without backend evidence, limit claims to frontend behavior. Sources: RFC9110, OWASP-FE, OWASP-AUTH.

## 06 CSRF and CORS

Identify automatically attached credentials, methods/content types, SameSite, Origin/Referer/Fetch Metadata, framework protection, mandatory headers, actual CORS. In authorized isolated origins trace client submission and server validation; distinguish request sent, server effect, and readable response.

No CSRF token does not prove exploitability; JWT/JSON/SameSite do not independently prove safety. Check equivalent controls and real architecture. Prefer supported framework protection, validate state-changing requests, constrain origins/credentials, preserve legitimate cross-origin flows. CORS is not object authorization. Missing session/deployment evidence remains blocked with required headers/configuration. Sources: OWASP-CSRF, FETCH, OWASP-HTML5.

## 07 Markdown, rich text, AI output

Trace untrusted user/model/document/search/API/cache values to text/HTML/URL/CSS/script sinks, raw HTML plugins/highlighters/SVG/dynamic execution. Use harmless isolated markers for escaping, sanitization, protocols/embeds across partial streams/final/history/preview/export.

A string or unsanitized input alone is not proven XSS; establish untrusted source, dangerous sink, reachable execution. Text escaping is not arbitrary HTML sanitization. Use safe text by default, maintained context-appropriate sanitization/allowlists where needed, and isolate allowed code execution. Verify dangerous capabilities blocked while legitimate formatting survives, including postprocessing/plugin versions. Sources: OWASP-FE, OWASP-HTML5.

## 08 External links and redirects

Trace return/next/download/rich-content/user URLs, parsing, final navigation, and leaked sensitive query/referrer data. Test safe relative/encoded/cross-origin/protocol/redirect cases locally.

External links are not inherently vulnerabilities. Domain-substring matching/HTML escaping do not validate a URL. Use exact parsed protocol/target policy, bounded auth redirects, appropriate opener/referrer handling, then check allowed navigation and blocked unauthorized redirects/data transfer on supported browsers. Sources: HTML, OWASP-HTML5, RFC9110.

## 09 Iframes and messages

Inspect source/sandbox/permissions/shared origin, target origin, received `origin/source`, payload schema and capabilities. With isolated parent/child pages test wrong window/origin/schema/stale identity and redirected receivers.

A wildcard, missing sandbox, or iframe alone is not confirmed exploitation; assess sensitive payload/capability. Never trust role/userId in messages or domain substrings. Minimize capabilities, validate exact endpoints/schema, isolate executable untrusted content, document alternatives when origin cannot be fixed. Verify valid embedding and rejection of unauthorized identity/data/privileged actions. Sources: OWASP-HTML5, HTML.

## 10 Upload, download, export

Inspect client hints versus server validation, names, buckets, signed-link authority/expiry, responses/jobs. Use small harmless files/synthetic data and authorized direct APIs; do not upload private material to third parties.

Accept/extensions/disabled controls are not trusted validation; downloadable does not automatically mean exposure. Enforce server type/size/object authorization, bounded resources, active-content isolation, temporary access and cleanup/recovery. Test allowed use, denied access, expiration/cancel/retry and actual usable files. Missing policies/accounts stay blocked. Sources: OWASP-AUTH, OWASP-FE, SUPABASE-RLS.

## 11 Dependencies and supply chain

Read manifests/locks/runtime/install scripts/CDN code/component origins/licenses/advisories/CI permissions/update policy. Establish actual resolved/transitive versions and reachable affected paths using maintainer advisories when needed. Inspect installation before letting untrusted scripts access an environment with secrets.

Audit counts, old versions, suspicious names, and CVEs alone do not prove exploitability; locks/popularity/official branding do not prove safety. Remove unnecessary dependencies, use reproducible installs and controlled upgrades, restrict third-party/CI privileges, prefer trusted immutable action references, and recheck build/core paths/permissions. Do not force-upgrade everything to clear warnings. Sources: NPM-CI, GHA-SECURE.

## 12 Development, preview, production builds

Read real script chains, framework/builder/runtime versions, TS configuration, CI/deployment, mocks/proxies/APIs. Inspect side effects before typecheck/lint/tests/build. Check production output deep-link refresh, asset base, lazy-load errors, environment and supported browsers.

Dev-server success does not prove build success; build success does not prove typecheck ran. Verify the actual pipeline rather than extrapolating one builder's defaults. Separate preview/production identities/endpoints/callbacks/secrets; validate required configuration. Reproduce a clean production build and inspect the artifact, preserving commands/versions/exit codes. Unavailable production headers/domains/callbacks remain blocked. Sources: VITE-FEAT, VITE-BUILD, VITE-ENV, TS-BASICS, NPM-CI.

## 13 Caches and Service Workers

Distinguish HTTP/CDN/SSR/query/memory/browser/Cache API. Inspect personalized keys/headers, scope/update/activation, and sensitive persistence. Test first/old-tab/offline/reconnect/account/tenant/new-release combinations in isolation.

`no-store` does not clear every cache; application-managed Cache API entries need their own lifecycle. Avoid disabling all caching by default. Separate static/personalized strategies, include identity semantics, exclude or safely clear sensitive entries, preserve drafts, and support old clients and worker recovery. Verify no cross-account display, stale overwrite, or unsafe upgrade. Missing CDN/worker configuration limits coverage. Sources: RFC9111, MDN-CACHE, OWASP-HTML5, VITE-BUILD.

## 14 Release and rollback

Connect commit/build/deploy/assets/configuration/migrations/monitoring versions. Review flags/history/compatibility/rollback ownership. Exercise old/new client/API/chunk/configuration combinations only in an authorized isolated deployment.

Frontend rollback does not roll back database/external effects/jobs. A hosting button does not prove recovery. Retain artifacts and compatibility windows, phase breaking migrations, define rollout/stop metrics and owners where needed. Recheck key journeys/identity/data after actual rollback; distinguish platform and application responsibilities. An unexecuted drill is a plan. Sources: VERCEL-ROLLBACK, VITE-BUILD, RFC9111.

## 15 Logs, analytics, privacy

Inspect console/errors/requests/events/replay/screenshots/forms/chat/document collection, SDK versions/purpose/recipients/filtering/access. Use synthetic sensitive markers to inspect emitted events and authorized receiving records across success/validation/error paths.

Default redaction is not proof all data is protected; distinguish policy/contracts/law/engineering advice. Use allowlists/minimal collection, source-side exclusion of credentials/sensitive content, explicit replay masking/retention/deletion/access. Diagnostics failure must not break core tasks. Verify correlation without marker transfer, plus offline SDK behavior; absent receiver visibility limits claims. Sources: OWASP-LOG, GHA-SECURE, actual SDK privacy docs.

## 16 Errors and monitoring

Inspect render/event/async/request/resource/init boundaries, maps/releases/alerts. Inject safe isolated failures by category and verify user recovery plus monitoring.

Check framework/version-specific catch scope; a render boundary does not automatically cover handlers, general async callbacks, SSR, or its own errors. Global handlers do not replace reporting handled failures. Isolate recoverable regions; correlate redacted request/release/action IDs. Recheck production reporting and maps. No events does not prove no failure: initialization gaps, shutdown, offline, sampling and blocking can hide it. Sources: REACT-BOUNDARY, OWASP-LOG.

## 17 CI and evidence meaning

Read actually invoked commands, assertions, mocks, excludes/skips/retries/data/reports. Distinguish unit/component/contract/integration/E2E/visual/accessibility/performance. Verify real business outcomes, such as saved values read back, rather than toast alone. Mocks should cover faults with substitutions disclosed; bounded real-service tests require a controlled target.

Zero exit, matching screenshot, green tests, and line coverage cannot prove all behavior, browser support, or safety. Exclude swallowed errors, empty tests, skips, and unlimited retries from false completion. Use risk-appropriate layers, isolated data/credentials, observable locators/waits, failure traces, and counterexamples that fail before a fix.

Automated accessibility cannot replace keyboard/focus/assistive-technology checks; emulation is not a real device; browser E2E is not an authorization audit; no real backend means no verified persistence/permissions. State denominator/environment/exclusions for every coverage claim. Sources: PLAYWRIGHT-BP, PLAYWRIGHT-A11Y, GHA-SECURE.

## Repair tasks and handoff

Each finding/risk needs affected units/boundary, evidence/impact, minimal safe preconditions/steps/actual/expected, missing links, exact owning mechanism and location, frontend/backend/platform roles, migration/compatibility, recheck layer/input/output/failure criteria, and blocked-unlock conditions. Prioritize consequence/reachability/data risk/dependencies, not generic tool counts or historical defect percentages. A frontend report is not whole-system security certification.
