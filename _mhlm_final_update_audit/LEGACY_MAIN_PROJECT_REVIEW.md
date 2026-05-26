# Legacy Main Project Review

Date: 2026-05-26

## Reviewed Legacy Sources

Two local legacy sources were identified:

- `/home/l/Desktop/Legacy-Mixed-Root-Archive`
- `/home/l/github-audit/LLM-MHLM-Main-Project`

Both were treated as read-only historical reference sources.

## Legacy-Mixed-Root-Archive

This archive contains:

- mixed root README snapshots,
- migration command scripts,
- continuity bridge material,
- operator-review material from `research_workspace`,
- public tooling unrelated to the MHLM final freeze target.

Observed relevant files include:

- `mixed_roots/LLM_MHLM_Main_Project_README.md`
- `mixed_roots/LLM_MHLM_migration_commands.sh`
- `DEPRECATED_MIXED_ZONES.md`
- `README.md`

Decision: LEGACY_REFERENCE_ONLY. The Master Library already incorporates the legacy mixed-root lineage as extracted evidence. Re-importing this tree would recreate mixed-authority ambiguity.

## LLM-MHLM-Main-Project

The old mixed root contains:

- LSC material,
- MHLM material,
- shared tooling,
- migration and duplicate-resolution documents,
- older archive packages.

Observed relevant files include:

- `MHLM/README.md`
- `MHLM/MDLH-v1.0/README.md`
- `docs/DUPLICATE_RESOLUTION.md`
- `docs/MIGRATION_PLAN.md`
- `LEGACY_MIXED_ROOT_ARCHIVED.md`
- `LEGACY_ARCHIVE_STATUS.md`

Decision: LEGACY_REFERENCE_ONLY. The repository is not reactivated and no direct import is recommended during this final update.

## Rationale

The old mixed root is historically important but authority-unsafe. It contains valid lineage evidence alongside LSC, tooling, and migration material. The current update package already records the legacy lineage inside the Master Library and final review reports. Importing additional legacy files now would increase duplication and weaken the freeze boundary.

## Exceptions

No unique, clearly MHLM/MDLH-only legacy file was identified that must be imported now. If a human operator later identifies a missing legacy artifact, it should be imported only under an archive/legacy/provenance label, never as current canonical methodology.
