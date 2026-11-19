# Meta-Harness: End-to-End Optimization of Model Harnesses

## Full Paper Title

Meta-Harness: End-to-End Optimization of Model Harnesses

## Authors and Affiliations

Yoonho Lee, Roshen Nair, Qizheng Zhang, Chelsea Finn (Stanford); Kangwook Lee (KRAFTON); Omar Khattab (MIT). Author order: Lee, Nair, Zhang, Lee, Khattab, Finn.

## Publication Date

First submission and reviewed version: 2026-03-30, arXiv v1. Checked against the 2026-11-19 cutoff.

## Venue or Preprint Status

COLM 2026 is reported in the [author project’s BibTeX](https://yoonholee.com/meta-harness/); official proceedings acceptance was not independently verified. An arXiv version is available.

## Paper URL / DOI

[Paper, v1](https://arxiv.org/html/2603.28052v1); [arXiv DOI](https://doi.org/10.48550/arXiv.2603.28052).

## Official GitHub Repository

[stanford-iris-lab/meta-harness](https://github.com/stanford-iris-lab/meta-harness), linked as official code by the author project; a separate [optimized TerminalBench artifact](https://github.com/stanford-iris-lab/meta-harness-tbench2-artifact) is linked in the paper. The main repository contains classification and TerminalBench reference experiments.

## Research Problem

Harness behavior depends on long execution histories. Can a proposer that selectively inspects full prior code, scores, and traces optimize harnesses more effectively than optimizers restricted to summaries or scalar rewards?

## Methodology and Algorithm

For frozen model M, optimize H to maximize expected rollout reward E[r(τ,x)], optionally retaining a score–cost Pareto frontier. A coding-agent proposer navigates a filesystem containing all past candidate programs and traces, writes new single-file Python harnesses, and submits valid candidates to evaluation. No fixed parent-selection rule determines which predecessor must be edited. The proposer is Claude Code with Opus 4.6; the target model can differ. The outer improvement harness itself is not shown undergoing recursive optimization. See §3 and Algorithm 1.

## Key Contributions

The main contribution is a feedback interface and code-space search procedure. Trace-access ablations test whether diagnostic detail matters. Transfer experiments distinguish discovered reusable context algorithms from simply larger prompts; however, the coding experiment is deliberately benchmark-specific discovery.

## Experimental Setup

Text classification uses GPT-OSS-120B with 20 iterations and 40 candidates. Math search uses GPT-OSS-20B, 250 search problems, 40 iterations, and 109 retrieval harnesses; final evaluation covers 200 IMO-level problems with three samples each. The 500,000-plus-example retrieval corpus receives string filtering and manual retrieval checks. Coding searches and evaluates on the same 89 TerminalBench-2 tasks.

## Benchmarks and Baselines

LawBench, Symptom2Disease, USPTO-50k, nine OOD classification datasets; IMO-AnswerBench/IMO-ProofBench/ArXivMath; TerminalBench-2. Baselines include ACE, MCE, few-shot prompting, GEPA, OpenEvolve, best-of-N, and the text-search component of TTT-Discover. Classification optimizer comparisons match proposer and candidate evaluations, not necessarily total tokens.

## Quantitative Results

Author-reported figures; no experiments were independently reproduced.

| Setting | Comparator | Meta-Harness | Source |
|---|---:|---:|---|
| Three classification test sets, accuracy | ACE 40.9% | 48.6% | Table 2 |
| Additional context, thousands of tokens | ACE 50.8 | 11.4 | Table 2 |
| Nine unseen classification datasets | ACE 70.2% | 73.1% | Table 5 |
| Math mean accuracy across five models | No retrieval 34.1%; BM25 37.5% | 38.8% | Table 6 |
| TerminalBench-2, Opus 4.6 | Terminus-KIRA 74.7% | 76.4% | Table 7 |

The paper’s method text includes the search model among five evaluation models, so “five unseen models” overstates model holdout.

## Limitations

TerminalBench search/evaluation overlap invalidates an unseen-task interpretation of its gain. Regex/manual leakage audits do not rule out latent task fitting. Paper Table 7 includes ForgeCode at 81.8%, contradicting an unconditional “best Opus harness” claim on the project page. Filesystem access, coding-agent strength, and flexible search choices co-vary, limiting attribution to trace detail alone. Available diagnostic tokens are not tokens actually consumed.

## Reproducibility

The MIT main repository provides two reference experiments, uv setup, and proposer wrappers. Its release note states the cleaned code was checked for execution only, not full numerical replication. The separate Harbor artifact adds environment bootstrapping over Terminus-KIRA. No code was run here. Preserve model dates, candidate selection, task IDs, and corpus filtering. Project-page context values use characters; paper Table 2 uses tokens.

## Open Research Questions

Under identical aggregate token budgets, does full-history access still outperform a carefully designed summary? Can coding gains survive unseen repositories and benchmarks? How much search cost is recovered when the discovered harness is deployed repeatedly?
