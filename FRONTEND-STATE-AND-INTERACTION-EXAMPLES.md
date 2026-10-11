# LNASF Frontend State and Interaction Examples

**Status:** Exploratory reference examples of selected LNASF principles  
**Reviewed:** 2026-10-11

This document records two intentionally limited frontend examples of the Learning-Native Adaptive Software Framework (LNASF). They explore different adaptation boundaries: learning from application-state transitions in a reusable React hook, and learning from interaction-event sequences in a drag-and-drop workflow demo. Neither is a complete implementation of the framework.

## Shared design principles

The examples are evaluated against the selected parts of the LNASF loop:

Observe → Learn → Predict → Decide → Adapt → Measure

The important separation is between learning a pattern, predicting what may happen next, and deciding whether any action is permitted. Deterministic application behavior remains available when evidence is weak or policy constraints reject adaptation.

## Implementation matrix

| Repository | Host runtime and role | Observation and model | Decision and bounded adaptation | Fallback and limitations |
| --- | --- | --- | --- | --- |
| [LNASF-Adaptive-React-useState-Hook](https://github.com/peymanpro/LNASF-Adaptive-React-useState-Hook) | TypeScript library integrating a learnable state engine with React | Observes committed state transitions and maintains online transition-frequency counts. Prediction uses observed destination frequencies; a Wilson-based confidence calculation and prediction margin are exposed to the policy. | Adaptation is attempted only when the application explicitly calls `learning.advance()`. Confidence, optional margin, and application-defined safety constraints gate the decision. | Normal `setState` updates remain deterministic. A rejected prediction falls back to the current state. The model is local to the running instance; synthetic workload experiments do not establish general performance or accuracy guarantees. |
| [LNASF-Adaptive-Next-dnd-kit-Playground](https://github.com/peymanpro/LNASF-Adaptive-Next-dnd-kit-Playground) | Next.js, React, TypeScript and dnd-kit interactive list/Kanban demo | Observes successful list reorders, task reorders and cross-column moves. It learns adjacent event-category transitions in a bounded window of at most 100 observations. Task text and other task content are not model features. | The UI may display an advisory next-step suggestion only when the leading transition has at least three samples and at least 65% empirical confidence. It does not automatically reorder or move items. | Learning exists only in page-session memory and can be cleared. Suggestions are descriptive heuristics; the project has no demonstrated productivity gain, validated predictive performance, or dedicated automated unit-test coverage for the transition model. |

## Evidence and evaluation boundaries

### React state hook

The repository contains a Vitest test suite and repeatable scripts for benchmarks and synthetic experiments covering transition learning, confidence, policy thresholds, prediction margin, probability quality and reliability. The README reports results on synthetic traces only and explicitly notes that the benefit of prediction margin has not been established. These experiments should not be interpreted as proof of superiority over ordinary React `useState` in production applications.

### dnd-kit workflow demo

The implementation exposes observation and transition counts, empirical support and confidence, and a user-controlled recommendation display. A GitHub Actions quality workflow is configured for type checking, linting, production build and dependency audit. This document does not claim that a successful run has been verified. Dedicated tests of the workflow model and a controlled evaluation of recommendation quality remain follow-up work.

## Scope and limitations

- These are examples of selected LNASF principles, not complete implementations of every framework mode or capability.
- Neither example includes distributed or cross-session model sharing.
- The workflow demo is advisory; it does not autonomously change the user's board or list.
- No real-world productivity, latency or performance improvement is claimed without an appropriate baseline, reproducible workload and reported measurements.
- Model confidence and empirical frequency are policy inputs, not guarantees that a future prediction will be correct.

For the broader architectural concept, see the [Learning-Native Adaptive Software Framework (LNASF) specification repository](https://github.com/peymanpro/Learning-Native-Adaptive-Software-Framewor-Or-LNASF).
