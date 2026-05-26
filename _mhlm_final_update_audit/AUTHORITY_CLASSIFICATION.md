# Authority Classification

Date: 2026-05-26

## Authority Domains

| Domain | Meaning in this repository |
| --- | --- |
| MHLM_MDLH_CANONICAL | Current MHLM/MDLH methodology, freeze orientation, and canonical archive index material. |
| MODEL_RESPONSE_EVIDENCE | Model outputs, critiques, reviews, and audit responses preserved as evidence of process, not truth. |
| PROVENANCE | Source paths, hashes, migration lineage, archive context, and custody records. |
| PROMPT_ARCHIVE | Prompts and prompt-derived records retained for lineage reconstruction. |
| RECURSIVE_CONSENSUS | Evidence about model convergence and recursive agreement. This is risk evidence, not validation. |
| CONTAMINATION_ANALYSIS | Material describing authority drift, hallucination lineage, provenance contamination, or mixed-source risk. |
| FREEZE_REPORT | Freeze scope, freeze checklist, post-freeze policy, and final archive boundaries. |
| LSC_CASE_STUDY_REFERENCE | LSC material referenced only as an unvalidated case study. |
| AOIA_REFERENCE_ONLY | AOIA material referenced only as runtime/provenance architecture case material. |
| LEGACY_MIXED_ROOT | Old mixed root material preserved for lineage only. |
| MIXED_UNCLEAR | Material whose authority or origin remains unclear and needs human review. |

## Authority Types

| Type | Use |
| --- | --- |
| canonical_methodology | Stable MHLM/MDLH methodology and repository policy. |
| evidence_archive | Preserved source artifacts with hash/provenance records. |
| model_response | AI/model outputs and reviews. |
| forensic_audit | Structured critique or audit reports. |
| provenance_record | Hashes, source paths, custody, and import records. |
| duplicate_index | Duplicate and overlap reports. |
| freeze_report | Freeze preparation and freeze boundary files. |
| legacy_lineage | Historical records from old mixed roots. |
| case_study_reference | LSC/AOIA references used as study material only. |
| appendix_material | Supporting material that is not canonical methodology. |
| mixed_unclear | Needs explicit human review before promotion. |

## Candidate Classification Summary

| Candidate | Classification | Authority domain | Authority type | Reason |
| --- | --- | --- | --- | --- |
| `MHLM_Ultra_Master_Library.pdf` | IMPORT_TO_CANONICAL | MHLM_MDLH_CANONICAL, PROVENANCE, FREEZE_REPORT | evidence_archive, provenance_record | Final archive consolidation and freeze input; not a new theory release. |
| `MHLM_Board_Review_Claude (1).pdf` | IMPORT_TO_ARCHIVE | MODEL_RESPONSE_EVIDENCE, CONTAMINATION_ANALYSIS | model_response, forensic_audit | Review evidence from Claude; useful critique, not validation. |
| `kimirrr.pdf` | IMPORT_TO_ARCHIVE | MODEL_RESPONSE_EVIDENCE, CONTAMINATION_ANALYSIS | model_response, forensic_audit | Review evidence from Kimi; useful critique, not validation. |
| `deepseek25may` | IMPORT_TO_ARCHIVE | MODEL_RESPONSE_EVIDENCE, CONTAMINATION_ANALYSIS | model_response, forensic_audit | DeepSeek forensic and grant-readiness critique. |
| `gemini` | IMPORT_TO_ARCHIVE | MODEL_RESPONSE_EVIDENCE, CONTAMINATION_ANALYSIS | model_response, forensic_audit | Gemini infrastructure critique. |
| `mhlm_review.html` | IMPORT_TO_ARCHIVE | MODEL_RESPONSE_EVIDENCE, CONTAMINATION_ANALYSIS | model_response, forensic_audit, appendix_material | Source HTML for Polish review; paired with rendered PDF. |
| `/home/l/Desktop/Legacy-Mixed-Root-Archive` | LEGACY_REFERENCE_ONLY | LEGACY_MIXED_ROOT | legacy_lineage | Mixed authority source; do not reactivate. |
| `/home/l/github-audit/LLM-MHLM-Main-Project` | LEGACY_REFERENCE_ONLY | LEGACY_MIXED_ROOT | legacy_lineage | Old mixed root; do not re-import blindly. |
| `LSC-Research` | LEGACY_REFERENCE_ONLY | LSC_CASE_STUDY_REFERENCE | case_study_reference | Read-only reference; not modified. |
| `AOIA-Core` | LEGACY_REFERENCE_ONLY | AOIA_REFERENCE_ONLY | case_study_reference | Read-only reference; not modified. |
