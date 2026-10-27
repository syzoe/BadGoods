# State, data, and asynchronous behavior

Read the actual routes, request layer, state ownership, API contracts, and callers. Choose applicable checks rather than requiring a particular framework/store/state-machine library. Use the entities, fields, and status vocabulary in [Ledger contract](ledger-contract.md).

## 1. Establish ownership and invariants

For each source of state, record owner, lifetime, update trigger, persistence, and invalidation:

| Source | Trace | Main risk |
|---|---|---|
| Server facts | Entity/version/permissions/job/normalized result | Local timer or toast pretending to confirm completion |
| URL | Resource/filter/page/sort/shareable view | Duplicate local state drifting out of sync |
| Draft | Unsaved input/selection/configuration | Refresh overwrites edits or moves them to another entity |
| Temporary UI | Expansion/focus/overlay/drag/hover | Unexpected sharing or loss across pages |
| Derived value | Counts/availability/validity/labels | Multiple stored copies disagree |
| External process | Subscription/poll/stream/upload/job | Incorrectly coupled to page lifetime |

Write business invariants first: details match the current URL entity; final results come from confirmed submissions; tenant changes cannot expose old caches. Separate mutually exclusive states from independent dimensions such as running job + disconnected logs + pending cancellation.

Cover reachable initial/wait/success/failure/interruption/recovery/invalidation transitions and meaningful combinations. Explain omitted combinations. Distinguish omitted prototype scope from broken promised behavior; `useState`, long files, or absence of Redux are not defects by themselves.

## 2. Routes and history

For every page check menu entry, direct URL, refresh, forward/back, new tab, and applicable nested/modal/subpath/server fallbacks. Reconstruct details from resource identity rather than a transient object from the previous page.

Validate path/query IDs, enums, negative/out-of-range pages, encoded values, expired cursors. Name the owner of URL/local state, pagination invalidation, and push-versus-replace behavior; typing should not create unusable history.

Distinguish missing/deleted/denied/login-required/load-failed states. Preserve safe return destinations without open redirects. Check list return restores promised filters/sort/selection/scroll. Define unsaved-navigation/draft behavior; `beforeunload` is not reliable persistence. Revoked access/deleted entities must not remain actionable through history/cache.

## 3. Shared state and component identity

Trace actual owners/consumers across list/detail/dialog/statistics. Prefer stable IDs for selection; deliberate snapshots need explicit version semantics. Check identity after sort/insert/delete/page/virtualization, especially index/random/duplicate keys. Index keys in truly static identity-insensitive lists are not automatically wrong.

Define preserve/reset/migrate/revalidate behavior on entity/workspace/mode changes. Check nested component definitions causing remounts, controlled versus default values, stale initialization, and global store/context/client lifetime across identities. Keep shared server data separate from local drafts and maintain the DEF-to-CMP impact map. A shared-code defect does not prove every instance's runtime impact.

## 4. Forms and drafts

Track loaded baseline, current draft, submitted snapshot, and server-confirmed value with concrete data.

| Situation | Required question |
|---|---|
| Async defaults arrive | Are existing edits protected or explicitly reconciled? |
| Upstream field changes | Are dependent options/values revalidated or migrated? |
| Hidden/disabled field | Does stale content submit unexpectedly? |
| Partial numeric edit | Can the user type without committing invalid intermediate values? |
| Server field error | Is it mapped, discoverable, focused appropriately, with draft preserved? |
| Background refresh | Are new server values distinct from unsaved edits? |
| Concurrent saves | Is version conflict detected instead of silent overwrite? |
| Edit while saving | Does the response confirm only its submitted snapshot? |
| Restore draft | Is it scoped by user/tenant/entity/schema version? |
| Reopen after save | Does it show the server's normalized accepted result? |

Choose autosave/undo/cross-device drafts/merge only when needed. Review sensitive persistence and retention so the next browser user cannot inherit private drafts. Client disabled states cannot substitute for server rules.

## 5. Runtime data contracts

For each API record request/response/errors, nullable/enumerated values, units, dates, pagination, and versions. Compare mocks to the real contract.

