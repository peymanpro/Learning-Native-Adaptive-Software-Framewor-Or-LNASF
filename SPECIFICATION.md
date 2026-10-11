# Learning-Native Adaptive Software Framework (LNASF)

**Author:** Peyman Salimi  
**Email:** salimipeyman@gmail.com  
**Version:** 0.1  
**Date:** 2026-08-28  
**Status:** Technical Concept and Architecture Specification


> **Research-positioning supplement — working draft (2026-10-11).** The prior-art analysis and candidate component contract below are provisional research additions to the editable Markdown. The existing `LNASF-v0.1-Technical-Specification.pdf` and `LNASF-v0.1.tex` remain historical Version 0.1 snapshots and do not yet contain this supplement. Do not cite the old PDF as containing these additions. The proposed distinction has not yet been established by a systematic literature review or empirical evaluation.

## Keywords

Machine Learning; Artificial Intelligence; Self-Adaptive Software; Adaptive Software; Online Learning; Runtime Adaptation; Learning-Enabled Software; Learning-Native Software Components; Adaptive Software Components; Software Libraries; Software Frameworks; Runtime Intelligence; Native Machine Learning; Scratch Machine Learning; Predictive Software; Adaptive Systems; Feedback-Driven Software; Learning-Based Adaptation; Frontend Intelligence; Backend Intelligence; Learning-Native Runtime.

## Abstract

Software has traditionally been built around rules that are designed in advance. Developers decide how a library should cache data, how a framework should schedule work, how a runtime should handle failures, or how a user interface should load resources.

That approach is predictable and often effective. However, real-world software rarely operates under stable conditions. Users behave differently over time, workloads change, network conditions fluctuate, and the cost of different execution strategies can vary significantly.

This document proposes the **Learning-Native Adaptive Software Framework (LNASF)**, a general architectural framework for building software components that can learn from their own runtime experience and use that knowledge to adapt future behavior.

The framework is intended for reusable software components, including libraries, frameworks, runtimes, developer tools, frontend systems, backend systems, and infrastructure components.

The central idea is a continuous feedback loop:

$$
Observe \rightarrow Learn \rightarrow Predict \rightarrow Decide \rightarrow Adapt \rightarrow Measure \rightarrow Learn
$$

LNASF does not claim to introduce machine learning, self-adaptive software, runtime adaptation, online learning, or learning-enabled components as new concepts. These areas have extensive prior research and established techniques.

The candidate contribution investigated here is a more specific architectural formulation: an explicit, reusable, and testable component-boundary contract for learning-enabled software. The contract makes observation, model updating, prediction evidence, adaptation admission, permitted actions, deterministic fallback, and outcome evaluation explicit. This document does not yet establish that the contract is novel relative to existing frameworks; that is the question addressed by the preliminary comparison and evaluation plan.

## 1. Motivation

Most software libraries and frameworks behave according to rules that are determined before deployment.

Examples include:

```text
timeout = 500 ms
retryCount = 3
cacheTTL = 5 min
prefetch = enabled
concurrency = 4
```

These values and strategies may work well in development and testing, but they are not necessarily optimal under every runtime condition.

Users change their behavior. Workloads change. Network conditions fluctuate. Failure patterns evolve. Resource availability varies. A policy that was reasonable yesterday may not be the best policy tomorrow.

LNASF asks a practical engineering question:

> Can a reusable software component observe its runtime experience, learn from that experience, and use the learned knowledge to make better decisions later?

## 2. Core Idea

The central concept of LNASF is a **Learning-Native Adaptive Software Component (LNASC)**.

Such a component has a normal deterministic implementation, but also contains a learning capability that can use runtime observations to improve selected decisions.

A simplified representation is:

$$
Component = Deterministic\ Baseline + Learning\ Layer + Adaptive\ Policy
$$

The learning layer does not replace the original software logic. It provides an additional source of information that can influence selected runtime decisions.

The fundamental learning loop is:

$$
O_t \rightarrow M_t \rightarrow \hat{Y}_{t+1} \rightarrow D_t \rightarrow A_t \rightarrow R_t \rightarrow M_{t+1}
$$

where $O_t$ represents observations at time $t$, $M_t$ represents the current learned model, $\hat{Y}_{t+1}$ is a prediction, $D_t$ is the decision, $A_t$ is the adaptive action, and $R_t$ is the observed result.

