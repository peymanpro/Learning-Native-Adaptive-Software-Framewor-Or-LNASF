# Zenodo Metadata and GitHub Archival

This file records the intended descriptive metadata for repository releases. The preferred publication path is Zenodo's GitHub integration, rather than a second, independent upload from GitHub Actions.

## Planned next-revision title (working draft)

Learning-Native Adaptive Software Framework (LNASF): Research Positioning and Candidate Component Contract

**Previous archival title:** Learning-Native Adaptive Software Framework (LNASF): Technical Concept and Architecture Specification

## Existing archival record and next revision

- **Current working source:** preliminary research-positioning draft dated 2026-10-11 (not yet released)
- **Previous specification snapshot:** Version 0.1
- **Planned next version:** not assigned until the source, final PDF, references, and metadata are synchronized and checked
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

No claim is made here that a new release has been published. The current draft is not yet synchronized with a revised, compiled PDF. The old PDF remains a Version 0.1 snapshot; prepare new archival metadata only after the research draft is finalized.
