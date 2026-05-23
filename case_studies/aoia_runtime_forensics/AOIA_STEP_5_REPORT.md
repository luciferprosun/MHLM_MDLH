# AOIA Step 5 Report - Test Constitution

## Objective

Define AOIA testing rules and add deterministic fail-fast tests for the current
isolated AOIA modules.

## Implemented

- `tests/test_aoia_determinism.py`
- `docs/TEST_CONSTITUTION.md`
- `docs/adr/0005-test-constitution-determinism-first.md`

## Test Coverage Added

- same input returns same `select_depth()` output
- threshold checks for `shallow`, `mid`, `deep`
- negative pressure raises `ValueError`
- config loads deterministically
- config is readonly after loading
- correlation id shape is stable

## Not Implemented

- No runtime integration tests.
- No provider tests.
- No network tests.
- No UI tests.
- No dashboard or telemetry tests.

## Validation

Validation command:

```bash
python3 -m unittest tests.test_aoia_determinism
```

