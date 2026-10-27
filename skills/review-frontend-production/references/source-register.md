# Primary sources and version checks

Use this register to trace rules, not as a fixed-version implementation manual. Open only sources relevant to the current question. Inspect installed versions/configuration first, then verify version-sensitive behavior online. Historical AI-quality studies and vendor marketing are not this project's defect rate, severity, or acceptance standard.

## Classify sources

- Standards: identify applicable version, section/criterion/protocol context; normative requirements differ from informative examples. A platform standard is not the whole product's acceptance contract.
- Official guidance: compare recommendations to actual constraints; an example architecture is not the only valid implementation.
- Framework/platform docs: match version, router mode, runtime, and hosting product; avoid cross-framework assumptions.
- Performance: distinguish recommended reference values, contractual metrics, and project budgets; record device/network/build/sample/percentile/date.
- Legal/compliance: verify applicable jurisdiction, contract, and requested standard separately; engineering guidance alone does not create a legal conclusion.
- Conflicts: retain version/condition differences and unresolved uncertainty rather than removing caveats.

## Check versions

1. Read manifest, actual lockfile, packageManager, runtime/framework configuration, and CI; use installed metadata for resolved versions when available.
2. Record declared ranges and resolved versions separately. Do not install/upgrade latest merely to identify a version.
3. Distinguish dev/build/preview/production/SSR/edge and trace actual script chains, including independent typecheck/lint/test stages.
4. Match official major/version docs, migration guides, and release notes. For rolling docs record access date and applicability.
5. Record browser/version/OS/input and real-device results. Emulators and one engine do not prove all target environments.
6. Inspect actual gateway/hosting configuration/responses before calling an absent source control a missing deployment capability; inaccessible configuration stays blocked.
7. Verify advisories' affected/fixed versions and reachable paths, not only scanner labels.
8. Cite title, stable URL, version/section, access date, and project evidence in persistent reports. Do not save session-only search reference IDs.

## Browser and protocol

