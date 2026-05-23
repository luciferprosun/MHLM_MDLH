# Canonical Language Drift Report

Review date: 2026-05-21

Canonical AOIA routing depth language:

```text
LOCAL
MID
PREMIUM
```

## Summary

Canonical language stable: NO.

Severity: MEDIUM.

The repository still contains legacy terms `shallow`, `deep`, and older DVM
terms such as `surface`. Some occurrences are expected biological research
language, while others affect AOIA config, tests, and older ADRs.

## Runtime-Affecting Files

These files affect implemented AOIA prototype behavior:

- `adaptive_routing/deterministic_router.py`
  - returns `shallow`, `mid`, `deep`
  - recommended replacement: `LOCAL`, `MID`, `PREMIUM`
- `adaptive_routing/config_loader.py`
  - expects `("shallow", "mid", "deep")`
  - recommended replacement: `("LOCAL", "MID", "PREMIUM")`
- `adaptive_routing/aoia_config.json`
  - contains `["shallow", "mid", "deep"]`
  - recommended replacement: `["LOCAL", "MID", "PREMIUM"]`
- `tests/test_aoia_determinism.py`
  - asserts legacy depth names
  - recommended replacement: assert canonical depth names after migration

Impact: runtime prototype only. The main terminal runtime is not wired to AOIA
routing, so this does not currently change user-facing terminal behavior.

## Documentation-Only Files

- `docs/adr/0002-minimal-deterministic-router-skeleton.md`
- `docs/AOIA_STEP_2_REPORT.md`
- `docs/AOIA_STEP_3_REPORT.md`
- `docs/AOIA_STEP_5_REPORT.md`
- `docs/LOGGING_PHILOSOPHY.md`
- `docs/AOIA_FOUNDATION_REVIEW.md`

Recommended handling: mark these as legacy phase reports or update them after a
formal terminology migration.

## Expected Biological Research Terms

- `adaptive_routing/dvm_research.md`

Terms such as `surface`, `deep`, and migration depth are biological context
terms here. They are acceptable if clearly separated from AOIA routing-depth
names.

## Non-AOIA Uses

- `web/styles.css`
  - `--accent-deep` is a CSS color token, not AOIA terminology.
- `tools/build_rhcsa_library.py`
  - `depth` is filesystem tree depth, not AOIA routing.
- `knowledge/raw/rhcsa_raw.txt`
  - PDF content contains command flags such as `--max-depth`.

## Recommended Replacements

- `shallow` -> `LOCAL`
- `mid` -> `MID`
- `deep` -> `PREMIUM`
- `Deep Mode` -> `LOCAL` or `PREMIUM` depending on the old context
- `Surface Mode` -> `PREMIUM` only if the old context meant high-resource mode

Because `deep` previously meant low-resource DVM-inspired mode in some early
documents, replacements must be reviewed manually. Do not run a blind search and
replace.

## Recommended Cleanup Sequence

1. Add a terminology ADR that supersedes `shallow/mid/deep`.
2. Update AOIA config and deterministic router in one small migration step.
3. Update tests in the same step.
4. Mark old phase reports and lowercase ADRs as legacy historical records.
5. Keep biological `surface/deep` language only in DVM research documents.
