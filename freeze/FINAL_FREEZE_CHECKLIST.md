# Final Freeze Checklist

Date: 2026-05-26

## Completed

- [x] Verified target repository path.
- [x] Verified Git remote for `MHLM_MDLH`.
- [x] Confirmed clean working tree before update.
- [x] Created Phase 1 audit reports.
- [x] Classified package candidates by authority domain and import decision.
- [x] Preserved final Master Library PDF under archive.
- [x] Preserved final model reports under model-response evidence.
- [x] Added SHA-256 manifests.
- [x] Added provenance policy.
- [x] Added cross-model consensus warning.
- [x] Added freeze boundaries and post-freeze policy.

## Human Review Before Commit

- [ ] Confirm binary PDFs should remain tracked in Git.
- [ ] Review `_mhlm_final_update_audit/IMPORT_DECISION_TABLE.md`.
- [ ] Confirm no LSC/AOIA authority leakage is introduced by the final package.
- [ ] Confirm model-response evidence language is acceptable.
- [ ] Run final `git status` and inspect staged/unstaged changes before commit.

## Human Review Before Any Public Archive

- [ ] Verify no private material exists in imported package files.
- [ ] Verify citation metadata if a Zenodo package is later created.
- [ ] Recompute SHA-256 manifest after any packaging step.
- [ ] Preserve current authority-separation policy in any external archive description.