The model may be updated using:

$$
M_{t+1}=U(M_t,O_t,R_t)
$$

## 3. What LNASF Is and Is Not

LNASF is an architectural proposal rather than a single machine-learning algorithm or product.

It is intended to provide a common way of reasoning about questions such as:

- What should a software component observe?
- What should it learn?
- What should it predict?
- How should predictions influence decisions?
- What constraints should limit adaptation?
- What should happen when the model is uncertain?
- How should the component determine whether an adaptation was useful?

LNASF does **not** claim to invent:

- machine learning;
- online learning;
- self-adaptive software;
- autonomic computing;
- MAPE-K;
- runtime adaptation;
- predictive prefetching;
- adaptive caching;
- adaptive scheduling;
- learning-enabled components.

These areas are treated as prior art and foundations.

## 4. Learning as a Software-Component Capability

LNASF treats learning as an explicit capability of a reusable software component.

Instead of thinking only in terms of:

```text
Application
    -> Library
       -> Execution
```

an adaptive component can be viewed as:

```text
Application
    -> Reusable Software Component
       -> Deterministic Behavior
       -> Learning Capability
          -> Runtime Experience
             -> Adaptation
```

The intention is not to turn every component into an autonomous system. The intention is to make adaptive capability a deliberate architectural choice.

## 5. Native Learning

One of the design principles of LNASF is **native learning**.

The learning layer should, as far as practical, operate within the language and runtime ecosystem of the host software.

Examples:

```text
TypeScript Library -> TypeScript Learning Engine
C# Library        -> C# Learning Engine
Go Library        -> Go Learning Engine
Rust Library      -> Rust Learning Engine
Python Library    -> Python Learning Engine
```

The baseline architecture should not require a different programming language, an external inference service, or a remote machine-learning runtime merely to provide adaptive behavior.

The intended baseline is therefore:

```text
Host Software
    -> Native Learning Layer
       -> Prediction
          -> Decision
             -> Adaptation
```

Native learning is a design principle proposed by LNASF. It is not presented as a historical first.

## 6. Scratch Learning

A reference implementation should not require a specialized machine-learning framework to execute the essential learning mechanism.

Learning methods may be constructed from fundamental computational primitives such as:

- arithmetic;
- probability;
- statistics;
- linear algebra;
- numerical methods;
- optimization;
- data structures.

For example:

$$
P(j|i)=\frac{N(i,j)}{N(i)}
$$

or an online parameter update such as:

$$
w_{t+1}=w_t-\eta\nabla L(w_t)
$$

The purpose is transparency and portability of the learning mechanism rather than avoidance of every standard-library function.

## 7. Prediction Is Not Action

A central LNASF principle is:

$$
Prediction \neq Action
$$

A prediction may be accurate while the associated action is still too expensive, risky, or unnecessary.

The decision process may therefore be modeled as:

$$
Decision=f(Prediction,Confidence,ExpectedBenefit,ExpectedCost,Constraints)
$$

One possible utility formulation is:

$$
U(a|x)=E[Benefit(a)|x]-E[Cost(a)|x]
$$

with the selected action represented as:

$$
a^*=\arg\max_a E[U(a|x)]
$$

subject to applicable constraints.

## 8. Confidence and Uncertainty

Adaptive behavior should account for uncertainty.

For example:

$$
P(A|X)=0.54
$$

may not justify an adaptation. By contrast:

$$
P(A|X)=0.96
$$

may justify it, depending on the cost and risk of the action.

An adaptive component may therefore use a threshold:

$$
Confidence \geq \tau
$$

before enabling a given adaptation.

## 9. Deterministic Fallback

A learning-enabled component must remain useful when learning is unavailable or unreliable.

Possible causes include insufficient data, model degradation, concept drift, privacy restrictions, unexpected runtime conditions, or resource limits.

The architecture therefore includes a deterministic baseline:

```text
Learned Policy
    -> Validate
       -> Safe? ---- Yes -> Adaptive Action
             \---- No  -> Deterministic Baseline
```

Conceptually:

$$
Behavior=Deterministic\ Baseline+Optional\ Adaptive\ Intelligence
$$

## 10. Levels of Adaptation

### 10.1 Parameter Adaptation

