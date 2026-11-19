# RRSI: Regularized Recursive Self-Improvement of Agent Harnesses

## Full Paper Title

RRSI: Regularized Recursive Self-Improvement of Agent Harnesses

## Authors and Affiliations

Peng Xia; Rujun Han; Zifeng Wang; Yanfei Chen; Yufan Zhuang; Yoonho Lee; Chengsong Huang; Han Yu; Zhongying CuiZhu; Yifei Ming; Huaxiu Yao; Burak Gokturk; Tomas Pfister; Chen-Yu Lee. Google Cloud AI Research except Lee (Stanford), Huang (Washington University in St. Louis), and Yao (UNC-Chapel Hill); Xia worked as a Google student researcher. v1’s Yufan Zhang spelling is superseded by v3’s Yufan Zhuang.

## Publication Date

First submitted 2026-09-21; reviewed v3 submitted 2026-10-04; cutoff 2026-11-19.

## Venue or Preprint Status

arXiv preprint; conference/journal acceptance not verified.

## Paper URL / DOI

[Paper, v3](https://arxiv.org/html/2609.24972v3); [arXiv DOI](https://doi.org/10.48550/arXiv.2609.24972).

## Official GitHub Repository

[google-research/rrsi](https://github.com/google-research/rrsi), explicitly linked in the paper; [official project](https://regularized-rsi.com/).

## Research Problem

Repeated selection on finite evolution tasks can reward benchmark-specific edits, random winners, and expensive machinery. Can search regularization preserve useful transfer without constraining the entire harness to a fixed template?

## Methodology and Algorithm

RRSI leaves the edit space open but limits the search trajectory. A cosine-annealed cardinality budget caps independently attributable edits: b_t = ceil[b_min +(b_max−b_min)(1+cos(πt/T))/2]. History records hypotheses, diffs, scores, costs, and rejections; stalls allocate exploration toward unused components. Before evaluation, a critic rejects benchmark-specific contents. Acceptance requires score at least S_best−δ, where δ is estimated from repeated base evaluations. For gains ΔS>δ, relative token growth must satisfy ΔC≤β0+β1ΔS; separate rules handle within-noise candidates. Unproductive components become deletion targets. L0/L1/L2 terminology denotes analogies, not optimization of literal norm penalties. See §3 and Appendix D.

## Key Contributions

The central contribution is explicit control of update size, leakage, noise, and cost with transfer-oriented evaluation. The results separate improvements on the evolution set from changes on pristine ID and OOD datasets.

## Experimental Setup

Claude Opus 4.8 is the principal frozen executor, proposer, analyst, and critic. Coding evolves on 89 Terminal-Bench 2.1 tasks; legal workspace evolution uses 120 Harvey LAB tasks with 40 held out; engineering uses 61 EngDesign tasks. Five OOD benchmarks are evaluated unchanged. Baselines share initial harness, policy, evolution set, and candidate budget.

## Benchmarks and Baselines

Meta-Harness, AHE, TTHE, HarnessX, unregularized evolution, and proposal/acceptance ablations. OOD evaluation covers SWE-bench Verified, JobBench, GDPval, APEX-Agents, and Frontier-Eng. Judge-scored workspace outcomes and simulator-scored engineering outcomes provide different feedback regimes.

## Quantitative Results

Author-reported; no independent reproduction.

| Setting / metric | Base | Comparator | RRSI | Source |
|---|---:|---:|---:|---|
| Workspace OOD mean | 39.7 | Unregularized 40.3 | 43.6 | Table 2 |
| Policy tokens/trial, millions | 1.56 | Unregularized 3.80 | 2.42 | Table 2 |
| Harvey LAB evolve score | 89.4 | Meta-Harness 93.0 | 90.5 | Table 1 |
| JobBench OOD score | 36.0 | Meta-Harness 37.1 | 40.7 | Table 1 |
| SWE-bench Verified, Opus | 82.0 | — | 83.8 | Table 3 |

The v3 JobBench table gives +4.7 points despite the abstract’s “up to 4.3” headline. Prefer the scoped table values.

## Limitations

RRSI remains about 55% more expensive per workspace trial than H0, despite saving about 36% against unregularized evolution. Matching candidate counts does not match critic/analysis expenditure. A noise band measured on H0 may miscalibrate later, more stochastic candidates; multiple adaptive comparisons remain. Atomic-edit counting is semantic and critic-dependent. Transfer gains show finite generalization, not a guarantee against hidden leakage or long-run drift.

## Reproducibility

The Apache-2.0 repository documents separate coding/workspace/engineering adapters, baseline/run/heldout commands, a stopping mechanism, and core tests. Code accessibility was verified; commands and scientific results were not executed. Replication should pin cost accounting, δ estimation, candidate budgets, pruning windows, and all judge/model snapshots.

## Open Research Questions

Which regularizer independently changes held-out performance under equal dollars? Can leakage screening detect implicit memorization? Would fresh validation rotations or formal sequential-testing controls outperform a fixed noise band as the harness distribution evolves?
