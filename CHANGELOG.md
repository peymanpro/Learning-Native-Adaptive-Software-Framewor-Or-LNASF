# Changelog

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
