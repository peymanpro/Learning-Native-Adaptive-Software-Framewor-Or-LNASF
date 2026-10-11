# Learning-Native Adaptive Software Framework (LNASF)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22142517.svg)](https://doi.org/10.5281/zenodo.22142517)

**Historical Technical Specification - Version 0.1**  
**Research status:** Candidate Component Contract and novelty are under validation; not included in the archived Version 0.1 PDF.

**Author:** Peyman Salimi  
**Date:** 2026-08-28  
**Status:** Technical disclosure / concept specification

## About

LNASF is a proposed architectural framework for building reusable software components that can observe runtime behavior, learn from experience, make constrained predictions and decisions, and adapt selected aspects of their behavior while retaining a deterministic fallback.

The central loop is:

`Observe -> Learn -> Predict -> Decide -> Adapt -> Measure -> Learn`

The framework is intended to be applicable to libraries, frameworks, runtimes, developer tools, frontend systems, backend systems, and infrastructure.

## Important Positioning

LNASF does **not** claim to invent machine learning, self-adaptive software, online learning, runtime adaptation, MAPE-K, predictive prefetching, or learning-enabled components. Those areas have substantial prior art.

The document records a specific proposed architectural formulation centered on:

- learning as an explicit reusable software-component capability;
- native learning within the host ecosystem;
- scratch implementations of learning mechanisms for reference implementations;
- explicit separation of prediction and decision;
- confidence and utility-aware adaptation;
- deterministic fallbacks;
- constrained runtime adaptation;
- applicability across multiple software layers and programming languages.

## Candidate Research Contribution (Under Validation)

The candidate contribution is the **LNASF Component Contract**: a proposed, testable component-boundary specification that makes observation, model updates, prediction/evidence, adaptation admission, allowed actions, deterministic fallback, and outcome evaluation explicit.

For a component `C`, the proposed contract is:

$
\operatorname{LCC}(C) = (B,O,M,P,G,A,F,E)
$

Here `G` is an explicit adaptation-admission gate separated from prediction; the other terms specify the baseline, observations, update procedure, prediction evidence, permitted actions, fallback, and evaluation/feedback.

The intended distinction is not a claim to invent online learning or self-adaptive software. Closely related prior art includes REX, ML-DEECo, component-based ML abstractions, and adaptive feedback-loop architectures. Whether the proposed contract adds a defensible distinction remains to be established by full-text comparison and controlled evaluation.

- [Research positioning and preliminary prior-art comparison](RESEARCH-POSITIONING.md)
- [Editable specification and proposed contract](SPECIFICATION.md#241-candidate-contribution-the-lnasf-component-contract)

## Reference Implementation

The [LNASF Adaptive Admin Console](https://github.com/peymanpro/LNASF-Adaptive-Admin-Console) is an application-level reference implementation of a **limited subset** of these principles. It uses a native TypeScript transition-frequency model, an explicit decision policy, constrained predictive route preloading, a deterministic fallback, and runtime counters.

This implementation is an engineering demonstration—not a claim that the full LNASF framework is complete or that adaptive preloading has already produced a measured performance gain. Its README documents the architecture, tests, evaluation protocol, and current limitations.

## Real-Time Communication Examples

The [LNASF real-time communication examples](REALTIME-COMMUNICATION-EXAMPLES.md) document five limited integrations across Express, NestJS, ASP.NET Core, Next.js and React. They make host-native learning, explicit prediction/decision separation, bounded adaptation, deterministic fallback, and runtime measurement executable. The document links the relevant code/test areas through each repository's README and records verified CI evidence. It distinguishes synthetic unit-level checks from real-world performance claims; these are selected reference examples, not complete LNASF implementations.

## Frontend State and Interaction Examples

The [LNASF frontend state and interaction examples](FRONTEND-STATE-AND-INTERACTION-EXAMPLES.md) document two limited research demonstrations: the [React useState hook](https://github.com/peymanpro/LNASF-Adaptive-React-useState-Hook) explores online state-transition learning with explicit adaptation and safety gates; the [Next.js dnd-kit playground](https://github.com/peymanpro/LNASF-Adaptive-Next-dnd-kit-Playground) learns from interaction-event sequences and presents user-controlled workflow suggestions. They demonstrate selected principles at different frontend boundaries, not the complete LNASF framework.

## Release and Archival Status

The DOI badge at the top refers to the existing Zenodo concept record and an earlier archival state; it must not be read as evidence that the new research-positioning supplement or proposed Component Contract is already included in the archived PDF.

The existing `LNASF-v0.1.tex` and `LNASF-v0.1-Technical-Specification.pdf` remain the Version 0.1 snapshots. The candidate contribution is currently in the editable Markdown and in `LNASF-v0.2-draft.tex`. The draft TeX has not yet been compiled and checked as a new PDF. **Do not publish a new version until the source, rendered PDF, metadata, references, and checksum manifest are synchronized and verified.**

The repository contains a manual GitHub Release workflow, but its end-to-end publication path has not been verified in this research revision. Do not treat a planned version or a workflow file as a completed release. Zenodo archival status should be confirmed in the account's GitHub integration before asserting that a new version has been archived.

## Files

- `SPECIFICATION.md` - editable specification with LaTeX math.
- `LNASF-v0.1.tex` - historical LaTeX source for the Version 0.1 PDF.
- `LNASF-v0.2-draft.tex` - revised working source with the proposed component contract; not yet compiled into a release PDF.
- `LNASF-v0.1-Technical-Specification.pdf` - rendered publication version.
- `references/` - bibliography source.
- `CITATION.cff` - software citation metadata for the versioned repository release.
- `metadata/SHA256SUMS.txt` - currently a stale-manifest warning; regenerate and verify hashes before any new release.
- `FRONTEND-STATE-AND-INTERACTION-EXAMPLES.md` - limited frontend state and workflow research examples.
- `RESEARCH-POSITIONING.md` - preliminary prior-art comparison, candidate contribution, and evaluation plan.
- `RELEASE-PROCESS.md` - versioned GitHub release and Zenodo archival setup.
- `CHANGELOG.md` - version history.

## Citation

Salimi, Peyman. (2026). *Learning-Native Adaptive Software Framework (LNASF): Technical Concept and Architecture Specification*, Version 0.1.
