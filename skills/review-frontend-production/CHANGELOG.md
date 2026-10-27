# Changelog

## 0.4.0-beta — 2026-10-27

- Made the repository README, skill instructions, nine reference guides, report templates, host metadata, example, and generated reports English. English is the report default; users can request another language without changing the application's own content language.
- Condensed repeated guidance while retaining all 32 component categories, eight instance dimensions, ten blueprint dimensions, and the existing quick/full and audit/implement workflows. Stable skill ID and ledger schema remain unchanged.
- Made capability limits, script inspection, evidence baselines, output safety, and the difference between proposed and executed acceptance checks easier to follow.
- Fixed ledger saves that could clobber an unrelated `<ledger>.writing` file or follow that sidecar's symlink. Saves now use unique atomic temporary files and clean up after failed serialization.
- Closed a discovery privacy gap: source-named symlinks pointing to excluded credential files inside the project are now skipped at the resolved-path boundary. External symlink protection remains in place.
- Added regression checks for sidecar preservation, symlink-target preservation, failed-save recovery/cleanup, and English default output. The suite now has 22 tests.
- Updated the fictional fixture to English as `fixture-v2-en`, retained historical evidence, and recorded new source/static checks without inventing browser results.
- Rebuilt the download ZIP from the complete skill directory, including optional host metadata and icon; package contents are checked against source.
- Kept the existing license status. Public download does not imply an open-source license.

## 0.3.0-beta — 2026-10-10

Historical release notes, translated from the original:

- Added a Chinese display name while preserving the stable English skill ID.
- Documented inputs, direct-use examples, outputs, and host capability fallback.
- Added a distribution ZIP with `SKILL.md` at its root and publishing-form guidance.
- Kept unverified platform eligibility, format, and review-time claims out of execution rules.

## 0.2.0-beta — 2026-10-10

Historical release notes, translated from the original:

- Added quick/full depth selection while retaining full-review coverage requirements.
- Added usage guidance, a fictional source-only example, and standard-library regression tests.
- Validated `review_depth`; quick mode cannot pass full-review or readiness gates.
- Excluded system metadata/caches from distribution and documented evidence/privacy/license/validation limits.

Existing rules and ledger structure remain compatible. Legacy ledgers without `review_depth` use full mode. These releases added no automatic browser review or product certification.