The component preserves its algorithm or strategy but changes parameters.

Examples include timeout, retry delay, cache TTL, debounce interval, concurrency limit, and prefetch threshold.

### 10.2 Strategy Adaptation

The component selects between predefined strategies.

For example:

```text
Prefetch Policy
    aggressive
    balanced
    conservative
```

### 10.3 Structural Adaptation

The component changes an execution path, composition, or selected implementation.

Structural adaptation is more complex and should be treated as an advanced capability.

## 11. Learning Modes

LNASF defines four operational modes.

### Passive

Observe and learn without changing runtime behavior.

### Advisory

Generate predictions or recommendations while leaving the final decision to the application or developer.

### Adaptive

Automatically apply adaptations that are explicitly permitted by policy.

### Autonomous

Continuously optimize behavior within explicit safety, resource, and policy constraints.

## 12. Learning Scope

### Local Learning

The model belongs to a component, application, session, process, device, or user.

### Shared Learning

Observations from multiple instances contribute to a shared model.

### Hybrid Learning

A shared model provides a baseline while local models adapt to local conditions:

$$
M=M_{global}+M_{local}
$$

The exact interpretation of this equation depends on the model family used by an implementation.

## 13. Feedback Loop

An adaptive action does not end the learning process.

```text
Observation
    -> Learning
       -> Prediction
          -> Decision
             -> Action
                -> Outcome
                   -> Evaluation
                      -> Model Update
                         -> Observation
```

The observed result of an action becomes evidence for subsequent learning.

## 14. Model Drift and Learning Failure

A learning-enabled component must consider:

- cold start;
- insufficient data;
- concept drift;
- distribution change;
- prediction error;
- adaptation instability;
- model degradation;
- unexpected outcomes.

Model health should therefore be treated as part of the component's runtime concerns.

## 15. Privacy

When observations represent user behavior, local-first learning is an important option for client-side systems.

```text
User Behavior
    -> Local Observation
       -> Local Model
          -> Local Adaptation
```

Remote aggregation should be optional, explicit, and governed by the application's privacy requirements.

## 16. Frontend Applications

Possible frontend applications include:

- predictive prefetching;
- adaptive loading;
- adaptive caching;
- request prioritization;
- adaptive debouncing;
- learnable state behavior;
- render/resource scheduling.

For example, a client may estimate:

$$
P(Page_B|Page_A)=0.87
$$

and then combine that estimate with confidence and network cost before deciding whether to prefetch Page B.

Predictive prefetching itself is established prior art and is included here only as an example application of the framework.

## 17. Backend Applications

A backend component may estimate:

$$
P(success|errorType,service)
$$

and choose among retry, delayed retry, or fail-fast behavior.

Other possible uses include:

- adaptive timeout;
- adaptive retry;
- adaptive concurrency;
- workload-aware scheduling;
- cache optimization;
- resource allocation.

## 18. Runtime and Infrastructure Applications

Runtime and infrastructure components may observe CPU utilization, memory pressure, I/O latency, request rate, queue depth, failure rate, and workload patterns.

A general workload loop can be represented as:

$$
Workload_t \rightarrow Prediction_t \rightarrow SchedulingDecision_t
$$

The same architectural model can be applied to recovery policies, resource allocation, execution strategy selection, and related operational decisions.

## 19. Independence from Programming Language

The architecture is intentionally language-independent.

The same conceptual cycle can be implemented in:

```text
TypeScript
C#
Java
Go
Rust
Python
```

The architecture is shared while implementation details remain native to the host ecosystem.

## 20. Independence from Learning Algorithm

LNASF does not require a particular learning algorithm.

Potential implementations include:

- frequency models;
- conditional probability;
- moving averages;
- Bayesian updating;
- Markov models;
- online gradient methods;
- contextual bandits;
- other suitable online learning methods.

The framework concerns the relationship between learning and software behavior, not a single model family.

## 21. Developer Model

An LNASF-enabled component should make several questions explicit:

```text
What does this component observe?
What does it learn?
What does it predict?
What decisions can learning influence?
What constraints limit adaptation?
What happens when confidence is low?
What is the deterministic fallback?
How is success measured?
```

The goal is to make adaptive behavior explicit and testable rather than mysterious.

## 22. Evaluation

