# BadGoods

Practical AI skills you can take into your own workflow.

## Frontend Review Assistant

Review a prototype or AI-generated frontend, find problems in pages and components, and turn the evidence into prioritized fixes and clear acceptance criteria.

**[Download the skill ZIP](downloads/review-frontend-production.zip?raw=true)** · **[Read the skill](skills/review-frontend-production/SKILL.md)** · **[See an example report](skills/review-frontend-production/examples/source-only/review.md)**

### Get started

1. Download and extract the ZIP. Add it to an AI tool that supports local skills, following that tool's installation instructions. `SKILL.md` is at the ZIP root.
2. Provide accessible source code, a URL, or screenshots, along with the main task you want reviewed.
3. Ask for a quick check or a full review:

> Use the Frontend Review Assistant to check this project. Focus on form submission and the mobile experience. List the evidence, user impact, fix order, and acceptance criteria. Do not change the code yet.

| Review | Best for | Deliverables |
|---|---|---|
| Quick check (default) | Finding the main risks in selected user journeys | A focused report, fix order, and unverified areas |
| Full review | Reviewing every discovered page and component instance | A coverage ledger, evidence, component plans, implementation tasks, and acceptance checks |

The assistant changes application code only when you ask it to implement fixes. Reports default to English; request another language when needed. The stable skill ID is `review-frontend-production`.

Screenshots support visual observations about the states shown. Source review, browser testing, and backend verification are different forms of evidence. Browser access and script execution depend on the AI tool hosting the skill.

### What's included

- [`skills/review-frontend-production/`](skills/review-frontend-production/): instructions, review guides, Python helpers, regression tests, and a fictional source-only example.
- [`downloads/review-frontend-production.zip`](downloads/review-frontend-production.zip): the same skill, packaged for download with `SKILL.md` at the root.

Version: **0.4.0-beta**. See the [changelog](skills/review-frontend-production/CHANGELOG.md) for improvements and the [validation record](skills/review-frontend-production/VALIDATION.md) for checks actually performed. Passing the helper tests does not certify any reviewed product as ready to launch.

This repository contains the skill and fictional examples. It does not include client projects or customer data.

## License status

This is a public beta. An open-source license has not been selected. Download availability does not itself grant commercial-use, modification, or redistribution rights. See the [license notice](skills/review-frontend-production/LICENSE-NOTICE.md).
