# Idea 3: Utility-Aware Harness Adaptation

**Status:** Proposed causal estimation and selection study; no causal effect has been measured in this repository. **Novelty status:** Open.

## Problem Statement

Predict whether enabling a proposed harness or skill update will improve a particular executor's performance on a task distribution, after accounting for inference and adaptation cost. The prediction must support rejecting uncertain updates and transferring beyond the task families used to fit it.

## Motivation

An updater can produce plausible modifications that an executor ignores, misunderstands, or overuses. Skill utilization is an intermediate behavior, while task benefit is an outcome contrast. A utility estimator could allocate expensive evaluations and prevent low-value context expansion.

## Related Work

| Work | Existing idea | Required differentiation |
| --- | --- | --- |
| [Harness Updating Is Not Harness Benefit](https://arxiv.org/abs/2605.30621) | Separates updater capability and executor benefit | An intervention-trained predictor with calibrated transfer |
| [HDA](https://arxiv.org/abs/2610.22466) | Attribution using compute-matched and shortcut-neutralized controls | Predictive selection before full evaluation, with direct randomized effects |
| [GEPA](https://arxiv.org/abs/2507.19457) | Feedback-driven prompt evolution and Pareto selection | Conditional benefit prediction beyond prompt search |
| [HMED](https://arxiv.org/abs/2610.07979) | Revision effects from common-state replay | Cross-executor causal data and uncertainty-aware policy value |
| [RRSI](https://arxiv.org/abs/2609.24972) | Regularized editing and pruning | Evidence that learned utility improves on conservative rules |
| [TRUST](https://arxiv.org/abs/2611.10787) | Statistically controlled sequential admission with contextual evidence allocation | Conditional edit/executor utility and policy transfer beyond gate design |
| [AHE-Beta](https://arxiv.org/abs/2611.24924) | Requirement-driven proposals and simulated-user review | Outcome-calibrated utility beyond a requirement-compliance gate |
| [SkillsBench](https://github.com/benchflow-ai/skillsbench) | Skill/no-skill evaluation | Generalization across generators and executor families |

## Limitations of Existing Methods

Positive development deltas are selected noisy estimates. Removing a detected shortcut is an informative intervention but does not discover every shortcut. Observational skill invocation is confounded by task difficulty and model confidence. This review does not establish that causal harness selection is an unexplored area; a fresh related-work search is required before claiming novelty.

## Research Hypothesis

A predictor trained on randomized update exposure, with outcome and cost modeled jointly, will choose useful updates on new task families more accurately than validation-score-only selection or invocation heuristics at the same evaluation budget.

## Proposed Algorithm

Create an intervention dataset from candidate edits generated without final-test access. For each pre-edit task context, randomly assign the update enabled or disabled in fresh, isolated environments; use a paired crossover when the environment can be reset faithfully. Keep tool access and execution caps fixed. Record success, latency, tokens, invocation, and failure type.

Fit treatment-specific outcome and cost models on development families. Calibrate uncertainty on separate validation families. Select updates when a conservative utility estimate exceeds a prespecified threshold; abstain when a new executor or edit lies outside support. Evaluate the learned selection policy against random selection and direct paired evaluation. Do not condition the primary analysis on whether the skill was invoked after assignment.

## Mathematical Formulation

Let $x=(\tau,\theta,h,u)$ encode pre-treatment task features, executor identity, incumbent harness, and the **specific candidate edit** $u$. For each fixed edit, $A\in\{0,1\}$ randomizes its availability, and $Y(a;u),C(a;u)$ are its potential outcomes and costs. The target, suppressing $u$ only because it is included in $x$, is

$$
\tau_\lambda(x)=\mathbb{E}[Y(1)-Y(0)\mid x]-\lambda\mathbb{E}[C(1)-C(0)\mid x].
$$

For binary reward, estimate treatment outcomes with cross-fitting and evaluate policy value on randomized held-out logs with known propensity $e(x)$. A doubly robust value estimate for selection policy $\pi$ is

$$
\widehat V(\pi)=\frac1n\sum_i\left[\widehat\mu_{\pi(x_i)}(x_i)+
\frac{\mathbf{1}\{A_i=\pi(x_i)\}}{p(A_i\mid x_i)}
(U_i-\widehat\mu_{A_i}(x_i))\right],\quad U_i=Y_i-\lambda C_i.
$$

Randomization, consistency, overlap, and no cross-run interference are necessary. Candidate edits and their versions cannot be pooled as an unspecified binary treatment. Shared memory, caches, or persistent environment mutations can violate the assumptions. Task-level pairing reduces variance only when resets and stochasticity are understood. Confidence bounds must reflect model fitting and policy selection, not only outcome noise. For choosing among several edits, use a multi-arm policy with known assignment propensities, or screen on one split and assess the selected edit on independent data.

## Experimental Design

Use SkillsBench and ToolSandbox for skill and tool updates, with ALFWorld as a distinct environment. Split by task family, not execution trace. Cross several updater and executor sizes; reserve one executor family for transfer. Use simple, compositionally combined, and deliberately irrelevant updates to test specificity. Test equal token caps and equal dollar budgets separately because one does not imply the other.

Primary endpoint: policy utility on a sealed task-family split at a fixed development budget. Secondary endpoint: prediction calibration under model shift. Run independent candidate-generation/search seeds and multiple execution seeds. Ablate causal randomization, executor features, cost penalty, calibration, and abstention. A matched-information baseline sees the same traces and labels.

## Baseline Methods

Never update; always update; random update; validation delta threshold; confidence-bound selection using direct paired rollouts; TRUST-style sequential admission; skill invocation frequency; GEPA-style validation/Pareto selection where applicable; RRSI-style regularization; HMED-style revision-effect memory. A best-after-test selector is prohibited as a deployable baseline and can only be an explicitly labeled retrospective ceiling.

## Evaluation Metrics

Policy value, held-out success, beneficial-update precision and recall, regret, coverage versus regression risk, cost-weighted calibration, and performance across updater/executor cells. Report utility for a prespecified range of $\lambda$ so a convenient cost conversion cannot manufacture the conclusion. Invocation and retrieval are explanatory secondary metrics.

## Expected Challenges

High variance in small effects; heterogeneous edit semantics; nonstationary APIs; expensive randomized logs; correlated tasks; and compositional interference between skills. For multi-skill interactions, extend beyond one-at-a-time ablations only after the single-update effect is established.

## Novelty Assessment

The potential contribution is a calibrated **conditional utility estimator and deployment selection policy**, demonstrated under randomized evidence and out-of-family transfer. Neither the observation that skills can hurt nor adding a scalar cost penalty is novel. If direct paired validation is equally effective at the same total budget, the learned estimator has not justified its complexity.

## Potential Publication Venues

ICML, NeurIPS, or ICLR for a general decision algorithm; ACL/EMNLP for an agent-centered evaluation; TMLR for rigorous evidence on adaptation utility. A workshop is appropriate for a limited pilot without broad transfer evidence.
