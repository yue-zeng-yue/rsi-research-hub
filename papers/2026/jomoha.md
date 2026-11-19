# JoMoHa: Joint Model–Harness Optimization with Reinforcement Learning

Reviewed against primary sources on 2026-11-19. Quantitative findings below are author-reported, not independently reproduced.

## Full Paper Title

JoMoHa: Joint Model–Harness Optimization with Reinforcement Learning

## Authors and Affiliations

Xudong Wu; Guangchen Lan; Mingqi Yuan; Jiayu Chen

Xudong Wu, Mingqi Yuan, and Jiayu Chen: The University of Hong Kong. Guangchen Lan: Salesforce AI Research.

## Publication Date

2026-11-08; reviewed v1.

## Venue or Preprint Status

arXiv preprint; no conference acceptance independently verified.

## Paper URL / DOI

[arXiv](https://arxiv.org/abs/2611.11499) · [Full text](https://arxiv.org/html/2611.11499v1) · [arXiv DOI](https://doi.org/10.48550/arXiv.2611.11499).

## Official GitHub Repository

[Author-linked code](https://github.com/xudongwu-0/coevolve); README identifies JoMoHa and exposes implementation instructions.

## Research Problem

Alternating model and runtime updates can damage both execution compatibility and the model trained from those executions. The paper asks whether learning the harness writer alongside the task solver prevents this mismatch better than a frozen external editor.

## Methodology and Algorithm

Two policies, Engineer and Solver, share terminal reward E[R] but train on their own generated tokens. The Engineer emits executable harness code, validated before execution; invalid proposals fall back to the base executor. SAO-based actor–critic updates use separate critics, collaboration context supplied only to critics, per-role return normalization, and partner-trajectory likelihood weights clipped to [0.5,2]. A joint, joint, Solver-only schedule gives a 2:3 Engineer:Solver update ratio. No differentiation through generated code is required.

## Key Contributions

It makes program generation trainable, adds coordination mechanisms, and uses saved-program/model cross-comparisons to separate improved model ability from runtime usefulness. These controlled swaps are more informative than a rising joint learning curve alone.

## Experimental Setup

The ALFWorld coordination study uses separate Qwen3.5-9B-class actors and critics initialized from Agent SFT, eight paired episodes per round, and 144 rounds. Validation is separate from training/test. Most external baseline numbers are inherited from Harness-R1; JoMoHa and its adapted WHALE comparison are locally evaluated by the authors.

## Benchmarks and Baselines

ALFWorld, WebShop, and DBBench; comparisons include weight-only, harness-only, Frozen Engineer, Agent SFT + Harness-R1, WHALE, and Joint-only. WHALE matches environment interactions and switches after eight interactions, but retains its RSFT-plus-search character.

## Quantitative Results

Table 4 gives success 97.0%, 45.8%, and 68.0%, averaging 70.3%, versus 63.1% average for WHALE. Frozen Engineer reaches 90.5% at ALFWorld round 144, compared with 97.0% jointly trained. Table 6 gives Joint-only 88.5%; individual coordination additions reach 91.5–92.5%. Table 5 fixes the later solver: initial program 92.5%, later program 96.5%, no harness 91.5%.

## Limitations

Coordination ablations and diagnosis center on ALFWorld; three benchmarks do not establish general-purpose programming performance. Several baselines are imported rather than rerun in one stack. The article does not report broad repeated-seed uncertainty or full end-to-end monetary cost. The long-phase alternating collapse is evidence about that implementation, not all alternating algorithms.

## Reproducibility

The full primary method, tables, and official README were checked; independent reruns were not performed. Reproduction should preserve the paired Engineer/Solver samples, code fallback behavior, reference policies, critic context, schedule, and checkpoint-selection protocol. The later-program swap score 96.5% is a different diagnostic setting from the headline 97.0%.

## Open Research Questions

Can collaboration-aware critics generalize across partner checkpoints and tasks? Would fewer expensive executions suffice with calibrated off-policy reuse? How stable is the shared sparse reward when harness changes affect observation semantics?

Primary reading: Sections 3–7; Tables 2–6; Algorithm 1.
