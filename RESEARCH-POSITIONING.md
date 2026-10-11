# LNASF Research Positioning and Candidate Contribution

**Status:** Research working document — preliminary prior-art comparison; novelty not yet established  
**Date:** 2026-10-11  
**Author:** Peyman Salimi

## 1. Purpose and claim discipline

This document narrows the research question behind the Learning-Native Adaptive Software Framework (LNASF). It does not claim that LNASF is the first learning-enabled, self-adaptive, feedback-driven, or component-based software architecture. Those ideas have substantial prior art.

The candidate contribution is more limited: **an explicit, reusable component-level contract that makes the learning-to-action boundary inspectable and testable**, with separately stated requirements for observations, model updates, predictions and evidence, adaptation admission, allowed actions, deterministic fallback, and outcome-based evaluation.

This is a research hypothesis and design proposal, not a finding that the combination is historically unprecedented. The comparison below is preliminary, not a systematic review. A publishable novelty claim requires a documented search protocol, full-text comparison with the closest works, and empirical evaluation.

## 2. Candidate contribution: the LNASF Component Contract

For a learning-enabled software component, define the proposed contract

`LCC(C) = (B, O, M, P, G, A, F, E)`

where:

- **B — Baseline:** deterministic behavior that remains available without adaptation.
- **O — Observation interface:** specifies what is observed, when it is observed, and the boundaries of the collected data.
- **M — Model/update procedure:** specifies how observations and outcomes update the learned state.
- **P — Prediction interface:** produces a prediction plus an explicit indication of evidence sufficiency or uncertainty.
- **G — Adaptation-admission gate:** is separate from the predictor and determines whether a proposed action is permitted.
- **A — Action set:** enumerates the adaptations the component is allowed to perform and any resource bounds.
- **F — Fallback/abstention behavior:** returns to the baseline or an advisory-only result whenever admission conditions fail.
- **E — Evaluation and feedback:** measures outcomes and adaptation overhead, then feeds the outcome into subsequent learning where appropriate.

The gate is proposed as an explicit contract obligation rather than an implicit branch inside the learning model. A candidate admission rule is:

`G_t(a) = [q_t \geq \epsilon] \land [S(a,o_t)=\mathrm{true}] \land [\widehat{\Delta U}_t(a)-C_{adapt,t}>\lambda]`

and

`a_t = a_t^{adapt}` if `G_t(a_t^{adapt})` is true; otherwise `a_t = B(o_t)` (or the component returns an advisory result in advisory mode).

Here, `q_t` denotes an application-defined evidence-adequacy measure, `S` a hard safety/resource constraint, `\widehat{\Delta U}` an estimated utility improvement, `C_{adapt}` the cost of adapting, and `\epsilon, \lambda` domain-specific thresholds. These are not universal constants, and confidence scores must not be described as calibrated probabilities unless calibration has been evaluated.

A stronger prior-art constraint must be acknowledged: Rainbow already provides reusable architecture-based self-adaptation infrastructure [11], and FORMS proposes a unifying reference model for formal specification of distributed self-adaptive systems [10]. Therefore, LNASF cannot plausibly claim novelty merely for being a reusable/unifying adaptation architecture. The narrower research question is whether an explicit contract for **learning-enabled component behavior and the admission of learned actions**, together with verifiable conformance tests and outcome-cost evaluation, provides a distinct and useful artifact beyond these frameworks and the closer ML-specific systems.

### What is and is not claimed

**Candidate contribution:** a structured contract and associated conformance/evaluation method for learning-enabled reusable components.

**Not claimed as new by themselves:** online learning; the Monitor/Analyze/Plan/Execute or related feedback-loop families; separating learning from adaptation; component-based self-adaptation; model uncertainty; safety constraints; deterministic fallback; native-language implementation; or measuring latency/cost.

**Still unproven:** that this contract is absent from existing frameworks, that it is meaningfully different from combinations already described in REX, ML-DEECo, component-based ML abstractions, and adaptive-loop architectures, or that adopting it improves outcomes.

## 3. Preliminary comparison with relevant prior work

