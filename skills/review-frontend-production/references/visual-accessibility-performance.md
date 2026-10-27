# Visual, accessibility, and performance verification

Choose checks from the actual page/instance inventory and supported tasks, devices, languages, themes, accessibility and performance goals. Preserve design decisions unless evidence shows a defect or conflict. Distinguish unsupported environments from broken promised support; basic semantics/keyboard/IME are relevant to supported interaction, not only international products.

Keep source inspection, design comparison, automated scans, emulation, real browser, real device, and assistive-technology evidence distinct. Missing tools/accounts/references/builds remain specific gaps. Use authorized isolated data rather than real orders, paid jobs, or destructive actions.

## V01 Evidence record

Record scope/PAGE/CMP/SCN/baseline; browser/version/OS/viewport/DPR/input/language/theme; role/data/quantity/boundaries; preconditions/action/reversal/wait; actual layout/focus/request/console/trace/announcement; verdict/reason; located screenshots/test/source/trace. Reasoning alone cannot replace an executed pass.

## V02 Page visual baseline

Identify user-approved current references/design system/product conventions and expose conflicts. Without a reference, report usability/internal-consistency findings or design proposals, never invented similarity scores.

Align viewport/zoom/content/font/theme/state before comparison. Cover reachable default/content/empty/loading/error and relevant focus/pressed/busy/invalid/read-only states. Inspect below the fold, fixed/bottom actions, overlays and expanded branches, not only the first screenshot.

Save comparable baseline/current captures when available; locate actual DOM/style causes. Mask only known nondeterminism, never broken or unstable components. Explain environment/font/antialias noise.

| Layer | Trace |
|---|---|
| Structure | Headings, grouping, reading order, primary/secondary actions |
| Layout | Containers, columns, spacing, alignment, overflow, fixed regions |
| Typography | Actual loaded fonts/weights, size, line height, fallback |
| Color | Semantic tokens, overlays, border/focus, transparency, themes |
| Media | Ratio, crop, resolution, placeholder/reserved size |
| State | Stable layout and meaningful loading/error/disabled feedback |

## V03 Styles and real content

Trace tokens/shared definition/local overrides/inline styles and fix the smallest owning layer. Preserve justified differences. Check reset/scope/load order/cascade rather than stacking specificity.

Separate icon dimensions from hit area. Check fixed heights with wrapped/errors/enlarged text; flex/grid minimums, long-word wrapping, readable truncation; zero/empty/null/missing/long IDs/names/URLs; correct currency/ratio/date/unit precision.

For supported locales test longest copy, pluralization/CJK breaks/number separators/fonts and RTL mixed content where promised. DOM/read/keyboard order should remain coherent despite CSS order. Test realistic empty/one/typical/long/error lists at agreed scale, not arbitrary millions. Recheck actual theme tokens and overrides.

## V04 Microinteraction and interruption

Distinguish input received, work running, and outcome confirmed. Observe real painted feedback/focus/layout/request/results; setting loading state does not prove it appeared before blocking work.

Differentiate hover/focus-visible/active/selected/disabled/current route. Reverse transitions mid-animation; old callbacks must not override new state. On failure restore usable controls/drafts/focus. Late results must not erase new input or redirect unexpectedly.

For cancellation name what stops: presentation, transport, or confirmed server task. Motion timing follows design and evidence, not a universal duration. Auto-scroll only for explicit intent or active following; keep history position and a return-to-latest action. Reduced motion must preserve meaningful feedback.

Test overlay open-close-open during entry; query-change/clear before response; submit-timeout/back/retry; drag-out/cancel; stream-session-switch/disconnect/stop; delete-current then return. Inspect state, identity, side-effect count, focus, scroll locks and cleanup.

## V05 Responsive combinations

Maintain every page's supported-state matrix before choosing combinations. Check normal layout and both sides of actual breakpoints, adding critical width values. Add narrow + long/error/expanded combinations where they affect size/focus/actions.

Use justified representative/pairwise combinations and disclose gaps. Desktop includes narrow windows/wide screens/zoom; mobile promises add touch/orientation/soft keyboard. Emulation does not prove real IME/browser chrome/keyboard behavior.

Check applicable text-resize/reflow criteria and legitimate two-dimensional-content exceptions without excusing whole-page overflow. Mobile includes browser bars, visual viewport, safe areas, keyboard, nested touch/wheel/key scroll. Resize/rotation must preserve entity/edit state and overlay/chart/table alignment. Useful stress cases include modal + keyboard + error and wide table + frozen columns + zoom. Do not silently narrow promised support.

## V06 Stacking, positioning, scrolling

Map scroll containers, fixed/sticky regions, transformed ancestors, clipping, and portal mount points. Diagnose overflow/stacking/containing-block/viewport causes instead of endlessly increasing z-index.