- Distinguish zero, empty, missing, null, unknown, not calculated; inspect truthy fallbacks.
- Check precision, integer bounds, scientific notation, seconds/milliseconds, percentages/ratios, timezones/ranges; centralize conversions where appropriate.
- Treat JSON, URL parameters, persisted drafts, and messages as runtime inputs. TypeScript assertions/types do not validate external values.
- Use the project's existing validation at relevant trust/high-impact boundaries; avoid repetitive internal parsing or new libraries for ceremony.
- Structural validity is distinct from business permission, balance, availability, and allowed state.
- Plan unknown enums, optional fields, renamed fields, old clients/new servers, and stale drafts. Unknown must not silently mean success.
- Define latest versus pinned resource/configuration versions versus submission snapshots; preview and execution must refer to checkable identities.
- Do not invent precise progress or missing backend fields. Create owned contract-confirmation tasks when needed. A schema file alone is not a passed contract test.

## 6. Reads and recovery

Separate initial load, valid empty, refreshing old data, failed refresh, denied access, and partial failure. Check HTTP status and parsing as well as exceptions. Distinguish network/timeout/cancel/authentication/authorization/business/server failures and offer appropriate recovery.

Label stale data by risk. Preserve independent regions when one request fails, while respecting actual dependencies. Filtering/counting/sorting only a loaded page must not claim whole-dataset scope. Define current-page/cross-page/all-matching selection, and recheck it after query changes.

Cover deleted last items, empty pages, changed/unknown totals, duplicates, invalid cursors, and late pages. Retry according to semantics; permanent parameter failures and unknown writes are not generic retriable reads. Record redacted request conditions, status, visible outcome, recovery, and final result as evidence.

## 7. Races and effect lifecycle

Use deterministic delays/order, not random slow networks:

| Race | Invariant |
|---|---|
| Search A then B, A returns last | Input and results still describe B |
| Detail A → B | A's result/error/toast cannot overwrite B |
| Filter and page change | Old-condition pages cannot enter the new list |
| Two autosaves | Older saves cannot overwrite newer edits, including server-side |
| Refresh versus optimistic mutation | Old snapshot cannot silently erase pending intent |
| Events after unmount | No writes to another page; release owned resources |

Inspect effect dependencies, stale closures, handlers, polling overlap, resubscription, cleanup. Preserve useful effects; route user-intent writes through the relevant action instead of accidental mount/synchronization replay. Accept query libraries, router loaders, identity checks, cancellation, or stale-result filtering when they demonstrably work.

`AbortController` can end client waiting/reading; it does not prove the server never executed or rolled back a write. Review server ordering/idempotency/versioning separately.

## 8. Writes and optimism

For create/save/delete/start/stop/regenerate explain unsent, awaiting confirmation, confirmed success/failure, and unknown outcome, using the project's terminology.

Test repeated click/key activation, multiple tabs, timeout/retry. Distinguish explicit rejection from executed action with lost response. Retain submission identity and query/recover unknown outcomes. Agree server idempotency scope, lifetime, and same-key/different-payload behavior for high-impact operations; retries of one intent reuse identity, new intents receive new identity. A client random ID/boolean alone is not deduplication.

For batches distinguish whole success, partial success, and per-item failure; retry failures without replaying successful effects. Use optimism only where appropriate; payment/permission/cancellation may need pending confirmation. Track each mutation's identity/entity/value. Avoid rolling back an old whole snapshot over later successful edits; choose serialization, operation-specific undo, replay, or refetch/merge.

Reconcile server normalization, temporary IDs, sort/count/detail caches, and pending markers on every outcome. Preserve drafts on version conflicts. Define success in business terms, not simply Promise resolution.

## 9. Cache and tenancy

Record result identity: relevant tenant/workspace, user permission scope, entity/version, filter/sort/page/cursor/representation. Include what changes the result and its identity boundary, without needless keys.

Handle visible and persistent caches, requests, and subscriptions on logout/account/tenant/permission change. Trace mutation effects on lists/details/summary/selectors/quota/permissions. Specify exact update, invalidation, or revalidation. Check freshness/GC/refocus/reconnect/poll/persistence against real needs.

Keep cache refresh separate from drafts; define missing/deleted/revoked/stale-version outcomes. Add cross-tab/offline/cross-device synchronization only when required. Correct keys cannot replace server authorization; correct server authorization cannot prevent stale frontend disclosure by itself.

