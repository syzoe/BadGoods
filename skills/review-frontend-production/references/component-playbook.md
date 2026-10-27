# Component review playbook

Locate real UI units before selecting a section. These are conditional review prompts, not features every application must implement. For each applicable component record states, actions/reversal, semantics/keyboard, data/layout, acceptance, and the smallest repair. Acceptance examples remain plans until executed with evidence.

Use existing components, tests, and public APIs. Cover only promised capabilities: asynchronous, permission, remote-data, multi-select, and editable behavior apply when present. Explain non-applicability. Test hover with a pointer and discoverable alternatives on touch. Cover meaningful combinations such as read-only + error or refreshing + stale value.

Honor the session's authority for writes, paid calls, and deletions; use isolated data where appropriate. Record browser/viewport/input/identity/data, steps, outcomes, and EV. Separate static confirmation, live reproduction, unknowns, and non-applicability. A clean scan is not a universal pass.

## Shared definitions and page instances

- Definition: implementation/version, public interface, internal states, semantics, events, base styles, keyboard contract. Its evidence applies only to tested variants.
- Instance: route/region/entity, props, labels/IDs, permissions, local data/CSS, clipping, stacking, responsive layout, parent form, bubbling, callbacks, focus return.
- Journey: upstream/downstream state, cross-control focus, failure, cancellation, refresh, recovery, server outcome.

Map every definition to its instances. Repeated records may use justified equivalent classes; different contracts remain distinct. Recheck all materially different callers and high-risk instances after a shared fix. Fix caller defects at the caller instead of changing a sound shared contract. State “6 of 8 instances verified; 2 lack test-role access,” never “the library passed, so every page passed.”

## Section combinations

| Page type | Start with |
|---|---|
| Settings/form | C01, C03–C09, C14, C29; C10–C13 for overlays |
| Data management | C16, C18–C25, C29, C32; each row action's C01/C12 |
| Document workspace | C11, C24, C26, C28, C32; scrolling/focus/long sessions |
| AI conversation/jobs | C04, C25, C29–C32; session identity and server cancellation |
| Public/information page | C02, C16–C18, C27–C29; SEO only where required |

A unit may use several sections, such as C06/C21/C22 for a searchable multi-select filter. For unlisted components, derive checks from the same six dimensions.

## C01 Buttons and icon buttons

- **States/actions:** default, focus, pressed, disabled; async busy/failure/success/revoked permission. Test double activation, key repeat, cancellation or navigation while busy, accidental parent actions.
- **Semantics/layout:** native button, explicit form type, meaningful name; `aria-disabled` needs actual enforcement. Check longest supported labels, spinner sizing, icon alignment, touch area, adjacent actions.
- **Acceptance:** keyboard activate twice under controlled delay; check feedback, actual side-effect count, and retry after failure.
- **Repair:** correct semantics/form behavior, bind busy state to the real request, and establish server idempotency for repeated creation where needed.

## C02 Links and navigable areas

- **States/actions:** current/focused, missing/denied/expired targets; open, new tab, copy, deep-link refresh, history, child-button bubbling.
- **Semantics/layout:** real `href` and distinguishable names; preserve native navigation. Check long URLs/titles, wrapping/truncation, nested interactive elements.
- **Acceptance:** directly open the destination, navigate history, use keyboard, and test an unavailable target's recovery.
- **Repair:** restore link/router contracts; separate card navigation and inline actions. Add external/download explanations only where useful.

## C03 Single-line inputs

- **States/actions:** empty/value/focus/read-only/disabled/invalid; pending/stale async validation. Type, paste, clear, undo, autofill, edit mid-string; change value during validation.
- **Semantics/layout:** labels/help/errors, purpose-appropriate type/input mode/autocomplete; preserve password managers/paste. Test IME, emoji, whitespace, long values, numeric intermediate text and caret stability.
- **Acceptance:** confirm an IME candidate, paste/undo/edit, and compare displayed/submitted values, errors, caret.
- **Repair:** separate editing text from parsed values, defer destructive formatting, ignore stale validation, enforce essential rules server-side.

## C04 Multiline text and message composers

- **States/actions:** whitespace/newlines/limits/drafts/sending/failure; attachment combinations. Distinguish Enter-to-send, modifier newline, IME confirmation; continue typing after sending, switch conversation, cancel/recover.
- **Semantics/layout:** named textbox, clear send rules, normal editing shortcuts; max height, internal scrolling, long paste, soft keyboard. Define character/byte/token limits precisely.
- **Acceptance:** Enter confirms an IME candidate without sending; a failed send preserves draft/attachments/focus; test soft keyboard on a real target device.
- **Repair:** composition-aware handling, per-conversation drafts, stable submission identity; a completed send must not erase a newer draft.

