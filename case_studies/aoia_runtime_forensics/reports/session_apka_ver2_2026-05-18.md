# Session Save: apka ver2

Date: 2026-05-18

## What changed

- Switched the runtime default provider from Gemini to Aureon.
- Added `providers/aureon_provider.py` as the default provider wrapper.
- Kept Gemini as a fallback only when needed.
- Added Obsidian vault memory under `obsidian_vault/`.
- Mirrored runtime memory and session notes into the vault.
- Added `/vault` local command and local router handling for vault queries.
- Updated the system prompt to prefer local-first execution.
- Made browser imports optional so the runtime can still load without Playwright.
- Added tests for Aureon defaulting and vault creation.

## Verification

- `python3 -m py_compile ...` passed
- `python3 -m unittest discover -s tests -v` passed
- Browser tests were skipped because Playwright is not installed in the current system Python

## Notes

- Existing Gemini support remains available as a fallback provider.
- The current brain default for a fresh run is `aureon/aureon-queen`.