An adaptive component should be compared against a deterministic baseline.

Potential metrics include:

$$
Latency,
CPU,
Memory,
NetworkCost,
ErrorRate,
PredictionAccuracy,
AdaptationOverhead,
FalseAdaptationRate
$$

A general net-utility formulation is:

$$
NetUtility=Benefit-Cost-AdaptationOverhead
$$

The important question is not merely whether a model can predict something, but whether learning produces a measurable engineering benefit after learning and adaptation costs are included.

## 23. Prior Art and Related Work

LNASF sits within established research on autonomic computing and self-adaptive systems [1, 2], the use of machine learning in self-adaptation [3], online runtime learning and component assembly [4], machine-learning-enabled self-organizing components [5], component-based ML abstractions for self-optimizing systems [6, 7], adaptable feedback-loop architectures [8], reusable architecture-based self-adaptation infrastructure [11], and the FORMS unifying reference model for distributed self-adaptive systems [10].

These works are not peripheral: REX directly combines online learning with runtime adaptation of software components; ML-DEECo and subsequent component-abstraction work explicitly integrate machine learning into component-based adaptive systems; and HAFLoop studies reusable architectures for feedback-loop adaptation. Accordingly, LNASF does not claim to originate runtime learning, component-level self-adaptation, reusable adaptation loops, or the individual principles listed below.

The literature comparison in [RESEARCH-POSITIONING.md](RESEARCH-POSITIONING.md) is a focused preliminary analysis, not an exhaustive or protocol-driven systematic review. Detailed novelty claims must wait until the closest works have been compared from their full texts using an explicit search and screening method.

## 24. Position Relative to Prior Art

LNASF does not claim to invent:

- machine learning or online learning;
- self-adaptive software or autonomic computing;
- MAPE-K or feedback-loop adaptation;
- runtime learning and adaptation of software components;
- predictive prefetching, adaptive caching, or adaptive scheduling;
- confidence/uncertainty estimation, decision policies, safety constraints, or deterministic fallback as isolated concepts.

The candidate contribution is a more specific architectural formulation: **an explicit, reusable, and testable component-boundary contract for learning-enabled software**. It requires the component design to state what it observes and learns, how predictions and their evidence are represented, how a separate gate admits or rejects candidate adaptations, which actions are allowed, which deterministic fallback is retained, and how outcomes and adaptation overhead are measured.

This is a candidate contribution—not a proven claim of historical originality. Prior approaches may already provide equivalent or overlapping mechanisms. The comparison and evaluation required to decide that question are recorded in [RESEARCH-POSITIONING.md](RESEARCH-POSITIONING.md).

### 24.1. Candidate Contribution: The LNASF Component Contract

For a learning-enabled component `C`, the proposed contract is:

$$
\operatorname{LCC}(C) = (B,O,M,P,G,A,F,E)
$$

where:

- `B`: deterministic baseline behavior;
- `O`: observation interface and collection boundaries;
- `M`: learning model and update procedure;
- `P`: prediction interface, including evidence sufficiency or uncertainty;
- `G`: explicit adaptation-admission gate, separate from the predictor;
- `A`: permitted adaptation actions and resource bounds;
- `F`: deterministic fallback or abstention behavior;
- `E`: outcome evaluation and feedback into subsequent learning.

One candidate gate is:

$$
G_t(a) =
[q_t \geq \epsilon]
\land [S(a,o_t)=\mathrm{true}]
\land [\widehat{\Delta U}_t(a)-C_{\mathrm{adapt},t}>\lambda]
$$

The component applies an adaptive action only when the gate passes. Otherwise it uses `B(o_t)`, or returns an advisory result in advisory mode. Here `q_t` is an application-defined evidence-adequacy measure; `S` is a hard safety/resource constraint; `\widehat{\Delta U}_t` is estimated utility improvement; and `C_{adapt}` is adaptation cost. Thresholds `\epsilon` and `\lambda` are application-specific and require evaluation. An uncalibrated confidence score must not be presented as a calibrated probability.

The candidate distinction is the **explicit contract and its conformance/evaluation obligations at the reusable component boundary**, not the invention of any one of these ingredients. Whether this contract is sufficiently different from REX, ML-DEECo, component-based ML abstractions, and existing adaptive-loop architectures remains an open research question. In particular, FORMS [10] and Rainbow [11] prevent LNASF from claiming distinction merely because it offers a reusable or unifying adaptation architecture.

