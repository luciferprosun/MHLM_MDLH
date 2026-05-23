# AOIA Step 2 Report - Minimal Deterministic Router Skeleton

## Objective

Create the first deterministic router skeleton without networking or runtime
integration.

## Implemented

- `adaptive_routing/deterministic_router.py`
- `docs/adr/0002-minimal-deterministic-router-skeleton.md`

## Router Contract

Function:

```python
select_depth(pressure: int) -> str
```

Outputs:

- `shallow`
- `mid`
- `deep`

Thresholds:

- `0..33` -> `shallow`
- `34..66` -> `mid`
- `67+` -> `deep`

## Not Implemented

- No network checks.
- No traffic analysis.
- No provider selection.
- No token policy.
- No integration with `main.py`.
- No UI changes.
- No autonomous behavior.

## Validation

Validation performed:

- Python compile check.
- Sample output check for `0`, `34`, and `67`.

