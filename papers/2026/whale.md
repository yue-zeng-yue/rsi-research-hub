# WHALE: A Simple Recipe for Joint Harness-Weight Optimization

Reviewed against primary sources on 2026-11-19. Quantitative findings below are author-reported, not independently reproduced.

## Full Paper Title

WHALE: A Simple Recipe for Joint Harness-Weight Optimization

## Authors and Affiliations

Haechan Kim; Yoonho Lee; Gisang Lee; Chelsea Finn; Kangwook Lee

Haechan Kim: KRAFTON and KAIST. Yoonho Lee and Chelsea Finn: Stanford University. Gisang Lee and Kangwook Lee: KRAFTON.

## Publication Date

2026-08-31; reviewed v1.

## Venue or Preprint Status

arXiv preprint; no conference acceptance independently verified.

## Paper URL / DOI

[arXiv](https://arxiv.org/abs/2609.00196) · [Full text](https://arxiv.org/html/2609.00196v1) · [arXiv DOI](https://doi.org/10.48550/arXiv.2609.00196).

## Official GitHub Repository

[Official implementation](https://github.com/krafton-ai/WHALE); linked in the paper and verified through its README.

## Research Problem

An agent may be limited by model behavior or by the code that exposes observations, parses actions, and controls execution. Improving one component changes the useful search space of the other. The paper studies how to coordinate these two update timescales.

## Methodology and Algorithm

The objective is J(θ,h)=E[R(x,τ)] for trajectories induced by weights θ and executable harness h. WHALE alternates online rejection-sampling fine-tuning under fixed h with Meta-Harness code search under fixed θ. Successful trajectories supply model-generated-token SFT targets. A fixed schedule uses 0.6 training epochs and six search iterations per cycle. An adaptive variant switches after minimum durations and training-score stagnation, without using test or validation scores to trigger switches.

## Key Contributions

The main contribution is a controlled alternation study, including full-program versus prompt-only adaptation and short alternation versus one long weight-then-harness schedule. The proposer and update algorithm remain externally specified; the paper does not train the proposer to become a better optimizer.

## Experimental Setup

Qwen3.5-2B handles search QA and mathematics; Qwen3.5-4B handles chess. Each harness-search pool has 256 training examples. Weight training uses 18,946 QA, 17,917 math, or 16,384 chess examples. Evaluation samples eight trajectories per item; mean@8 is average correctness, not success-at-least-once pass@8. Claude Opus 4.7 proposes harness edits.

## Benchmarks and Baselines

Seven QA test sets total 700 questions; AIME 2024/2025 contribute 60 problems; Lichess contributes 256 disjoint puzzles. Baselines are weight-only, harness-only, stagewise optimization, and an adapted Fast–Slow Training control using the same schedule/operators but restricting edits to prompts.

## Quantitative Results

Appendix C Table 2: fixed-schedule WHALE achieves 48.34%, 24.79%, and 29.83% best mean@8 for QA, math, and chess; weight-only gives 38.27%, 15.42%, and 22.17%, and harness-only 38.29%, 0.42%, and 19.82%. Section 6.2 reports adaptive QA 52.82% and math 26.46%; the best swept fixed math schedule reaches 28.33%, so adaptation is not uniformly best.

## Limitations

Results cover small models and three domains. Curves emphasize best observed test accuracy, which must be distinguished from a preselected final checkpoint. Target-agent rollout counts omit proposer compute, so “fewer rollouts” is not a complete cost comparison. The unstable two-iteration math schedule demonstrates sensitivity to noisy acceptance.

## Reproducibility

Official implementation and primary algorithms/tables were inspected; independent reruns were not performed. Exact search space, verifier, phase budgets, and proposer version are necessary. The reported FST control is an intentionally adapted prompt-restricted comparison rather than an unrestricted reproduction of all FST designs.

## Open Research Questions

Can switching optimize total dollars or GPU time rather than training patience? Can candidate acceptance account for stochastic uncertainty, and can the harness proposer itself learn while maintaining compatibility?

Primary reading: Sections 3–6; Appendix A; Appendix B Table 1; Appendix C Tables 2–3.