A possible testable invariant is that a component must not apply a learned adaptation when evidence is insufficient, a hard constraint fails, or predicted net benefit does not exceed the specified threshold. The invariant must be encoded as tests and checked in each reference implementation; this document alone does not establish it.

## 25. Research Hypothesis

The central hypothesis for the candidate contribution is:

> An explicit LNASF Component Contract—with inspectable observation, model-update, prediction-evidence, adaptation-admission, allowed-action, fallback, and evaluation obligations—can make adaptive behavior easier to inspect and test than implementations where these concerns remain implicit, while preserving safe fallback and accounting for adaptation overhead.

This is an empirical hypothesis, not an established result. It should be evaluated by contract-conformance checks, controlled comparisons with a deterministic baseline, component-level ablations, and measurements of both outcome quality and adaptation cost.

## 26. Potential Software Family

A possible family of implementations is:

```text
Learning-Native Software
|
+-- Frontend
|   +-- Predictive Prefetch
|   +-- Adaptive Loading
|   +-- Adaptive Cache
|   +-- Learnable State
|
+-- Backend
|   +-- Adaptive Retry
|   +-- Adaptive Timeout
|   +-- Adaptive Scheduling
|   +-- Adaptive Concurrency
|
+-- Runtime
|   +-- Workload Prediction
|   +-- Resource Allocation
|   +-- Execution Adaptation
|
+-- Infrastructure
    +-- Failure Prediction
    +-- Recovery Policies
    +-- Resource Optimization
```

These are possible implementation directions, not claims that each technique is novel.

## 27. Development Roadmap

### Phase 1 - Concept

Formalize terminology, boundaries, principles, and architecture.

### Phase 2 - Mathematical Learning Core

Implement simple learning mechanisms from fundamental mathematical and computational primitives.

### Phase 3 - Reference Implementation

Build the first learning-native component in TypeScript, with a React integration as the initial practical demonstration.

### Phase 4 - Evaluation

Compare learning-enabled behavior with a deterministic baseline under realistic workloads.

### Phase 5 - Advanced Learning

Explore Bayesian models, Markov models, online learning, contextual models, and bandit-based decision methods.

### Phase 6 - Additional Ecosystems

Investigate native implementations for C#, Go, Rust, Python, and Java.

### Phase 7 - Framework and Runtime Applications

Explore applications in larger libraries, frameworks, runtimes, and infrastructure systems.

## 28. Limitations and Open Questions

Important open questions include:

- How should cold start be handled?
- How should model drift be detected?
- How can adaptation remain stable under noisy observations?
- When does learning cost more than it saves?
- How can adaptive behavior remain reproducible during testing?
- What safety guarantees are appropriate for autonomous adaptation?
- How should privacy constraints shape observation and learning?
- How can the architecture remain consistent across different programming languages and runtimes?

These questions are part of the intended future research and engineering work.

## 29. Design Principles

### Principle 1 - Learning is a capability

Learning is treated as an explicit software-component capability.

### Principle 2 - Native execution

The learning layer should remain native to the host ecosystem whenever practical.

### Principle 3 - Scratch learning core

Reference implementations should make the essential learning mechanism understandable from fundamental computational primitives.

### Principle 4 - Prediction is not action

Predictions must pass through explicit decision policies.

### Principle 5 - Adaptation is constrained

Adaptive behavior must operate within defined resource and safety constraints.

### Principle 6 - Deterministic fallback

The component must retain a predictable baseline behavior.

### Principle 7 - Feedback matters

Adaptation outcomes should contribute to subsequent learning.

### Principle 8 - Learning should be measurable

An adaptive component should be evaluated against an appropriate deterministic baseline.

## 30. Scope of This Disclosure

The Version 0.1 technical disclosure records the author's proposed terminology, architectural organization, mathematical framing, design principles, and implementation directions for LNASF. The editable Markdown now includes a dated research-positioning supplement proposing the LNASF Component Contract for further investigation. That supplement is a working draft; it is not yet synchronized into the historical Version 0.1 TeX/PDF, and its novelty has not been established by a systematic comparison or empirical evaluation.

The project intentionally distinguishes established prior art from candidate contributions still requiring validation.

