# Import Decision Table

Date: 2026-05-26

## Decisions

| Source | Decision | Destination | Notes |
| --- | --- | --- | --- |
| `/home/l/Desktop/master libaryyyyy/last raport 4 mhlm /MHLM_Ultra_Master_Library.pdf` | IMPORT_TO_CANONICAL | `archive/final_master_library/2026-05-25_MHLM_Ultra_Master_Library/source/MHLM_Ultra_Master_Library.pdf` | Preserve as final Master Library archive artifact with SHA-256 manifest. |
| `/home/l/Desktop/master libaryyyyy/last raport 4 mhlm /MHLM_Board_Review_Claude (1).pdf` | IMPORT_TO_ARCHIVE | `model-responses/final_audit_round_2026-05-25/claude/MHLM_Board_Review_Claude_2026-05-26.pdf` | Model critique evidence only. |
| `/home/l/Desktop/master libaryyyyy/last raport 4 mhlm /kimirrr.pdf` | IMPORT_TO_ARCHIVE | `model-responses/final_audit_round_2026-05-25/kimi/Kimi_MHLM_MDLH_Review_2026-05-26.pdf` | Model critique evidence only. |
| `/home/l/Desktop/master libaryyyyy/last raport 4 mhlm /deepseek25may` | IMPORT_TO_ARCHIVE | `model-responses/final_audit_round_2026-05-25/deepseek/DeepSeek_Forensic_Architecture_Grant_Readiness_Review_2026-05-26.md` | Store as text evidence; source file has no extension. |
| `/home/l/Desktop/master libaryyyyy/last raport 4 mhlm /gemini` | IMPORT_TO_ARCHIVE | `model-responses/final_audit_round_2026-05-25/gemini/Gemini_Critical_Infrastructure_Review_2026-05-26.md` | Store as text evidence; source file has no extension. |
| `/home/l/Desktop/master libaryyyyy/last raport 4 mhlm /mhlm_review.html` | IMPORT_TO_APPENDIX | `model-responses/final_audit_round_2026-05-25/kimi/mhlm_review.html` | Preserve source/rendering context for Kimi-style Polish review. |
| `/home/l/Desktop/Legacy-Mixed-Root-Archive` | LEGACY_REFERENCE_ONLY | none | Reviewed for lineage; no direct import. |
| `/home/l/github-audit/LLM-MHLM-Main-Project` | LEGACY_REFERENCE_ONLY | none | Reviewed for lineage; no direct import. |

## Explicit Non-Imports

| Source class | Decision | Reason |
| --- | --- | --- |
| LSC theory material | EXCLUDE from current update | LSC is read-only case-study material in this repository. |
| AOIA runtime source | EXCLUDE from current update | AOIA-Core remains separate and read-only. |
| Legacy mixed root scripts/tooling | LEGACY_REFERENCE_ONLY | Would reintroduce mixed-authority material. |
| Expanded extraction tree `/home/l/Desktop/MHLM_Ultra_Master_25maj` | DUPLICATE_SKIP | Master Library already indexes the tree; re-expansion would create recursive duplicate growth. |

## Human Review Flags

No package file is blocked from archival import. Promotion of any model report from evidence to canonical methodology is explicitly blocked unless a future human review creates a separate methodological document with source citations and clear non-validation language.
