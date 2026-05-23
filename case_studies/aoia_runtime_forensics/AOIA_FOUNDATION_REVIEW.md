# AOIA Foundation Stabilization Review

Review date: 2026-05-21

Scope:

- `docs/`
- `docs/ADR/`
- `docs/adr/`
- `adaptive_routing/`
- `knowledge/`
- parser chain
- canonical pipeline
- index generation
- context generation
- injection preparation
- validators
- tests
- export structure

## Current Architecture Status

The AOIA foundation is currently a local-first, file-based, deterministic
foundation. The new RHCSA pipeline is static and staged:

```text
PDF -> raw text -> sections -> canonical commands -> keyword index -> context pack -> injected context
```

The pipeline does not call models, does not create embeddings, does not use a
database, and does not modify the main router or runtime.

The existing application still contains older local RHCSA runtime memory code in
`knowledge/rhcsa_engine.py`. That older code is separate from the new static
AOIA pipeline and should be treated as legacy application functionality unless
explicitly migrated later.

## Strengths

- AOIA constraints and non-goals are documented clearly.
- Canonical language exists in `docs/GLOSSARY.md`.
- Deterministic processing is implemented with local files and standard Python.
- Builder scripts use stable ordering, explicit validation, and stdout reports.
- Knowledge artifacts are plain JSON and easy to inspect.
- The parser chain is staged and reversible through intermediate artifacts.
- No vector database, embeddings, semantic ranking, or AI enrichment were added
  to the new pipeline.
- Export reporting exists in `exports/EXPORT_REPORT.md`.

## Weaknesses

- Canonical terminology is not fully aligned: `docs/GLOSSARY.md` locks
  `LOCAL/MID/PREMIUM`, while older `adaptive_routing/aoia_config.json` and
  `deterministic_router.py` still use `shallow/mid/deep`.
- ADRs exist in two locations: `docs/ADR/` and `docs/adr/`.
- `knowledge/rhcsa_engine.py` contains local retrieval and scoring behavior that
  predates the current static AOIA pipeline.
- Generated cache directories such as `__pycache__/` exist in the working tree.
- `scripts/` was referenced in export requirements but does not exist in this
  project.
- `context_pack_builder.py` has a hardcoded default query (`network ports`).
  This is deterministic, but it should remain a tool default, not runtime policy.

## Drift Risks

Architecture drift risk: MEDIUM.

Reasons:

- Legacy RHCSA retrieval/scoring code can be confused with the new AOIA static
  lookup pipeline.
- Dual ADR directories create governance ambiguity.
- Old routing depth names can reintroduce terminology drift.
- Context and injection artifacts are close to prompt-use boundaries, so future
  integration must remain explicit and reviewed.

No evidence was found that the new AOIA pipeline currently performs semantic
retrieval, autonomous behavior, runtime learning, vector search, or AI
middleware work.

## Simplification Opportunities

- Choose one ADR directory and mark the other as legacy or migrate it in a
  dedicated cleanup phase.
- Create a terminology migration plan for `shallow/mid/deep` to
  `LOCAL/MID/PREMIUM`, or explicitly document the old names as legacy.
- Move or label `knowledge/rhcsa_engine.py` as legacy runtime memory so it is
  not mistaken for the static AOIA Knowledge Pack pipeline.
- Add a small `knowledge/README.md` that explains the difference between:
  static AOIA artifacts, legacy RHCSA runtime memory, examples, and validators.
- Add a cleanup target or export-only rule for generated caches.
- Consider replacing the hardcoded default context query with a small static
  JSON query list in a later phase, if more context packs are needed.

## Deterministic Compliance Assessment

Status: PASS WITH WATCH ITEMS.

Observed deterministic guarantees:

- JSON outputs are stable and ordered where required.
- Index keys are sorted alphabetically.
- Command lists in the index are sorted alphabetically.
- Context pack keywords are sorted.
- Duplicate commands are removed by exact command string.
- Builders are local-only and use no network calls.
- Validators fail fast on malformed input.

Watch items:

- `section_parser.py` is deterministic but heuristic. It extracts command-like
  cells from PDF text and can preserve PDF extraction artifacts as command
  candidates.
- Builder scripts write output files when run. That is acceptable for local
  build tools, but they should not be called implicitly by runtime code.
- Existing legacy runtime memory code uses scoring. It should not be described
  as part of the new deterministic AOIA pipeline.

## Boundary Compliance Assessment

Status: PASS.

The reviewed AOIA foundation preserves these boundaries:

- stateless foundation
- local-first file processing
- no embeddings
- no vector database
- no semantic ranking in the new pipeline
- no adaptive scoring in the new pipeline
- no runtime learning
- no autonomous behavior
- no router/runtime modification from the new pipeline

## Maintainability Assessment

Status: MODERATE TO GOOD.

The staged file pipeline is easy to inspect and debug. Each tool has a narrow
responsibility. Documentation is present for each major stage.

Maintainability risk comes mainly from overlap:

- old docs vs new canonical docs
- old ADR location vs new ADR location
- old RHCSA runtime memory vs new static Knowledge Pack pipeline

These are naming and governance issues, not immediate implementation failures.

## Stability Assessment

Foundation stable: YES.

Critical issues detected: NONE.

Non-critical issues detected:

- terminology inconsistency between canonical docs and older router config
- duplicate ADR directory locations
- legacy RHCSA scoring/retrieval code adjacent to static AOIA artifacts
- cache files present in the working tree

## Validation Performed

Commands run:

```text
python3 validator.py knowledge/
python3 -m unittest tests.test_aoia_determinism tests.test_knowledge_validator
python3 -m json.tool knowledge/canonical/rhcsa_commands.json
python3 -m json.tool knowledge/index/command_index.json
python3 -m json.tool knowledge/context/context_pack.json
python3 -m json.tool knowledge/injection/injected_context.json
python3 -m py_compile knowledge/tools/pdf_extract.py knowledge/tools/section_parser.py knowledge/tools/canonical_builder.py knowledge/tools/index_builder.py knowledge/tools/context_pack_builder.py knowledge/tools/context_injector.py knowledge/validator/validator.py adaptive_routing/config_loader.py adaptive_routing/deterministic_router.py
```

Results:

- Knowledge example validator: OK
- AOIA determinism and validator tests: OK, 14 tests
- JSON artifact validation: OK
- Python compile validation: OK

## Final Review Summary

Foundation stable: YES

Architecture drift risk: MEDIUM

Readiness for next phase: YES, with governance cleanup recommended before
runtime integration.

Critical issues detected: NONE

Recommended next step:

Perform a cleanup-only governance phase that resolves ADR directory duplication,
labels legacy RHCSA runtime memory, and aligns routing-depth terminology. Do not
start runtime integration until those naming and boundary issues are explicit.
