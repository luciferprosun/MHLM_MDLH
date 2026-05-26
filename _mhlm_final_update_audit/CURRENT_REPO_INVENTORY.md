# Current Repo Inventory

Date: 2026-05-26
Target path: `/home/l/Desktop/MHLM_MDLH`
Remote: `https://github.com/luciferprosun/MHLM_MDLH.git`
Branch/status at intake: `main...origin/main`, clean working tree before this audit.

## Phase 0 Finding

The shell session started in `/home/l`, which is not the MHLM/MDLH repository. The correct local target was identified as `/home/l/Desktop/MHLM_MDLH` because:

- it is a Git repository,
- its remote is `luciferprosun/MHLM_MDLH`,
- its root documents describe MHLM/MDLH scope and authority boundaries,
- sibling repositories `LSC-Research` and `AOIA-Core` exist separately and were not modified.

## Root Files

Observed root-level files before update:

- `.gitignore`
- `AUTHORITY_SCOPE.md`
- `LICENSE`
- `README.md`
- `ROADMAP.md`

Observed root-level directories before update:

- `MDLH-v1.0/`
- `ai-workflows/`
- `archive/`
- `case_studies/`
- `convergence-analysis/`
- `docs/`
- `epistemic-analysis/`
- `evaluation/`
- `figures/`
- `logs/`
- `papers/`
- `prompts/`
- `reproducibility/`

## Existing Authority Signals

`README.md` defines this track as research on:

- model-output provenance,
- hypothesis-vs-validation separation,
- reproducibility of AI-assisted workflows,
- epistemic amplification and disagreement analysis.

`AUTHORITY_SCOPE.md` allows:

- LSC case-study references,
- prompt archives,
- model comparison reports,
- convergence and drift analysis,
- forensic timelines,
- AOIA stabilization and audit reports as case material.

It forbids presenting LSC as canonical physics inside MHLM/MDLH and forbids treating AOIA runtime source as MHLM's primary authority.

## Existing Archive/Lineage Material

The repository already contains:

- legacy MHLM/MDLH material under `MDLH-v1.0/`,
- model-track logs under `logs/model-tracks/`,
- legacy duplicate reports under `epistemic-analysis/legacy/`,
- AOIA case-study forensics under `case_studies/aoia_runtime_forensics/`,
- earlier reproducibility/Zenodo artifacts under `reproducibility/zenodo-archives/`.

## Current Update Constraint

This update should be additive and authority-separated. No LSC theory files, AOIA runtime files, Zenodo uploads, GitHub releases, or active runtime application code should be changed by this final freeze preparation.