Coordinate modality/inertness/focus/scroll; nonmodal overlays keep reasonable background access. The top active layer owns Escape/outside-click/focus return, not every layer. Check scrollbar appearance/removal and layout shift, sticky headers/footers/banners obscuring focused controls, nested-edge scrolling, scrollIntoView target, prepend/image/font anchoring, list/history restoration and pane minimums.

[WCAG 2.4.11 AA](https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum.html) concerns a focused component being entirely hidden by author content, with specified conditions. Distinguish it from stronger full-visibility goals and focus-indicator criteria.

## V07 IME and editing

For supported Chinese/Japanese/Korean inputs, use actual target composition behavior when possible; English automation fill is insufficient. Observe permitted composition/key/input events. Enter during candidate selection must not send/submit prematurely; validation/search/formatting cannot corrupt composition or caret.

A single `isComposing` branch is not universal browser proof. Do not add deprecated keyCode workarounds without compatibility evidence. Check paste/cut/undo/redo/mid-string/selection/autofill and voice when supported. Preserve reasonable system/editor/assistive shortcuts.

Allow legitimate numeric intermediate text and parse at intentional boundaries. Define grapheme/character/byte/token counts. Preserve password manager/paste/autocomplete. Responses must not clear new drafts; route/entity/remount changes need intentional value/caret/selection behavior.

Minimum sequence: select a supported IME; enter candidates and confirm with Enter; edit in the middle and undo/redo; paste newlines/emoji/boundary data; fail validation/submission, edit and retry; compare display/request/caret/error/entity. No actual composition environment means unverified.

## V08 Keyboard and focus

Complete the main task from page start using keyboard. Inspect Tab/Shift+Tab/read order, visible focus, skip paths, titles. Distinguish focus/selection/expansion/hover/current route.

Choose actual composite pattern before arrows/confirm/Escape; do not intercept arrows globally. Prefer native buttons/links. `aria-disabled` must prevent actions; disabled explanations need appropriate discoverability.

Test modal initial focus/trap/close/return, removed trigger, nonmodal escape paths, focus after delete/move/filter/page/reorder, route transitions/error summaries/background updates. Nested Escape must not accidentally exit multiple contexts. Inspect actual focused node and visible outcome; `tabindex` alone proves little.

## V09 Semantics and screen readers

Inspect actual DOM/accessibility tree, not screenshots. Check heading/landmark/list/table/form grouping, names of icon/repeated actions/fields, help/errors/IDs, dynamic state relationships and mounting. Placeholder/color alone cannot label or explain errors.

Ensure background/hidden content and current focus agree. Announce results/errors/counts at appropriate urgency; avoid an assertive whole page or per-token announcements. Check virtual/lazy content order/position/quantity and equivalent chart/media/document information.

With a screen reader, record software/browser combination and execute the main task, form failure, and dialog cycle. Without it, report semantic/scan evidence while preserving untested announcements/browse-mode/composite experience. A clean automated scan does not establish WCAG conformance or whole-site coverage.

## V10 Preferences, contrast, motion

Measure text/control contrast against real backgrounds, overlays/themes/gradients; apply the correct criterion and exceptions for text sizes/nontext/inactive controls. Use non-color cues for important state.

Check actual target hit areas/spacing under [WCAG 2.5.8 AA](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html): 24 by 24 CSS pixels or applicable spacing/equivalent/inline/user-agent/essential exceptions. Do not mislabel a 44 by 44 enhanced target as a universal AA requirement.

Test reduced motion for parallax/panning/zoom/autoscroll/loops while preserving feedback; pause/stop/hide for applicable autoplay/updates; forced colors/high contrast where supported; text resizing/spacing and reachable controls; flashing against actual criteria. Separate simulated preferences from real OS tests.

## V11 SSR and public pages

Apply SSR/prerender/hydration/SEO checks only where used or needed; do not force migration for “production quality.” Identify actual client/server/static/hybrid boundaries. Internal apps primarily need usable entry/auth/deep links, not automatic indexing/sitemaps.

For SSR compare initial HTML and hydrated output with matched data/locale/timezone. Trace time/random/browser-only APIs/invalid markup and personalized cache/request identity. A client marker does not automatically preclude server-generated initial HTML; match framework/version.

Fix concrete hydration mismatches instead of suppressing all warnings or disabling SSR. Evaluate no/delayed/failed JS against the product promise. For indexable pages inspect real links, titles/descriptions/canonical/status and missing-resource behavior. Do not assume client rendering makes indexing impossible. Explain SSR benefits, server/caching/freshness costs and smallest migration; source alone cannot prove hydration succeeds.

## V12 Performance measurement

Name the actual problem: load, interaction paint, API wait, long-session slowdown, or layout instability. Bind it to page/action/data/device. Prefer production builds; dev measurements are diagnostic and limited.

Record baseline/revision/browser/hardware/network/CPU/cache/identity/sample conditions; compare like for like. Use sensible repeated observations and variability, not the fastest run. Without a baseline, do not invent percentage gains.