## C05 Checkboxes, radios, switches

- **States/actions:** checked/unchecked/disabled/read-only/mixed, pending save/rollback. Label activation, keyboard, rapid toggling, remote failure and removed options.
- **Semantics/layout:** native controls where appropriate, named groups/options, radio keyboard model, mixed only where supported. Check long labels/help, hit regions, adjacent links.
- **Acceptance:** none → partial → all → none; paginate/filter and inspect actual selection scope; verify the server after failed save.
- **Repair:** define page/all-result selection, stable IDs, optimistic rollback, consistent value types.

## C06 Selectors and comboboxes

- **States/actions:** closed/open/active/selected/no results/disabled; remote loading/failure/removed selection/stale query. Open/select/cancel/clear/outside click; close or change query mid-request.
- **Semantics/layout:** choose actual select/combobox/listbox behavior; arrows, active option, confirm/Escape/focus. Ordinary options are not automatically menu items. Test duplicate labels/different IDs, long/many options, clipping and viewport edges.
- **Acceptance:** keyboard choose/cancel; reorder query responses; preserve the selected ID/name when absent from current results.
- **Repair:** separate query, active option, selected value; bind request identity and stable option IDs. Window only with measured need.

## C07 Numeric steppers and sliders

- **States/actions:** bounds/default/empty/invalid/disabled, crossing range handles; typing/stepping/holding/dragging/wheel/pointer cancellation.
- **Semantics/layout:** named control/handles, range/value semantics, keyboard adjustment and understandable value text. Test negatives, decimals, precision, units/locales/narrow widths.
- **Acceptance:** edit intermediate and boundary values, blur/submit, set the same result with pointer and keyboard, inspect serialization.
- **Repair:** shared bounds/step rules, separate display/storage units, intentional clamping, appropriate precision for the business.

## C08 Date and time controls

- **States/actions:** empty/valid/invalid/disabled dates/range endpoints; cross-day/DST where relevant. Type/pick/clear/change month/cancel; change start, locale, or timezone.
- **Semantics/layout:** label/format, applicable calendar keyboard model, overlay focus/return. Check leap days, month names, 12/24-hour formats, narrow layouts/errors; distinguish date-only from instants.
- **Acceptance:** view one sample in two supported zones; test leap day, reversed range, and time boundary against API values.
- **Repair:** define business timezone/data meaning/inclusive bounds; locale-aware formatting; do not automatically convert birthdays to UTC timestamps.

## C09 Forms and multi-step wizards

- **States/actions:** pristine/dirty/invalid/submitting/success/failure; conditional steps/draft restoration. Click/Enter/reset/cancel/back/refresh; retry after unknown timeout outcomes.
- **Semantics/layout:** real form/grouping/labels/error summary, meaningful failure focus, current step. Test multiple/server/cross-field errors, hidden fields, long help; inspect whether hidden stale values submit.
- **Acceptance:** return to an earlier step, fail final submission, preserve values, locate field errors, and verify actual creation count.
- **Repair:** explicit edit/submission transitions, distinct client/server validation, deduplication, dirty-navigation and final-success contracts.

## C10 Modal dialogs

- **States/actions:** entering/open/exiting/closed, async busy/failure/nesting. Trigger/close/cancel/Escape/backdrop; close during submit or after trigger removal.
- **Semantics/layout:** named dialog and real modality, initial focus, trapped Tab, logical focus return; long content, zoom, small viewport/keyboard, reachable actions and scroll lock.
- **Acceptance:** keyboard open/traverse/close, inaccessible background, sensible return after deleting the trigger.
- **Repair:** use proven native/existing modality; coordinate inertness, scrolling, focus. `aria-modal` alone does not implement behavior.

## C11 Drawers and side panels

- **States/actions:** open/closed/loading/failure/dirty; modal/nonmodal breakpoints. Switch entity, close/back/resize during save/load.
- **Semantics/layout:** choose dialog versus region according to actual modality; no arbitrary focus trap. Check remaining content width, nested scroll, fixed actions, full-screen mobile mode.
- **Acceptance:** rapidly switch entities and cross the breakpoint; inspect identity, focus, drafts.
- **Repair:** bind entity and load lifecycle, intentional reset/preservation; define visual layout and modality separately.

