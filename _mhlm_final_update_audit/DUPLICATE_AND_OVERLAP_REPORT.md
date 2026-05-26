# Duplicate And Overlap Report

Date: 2026-05-26

## Method

The package SHA-256 hashes were compared against the existing repository file hash inventory generated before import. No exact hash match was observed for the six package inputs.

Package hashes:

| File | SHA-256 |
| --- | --- |
| `MHLM_Ultra_Master_Library.pdf` | `6eb4386892a82190b052da3ff8f4c4e856650df76339ccd2ddbc804b7b8dae89` |
| `MHLM_Board_Review_Claude (1).pdf` | `5ccc9fae7c1dd13c8423092aaf4e940884047b722dd26d55b475846351114b86` |
| `kimirrr.pdf` | `f322759583d9c173d0f5e42bb6632407097df7d231e126b45b09897b47b40fe6` |
| `deepseek25may` | `030e08ed37ad3d367868161db5f90073d2e9f5930023d5b7f8dc664a78184dab` |
| `gemini` | `0099999c4f3793ed97f3a77832e805a60be08df6c1ff25c0a51a5ef4dd79f179` |
| `mhlm_review.html` | `3087ea3aba8006300bcc680720d48ac980b2452b3160a83fcc9d31bf6d9bc534` |

## Exact Duplicates

No exact duplicate of the final package files was found in the current MHLM/MDLH repository before import.

## Semantic Overlap

Semantic overlap exists with older material:

- `MDLH-v1.0/` and `logs/model-tracks/` contain prior model-response rounds.
- `epistemic-analysis/legacy/` contains older legacy duplicate reports and mixed-root summaries.
- `reproducibility/zenodo-archives/` contains earlier MHLM/LSC archive packages.
- `case_studies/aoia_runtime_forensics/` contains AOIA case-study reports that should remain case material only.

This overlap is historical, not a reason to overwrite existing files.

## Master Library Duplicate Context

The new Master Library reports:

- 874 canonical extraction manifest rows,
- 6929 duplicate rows in the prior duplicate index,
- 2309 text-like files indexed in the extraction tree.

This means the final import should avoid recursive extraction of the Master Library back into the repository. The PDF and reports should be preserved as freeze artifacts, with hashes and manifest records, not exploded into thousands of files.

## Decision

Import the six package inputs once, under separated archive and model-response evidence paths. Do not re-expand the external extraction tree. Do not import legacy mixed-root files directly.