| ID | Primary source | Use and limits |
|---|---|---|
| HTML | [WHATWG HTML](https://html.spec.whatwg.org/multipage/) | Native semantics/forms/navigation/iframes/messages; verify target-browser behavior, not semantics alone |
| FETCH | [WHATWG Fetch](https://fetch.spec.whatwg.org/) | Credentials/requests/responses/redirects/CORS; sent, executed, and readable are distinct |
| RFC9110 | [HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110.html) | Idempotency/retry including §9.2.2; method name alone does not prove business idempotency |
| RFC9111 | [HTTP Caching](https://www.rfc-editor.org/rfc/rfc9111.html) | Cacheability/authentication/directives/validators; not all application caches follow HTTP cache rules |
| MDN-CACHE | [Cache API](https://developer.mozilla.org/en-US/docs/Web/API/Cache) | Application-managed entry lifecycle/compatibility; distinguish it from HTTP headers |

## Accessibility and performance

| ID | Primary source | Use and limits |
|---|---|---|
| WCAG22 | [WCAG 2.2](https://www.w3.org/TR/WCAG22/) | Requested level and applicable criteria/exceptions; distinguish conformance from legal applicability and automated scan results |
| ARIA-APG | [WAI APG](https://www.w3.org/WAI/ARIA/apg/) | Dialog/tabs/menu/combobox semantics and keyboard guidance; examples are not exhaustive mandatory implementations |
| VITALS | [Web Vitals](https://web.dev/articles/vitals) | Recheck current metrics/thresholds/measurement; lab observation differs from field percentiles and a single Lighthouse score |

If adopting LCP/INP/CLS recommendations, identify them as experience goals, apply the correct mobile/desktop p75 population, and do not claim field compliance without real samples. Accessibility guidance also links [target-size minimum](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html) and [focus not obscured](https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum.html) to their exact conditions and exceptions.

## Frameworks, builds, tests

| ID | Primary source | Use and limits |
|---|---|---|
| REACT-BOUNDARY | [React error boundaries](https://react.dev/reference/react/Component#catching-rendering-errors-with-an-error-boundary) | Rendering/reporting/catch scope; verify event/async/SSR/self-error and version-specific transition behavior |
| TS-BASICS | [TypeScript basics](https://www.typescriptlang.org/docs/handbook/2/basic-types.html) | Static checking/emission/type erasure; annotations do not validate API values |
| VITE-FEAT | [Vite TypeScript](https://vite.dev/guide/features#typescript) | Transpilation versus checking; inspect actual build scripts for tsc/other checkers |
| VITE-ENV | [Vite environment/modes](https://vite.dev/guide/env-and-mode) | Exposure prefix/build replacement/precedence; .env presence does not establish browser secrecy |
| VITE-BUILD | [Vite production build](https://vite.dev/guide/build) | Browser targets/base/lazy assets/options; defaults change by major |
| PLAYWRIGHT-BP | [Playwright best practices](https://playwright.dev/docs/best-practices) | Visible behavior/isolation/assertion waits/traces/browser matrix; tested cases do not prove untested paths |
| PLAYWRIGHT-A11Y | [Playwright accessibility](https://playwright.dev/docs/accessibility-testing) | Automated scope/states/manual assessment; WCAG rules differ from extra best-practice rules |

For Vue, Angular, Next.js, Svelte, routers, component/query libraries, use their official version-matched docs. Do not migrate a project to tools listed here or generalize Vite behavior to every framework.

## Security and authorization

| ID | Primary source | Use and limits |
|---|---|---|
| OWASP-FE | [Web Frontend Security](https://cheatsheetseries.owasp.org/cheatsheets/Web_Frontend_Security_Cheat_Sheet.html) | Client trust/secrets/text/HTML; absence of a suggested library does not itself prove a vulnerability |
| OWASP-AUTH | [Authorization](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html) | Request/object/field/resource/default-deny controls at a trusted service, not UI guards |
| OWASP-HTML5 | [HTML5 Security](https://cheatsheetseries.owasp.org/cheatsheets/HTML5_Security_Cheat_Sheet.html) | Storage/message origins/cross-origin/embedding/offline; follow platform sources for implementation details |
| OWASP-CSRF | [CSRF Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html) | Identity carriage/server validation/equivalent controls by architecture; no token alone is not proof |
| OWASP-LOG | [Logging](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html) | Correlation/minimization/failure/access/alerts; frontend analytics is not trusted business audit |
| SUPABASE-RLS | [Supabase RLS](https://supabase.com/docs/guides/database/postgres/row-level-security) | Grants/policies/roles/operations/views/functions/tests; distinguish public keys from service secrets |

For XSS/CSP/uploads/sessions/OAuth/supply chains, follow relevant OWASP topics and the framework's official protection docs. Establish threat and execution path before concluding from keywords.

## Delivery and operations

| ID | Primary source | Use and limits |
|---|---|---|
| NPM-CI | [npm ci v11](https://docs.npmjs.com/cli/v11/commands/npm-ci/) | Locks/clean installs; switch to the project's actual npm version before applying options |
| GHA-SECURE | [GitHub Actions secure use](https://docs.github.com/en/actions/reference/security/secure-use) | Least privilege/action refs/untrusted input/secrets; recheck current defaults/features |
| VERCEL-ROLLBACK | [Vercel rollback](https://vercel.com/docs/instant-rollback) | Hosting/config recovery; does not prove database/external API/old-client compatibility |

For monitoring/replay SDKs inspect actual version capture/privacy/maps/release docs and test synthetic markers. Do not infer defaults from product branding.

## Cite in reports

For a hard violation cite applicable rule and section; for advice state benefit and conditions. External rules establish expectations, not project reproduction. Give located redacted project evidence separately, including measurement conditions where needed.

Write project version + documentation version + verified behavior; lower confidence when applicability is unknown. Do not use marketing, media retellings, historical generated-code vulnerability percentages, or unrelated incidents as this project's pass/fail basis. Update relevant rules as needed rather than indiscriminately fetching the entire register for every review.
