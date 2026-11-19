# Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents

## Full Paper Title

Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents

## Authors and Affiliations

Jenny Zhang; Shengran Hu; Cong Lu; Robert Lange; Jeff Clune. The reviewed arXiv byline lists University of British Columbia and Vector Institute for Zhang, Hu, Lu, and Clune; Sakana AI for Hu, Lu, and Lange; Canada CIFAR AI Chair for Clune. OpenReview renders Lange as Robert Tjarko Lange.

## Publication Date

First submitted 2025-05-29; reviewed arXiv v3, submitted 2026-03-12. Literature cutoff: 2026-11-19.

## Venue or Preprint Status

ICLR 2026 Poster, supported by the official OpenReview author-results listing; the individual forum currently presents a browser-verification challenge. [Conference record](https://openreview.net/forum?id=pUpzQZTvGY).

## Paper URL / DOI

[Paper, v3](https://arxiv.org/html/2505.22954v3); [arXiv DOI](https://doi.org/10.48550/arXiv.2505.22954).

## Official GitHub Repository

[jennyzzt/dgm](https://github.com/jennyzzt/dgm), explicitly linked in the paper. The repository supplies the search implementation and links experiment logs.

## Research Problem

Can a coding agent autonomously improve its own implementation without requiring formal proofs that each rewrite is beneficial? A second issue is whether retaining mediocre intermediate agents helps discover improvements that greedy replacement misses.

## Methodology and Algorithm

The mutable object is Python agent code around frozen foundation models. A parent diagnoses benchmark traces, receives a proposed engineering task, and edits its own repository. Candidates must compile and retain editing functionality before entering an expanding archive. Parent sampling favors performance and underexplored lineages while retaining nonzero probability for other candidates. This permits a temporarily worse descendant to become a useful stepping stone. Archive management and instruction-generation machinery remain fixed; empirical evaluation replaces the Gödel Machine’s proof requirement. See §3 and Appendix C.

## Key Contributions

The contribution is an executable self-modification loop with an archive, accompanied by ablations and cross-model/cross-benchmark transfer. It establishes bounded agent-code improvement, not a theorem of beneficial rewrites or indefinite acceleration.

## Experimental Setup

Eighty generated agents per run; two concurrent iterations for SWE-bench and four for Polyglot. Claude 3.5 Sonnet (New) performs modification; evaluation uses that model for SWE-bench and o3-mini for Polyglot. Staged screening uses 10 tasks, expanded subsets, and 200 SWE-bench tasks for strong candidates. Appendix E.1 estimates about $22,000 and two weeks for a SWE-bench campaign versus about $10,000 for each principal ablation.

## Benchmarks and Baselines

SWE-bench Verified subsets and Aider Polyglot; controls fix the modifying agent or remove the archive. Appendix C adds greedy parent selection. Aider and open coding-agent comparisons are contextual baselines, not universal compute-matched controls.

## Quantitative Results

All results are author-reported; no experiment was independently reproduced.

| Condition / metric | Comparator | DGM | Source |
|---|---:|---:|---|
| SWE-bench, 200-task reported evaluation | Initial 20.0% | 50.0% | §4.2–4.4, Fig. 2 |
| Full Polyglot success | Initial 14.2% | 30.7% | §4.4 |
| Polyglot search subset, 50 tasks | Initial 14.0% | 38.0% | §4.4 |
| SWE-bench, greedy-selection ablation | Greedy 39.7% | 50.0% | Appendix C, Table 1 |

The subset and full-Polyglot figures must not be interchanged.

## Limitations

The prominent SWE-bench figure is neither a fresh 500-task test nor a compute-matched estimate of self-improvement efficiency. Repeated subset selection permits adaptive overfitting; additional transfer evidence is stronger than the search score but still finite. Improvements may increase inference expenditure. Coding competence is used as a proxy for modification competence, which need not hold outside coding. A valid executable edit is not proof of a causal or safe improvement.

## Reproducibility

The author repository documents Docker, Python dependencies, Polyglot preparation, DGM_outer.py, and external model-output logs; its badge states Apache-2.0. API availability, model revisions, staged task lists, seeds, and full proposal/evaluation costs must be pinned. Code availability was checked; installation, artifact completeness, and numerical reproduction were not verified.

## Open Research Questions

Does archive search still win when API dollars and evaluation calls are matched? How much improvement survives a permanently sealed task distribution? Can the system improve its selection mechanism, or does progress depend mainly on spending more computation through a fixed outer loop?