Measure actual in-page input/search/switch/scroll/output plus repeated open/close/entity/background lifecycles. Use existing authorized real-user data if available; do not add telemetry without authority or upload sensitive content.

| Symptom | Evidence | Do not confuse |
|---|---|---|
| Key content late | LCP, resource chain, fonts/images, server/render | Warm local cache with first visit |
| Interaction feedback late | INP or event/main-thread trace | INP with whole API round trip |
| Unexpected shift | CLS and actual shift sources | Initial-load-only observation with session stability |
| Blocking CPU | Long tasks, calls, layout/paint | State set with feedback painted |
| Large content slow | DOM/render/data processing | Record count alone with virtualization need |
| Session growth | Retained resources after repeated lifecycles | One heap increase with proven leak |
| Slow API, responsive UI | Queue/network/backend/cache/conversion | Memoization with network repair |

[Web Vitals](https://web.dev/articles/vitals) currently recommends LCP ≤ 2.5 s, INP ≤ 200 ms, CLS ≤ 0.1, evaluated at the 75th percentile separately for mobile/desktop. Recheck current official definitions when used. One lab run is not field p75; Lighthouse score is not all performance; TBT is not INP. Business end-to-end job/export/file latency is distinct from these metrics.

## V13 Evidence-driven performance repairs

| Evidence | Conditional repair | Regression costs |
|---|---|---|
| Unneeded module blocks entry | Route/feature splitting, defer/prioritize | First-use load/failure/retry |
| Fonts/images delay content | Appropriate media, formats, loading/reserved size | Quality/fallback/crop/layout |
| Synchronous long work | Chunk/yield/worker where justified | Transfer/cancel/copy/identity |
| Local input rerenders everything | Narrow ownership/stabilize boundaries, then cache | Stale closures/consistency/complexity |
| Excess DOM/paint at real scale | Pagination/query/incremental/virtualization | Focus/screen reader/find/print/selection/scroll |
| Duplicate/reordered requests | Ownership/dedupe/invalidation/stale filtering | Identity/freshness/offline |
| Stream repeatedly reparses long history | Batch/stable blocks | Partial state/copy/announcements/scroll |
| Changing dimensions | Reserve space, stable async/fallback | Extreme content/narrow layouts |
| Retained resources | Cleanup owned timers/subscriptions/URLs/connections/cache | Shared consumers still using them |

A main-thread task over 50 ms is a diagnostic long-task clue, not a universal business-operation deadline. Do not universally add memoization, virtualization, Workers, or one animation technique. Preserve required content/semantics/diagnostics. Recheck the original issue and affected risks; stop optional testing when sufficient.

## V14 Tools and execution

Discover project and host capabilities; follow documented interfaces and access rules. Reuse installed runners. No assumed API, handle, authentication, browser, Playwright installation, or connector capability.

Use `rg` to locate relevant semantics/events/styles/resources, then read definitions and callers. Keyword presence/absence does not establish defects. In available browsers set real preconditions, use documented state/DOM APIs and contextual locators, execute main/reversal paths, wait for actual conditions, inspect focus/results/requests/console, and save evidence where possible.

Read scripts before tests. Prefer behavior-based counterexamples and deterministic response order; dialog presence alone does not prove modality. Keep actual IME/manual/device gaps. Record runner/rules/state and distinguish absent dependency, skipped/failed/timed-out command from pass. Never present example code or expected output as executed results.

## V15 Findings and handoff

For every relevant page/state/instance retain location, verification level, environment/data/role/action/interruption, user impact, specific owning mechanism, smallest change, acceptance and affected callers, baseline comparison, and remaining limits.

Separate design differences/usability/performance/product tradeoffs. State conditions/benefits/migration/backend dependencies without unsupported rewrite prescriptions. Full review means reconciling the inventory and explaining every unchecked/not-applicable item, not merely listing many findings. Missing tools/devices/roles/builds limit evidence, not automatically code quality.

## Primary references

Use [WCAG 2.2](https://www.w3.org/TR/WCAG22/), [APG](https://www.w3.org/WAI/ARIA/apg/patterns/), [modal dialogs](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/), [cross-browser testing](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Testing/Introduction), [VisualViewport](https://developer.mozilla.org/en-US/docs/Web/API/VisualViewport), [isComposing](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/isComposing), [reduced motion](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@media/prefers-reduced-motion), [date formatting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat), [React hydration](https://react.dev/reference/react-dom/client/hydrateRoot), [Google JavaScript SEO](https://developers.google.com/search/docs/crawling-indexing/javascript/javascript-seo-basics), [Web Vitals](https://web.dev/articles/vitals), [long tasks](https://web.dev/articles/optimize-long-tasks), [Playwright assertions](https://playwright.dev/docs/test-assertions) and [emulation](https://playwright.dev/docs/emulation), matching actual project versions and supported environments.