## 10. Sessions and permissions

Test expiry/revocation/account change while open. Avoid refresh storms, repeated login dialogs, and infinite retry. After refresh verify requests still belong to the same authorized identity; never replay the previous user's pending writes under a new account.

Do not auto-resend non-idempotent unknown writes after login; query their identity first. Reauthentication cannot repair denied permission. Preserve safe drafts/destinations without cross-identity leakage. Missing operation permissions/version checks remain backend tasks. Do not probe unrelated accounts or record cookies/tokens.

## 11. Jobs and cancellation

Model request, durable job, live connection, and artifact separately. Accepted/created/running/succeeded are distinct facts. Persist job identity to recover after refresh instead of recreating jobs.

Use server-supported phases and business success conditions, including processing/upload failures after computation. Separate phase, connection, cancellation request, and artifact availability. Handle cancelled-versus-completed races, rejected cancellation, and unknown outcomes honestly; only confirmed terminal state supports “cancelled.”

Use stages/counts without a known total rather than fabricated percentages. Define terminal polling/stream stop, backoff, visibility, reconnect/resume, cleanup. Bind logs/metrics/artifacts to run/attempt IDs. Distinguish deleting a record/artifact/job, cancelling execution, and retrying. Missing cancellation/idempotency/cursors/query contracts get owned backend tasks; honest pending/disconnected UI is a valid interim state, not end-to-end completion.

## 12. AI streaming

Apply only to actual streaming/conversation/tool workflows and their protocol; not every stream is SSE.

| Situation | Check |
|---|---|
| Character/JSON split across chunks | Incremental decoding and framing; chunk is not message |
| Reconnect/replay/duplicates | Message/run/event identity, deduplication/resume/gap recovery |
| Conversation switch | Old stream cannot write into new conversation |
| Stop | Distinguish stop display, transport close, server cancel; preserve partial output/reason |
| Disconnect | Incomplete is interrupted/recoverable, not automatic success |
| Regenerate/edit branch | Explicit replace/branch/append and old-response isolation |
| Partial tool arguments | No execution before complete validation; correlate call/result/error |
| Tool retry | Server idempotency/query; no duplicate messages/payments/jobs |
| Long output/history | Bounded rendering/cache/subscription lifetime; no stream recreation |
| Terminal event | Correct complete/refused/truncated/cancelled/error state |

Render partial Markdown/links/code safely. Manage announcements, focus, and follow-scroll without interrupting history reading. Token/cost/time/tool traces need a source and estimated/final distinction; model text is not proof of server execution.

## 13. Fault scenarios and handoff

Use ledger preconditions, nonempty steps/expected, all six context fields, risk, and IDs. Evidence records need actual kind/location/time/baseline/summary; contracts are specifications, screenshots artifacts, neither a live pass. Planned verification goes in task scenario IDs; executed evidence goes in evidence IDs.

Start with relevant single faults, then high-impact combinations: reordered/lost responses; repeated actions/entity changes/refresh/history; editing + refresh/concurrent tabs; tenant change + late request/expiry + unknown write; cancellation + completion/stream interruption; partial bulk success + changed selection scope.

Use authorized isolated services or replayable mocks and disclose substitution limits. Unavailable runtime means static findings and blocked scenarios; use investigate plans for unknowns, not retain or certain invented rewrites. At handoff answer whose data, which version, when confirmed, whether complete, and how failure recovers. Preserve remaining backend dependencies.

## Primary references

Match project versions before applying: [React state structure](https://react.dev/learn/choosing-the-state-structure), [state preservation](https://react.dev/learn/preserving-and-resetting-state), [effects](https://react.dev/learn/you-might-not-need-an-effect), [TypeScript types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html), [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch), [HTTP semantics](https://httpwg.org/specs/rfc9110.html), [OpenAPI](https://spec.openapis.org/oas/latest.html), [query keys](https://tanstack.com/query/latest/docs/framework/react/guides/query-keys), [optimistic updates](https://tanstack.com/query/latest/docs/framework/react/guides/optimistic-updates), [router state](https://reactrouter.com/explanation/state-management), and [network concurrency](https://reactrouter.com/explanation/concurrency).
