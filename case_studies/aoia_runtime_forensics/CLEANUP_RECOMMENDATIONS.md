# Cleanup Recommendations

Review date: 2026-05-21

This document identifies cleanup opportunities only. No files were deleted
during this phase.

## Safe Deletions

Safe to delete after user approval:

- project-level `__pycache__/` directories
- `*.pyc` files
- `.pytest_cache/` if it appears later
- temporary zip staging directories outside the project

Current scan found:

- `__pycache__/` directories: 192
- `*.pyc` files: 1742

Most cache files are inside `.venv/`, which should normally be excluded from
exports rather than manually cleaned.

## Do Not Delete Automatically

- `checkpoints/`
- `exports/`
- `knowledge/raw/`
- `knowledge/parsed/`
- `knowledge/canonical/`
- `knowledge/index/`
- `knowledge/context/`
- `knowledge/injection/`
- `state/`
- `memory/`
- `obsidian_vault/`

These may contain restore points, generated canonical artifacts, or local
runtime/project history.

## Gitignore Recommendations

No `.gitignore` was found at repository root.

Recommended entries:

```text
.venv/
__pycache__/
*.pyc
.pytest_cache/
node_modules/
logs/
screenshots/
state/browser_profile/
exports/*.zip
checkpoints/*.tar.gz
```

Do not ignore canonical generated knowledge artifacts unless a later decision
marks them as rebuild-only. For now, keep these trackable:

```text
knowledge/raw/rhcsa_raw.txt
knowledge/parsed/rhcsa_sections.json
knowledge/canonical/rhcsa_commands.json
knowledge/index/command_index.json
knowledge/context/context_pack.json
knowledge/injection/injected_context.json
```

## Reproducibility Considerations

- The RHCSA pipeline is reproducible only if the source PDF and local extractor
  tools remain available.
- `pdftotext` output can vary across tool versions, so retaining
  `knowledge/raw/rhcsa_raw.txt` is useful.
- Keeping intermediate JSON artifacts makes later diffs and audits easier.
- Cache removal does not affect reproducibility.

## Export Recommendations

Canonical exports should continue to exclude:

- `.venv/`
- `__pycache__/`
- `*.pyc`
- `.pytest_cache/`
- `node_modules/`
- `.git/`
- browser profile caches
- runtime logs
- recursive checkpoint archives

Full archival backups may include more local state, but they should be clearly
labeled as private machine backups, not collaborator packages.