## C12 Popovers and action menus

- **States/actions:** open/closed/active/disabled/busy/failure/revocation. Trigger/outside click/Escape/select, scroll/resize/nesting without background activation.
- **Semantics/layout:** distinguish action menu, navigation links, and form popover; apply menu arrows/roving focus only to a menu. Test corners, long items, flipping, clipping, stacking, scroll anchors.
- **Acceptance:** open the last row's menu, scroll and keyboard-select; verify bound entity and no stray background action.
- **Repair:** existing positioning/dismissal/overlay coordination; fix clipping/context rather than escalating z-index indefinitely.

## C13 Tooltips and help

- **States/actions:** delay/keyboard show/dismiss, pointer enter/leave, focus, Escape; touch equivalent. Keep hover help readable when pointer enters it.
- **Semantics/layout:** associate description; essential labels cannot live only in a tooltip. Interactive content needs a suitable popover. Check long text, zoom, edges, occlusion.
- **Acceptance:** discover icon meaning without a mouse, access equivalent touch information, preserve focus.
- **Repair:** persistent help for essential content and predictable show/hide behavior; `title` alone is not a complete help system.

## C14 Notifications, banners, error summaries

- **States/actions:** information/success/warning/failure/dismissed, concurrent deduplication/stacking/updates; dismiss/retry/undo/locate errors through route changes and timeout.
- **Semantics/layout:** announcement urgency matches meaning; keyboard-accessible actions; routine success does not steal focus. Check long errors, narrow screens, fixed controls, sensitive server details.
- **Acceptance:** trigger success/failure, test real announcements when possible, ensure old errors cannot overwrite newer success.
- **Repair:** event/job identity, persistent entry for required actions, real server-supported undo.

## C15 Tabs and segmented views

- **States/actions:** selected/focused/disabled/loading/error, retained local state. Switch quickly, deep-link, leave dirty/pending panels.
- **Semantics/layout:** distinguish tabs from route links; tab/panel associations and appropriate automatic/manual activation. Check overflow, long labels, narrow widths, panel height, separate focus/selection.
- **Acceptance:** keyboard switch to a slow tab and back; inspect active panel, focus, URL, draft behavior.
- **Repair:** stable identity and explicit activation; automatic activation only where panel display latency permits.

## C16 Navigation, sidebars, breadcrumbs

- **States/actions:** current/expanded/collapsed/permission-filtered, async menu failure, mobile drawer; deep-link/refresh/history and navigate while expanded.
- **Semantics/layout:** named navigation, links/current location, skip path; ordinary site links do not require desktop menu semantics. Check long/deep paths and icon-only names.
- **Acceptance:** open a child URL, refresh and keyboard-return; open/navigate/close on narrow screen with no leftover focus trap or scroll lock.
- **Repair:** consistent route metadata and separate expansion/current-route state; enforce permissions server-side.

## C17 Disclosures and accordions

- **States/actions:** expanded/collapsed/loading/error, multi-open rules; toggle repeatedly, follow internal links, collapse during loading/error.
- **Semantics/layout:** native disclosure or activating button, synchronized expanded state, no hidden focus stops. Check long headings/content, animation height, fixed areas, reading position.
- **Acceptance:** close a section containing focus according to product rules; verify focus, preserved values, discoverable error.
- **Repair:** explicit hide/unmount and preservation strategy; correct height/focus behavior; mutual exclusion only when needed.

## C18 Cards, lists, repeated items

- **States/actions:** empty/one/many/selected/unavailable/loading/local failure/busy; insert/delete/reorder/select/details and act after reorder.
- **Semantics/layout:** appropriate list structure, contextual repeated names, separate card navigation/selection/child buttons. Test mixed heights, missing data, long names, image ratios, grid/read order.
- **Acceptance:** create duplicate names, delete/reorder one, act on the other; inspect actual IDs, local state, focus.
- **Repair:** stable business identity, per-entity state, suitable layout; do not use index identity for mutable records.

## C19 Tables and interactive grids

- **States/actions:** loading/empty/error/selected/sorted/missing; editing/invalid/save/conflict/partial bulk success. Sort/filter/page/resize/act while editing or after selection changes.
- **Semantics/layout:** table/header/sort relationships by default; grid only with its keyboard model. Test long/zero/null cells, units, wide/frozen tables, nested scroll, real scale.
- **Acceptance:** select, sort/page, run an authorized controlled bulk operation; verify scope, individual failures, focus, headers.
- **Repair:** stable rows/columns, explicit server sort/pagination contracts; virtualize only with evidence and recheck accessibility/find/print/focus.

