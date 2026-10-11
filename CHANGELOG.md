# Changelog

## 0.2.0 - 2026-10-11 (research draft; not yet published)

- Added a preliminary prior-art comparison and made the candidate LNASF Component Contract explicit.
- Distinguished the proposed component-boundary contract from established work on online runtime learning, self-adaptive software, ML-enabled components, and adaptive feedback loops.
- Added the close architectural prior art FORMS and Rainbow, plus DOI/official links for the related-work set.
- Added a candidate evaluation plan with baseline comparisons, admission-gate ablations, safety/fallback checks, and adaptation-cost measurements.
- Added `LNASF-v0.2-draft.tex` as an unpublished working source. It has not yet been compiled or checked as a publication PDF.
- Added a publication-readiness gate to the release workflow.
- Preserved the original Version 0.1 TeX/PDF as historical snapshots. No new GitHub Release or Zenodo archive is claimed by this draft.
- The SHA-256 manifest is marked stale and must be regenerated from actual repository files before publication.

## 0.1.0 - 2026-08-28

Initial technical concept and architecture specification.

- Defined Learning-Native Adaptive Software Component (LNASC).
- Defined the Observe -> Learn -> Predict -> Decide -> Adapt -> Measure -> Learn loop.
- Defined native-learning and scratch-learning principles.
- Separated prediction, decision, confidence, utility, safety constraints, and adaptation.
- Defined deterministic fallback behavior.
- Defined parameter, strategy, and structural adaptation levels.
- Defined passive, advisory, adaptive, and autonomous operating modes.
- Defined local, shared, and hybrid learning scopes.
- Mapped potential frontend, backend, runtime, and infrastructure applications.
- Documented relevant prior art and references.
