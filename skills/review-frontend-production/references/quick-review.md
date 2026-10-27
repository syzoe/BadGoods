# Quick review

Find risks in selected core journeys and deliver a concise, inspectable partial review. Follow the evidence, permission, and design-preservation rules in `SKILL.md`. Full-ledger, per-instance blueprint, and full-coverage gates are not required here.

1. Record project location, version, access, user goal, and limits. State that the depth is `quick` and does not establish whole-site coverage.
2. Inspect directories, routes, and main entry points. List discovered pages, select the requested journeys or highest-impact tasks, and explain selection and omissions. The optional discovery helper produces candidates only.
3. Check success, failure, and recovery, plus directly related interactions, state, accessibility, data, and permission boundaries. Load only the relevant component/topic sections.
4. Give each finding a location, evidence kind, reproduction conditions or source reasoning, actual/expected behavior, impact, priority, repair direction, and verification. Separate static risks from executed reproduction.
5. Lead with the largest user impact. Include other findings and unverified areas without a fixed finding quota. With no findings, report the checked scope; “none found” does not mean “no defects.”
6. Deliver `quick-review.md`: scope/baseline, findings, fix order, unchecked/blocked areas, next actions. Save evidence separately as needed. Honor an explicit time budget and preserve unfinished checks.

Do not require `--require-plan`, `--require-complete`, or `--require-ready`. If using a ledger, set `project.review_depth` to `quick`; never use it to evade a requested full review.

To upgrade to full, preserve findings and original evidence under stable IDs, then complete pages, definitions, instances, scenarios, and plans. Continue an authorized upgrade without requesting review permission again.