## C20 Trees and hierarchical selection

- **States/actions:** expansion/selection/mixed/leaf/disabled/lazy failure/changed children; move/delete/search/collapse during load, invalidated parent.
- **Semantics/layout:** real tree hierarchy and keyboard model only where appropriate. Test depth, long/duplicate names, illegal/cyclic data, narrow widths.
- **Acceptance:** keyboard-expand, remove focused node, load children under partial selection; verify propagation and focus.
- **Repair:** separate identity/expanded/selected sets, explicit propagation rules, trusted-layer hierarchy/permission enforcement.

## C21 Search and suggestions

- **States/actions:** initial/edit/query/results/empty/failure/clear/stale results; IME, rapid changes, submit/select, reversed responses.
- **Semantics/layout:** search name/results status, combobox only for actual suggestions, no focus theft per character. Test long/special/CJK/emoji queries, duplicate names, safe highlight.
- **Acceptance:** A then B, return B then A; results remain B. Clearing cannot be undone by a late response.
- **Repair:** deliberate submit/debounce, request-query identity, cancel/ignore old responses, safe text highlighting.

## C22 Filters, sorting, condition chips

- **States/actions:** default/draft/applied/no results/failure/saved-view changes/conflict; apply/cancel/remove/reset/back and inspect page/selection/old results.
- **Semantics/layout:** named filters/removal, toggle versus display label, trackable focus. Check many/long conditions, ranges, wrapping, locale, empty versus all.
- **Acceptance:** apply then refresh/share/back per product promise; remove focused chip and inspect focus.
- **Repair:** separate draft/applied query; consistent URL/API/local serialization and explicit pagination/selection invalidation.

## C23 Pagination, load-more, infinite scroll

- **States/actions:** first/middle/last/loading/failure/end, changing totals; page/size/load/refresh/back, change filter during pending load.
- **Semantics/layout:** named controls/current position/new-result feedback, reachable footer. Test zero/unknown totals, short pages, dynamic heights, anchors.
- **Acceptance:** delete last-page record, change filter, return old request; verify no omissions/duplicates and a valid position.
- **Repair:** contract-appropriate page/cursor, stable-ID deduplication, explicit append/replace/invalidate. Do not impose infinite scroll on small lists.

## C24 Dragging, reordering, resizable panes

- **States/actions:** idle/drag/valid-invalid target/finish/cancel/save failure; edges/autoscroll/original position/Escape/pointer cancel/rapid reversal, touch scroll conflict.
- **Semantics/layout:** non-drag alternative; named/ranged keyboard-adjustable separators, outcome feedback. Test scroll/zoom/axes/minimum pane bounds/long items.
- **Acceptance:** accomplish the same move using a click alternative, cancel at an edge, inspect order/focus/save.
- **Repair:** pointer/cancel cleanup, stable IDs and explicit targets, valid bounds; mouse-only completion is insufficient.

## C25 Uploads and attachment queues

- **States/actions:** selecting/validating/queued/uploading/processing/success/failure/cancel, resume if supported; same-file reselection, same names/different files, remove/retry/navigation/offline.
- **Semantics/layout:** accessible file-picker alternative to drag, limits, named queue actions/progress. Test empty/boundary/mismatched-content files, long names, partial batches, missing previews.
- **Acceptance:** upload isolated valid/invalid samples, cancel/retry; verify IDs, final processing result, editable body.
- **Repair:** distinguish transfer from server processing, release previews, trusted file validation/authorization, idempotent retries where needed.

## C26 Rich-text and code editors

- **States/actions:** load/empty/content/read-only/dirty/save/failure/conflict; composition/paste/undo/redo/select/copy/shortcuts/document switch, close while saving.
- **Semantics/layout:** named editor, reachable toolbar and escape path, preserve normal shortcuts; long lines/docs, fences/tables/broken images/zoom, selections/scroll/overlays.
- **Acceptance:** IME plus toolbar/undo, switch documents then return old save; verify identity/content/selection.
- **Repair:** editor transactions/document model, separate source/rendering, safe rich content, versioned saves/conflict policy.

## C27 Charts, maps, data visualizations

