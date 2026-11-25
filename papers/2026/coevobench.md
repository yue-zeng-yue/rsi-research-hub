# CoEvoBench

**Reviewed:** 2026-11-25. **Evidence:** Primary-reviewed; all experimental results remain author-reported. No independent run.

## Full Paper Title

CoEvoBench: Can LLMs Drive Recursive Co-Evolution of Agentic Systems?

## Authors and Affiliations

Chuan Xiao, Baojie Wang, Haizhao Fan, Hongzhe Du, and Xander Xu. The title block lists Zhejiang University, Alibaba Group, and Shanghai Jiao Tong University. Individual affiliation mapping is **Not verified** because the inspected HTML loses the author superscripts.

## Publication Date

First submitted 2026-11-20, 04:40:59 UTC. Reviewed v1; no later revision appeared in the inspected record.

## Venue or Preprint Status

arXiv preprint. Peer-reviewed acceptance: **Not verified**; no venue record was established.

## Paper URL / DOI

[Canonical record](https://arxiv.org/abs/2611.27116) · [Reviewed v1](https://arxiv.org/html/2611.27116v1). The record lists `10.48550/arXiv.2611.27116` with registration pending.

## Official GitHub Repository

[AlibabaResearch/CoEvoBench](https://github.com/AlibabaResearch/CoEvoBench), linked by the paper; inspected commit `d39a924c8985806933c94777d8e969d6e756262c`. The [pinned README](https://github.com/AlibabaResearch/CoEvoBench/blob/d39a924c8985806933c94777d8e969d6e756262c/README.md) describes a substantive but incomplete implementation: current images lack completed Docker/GPU acceptance, and operator final evaluation and comparison have unresolved integration and integrity issues.

The inspected [BFCL provenance module](https://github.com/AlibabaResearch/CoEvoBench/blob/d39a924c8985806933c94777d8e969d6e756262c/src/coevobench/bench/bfcl/provenance.py) validates source hashes while explicitly distinguishing reconstructed implementation from unverified historical equivalence. Public code is therefore not evidence that the paper's exact runs can already be reproduced.

## Research Problem

Evaluate a research agent choosing between model training and harness modification, including whether successive decisions produce additional gains.

## Methodology and Algorithm

Researchers modify a target pair using visible tasks and score-only selection feedback, then freeze a submission for separate testing. The benchmark audits development histories. Its main sanction replaces contaminated weights with base weights while retaining the final harness; a stricter sensitivity analysis discards both. See Sections 3 and 5 and Appendix 19.

## Key Contributions

The useful addition is an evaluation setting where component choice is itself a research decision. **Review assessment:** compare this with [JoMoHa](jomoha.md), which supplies an optimization method. A benchmark exposing both components does not establish that its researcher learns a better improvement algorithm.

## Experimental Setup

Five researcher configurations, two target families, and three development runs per researcher–domain pair. Each run permits 24 hours, four H20 GPUs, and a $100 teacher allowance; researcher API expenditure is separate. Section 4 and Appendix 14 distinguish these costs.

## Benchmarks and Baselines

SWE-bench Verified, TB-Lite, AppWorld easy, telecom, and BFCL-V4. Controls include initial pairs, instruction-tuned reference pairs, and component swaps. The [README's pinned split table](https://github.com/AlibabaResearch/CoEvoBench/blob/d39a924c8985806933c94777d8e969d6e756262c/README.md) identifies subsets; these are not interchangeable with full public leaderboards.

## Quantitative Results

Table 1, Qwen3.5-9B target, weighted aggregate: base **1.09**, GPT-6 Astra researcher **31.23**, reference **37.42**. These are percentage-scale scores, not ordinary mean success. The derived gap closure is `(31.23 - 1.09) / (37.42 - 1.09) = 82.96%`.

Section 5.1 finds gains concentrated early, while later gains still occur. Its illustrated trajectories are selected examples; they do not establish that every run stops improving after one step.

## Limitations

**Review analysis:** distinguish a weak initialization from a competitive deployment baseline. Gap-normalized weighting also gives different importance to domains; inspect individual results before using the aggregate to select an environment.

Holding GPU time fixed does not equalize researcher-token cost or CLI behavior. The model–CLI pair is the evaluated researcher, so attributing all differences to model intelligence would exceed the comparison.

Replacing compromised weights cannot prove that retained harness decisions were unaffected by prohibited information. The stricter audit analysis is valuable; a reproduction should report both treatments and retain violation counts. Likewise, selected trajectory illustrations should not be interpreted as the distribution of all runs. Evidence of later gains is distinct from evidence of improving a common starting agent more efficiently.

## Reproducibility

Inspected methods, main tables, cost accounting, repeated-evaluation and audit appendices, the pinned README, and BFCL provenance code. No dependencies, benchmark environments, or experiments were executed. Historical artifact equivalence and complete end-to-end acceptance remain **Not verified**.

## Open Research Questions

Can a compatibility predictor choose the next intervention better than a scalar gate at equal total cost? Freeze a candidate pool, compare selectors, and then test prospectively with independent search seeds. Include a fixed researcher and common starting states before claiming improved improver quality. This updates the nearest-work analysis in the [compatibility proposal](../../research/model-harness-compatibility.md).
