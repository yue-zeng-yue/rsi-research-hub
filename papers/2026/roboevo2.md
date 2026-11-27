# RoboEvo²

**Reviewed:** 2026-11-27. **Evidence:** Primary-reviewed; results are author-reported. Code inspected; no independent run.

## Full Paper Title

RoboEvo²: Recursive Robot Self-Improvement via Harness–Policy Co-Evolution

## Authors and Affiliations

Chenzhi Liu, Jiehong Lin, Wei Huang, Xuzhao Huang, Bo Wang, and Xiaojuan Qi (The University of Hong Kong); Haoyuan Li and Chenyeyang Cai (Zhejiang University); Yang Zhang and Zhongrui Wang (Southern University of Science and Technology); Junchao Huang (The Chinese University of Hong Kong, Shenzhen); Kazuhiro Kosuge (City University of Hong Kong). The canonical author order is recorded in the catalog.

## Publication Date

First arXiv submission and reviewed v1: 2026-11-25, 16:39:10 UTC (November 26 in Asia/Shanghai).

## Venue or Preprint Status

arXiv preprint. Peer-reviewed acceptance: **Not verified**; no proceedings record was identified.

## Paper URL / DOI

[Canonical record](https://arxiv.org/abs/2611.34675) · [Reviewed v1](https://arxiv.org/html/2611.34675v1) · [PDF](https://arxiv.org/pdf/2611.34675v1) · [arXiv DOI](https://doi.org/10.48550/arXiv.2611.34675).

## Official GitHub Repository

[Author-linked source](https://github.com/kaiknower/RoboEvo2/tree/cd0a8ee12dd9e4616d8804ef5ffed537d4f5d63d) and [project page](https://kaiknower.github.io/RoboEvo2/). The inspected commit contains evolution, hybrid evaluation, and policy-training modules. Its README links policy weights and states that the evaluator still needs a companion runtime and user-supplied model integration. Complete native reproduction is **Not verified**.

## Research Problem

Convert successful agentic recovery into a policy that can act without invoking the coding agent as often, while using remaining policy failures to prioritize the next harness update.

## Methodology and Algorithm

Sections 3.1–3.4: policy-to-harness evolution uses execution feedback to search code, demonstration-conditioned code, and code invoking learned skills. It verifies successes and prefers smoother motion among successful candidates, then updates skills, memory, and routing. Harness-to-policy evolution uses verified trajectories for supervised updates. Counterfactual Preference Distillation contrasts failed and corrected continuations from the same initial state relative to a frozen reference; asymmetric penalties constrain the update. Failure-aware sampling and elastic weight consolidation retain earlier coverage. Optional PPO is an additional stage, not part of the headline pre-PPO comparison.

## Key Contributions

**Review assessment:** the paired failure/correction signal and standalone-versus-hybrid evaluation distinguish partial policy internalization from rescue by the harness. The evolving policy and harness form a reciprocal loop, but this does not by itself show that the coding agent's improvement capability has increased.

## Experimental Setup

Section 4.1 and Appendices C, D, and G: the primary comparison uses the pi-0.5 policy and GPT-6 Astra coding agent, with eight evolution rounds for LIBERO-PRO and five for RoboTwin C2R. Evolution seeds differ from initial training data and final episode seeds are separately held out. LIBERO-PRO evaluates 800 episodes across eight perturbation settings; RoboTwin C2R evaluates 5,000 episodes across 50 bimanual tasks. Independent full-loop run count and matched total resource cost: **Not verified** for the headline comparison.

## Benchmarks and Baselines

Use initial pi-0.5 and harness as round-zero controls. Standalone runs the policy alone; hybrid permits recovery by the harness. Table 3 freezes one component at a time. Published comparisons in Table 2 retain their original protocols and are not assumed equal-cost.

## Quantitative Results

Figure 3 and Table 16: from round zero to round eight, pi-0.5 on the held-out LIBERO-PRO episodes improves from 11.0% to 84.1% standalone and from 30.4% to 90.5% hybrid, before optional PPO. At round three, the same benchmark's full loop reaches 52.3% standalone and 68.3% hybrid; the fixed-harness variant reaches 33.6% and 49.0%, respectively (Table 3). These author-reported aggregate rates lack verified uncertainty over independent full-loop seeds. Figure 3's API expense tracks the coding agent per round, not total training, simulation, or deployment cost.

## Limitations

Appendix H notes limited atomic skills and dependence on a task-success check for trajectory admission. **Review analysis:** transfer to new seeds is not equivalent to transfer to entirely new task families. Changing the policy and harness together also changes the data acquired by the improver; the trajectory does not isolate changes in the improver itself. Initial demonstrations remain part of the training provenance.

## Reproducibility

Inspected Sections 3–4, Figure 3, Tables 2, 3, 5, and 16, and Appendices C, D, G, and H. The public implementation contains substantive runners and recipes, but the companion environment, exact model access, and full run equivalence were not verified. No simulator or training execution was performed.

## Open Research Questions

Cross earlier and later harness and policy checkpoints from identical initial states and match the intervention budget to identify compatibility effects. Measure success per whole-loop resource unit with simulator, training, proposal, failed repair, and evaluation costs included.
