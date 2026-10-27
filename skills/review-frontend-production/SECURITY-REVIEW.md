# Security review — 0.4.0-beta

Date: 2026-10-27. Scope: the complete skill directory, including instructions, references, examples, metadata, tests, and both Python helpers. Manual review and SkillSpector v2.3.12 static analysis only; no LLM analysis or paid provider call.

## Confirmed defects repaired

1. **Predictable temporary ledger file.** The old save helper used `<ledger>.writing`, clobbering an unrelated file or following its symlink. The helper now writes to a unique sibling temporary file and atomically replaces the ledger. Failed serialization preserves the original and removes its temporary file. Regression checks cover each case.
2. **Credential-file aliases during fallback discovery.** The directory-walk fallback could read an excluded credential file through a source-named in-project symlink. The helper now checks the resolved target before reading. Tests force the fallback and cover internal credential aliases plus external symlinks; the original implementation demonstrably exposed the synthetic declaration.

## Static scanner verdict

**DO_NOT_INSTALL. This is not a passing security scan.** Static component coverage is 100%; LLM analysis is disabled, and the report's overall `is_complete` remains false. No finding baseline or suppression was applied. No installation is part of this repository-editing task.

The scanner reports these rule families:

| Rule | Reported concern | Source review context |
|---|---|---|
| AST4 | External process execution | Discovery runs a fixed `rg` argument list; tests run the bundled ledger CLI with controlled arguments. Both explicitly use `shell=False`. These remain process-execution capabilities, not a sandbox guarantee. |
| OH1 | Unvalidated model output reaching a command | The discovery command is constructed from fixed flags/exclusion constants, not model text or scanned source. The project directory is passed as `cwd`, not interpolated into a shell. The generic flag remains unsuppressed. |
| PE3 | Credential-file access | Matches include documentation warning about exposed configuration, exclusion checks, and synthetic tests. The reviewed discovery paths exclude credential names and resolved credential targets. The flags do not by themselves demonstrate credential theft. |
| LP3 | Missing permissions field | No top-level `permissions` field is declared. The package validator rejects that field; inventing unsupported metadata would not enforce least privilege. The instructions describe authority and capabilities, and the host remains responsible for actual permissions. |

Manual source review did not establish the command-injection or credential-theft paths claimed by those generic flags. That assessment does not convert the scanner verdict to SAFE or authorize bypassing an installation gate. Resolve or explicitly review the outstanding verdict under the intended host's installation policy before installing.

## Execution and privacy boundaries

The helpers use Python's standard library. Discovery lists and reads eligible source/configuration files; it does not run package scripts, load the application, or make network calls. It may invoke installed `rg`. The ledger helper reads/writes the requested ledger/report paths. Test subprocesses invoke the bundled CLI with synthetic temporary data.

Discovery is bounded and heuristic, not complete inventory. Reports can expose project paths, package names, routes, and symbols; review/redact outputs before sharing. Documentation instructs agents to inspect project scripts and respect authority for real external effects. Static review cannot certify every host, dependency environment, browser interaction, backend control, or future revision.