This document is a technical disclosure. It is not legal advice and does not by itself create exclusive rights in abstract ideas or guarantee patentability.

## 31. Citation

Salimi, Peyman. (2026). *Learning-Native Adaptive Software Framework (LNASF): Technical Concept and Architecture Specification*, Version 0.1.

## References

1. Kephart, J. O., & Chess, D. M. (2003). The Vision of Autonomic Computing. *IEEE Computer*, 36(1), 41–50. DOI: [10.1109/MC.2003.1160055](https://doi.org/10.1109/MC.2003.1160055).
2. Wong, T., Wagner, M., & Treude, C. (2022). Self-adaptive systems: A systematic literature review across categories and domains. *Information and Software Technology*, 148, Article 106934. DOI: [10.1016/j.infsof.2022.106934](https://doi.org/10.1016/j.infsof.2022.106934).
3. Gheibi, O., Weyns, D., & Quin, F. (2022). Applying Machine Learning in Self-Adaptive Systems: A Systematic Literature Review. *ACM Transactions on Autonomous and Adaptive Systems*. DOI: [10.1145/3469440](https://doi.org/10.1145/3469440). Preprint: arXiv:2103.04112 (2021).
4. Porter, B., Grieves, M., Rodrigues Filho, R., & Leslie, D. (2016). REX: A Development Platform and Online Learning Approach for Runtime Emergent Software Systems. *Proceedings of OSDI 2016*, 333–348. [USENIX paper](https://www.usenix.org/conference/osdi16/technical-sessions/presentation/porter).
5. Töpfer, M., Abdullah, M., Kruliš, M., Bureš, T., & Hnětynka, P. (2022). ML-DEECo: A Machine-Learning-Enabled Framework for Self-organizing Components. *ACSOS 2022 Companion*. DOI: [10.1109/ACSOSC56246.2022.00033](https://doi.org/10.1109/ACSOSC56246.2022.00033).
6. Töpfer, M., Abdullah, M., Bureš, T., Hnětynka, P., & Kruliš, M. (2023). Machine-learning abstractions for component-based self-optimizing systems. *International Journal on Software Tools for Technology Transfer*, 25, 717–731. DOI: [10.1007/s10009-023-00726-x](https://doi.org/10.1007/s10009-023-00726-x).
7. Abdullah, M., Töpfer, M., Bureš, T., Hnětynka, P., Kruliš, M., & Plášil, F. (2023). Introducing Estimators—Abstraction for Easy ML Employment in Self-adaptive Architectures. *ECSA 2022 Tracks and Workshops*, 370–385. DOI: [10.1007/978-3-031-36889-9_25](https://doi.org/10.1007/978-3-031-36889-9_25).
8. Zavala, E., Franch, X., Marco, J., & Berger, C. (2020). HAFLoop: An architecture for supporting Highly Adaptive Feedback Loops in self-adaptive systems. *Future Generation Computer Systems*, 105, 607–630. DOI: [10.1016/j.future.2019.12.026](https://doi.org/10.1016/j.future.2019.12.026).
9. Peffers, K., Tuunanen, T., Rothenberger, M. A., & Chatterjee, S. (2007). A Design Science Research Methodology for Information Systems Research. *Journal of Management Information Systems*, 24(3), 45–77. DOI: [10.2753/MIS0742-1222240302](https://doi.org/10.2753/MIS0742-1222240302).
10. Weyns, D., Malek, S., & Andersson, J. (2012). FORMS: Unifying Reference Model for Formal Specification of Distributed Self-adaptive Systems. *ACM Transactions on Autonomous and Adaptive Systems*, 7(1), Article 8, 1–61. DOI: [10.1145/2168260.2168268](https://doi.org/10.1145/2168260.2168268).
11. Garlan, D., Cheng, S.-W., Huang, A.-C., Schmerl, B., & Steenkiste, P. (2004). Rainbow: Architecture-Based Self-Adaptation with Reusable Infrastructure. *IEEE Computer*, 37(10), 46–54. DOI: [10.1109/MC.2004.175](https://doi.org/10.1109/MC.2004.175).

The expanded related-work comparison is preliminary, not systematic. See [RESEARCH-POSITIONING.md](RESEARCH-POSITIONING.md) for the candidate contribution and remaining validation work.
