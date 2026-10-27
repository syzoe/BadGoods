# Frontend Review Assistant

Version: **0.4.0-beta** · 2026-10-27

An engineering review skill for prototypes and AI-generated frontends. It checks pages, states, and component instances, then produces evidence-backed findings, repair plans, and acceptance criteria.

## Choose a task

- **Quick check:** focus on core journeys and deliver a short partial review. This is the default.
- **Full review:** inventory every discovered page and component instance, track evidence and gaps, and prepare component plans and tasks.
- **Implement fixes:** make and recheck changes only when the user requests implementation.

Reports default to English. Ask for another language when needed; the application itself keeps its existing language and design unless the task changes them.

## Use the skill

The directory and stable skill ID are `review-frontend-production`. Add the whole directory to a host that supports local skills, using the host's installation instructions, or ask an agent to read `SKILL.md`. The downloadable ZIP places `SKILL.md` at its root and includes the same supporting files as this directory.

Example requests:

> Use $review-frontend-production for a quick frontend check. Focus on signup, login, and recovery after failed submissions. Report the main findings without editing source.

> Use $review-frontend-production for a full review. Inventory every page and component instance, then deliver the fix plan and unverified areas.

> Use $review-frontend-production to fix the confirmed P1 findings in this report and recheck affected journeys. Preserve the existing design.

Provide an accessible project path or URL and the core tasks. Include the supported devices and design references when available. Use isolated test identities through the host's approved authentication mechanism; never paste credentials into a report.

## Capabilities and outputs

The helpers use the Python 3 standard library; Python 3.9+ is recommended. `rg` is optional: discovery falls back to a bounded directory walk. Browser review requires host-provided browser/testing tools. Application build tools come from the project, not this package.

| Input | Supported conclusions | Remaining gaps |
|---|---|---|
| Source and runtime | Static and executed checks, matched by baseline | Inaccessible services, roles, devices, or environments |
| Source only | Implementation review and definite static defects | Live interactions, real API behavior, measured performance |
| URL only | Observed states, navigation, and behavior | Hidden routes, source structure, backend controls, builds |
| Screenshots | Visible layout/content in captured states | Interaction, timing, unshown states, performance, security |

Quick output: `quick-review.md` and evidence as needed. Full output: `review.md`, `audit.json`, `coverage.md`, page reports, component plans, and tasks. Without Python, maintain the same ledger fields manually and disclose that validation was not run. Without file writing, deliver copyable content in chat.

Discovery emits candidates, not a complete inventory. Ledger validation checks declared structure and relationships, not evidence authenticity or product correctness. The [source-only example](examples/source-only/README.md) deliberately keeps its browser checks blocked.

## Verify the helpers

From this directory:

```sh
python3 -B -m unittest discover -s tests -v
python3 -B examples/source-only/verify_fixture.py
python3 -B scripts/audit_ledger.py check examples/source-only/audit.json --require-plan
```

The example's plan check should return `0`. Its `--require-complete` and `--require-ready` checks should return `2`: browser verification and release conditions remain unmet.

## Sharing and maturity

Exclude system metadata, Python caches, real project evidence, and account information from shared packages. Helper output may include absolute paths, package names, routes, and source locations; redact it before sharing. Examples here are fictional.

This is a beta. Cross-framework end-to-end behavior and every host's installation flow have not been validated. Optional `agents/openai.yaml` metadata and the SVG icon are included; a particular upload service may require a different format. No platform acceptance is implied.

See [CHANGELOG.md](CHANGELOG.md), [VALIDATION.md](VALIDATION.md), and [LICENSE-NOTICE.md](LICENSE-NOTICE.md).
