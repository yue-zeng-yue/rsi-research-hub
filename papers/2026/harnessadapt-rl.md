# Training the Whole Agent, Not Just the Model

Reviewed against primary sources on 2026-11-19. Quantitative findings below are author-reported, not independently reproduced.

## Full Paper Title

Training the Whole Agent, Not Just the Model

## Authors and Affiliations

Lingxiao Tang; Wei Tao; Yiwen Guo; Lingfeng Bao

Verified from PDF page 1: Lingxiao Tang and Lingfeng Bao: Zhejiang University. Wei Tao: LIGHTSPEED. Yiwen Guo: Independent Researcher.

## Publication Date

2026-10-20; reviewed v1.

## Venue or Preprint Status

arXiv preprint; no conference acceptance independently verified.

## Paper URL / DOI

[arXiv](https://arxiv.org/abs/2610.28069) · [Full text](https://arxiv.org/html/2610.28069v1) · [arXiv DOI](https://doi.org/10.48550/arXiv.2610.28069).

## Official GitHub Repository

[Official HarnessAdapt-RL repository](https://github.com/lingxiaotang/HarnessAdapt-RL); primary paper and README link training code, evolved harness, data, and model weights.

## Research Problem

Policy-only reinforcement learning leaves recurring interaction failures in the runtime. The study asks which guidance should support training, how tools should change with the policy, and which learned runtime components must remain at deployment.

## Methodology and Algorithm

Two frozen teachers serve different roles. One generates task-specific mechanism-level repair guidance from paired trajectories, excluding concrete paths, symbols, and code. Another proposes executable tools/hooks from problems recurring across tasks. Compare candidate and incumbent under identical policy, tasks, skills, and rollout budgets. Accept only if observed pass rate or trainable-rollout rate improves without reducing the other. Fresh rollouts then train the policy with GRPO. Trainability excludes unusable and zero-contrast reward groups. Two epochs permit re-evolution; deployment removes skills and teachers but retains final tools/hooks.

## Key Contributions

The contribution is training-aware harness selection and a clear distinction between transient pedagogical guidance and persistent runtime support. Ablations compare concrete hints, general skill banks, mechanism-level skills, pre-evolution, repeated evolution, and deployment harness swaps.

## Experimental Setup

Qwen3.5-9B with mini-swe-agent trains on 1,058 R2E-Gym-Lite tasks disjoint from evaluation. GLM-5.3-Flash generates skills; GPT-5.6 Sol through Codex edits tools/hooks. GRPO gets 16,928 policy-training rollouts; full adaptation gets 8,464 training rollouts plus preparation/comparison for 18,056 total. Teacher costs are additional. Each configuration has one training run and three evaluation repeats.

## Benchmarks and Baselines

SWE-bench Verified, Multilingual, and Pro report mean pass@1. Baselines include GRPO under the base harness, OpenHands-GRPO, skill variants, pre-evolved harness, and a frozen first-epoch harness. Evaluations contain no further evolution or teacher help.

## Quantitative Results

Table 1 gives full-method 57.6%, 37.3%, 39.7%, versus GRPO 47.8%, 24.7%, 33.3%; macro-average gain is 9.6 points. Fixed-policy removal of evolved tools/hooks costs 4.8, 7.7, and 4.7 points. Appendix 9.4 reports pooled re-evolution gain 2.6 points with task-bootstrap interval [0.9,4.3]. Reusing the already-discovered final harness in a new training run yields scores within one point of full adaptation.

## Limitations

The paper explicitly limits evidence to one 9B model and software repair. Evaluation repeats and task-bootstrap intervals do not measure training-seed or harness-search variance. Finite candidate-rate comparisons are not significance tests; bundled proposals do not isolate individual tool effects. Reuse experiments exclude original discovery cost.

## Reproducibility

The method, cost appendix, limitations, swap tables, and official README were inspected; independent reruns were not performed. Reproduction must preserve preparation/comparison accounting and distinguish total rollouts from policy-training rollouts. Claimed teacher removal applies to deployment, not the training budget.

## Open Research Questions

Can trainability-aware selection avoid noisy acceptance without excessive validation? When can final harness discovery be amortized across models, and which tools transfer without costly re-evolution?

Primary reading: Sections 2–4; Tables 1–2; Limitations; Appendices 7–9, especially 8.4 and 9.7.
