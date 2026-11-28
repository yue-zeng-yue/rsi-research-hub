# EvoLink-Bench

**Review date:** 2026-11-28. **Evidence:** Primary-reviewed; scores are author-reported. Selected released source files were inspected but not executed.

## Full Paper Title

EvoLink-Bench: A Benchmark for Evaluating Self-Evolving Agents in Long-Horizon Interdependent Task Streams.

## Authors and Affiliations

Wei Chen, Xiaodong Lu, Weihao Shen, Gongxun Li, Xingyu Guo, Qihang Sun, Fuwei Zhang, Zhao Zhang, Yikun Ban, Shuang Li, Deqing Wang, and Fuzhen Zhuang, all listed under Beihang University on the v1 title page.

## Publication Date

First submitted 2026-11-25 at 14:00:22 UTC. The v1 title page is dated November 24; that is not the first public submission date. The arXiv history lists only v1 at the review cutoff.

## Venue or Preprint Status

arXiv preprint (cs.AI). Peer-reviewed acceptance: **Not verified**; no proceedings or acceptance record was established by exact-title discovery.

## Paper URL / DOI

[Canonical record](https://arxiv.org/abs/2611.34400) · [Reviewed v1](https://arxiv.org/html/2611.34400v1) · [arXiv DOI](https://doi.org/10.48550/arXiv.2611.34400). The arXiv record marks registration as pending; this is not a venue DOI.

## Official GitHub Repository

The paper title page links [EvoLink-Bench](https://github.com/BUAA-Self-Evolving/EvoLink-Bench); the author repository links the same arXiv record. Inspected [commit 110adacd](https://github.com/BUAA-Self-Evolving/EvoLink-Bench/tree/110adacd7339040a12ecacd8da795d9fcbd0d21f), including the runner, audit script and reproduction instructions. This is a substantive runtime release, not a complete archive of paper runs.

## Research Problem

An agent can retry a task, carry forward a file, or modify its learning state without becoming better at future tasks. The benchmark asks whether an agent uses past information and executable artifacts under delayed, interdependent demands. It is an evaluation protocol, not itself a new learning or model-training algorithm.

## Methodology and Algorithm

Sections 3–4 construct ordered task streams with distractors and dependencies. L1 tests acquisition, revision and application of facts, preferences and rules. L2 tests executable task behavior, including code, data and research artifacts. Reset reinitializes workspace and agent state and disables explicit post-turn updates; Frozen retains permitted state with updates disabled; Evolving retains that state and enables post-turn updates only where an adapter implements them. Task retries respond to public feedback and are distinct from an adapter update after the turn. Scoring separates last-submission reward, retries, state changes, and later probe performance; a file digest confirms persistence, not causal use.

## Key Contributions

The authors distinguish ordinary work products from deliberate learner-state changes and add probes after interdependent tasks. Combining controlled retention conditions with artifact dependencies is useful for testing the product of adaptation. The design does not, by itself, measure whether the improver becomes more capable from identical starting states.

## Experimental Setup

Section 5.1 evaluates DeepSeek V4 Flash and GLM-5.3 locally and GPT-6.1 Terra by API. Four frameworks recur in all three backbone configurations: Hermes, Prime Agent, Adaptive Auto-Harness and OpenCode. A fifth framework varies by backbone: DeepSeek Harness, ZCode and Codex respectively. DeepSeek and GLM each use 181 L1 turns across 10 streams and 144 L2 turns across 10 streams per framework–condition pair; Terra uses 369 L1 and 290 L2 turns across 20 and 24 streams. The total of 19,635 is a count of scored positions across conditions and frameworks, not distinct tasks. Appendix A distinguishes declared L1 task ceilings (12 model calls, 16 tool calls, 600 seconds) and task-specific L2 CPU ceilings (600–3,600 seconds) from actual use across runtime revisions. Exact matched total usage and repeated-run uncertainty are not available.

## Benchmarks and Baselines

L1 includes tasks adapted from ClawArena and dialogue streams; L2 uses execution-oriented tasks, including selected CPU AutoResearch. The construction also describes artifact-dependency, GPU and cross-benchmark streams, but the DeepSeek and GLM selections omit those dedicated panels. Compare conditions within the same backbone and framework, separately for L1 and L2. Reset is a no-retention comparator, Frozen a no-explicit-update comparator. OpenCode, DeepSeek Harness and ZCode lack an enabled native learner in the audited local configurations; their Evolving label does not imply an actual treatment.

## Quantitative Results

- For DeepSeek V4 Flash with **Prime Agent**, the mean last-submission reward on the 0–100 scale changes from **70.83 Frozen to 64.09 Evolving on L1**, but **52.58 to 67.35 on L2** (Table 2 and Section 6.2). These compare the selected 181 and 144 turn panels respectively, with state kept in both conditions and a post-turn learner enabled only in Evolving. There are no certified matched real-use budgets or repeated-run intervals.
- For **DeepSeek V4 Flash with Adaptive Auto-Harness**, the L2 Evolving-minus-Frozen difference is **+1.23 score points** across all 144 turns per condition but **+13.27** on the 30 final probe tasks per condition (Sections 5.5 and 6.3). This is a descriptive difference between two aggregates under the same section-specific protocol, not an isolated causal effect of a particular saved update.
- In the DeepSeek V4 Flash selected L1/L2 cohort pooled across frameworks and conditions, **327 of 1,321** executions entering a retry ultimately pass (**24.75%**, Section 5.4); this is conditional retry recovery under the recorded bounded submission protocol, not a pass rate over all tasks, nor evidence of improvement across turns.

## Limitations

Section 6.5 discusses uneven cohort coverage, recorded runs from several runtime revisions, incomplete cost information and absent repeat uncertainty. Backbone rankings would confound task and integration changes. Even within one backbone, the condition contrasts are descriptive rather than randomized causal estimates. Probe counts are small and may reflect previously produced artifacts, not generalized competence. This review does not infer that a framework's runtime label proves it updated or that any update made its next update better.

## Reproducibility

At the pinned source, the runner implements condition-aware state and learner handling, and the audit script checks recorded scoring evidence. The README links an external dataset download while the [reproduction guide](https://github.com/BUAA-Self-Evolving/EvoLink-Bench/blob/110adacd7339040a12ecacd8da795d9fcbd0d21f/docs/reproduction.md) says a versioned paper dataset and historical runs are not bundled and does not identify a public download. **Not verified:** whether the linked package matches the paper's historical task, verifier, runtime and results manifests. Private grading assets and exact launch configurations cannot be inferred from the checkout. Neither the offline example nor any model-backed benchmark was run for this review.

## Open Research Questions

Can a same-start fork isolate the value of one retained update from ordinary artifact retention? Compare frozen and updated states using identical workspace snapshots, budgets, task order, and repeated seeds; randomize update exposure and audit dependence on logged artifacts separately. Use [SIM](sim.md) and [Auditing the Product](auditing-product-recursion.md) as close comparators for optimizer memory and clean-start improver evidence. Improvement only on tasks that replay an existing artifact would not support a general capability claim.