- **States/actions:** data/empty/load/failure/selection/legend, live pause/stale/disconnect; hover or alternative query, zoom/reset/filter/resize.
- **Semantics/layout:** name/summary and appropriate equivalent data access; essential values cannot require color/hover alone. Check zero/negative/null/outliers/scales/labels/units, honest axes/aggregation.
- **Acceptance:** compare a known sample to plotted results; shrink container and retrieve essential data without hover.
- **Repair:** explicit mappings/units; choose sampling/aggregation/rendering for measured scale without changing meaning.

## C28 Images, video, audio, carousels

- **States/actions:** load/success/failure/placeholder; play/pause/buffer/end/format or permission failure. Seek/zoom/switch/close, route leave/background/media invalidation.
- **Semantics/layout:** purpose-based alt/captions/descriptions, keyboard playback, pause/manual carousel controls where applicable. Check crop/aspect/resolution/transparency/portrait media/captions/reserved space.
- **Acceptance:** fail a URL, resize, keyboard play/pause, leave; no stray audio or unclosable overlay.
- **Repair:** appropriate media semantics/loading/priority, distinct decorative/informational treatment and resource cleanup.

## C29 Loading, empty, error, placeholder units

- **States/actions:** first load versus refresh, no data versus no match, denied, partial/global failure; retry/create/back/offline recovery/late results after unmount.
- **Semantics/layout:** appropriate busy/status feedback, reachable retry/alternatives, no meaningless skeleton focus stops. Preserve space/hierarchy and label stale data honestly.
- **Acceptance:** return zero/denied/network error/partial data separately; inspect next actions, stale labels, real request state.
- **Repair:** explicit result types, independent error boundaries, meaningful terminal states instead of endless spinners.

## C30 AI streams, messages, tool results

- **States/actions:** first-event wait/receiving/tool-running/complete/truncated/failed/cancelled, reconnect/replay if supported; stop/retry/regenerate/copy/session switch/history reading.
- **Semantics/layout:** named authors/tools/actions, controlled announcements, preserve reading position/focus. Check incomplete Markdown/code/math/links/attachments and version-correct copy.
- **Acceptance:** split UTF-8/protocol frames, disconnect/duplicate events, switch session/stop; no cross-message corruption or false completion.
- **Repair:** incremental decoding/framing and stable run/message/event IDs, bounded/batched rendering, protocol completion and cancellation semantics, safe untrusted rich content.

## C31 Long jobs and run controls

- **States/actions:** queued/starting/running/needs-input/succeeded/failed/cancelling/cancelled/unknown; refresh/reconnect/retry/cancel/logs, lost submission response, cancel-complete race.
- **Semantics/layout:** named progress/controls, honest indeterminate progress, accessible log pause/copy/follow. Test long names/errors/logs, missing/regressing progress, mobile controls.
- **Acceptance:** create an authorized isolated job, retain ID, recover a lost response by querying, refresh/cancel and compare server terminal state.
- **Repair:** durable job IDs, explicit independent state dimensions, query recovery; server idempotency/authorization/versioning and confirmed cancellation.

## C32 Preview, download, export

- **States/actions:** preparing/generating/ready/failure/expired/no-preview, large-file limits; preview/page/zoom/download/cancel/regenerate after permission/link expiry.
- **Semantics/layout:** named document/controls/download, suitable equivalent content, no preview focus trap. Test file names, aspect/fonts/pagination/large tables, filters/timezone/units/export scope.
- **Acceptance:** download and actually open an isolated sample, compare contents/counts, expire the link and test recovery.
- **Repair:** separate generation/download-start/file-usability, manage temporary resources, trusted file/permission checks and spreadsheet formula risk where applicable.

## Turn observations into repair records

For each confirmed defect or important unknown give exact PAGE/CMP/DEF/source location; role/data/viewport/input/preconditions; evidence and execution level; user impact; state/event/data/semantic/layout/lifecycle cause; smallest repair with frontend/backend boundaries; normal and relevant reversal/regression acceptance; remaining dependencies.

Merge shared causes while retaining every instance and reproduction condition. For uncertain causes, specify the smallest distinguishing investigation. Repair shared-definition defects centrally, caller/layout defects locally, and business guarantees at the trusted boundary.

## Primary references

Use version-appropriate [WAI-ARIA APG patterns](https://www.w3.org/WAI/ARIA/apg/patterns/), [WCAG 2.2](https://www.w3.org/TR/WCAG22/), [modal dialog guidance](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/), [IME event documentation](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/isComposing), [Intl.DateTimeFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat), and [SSE documentation](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events). APG is implementation guidance, not complete conformance certification; native EventSource reconnect behavior does not apply to every custom streaming client.
