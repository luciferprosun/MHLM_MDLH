# Session Save: apka ver2 reconfiguration

Date: 2026-05-19

## Done

- Reconfigured the runtime for a local-first default brain.
- Set the default model to `aureon/aureon-queen`.
- Kept `/model` as an in-app switcher with presets and alias normalization.
- Made `/model gemini` update state without crashing on missing `google-genai`.
- Added a provider notice so model switching explains required API/runtime deps.
- Updated the README architecture and setup notes.
- Normalized the saved model state to Aureon.

## Verification

- `python3 -m py_compile ...` passed
- `python3 -m unittest discover -s tests -v` passed
- `bash run.sh` started the CLI runtime
- `/model` showed the local presets from the live CLI

## Notes

- Gemini remains optional and still requires `google-genai` plus `GEMINI_API_KEY` to actually generate responses.
- The packaged zip is meant to stay small and excludes runtime state, caches, and logs.
