# Validation record

## 0.4.0-beta — 2026-10-27

Environment: Python 3.14.6, macOS. No new runtime dependency was installed.

- **Regression suite: 22 tests passed.** Includes the existing evidence/state/reference/cycle/depth/legacy/CLI/discovery checks plus unique-save preservation, sidecar symlink protection, failed-save cleanup, English output, and internal credential-alias exclusion. Symlink checks exercise the directory-walk fallback explicitly.
- **Defect reproduction:** the original save helper removed an unrelated sidecar; the original discovery fallback exposed a synthetic declaration through a credential-file alias. Both are covered by the revised tests.
- **Skill frontmatter validator:** passed. Default Python lacked PyYAML, so the same installed validator was run with the existing SkillSpector Python environment, which already provides it. No package installation was needed.
- **Fictional fixture:** static parser passed; current English baseline is `fixture-v2-en`. New source/test records EV-003/EV-004 preserve the distinction from historical EV-001/EV-002.
- **Example gates:** schema and `--require-plan` exit `0`; `--require-complete` and `--require-ready` exit `2`, as intended. The example retains 31 blocked checks, one source-confirmed failure, and one blocked scenario.
- **English/local references:** repository prose, host metadata, fixture values, and generated output checked for untranslated Chinese; local Markdown file targets resolve. Legacy Chinese input recognition remains encoded in the validator for compatibility.
- **Distribution:** ZIP rebuilt from the skill directory, with `SKILL.md` at its root; source/package byte parity, clean entry names, and excluded caches/system metadata checked. Extracted-package tests and example checks are included in the release verification.
- **SkillSpector v2.3.12:** static-only scan, 100% component coverage, verdict **DO_NOT_INSTALL**. Overall analysis completeness remains false because LLM analysis is disabled. No suppressions/baselines. See [SECURITY-REVIEW.md](SECURITY-REVIEW.md) for the reported rule families and manual source assessment. This is not a security pass.
- **Selected primary sources:** W3C target-size/focus-obscuring guidance and Google's Web Vitals page checked while editing the English guides; this was not a complete external-link audit.

These checks verify the package and helpers, not a real frontend's end-to-end quality. Browser review, screen-reader use, real-device behavior, multiple real frameworks, every host's installation flow, and distribution-platform acceptance were not exercised. No local skill installation or application deployment was performed.

## Historical validation — 0.3.0-beta, 2026-10-10

The original record reported Python 3.8.5 on macOS; 17 standard-library regression tests, skill frontmatter validation, static fixture parsing, local Markdown links, and a limited public-sharing content check passed. Example plan exited 0 and complete/ready exited 2. System metadata/caches were excluded.

That historical record did not establish browser behavior, multi-framework compatibility, every host's installation, live availability of all external links, or acceptance by the intended upload platform. The earlier example also retained 31 blocked checks, one source failure, and one blocked scenario. These are historical claims, not new executions on Python 3.8.5.
