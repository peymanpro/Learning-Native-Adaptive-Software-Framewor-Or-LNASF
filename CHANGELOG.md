# Changelog

## Unreleased research draft (2026-10-11)

- Added a preliminary prior-art comparison and made the candidate LNASF Component Contract explicit.
- Distinguished the proposed component-boundary contract from established work on online learning, self-adaptive software, ML-enabled components, and adaptive feedback loops.
- Added references with DOI/official links and a draft evaluation plan.
- Added `LNASF-v0.2-draft.tex` as an unpublished working source. It has not yet been compiled or checked as a publication PDF.
- The existing Version 0.1 PDF and TeX are preserved as historical snapshots. No new release or Zenodo archive is claimed by this draft entry.

## 0.1.2 - 2026-10-11

Repository-level documentation and publication automation update. The underlying LNASF technical specification remains Version 0.1.

- Added a focused catalog of frontend state and interaction examples covering the learnable React state hook and the dnd-kit workflow demo.
- Linked the frontend examples document from the main LNASF overview.
- Corrected software citation metadata to use the canonical repository URL and repository release version.
- Added a controlled GitHub Actions release workflow that validates metadata, refreshes SHA-256 checksums, creates an annotated version tag, and publishes a GitHub Release using an account-owned token.
- Documented the Zenodo GitHub integration path for automatically archiving future releases when the repository is enabled in Zenodo.
- Expanded the checksum manifest to cover the versioned publication files.

No algorithms or claims in the Version 0.1 technical specification were changed by this repository release.

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
