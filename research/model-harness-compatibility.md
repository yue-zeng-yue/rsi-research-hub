# Idea 1: Compatibility-Aware Model–Harness Co-Evolution

**Status:** Research hypothesis and proposed experiment; no implementation or results. **Novelty status:** Unestablished. This proposal builds on existing co-evolution and interaction analyses.

## Problem Statement

Given a current pair $(\theta,h)$ and candidate model and harness updates, select a successor that improves held-out utility without excessive regressions on supported task families. The challenge is to predict **pair-specific** effects before paying for exhaustive evaluation of every combination.

## Motivation

Independent component scores can be misleading. An updated model may use a different planning strategy, or a harness may require capabilities absent from the updated model. Deployment needs a good pair, not the independently best component checkpoints. Negative interaction and absolute regression must be reported separately.

## Related Work

| Prior work | Existing overlap | Distinction that would need evidence |
| --- | --- | --- |
| [SIA](https://arxiv.org/abs/2605.27276) | Joint harness and weight adaptation | Pair-selection uncertainty and fresh audit controls |
| [HarnessForge](https://arxiv.org/abs/2606.01779) | Joint optimization of policies and harnesses | Risk-sensitive transfer across model families |
| [WHALE](https://arxiv.org/abs/2609.00196) | Adaptive allocation between weight and harness learning | Selection based on estimated interaction rather than training progress alone |
| [HarnessAdapt-RL](https://arxiv.org/abs/2610.28069) | Training-time harness adaptation | Calibration when executor or task distribution changes |
| [JoMoHa](https://arxiv.org/abs/2611.11499) | Coupled training and fixed-component comparisons | Cheap prediction of damaging pairings outside the training family |
| [On-policy correction](https://arxiv.org/abs/2609.09134) | Compatibility-preserving local supervision | Broader update selection beyond one correction recipe |
| [Teacher-free co-evolution](https://arxiv.org/abs/2611.15268) | Separate gates and factorial layer ablation | Risk-aware selection of multiple competing pairs |
| [TRUST](https://arxiv.org/abs/2611.10787) | Context-guided online testing with false-evolution-rate control under assumptions | Pair-specific and family-specific risk estimation beyond an aggregate admission gate |
| [Self-Improvement Memory](https://arxiv.org/abs/2611.18856) | Optimizer memory that transfers across compatible task/model changes | Predictive pair selection beyond replaying structured revision evidence |

## Limitations of Existing Methods

The reviewed papers establish useful mechanisms in their own settings. They do not establish a universal compatibility predictor, and this review is not an exhaustive proof that none exists. Aggregate success can obscure family-specific regressions. A sequential gate can accept each step without detecting vulnerability to later partner changes. The closest comparison must include local on-policy correction, not only naive expert imitation.

## Research Hypothesis

A predictor trained on crossed component interventions can rank candidate pairs more accurately than independent component rankings under a fixed evaluation budget. Calibration-aware abstention should reduce harmful accepted updates on unseen task families, with a measurable tradeoff in rejected beneficial updates.

## Proposed Algorithm

1. Build a versioned archive of model–harness pairs and four-cell crossover evaluations on development families.
2. Extract model capability probes, harness edit categories, tool-schema changes, rollout failure statistics, and measured cost. Do not include hidden answers or final-test scores.
3. Fit a conditional predictor of joint gain and regression risk with task-family cross-validation. Retain uncertainty and out-of-support flags.
4. Generate bounded model and harness candidates using existing update methods. Allocate diagnostic evaluations to pairs with uncertain interaction, not only high predicted mean reward.
5. Select a pair on a screening batch, then assess that frozen pair on an independent acceptance batch using the prespecified rule; otherwise retain the incumbent. If selection and acceptance must share data, use a justified simultaneous or selective-inference correction.
6. Evaluate the final selected pair and its constituent swaps on the sealed audit. Store rejected pairs and all costs.

## Mathematical Formulation

Let $J_{ij,k}$ be success on family $k$ for old/new components. Define interaction $\mathcal I_k=J_{11,k}-J_{10,k}-J_{01,k}+J_{00,k}$ and total gain $\Delta_k=J_{11,k}-J_{00,k}$. Use family weights fixed before search:

$$
\max_{(\theta',h')}\ \operatorname{LCB}\left(\sum_k w_k\Delta_k\right)-\lambda\Delta C,
\qquad \operatorname{UCB}\left(\sum_k w_k\mathbf{1}[\Delta_k<-\epsilon]\right)\le\rho.
$$

True $\Delta_k$ is unknown; finite-task estimates require hierarchical uncertainty or a prespecified family-level model. Do not substitute noisy per-task labels and call the resulting bound distribution-free. Confidence calibration is empirical unless assumptions supporting stronger guarantees are supplied. Repeated rounds also require prespecified error spending, fresh acceptance batches, or a valid sequential procedure; an ordinary interval does not remain valid under arbitrary selection and reuse. A deployment-weighted lower-tail reward objective is a useful sensitivity analysis.

## Experimental Design

Start with tool-using tasks from ALFWorld and ToolSandbox plus disjoint task templates from SkillsBench. Use two open-weight executor families that can be trained under available hardware; choose exact checkpoints and budgets before launch. Reserve at least one model family and one environment family for transfer. Compare equal total development cost, including predictor training, capability probes, and all four-cell evaluations. Run at least five independent outer-loop seeds for a confirmatory study, with the final count chosen from pilot variance and power calculations.

Evaluate a full factorial on the final artifacts even when search uses sparse pair evaluation. Ablate interaction features, uncertainty, regression constraints, and partner-aware candidate generation. Separate a fixed candidate-pool selection study from an end-to-end adaptation study so better generation is not confused with better selection.

## Baseline Methods

Frozen system; model-only; harness-only; alternating updates with a scalar validation gate; independent top-component selection; random pair selection under equal evaluation budget; on-policy local correction; a faithful relevant co-evolution baseline from HarnessForge or JoMoHa; and TRUST-style sequential admission. Include an expensive exhaustive validation selector as a diagnostic upper reference, with its extra cost explicitly reported. TRUST controls an expected false-evolution proportion under stated assumptions; it does not guarantee that every task family avoids regression.

## Evaluation Metrics

Sealed success, task-family regression rate, worst-family change, $\mathcal I_k$, risk calibration, accepted-update precision, beneficial-update rejection, total GPU-hours and API tokens, latency, and pair-selection regret relative to the fully evaluated candidate pool. Report confidence intervals and curves over budget.

## Expected Challenges

Sparse crossover labels; representation drift after training; correlated API errors; small task families; expensive full-grid validation; and reward saturation. Strong models may make few errors, limiting power. A predictor that abstains everywhere is safe but useless, so report coverage and utility jointly.

## Novelty Assessment

Co-evolution, four-cell ablation, local correction, and separate acceptance gates are already prior art. A potential contribution is a **calibrated, budget-constrained pair-selection algorithm that transfers to unseen partners**, supported by controlled crossover data. If gains disappear against equal-cost sequential validation or existing joint training, the novelty claim fails; publish the diagnostic dataset or negative result only if independently useful.

## Potential Publication Venues

ICLR, ICML, or NeurIPS for a general algorithm and robust evaluation; ACL or EMNLP for agent adaptation with language-specific analysis; TMLR or JMLR for a mature methodological study. These are scope-based possibilities, not acceptance predictions. Submission dates and journal indexing are not asserted here.
