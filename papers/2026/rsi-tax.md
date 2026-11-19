# The RSI Tax: When Recursive Self-Improvement Is Not Worth the Cost

Reviewed against primary sources on 2026-11-19. Quantitative findings below are author-reported, not independently reproduced.

## Full Paper Title

The RSI Tax: When Recursive Self-Improvement Is Not Worth the Cost

## Authors and Affiliations

Yitong Zhang; Ang Li; Yisen Wang

Yitong Zhang: School of Physics, Peking University. Ang Li and Yisen Wang: State Key Lab of General Artificial Intelligence, School of Intelligence Science and Technology, Peking University.

## Publication Date

2026-11-10; reviewed v1.

## Venue or Preprint Status

arXiv preprint; no conference acceptance independently verified.

## Paper URL / DOI

[arXiv](https://arxiv.org/abs/2611.13524) · [Full text](https://arxiv.org/html/2611.13524v1) · [arXiv DOI](https://doi.org/10.48550/arXiv.2611.13524).

## Official GitHub Repository

Not verified: no official code URL was found in the primary paper or exact-title repository searches. A missing located repository is not evidence that code does not exist.

## Research Problem

Deployed agents may become cheaper to run while consuming far more resources to obtain their improvements. This study asks whether retained memory, skill search, and harness evolution repay their complete improvement costs over a finite task stream.

## Methodology and Algorithm

For ordered tasks, score each task before using its feedback for later updates. Total token cost is N_total=N_task+N_RSI; the tax rate is N_RSI/N_task. Every attempted update counts, including rejected proposals and repeated validation. Tax calls are assigned to verification, exploration, writing, or a residual, and associated artifacts are tracked for subsequent use. This attribution is descriptive rather than a causal estimate of wasted computation.

## Key Contributions

The contribution combines an explicit end-to-end ledger with a low-cost baseline: Simple Reflection with Notes (SRN). Every four completed tasks, SRN rewrites a note of at most 2,048 tokens from recent failures, without extra candidate rollouts, validation, or retrieval search. Notes then enter task context, so reading them still counts as execution cost.

## Experimental Setup

Two backbones, DeepSeek V4.1 Flash and GPT-6 Luna, execute 105 positions from seven selected 15-task SWE-Chain-Evo chains and 89 Terminal-Bench 2.1 tasks. Chain state resets between repositories; terminal tasks use one fixed order. Six methods produce 2,328 scored method–task pairs with shared initial KIRA agent and nominal task limits.

## Benchmarks and Baselines

Static, ReasoningBank, EvoSkill, Meta-Harness, RRSI, and SRN. Streaming adaptations include re-scoring EvoSkill’s old frontier and a strict-improvement Meta-Harness selector. These differences are part of the evaluated implementation and should accompany comparisons with the original papers.

## Quantitative Results

Table 2: on DeepSeek terminal tasks, SRN scores 78.7% with 214.65M total tokens, versus Meta-Harness 77.5% with 762.57M. Meta-Harness execution alone is cheaper, 184.13M, but adds 578.45M improvement tokens. Mean within-setting total-token reductions for SRN are 65.6%, 71.0%, and 68.2% against Meta-Harness, EvoSkill, and RRSI. Section 5.2 attributes 74.8%, 78.1%, and 93.6% of their aggregate improvement costs to verification.

## Limitations

Two models, selected chains, a single terminal order, and insufficient repeated runs limit generalization. Tokens are not equivalent monetary or compute units across models. An unused artifact may still inform later search; removing its cost is not known to preserve outcomes. The results challenge these implementations, not every possible expensive self-improver.

## Reproducibility

Primary accounting definitions, protocol adaptations, result tables, and limitations were read. Independent reruns were not performed. Without a verified release, exact event-level reconstruction remains unverified; the appendices give accounting conventions and note prompts.

## Open Research Questions

Can an update policy forecast remaining reuse opportunities and choose whether to search, compress memory, or stop? Which verification calls can be removed through controlled interventions without changing final performance?

Primary reading: Sections 2–6; Tables 1–3; Appendices A–D.
