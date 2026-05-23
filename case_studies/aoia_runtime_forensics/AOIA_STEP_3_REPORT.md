# AOIA Step 3 Report - Configuration Layer

## Objective

Create a minimal AOIA configuration layer with immutable, startup-only,
validated config and readonly runtime behavior.

## Implemented

- `adaptive_routing/aoia_config.json`
- `adaptive_routing/config_loader.py`
- `docs/adr/0003-immutable-startup-configuration.md`

## Configuration Contract

Current config:

- version: `1`
- depths: `shallow`, `mid`, `deep`
- pressure thresholds:
  - `shallow_max = 33`
  - `mid_max = 66`
- runtime policy:
  - `load_timing = startup_only`
  - `mutable_at_runtime = false`
  - `network_required = false`

## Not Implemented

- No runtime integration.
- No live reload.
- No provider integration.
- No network checks.
- No UI controls.
- No mutable runtime policy.

## Validation

Validation performed:

- JSON parse check.
- Python compile check.
- `load_config()` sample check.
- readonly behavior check.

