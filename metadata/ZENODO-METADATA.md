# Zenodo Metadata and GitHub Archival

This file records the intended descriptive metadata for repository releases. The preferred publication path is Zenodo's GitHub integration, rather than a second, independent upload from GitHub Actions.

## Version 0.2.0 title (research proposal draft)

Learning-Native Adaptive Software Framework (LNASF): Research Positioning and Candidate Component Contract

**Previous archival title:** Learning-Native Adaptive Software Framework (LNASF): Technical Concept and Architecture Specification

## Archival version

- **Version:** 0.2.0 (research proposal draft)
- **Previous specification snapshot:** Version 0.1
- **Release title:** LNASF v0.2.0 — Research Proposal Draft
- **Creator:** Peyman Salimi
- **Canonical repository:** https://github.com/peymanpro/Learning-Native-Adaptive-Software-Framewor-Or-LNASF
- **Concept DOI currently linked from GitHub:** https://doi.org/10.5281/zenodo.22142517

## Description

The repository preserves an earlier Version 0.1 technical concept specification and now includes a preliminary working draft proposing the LNASF Component Contract. The draft distinguishes candidate architectural contribution from established prior art and explicitly leaves novelty validation and empirical evaluation open. It is not yet a new archived publication. Existing frontend and real-time examples demonstrate subsets of the framework and do not establish general performance improvements.

## Keywords

machine learning; artificial intelligence; self-adaptive software; adaptive software; online learning; runtime adaptation; learning-enabled software; learning-native software components; software libraries; software frameworks; runtime intelligence; native learning; adaptive systems; feedback-driven software; frontend adaptation; workflow learning; LNASF

## Metadata and versioning behavior

- The root `CITATION.cff` identifies the author, version, canonical repository URL, keywords, and description for the GitHub release.
- No root `.zenodo.json` is present; do not add one casually, because Zenodo gives `.zenodo.json` precedence over `CITATION.cff` when both exist.
- When this GitHub repository is enabled in Zenodo, future GitHub releases are automatically archived. Zenodo assigns a version-specific DOI for each new archived version while the concept DOI resolves to the latest version.
- The release workflow does not require a Zenodo API token for this integration. It cannot enable the repository inside a private Zenodo account or verify that the account toggle is on.

## Scope

Version 0.2.0 is intended to archive the compiled research proposal and its updated source, references, and metadata. It does not claim peer review, established novelty, or demonstrated performance improvements. Confirm the resulting version-specific DOI in Zenodo after the GitHub Release is published; the existing concept DOI reflects an earlier archival state until Zenodo processes the new release.
