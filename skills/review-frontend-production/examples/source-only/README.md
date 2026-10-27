# Fictional notes: a complete source-only review example

This is a teaching fixture, not a real business project or an accepted product.

Input: `project/index.html`. Scope: one page and three logical instances (form, input, clear button). Outputs: `audit.json`, `coverage.md`, `review.md`. Every instance has a blueprint, decision, and regression design; browser checks remain blocked.

From the skill root:

```sh
python3 -B examples/source-only/verify_fixture.py
python3 -B scripts/audit_ledger.py check examples/source-only/audit.json --require-plan
python3 -B scripts/audit_ledger.py check examples/source-only/audit.json --require-complete
```

Expected exit codes: `0`, `0`, `2`. The static script checks label association, explicit button type, and a nonempty accessible name. It cannot establish click, keyboard, layout, or security behavior. `evidence.txt` records actual static output.

The proposed repair is deliberately not implemented: the clear control lacks a handler. This demonstrates a confirmed source defect with unverified browser impact. The example's historical `fixture-v1` observations remain distinct from the `fixture-v2-en` baseline of the English fixture; timestamps are not invented.
