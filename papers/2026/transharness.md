# TransHarness

**Review date:** 2026-11-28. **Evidence:** Primary-reviewed; numerical results are author-reported.

## Full Paper Title

TransHarness: From Benchmark Overfitting to Transferable Harness Evolution.

## Authors and Affiliations

In source order: Tianze Xia, Zimo Wang, and Heng Tong (Huazhong University of Science and Technology); Zhaoxiang Liu and Shiguo Lian (Unicom Data Intelligence, China Unicom); Fan Huang (Xiamen University); Wenyu Liu (Huazhong University of Science and Technology); Yunchao Wei (Beijing Jiaotong University); and Xinggang Wang (Huazhong University of Science and Technology). Affiliations follow the versioned title page.

## Publication Date

First submitted 2026-11-25 at 04:15:25 UTC. The arXiv history lists only v1 at the review cutoff.

## Venue or Preprint Status

arXiv preprint (cs.AI). Peer-reviewed acceptance: **Not verified**; the source does not identify a proceedings record and exact-title discovery did not establish one.

## Paper URL / DOI

[Canonical record](https://arxiv.org/abs/2611.33757) · [Reviewed v1](https://arxiv.org/html/2611.33757v1) · [arXiv DOI](https://doi.org/10.48550/arXiv.2611.33757). The arXiv record marks registration as pending; this is not a venue DOI.

## Official GitHub Repository

**Not verified**. The inspected paper links upstream harnesses but not a paper-specific implementation; exact-title searches did not identify an author-linked TransHarness release. Upstream harness availability does not supply the evolved interventions or their validation pipeline.

## Research Problem

A coding harness optimized against one task distribution can regress on another. The paper asks whether reusable run-time intervention policies can transfer from separate source tasks to established coding and terminal benchmarks without changing the executor's weights or sacrificing too many baseline successes.

## Methodology and Algorithm

Sections 3.1–3.4 and Algorithm 1 construct candidates from contrasting successful and failed trajectories on the same task. Each author starts with the base harness and proposes an insertion point, an executable trigger over observable history, and diagnostic guidance. A reviewer can revise wording or request one rework; implementation checks test control flow. Cross-task replay of other archived source pairs checks trigger selectivity without claiming to measure counterfactual rescue. For event-triggered policies, the replay gate rejects activation in both trajectories on at least 90% of pairs or activation on successful-only pairs more often than failed-only pairs. Independent semantic review checks the diagnosis, its independence from the source solution, and whether the guidance is grounded in the current task. Session-start guidance is assessed separately from event-trigger counts. Surviving policies are composed in source order and frozen before target execution. The paper does not update the weights or improve the candidate-authoring procedure over successive generations.

## Key Contributions

The authors combine trace contrasts, executable interception, stored-trace replay and a semantic gate. The distinctive combination is selective timing plus evidence-directed reassessment under cross-benchmark evaluation; contrastive traces and validation gates are not new by themselves. Section 3.2 decomposes net binary gain into recovered baseline failures minus disrupted baseline successes under the stated coupling. Observed activation is not equivalent to causal intervention value.

## Experimental Setup

Sections 3.4 and 4.1 use 100 source tasks from SWE-bench Pro, covering 11 repositories; three runs of each base configuration per task supply 300 archived trajectories. The reported target panels contain 113 DeepSWE v1.1 tasks and 89 Terminal-Bench 2.1 tasks, with three evaluation runs. The source shares none of the DeepSWE repositories according to Section 4.2, not necessarily none of the underlying model pretraining data. Executors include DeepSeek V4.1 Flash (1017), GLM-5.3 Flash, and Qwen3.8-Flash-Next across lightweight and native harnesses. In paired base-versus-evolved tests the authors hold settings, tools, environment, and execution limits fixed. Appendix C.4 notes a separately versioned September executor for the DeepSeek Harness source collection. Distinct author, reviewer, and selector roles do not imply statistically independent errors.

## Benchmarks and Baselines

DeepSWE uses Mini-SWE and native harnesses; Terminal-Bench uses Terminus 2 and native harnesses. The method comparison uses Mini-SWE 2.4.6, DeepSeek V4.1 Flash (1017), and a shared source archive for TransHarness, Meta-Harness, Self-Harness and RRSI. Search budgets differ. No RRSI candidate passed its own gate, so the authors evaluated a source-ranked candidate rather than an accepted update. Public leaderboard rows in Table 1 are contextual, not matched engine or sampling comparisons.

## Quantitative Results

- On the DeepSWE panel above, the DeepSeek V4.1 Flash (1017) Mini-SWE comparison averages **73.2% base versus 76.4% evolved** across three paired runs (Table 2; Appendix C.6). Recovery and regression contribute **+13.0 and −9.7 percentage points** over all paired executions, not rates conditional on the corresponding starting outcome. The paired task-bootstrap 95% interval for the net gain is **[−2.4, 8.8] points**. Independent rounding explains the small discrepancy between displayed components and net gain.
- With DeepSeek V4.1 Flash (1017) and DeepSeek Harness on the 89 Terminal-Bench 2.1 tasks, the corresponding three-run score is **89.9% versus 95.5%**, with paired gain interval **[−1.1, 12.4] points** (Table 1; Appendix C.3). Neither interval rules out zero. The two scores use different harnesses and target panels.
- On the same DeepSWE method-comparison configuration, moving the same guidance to the first eligible event gives **72.6% versus 76.4%** for learned timing; regression contributions are **−13.3 versus −9.7 points** (Table 4, three-run target protocol). In the source-budget ablation, 25 and 50 source tasks with three trajectories per task yield scores below the base (Section 4.5, Table 3). Appendix C.4, Table 10 records **132.7M** construction and validation tokens for a separate archived replay construction run versus **798.1M** for the Meta-Harness adaptation with 200 fresh scored source runs. These method-specific budgets count cached inputs once and exclude shared archive collection and target evaluation; they are not matched total cost.

## Limitations

The paired intervals include zero for the highlighted configurations, and source downsampling produced negative transfer. The source suite and target suites remain concentrated in executable coding and terminal work; cross-benchmark does not imply arbitrary domain transfer. The authors report three target repetitions, not three independent full searches. Replay measures activation on historical paths, not how a new policy changes subsequent states. Section 4.5 and Appendix C qualify resource counts and appendix baselines; total archive cost, run-time overhead, and author/selector error correlation remain open. There is no late-versus-early improver comparison.

## Reproducibility

The paper provides gate rules, source selection, scoring conventions, and paired target outcomes in its appendices. **Not verified:** public release of the selected rules, exact archived traces and author/selector runtime, or a complete command for the reported search. Compare a frozen rule set with identical starting harness and source archive, logging end-to-end cost and paired target outcomes. No implementation was executed and no result was independently reproduced here.

## Open Research Questions

Can an independently calibrated selector preserve rescues while reducing disruption to already successful traces under task-family and executor shift? Compare replay plus semantic review against an equal-total-cost incumbent, with the same candidate pool and a sealed target audit. [AHE-Beta](ahe-beta.md), [Rethinking Evaluation](rethinking-evaluation.md), and [The Resolution Hypothesis](resolution-hypothesis.md) are close comparators for requirement-driven updates, held-out testing, and identifying small gains. Treat failure to improve the paired interval or the cost–risk trade-off as disconfirming evidence. This is a proposed test, not a result.