| Work | Established contribution relevant to LNASF | Consequence for LNASF positioning |
|---|---|---|
| Kephart & Chess (2003) [1] | Autonomic computing and self-managing systems | LNASF cannot claim to originate autonomous management or feedback-based self-management. |
| Wong et al. (2022) [2] | Systematic review of self-adaptive systems across categories and domains | Establishes a broad, mature field; LNASF needs a specific gap rather than a generic call for adaptation. |
| Gheibi, Weyns & Quin (2022) [3] | Systematic review of ML in self-adaptive systems; analyzes ML roles within feedback-loop architectures | Learning in the adaptation loop is existing work, not a novel premise. |
| Porter et al. / REX (2016) [4] | Runtime emergence, online learning, component-based assembly, and continuous runtime optimization | A particularly close comparator for learning-native, runtime-adaptive components. The proposed contract must be compared against its actual mechanisms, not just its abstract description. |
| Töpfer et al. / ML-DEECo (2022) [5] | ML-enabled framework for self-organizing components, supporting model training and prediction in simulations | Component-level learning abstractions already exist. LNASF must identify a concrete contract-level difference. |
| Töpfer et al. (2023) [6] | Machine-learning abstractions integrated into component-based self-optimizing systems, including optimization heuristics | Direct prior art against a broad claim that LNASF first makes learning a component capability. |
| Abdullah et al. (2023) [7] | Estimator abstractions to ease the use of ML in self-adaptive architectures | Directly relevant to reusable abstractions for integrating ML into adaptive architectures. Full-text comparison is required. |
| Zavala et al. / HAFLoop (2020) [8] | Modular, reusable architecture for adapting feedback-loop structure and parameters | LNASF cannot claim generic reusable adaptation loops or configurable adaptation structure as novel. |
| Peffers et al. (2007) [9] | Design Science Research Methodology, including artifact design, demonstration, evaluation, and communication | Provides a suitable methodological pattern for evaluating an architectural artifact; it is not evidence that LNASF's technical concept is novel. |
| Weyns, Malek & Andersson / FORMS (2012) [10] | Unifying reference model and formal vocabulary for distributed self-adaptive systems | Directly weakens a broad claim that LNASF's novelty is simply a unifying architecture or common vocabulary. The candidate contract must be narrower and compared in detail. |
| Garlan et al. / Rainbow (2004) [11] | Reusable infrastructure for architecture-based self-adaptation, with explicit monitoring, constraints, and adaptation strategies | Direct prior art for reusable architecture-based adaptation infrastructure and explicit adaptation policies. LNASF's candidate difference must be tied to learned-component contracts and conformance/evaluation obligations, not reusability alone. |

This table is intentionally conservative. It maps high-level overlap based on bibliographic records and available abstracts. It does **not** yet prove detailed equivalence or difference. Before a journal submission, the closest full texts—especially REX, ML-DEECo, the 2023 component abstractions, and Introducing Estimators—must be compared feature by feature.

## 4. Candidate research questions

- **RQ1 — Contract completeness:** Can the LNASF Component Contract be mapped to concrete interfaces, state, policies, and testable requirements in each reference implementation?
- **RQ2 — Gate transparency:** Does making the adaptation-admission gate explicit make it easier to test when a learned prediction is allowed to change software behavior?
- **RQ3 — Safe abstention:** Under cold start, sparse evidence, noisy observations, model drift, or violated constraints, does the component reliably select its baseline or advisory behavior?
- **RQ4 — Net benefit:** Does the complete design improve a declared outcome over a deterministic baseline after learning, adaptation, and measurement overhead are included?
- **RQ5 — Cross-context utility:** Can the same contract be implemented in multiple programming-language/runtime ecosystems without making the learning algorithm identical across those ecosystems?

These questions may be answered negatively. A negative result is useful: it may show that the contract needs refinement or that only a smaller subset adds practical value.

## 5. Minimum evaluation plan

Compare at least these configurations under the same event traces or workload generator:

1. **B0 — Deterministic baseline:** no learned adaptation.
2. **B1 — Prediction-only:** learn and report predictions, but do not adapt.
3. **B2 — Prediction with a gate:** only permit actions after evidence/uncertainty checks.
4. **B3 — Full candidate contract:** gated actions, hard constraints, deterministic fallback, outcome measurement, and feedback.

Include stable, changing, sparse/cold-start, noisy, and high-adaptation-cost conditions. Where possible, use repeated runs and report variability, not just a single mean. Separate synthetic trace-replay results from live application measurements.

Minimum metrics: task-specific utility or quality; latency/throughput where relevant; prediction quality and calibration where probabilistic claims are made; false-adaptation rate; constraint violations; fallback/abstention rate; time to useful adaptation; memory/resource cost; and total adaptation overhead.

Ablations should remove one contract obligation at a time (for example, no gate, no cost term, no deterministic fallback, or no outcome feedback). The paper should report the tests and negative cases, not only successful demonstrations.

## 6. Threats to validity and open work

- The current comparison is preliminary and may omit relevant papers or implementations.
- The contract components may overlap with abstractions already present in prior frameworks.
- A tuple or diagram alone is not a scientific contribution; its semantics, conformance rules, and evaluation must be operational.
- An evidence threshold is not automatically calibrated confidence.
- Synthetic traces do not demonstrate improved real-world application performance.
- Several repository examples currently demonstrate subsets of LNASF; they do not implement the complete framework.
- Cross-language applicability is a design goal until demonstrated by comparable implementations.
- The present document does not claim a patentable invention or provide legal advice.

## 7. Recommended defensible wording for a paper

> We propose the LNASF Component Contract as a candidate architectural specification for learning-enabled software components. The contract makes the observation, update, prediction, adaptation-admission, allowed-action, fallback, and outcome-evaluation responsibilities explicit at the component boundary. Its novelty is investigated relative to prior work on online runtime learning, ML-enabled component models, self-adaptive architectures, and adaptive feedback loops. The proposed contribution is therefore the contract's precise formulation and empirical evaluation—not the invention of its individual building blocks. The comparison must particularly establish what remains different from FORMS and Rainbow as well as the ML-specific frameworks.

Use the phrase “we are the first” only if a systematic prior-art search provides strong support. Until then, use “we propose,” “we formalize,” and “we evaluate,” and make the comparison itself a visible part of the paper.

## References

See [references/REFERENCES.md](references/REFERENCES.md) and [references/references.bib](references/references.bib) for the complete bibliographic records and DOIs.
