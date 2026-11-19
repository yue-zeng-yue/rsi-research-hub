# A Self-Improving Coding Agent

## Full Paper Title

A Self-Improving Coding Agent.

## Authors and Affiliations

Maxime Robeyns and Laurence Aitchison: University of Bristol. Martin Szummer: iGent AI. Affiliations follow the primary paper.

## Publication Date

First arXiv submission: 21 April 2025. Reviewed revision: v2, 16 May 2025. Evidence cutoff: 19 November 2026.

## Venue or Preprint Status

An [ICLR 2025 SSI-FM workshop paper](https://openreview.net/pdf?id=rShJCyLsOr) is linked by the official repository. The reviewed arXiv revision says it was submitted as a preprint to NeurIPS 2025; NeurIPS acceptance is **Not verified** and is not implied by that statement.

## Paper URL / DOI

[Version-pinned paper](https://arxiv.org/html/2504.15228v2); [arXiv DOI](https://doi.org/10.48550/arXiv.2504.15228).

## Official GitHub Repository

[MaximeRobeyns/self_improving_coding_agent](https://github.com/MaximeRobeyns/self_improving_coding_agent), explicitly linked by the paper. Inspected revision: `ed8275dca4d3c5dbf77229964351fe9b424797dc`.

## Research Problem

Can an agent improve its own executable orchestration and tools using benchmark feedback, without modifying the underlying language-model weights or relying on a separate, permanently fixed coding improver?

## Methodology and Algorithm

The outer loop selects the archived agent with highest utility, lets that agent inspect its own code and previous outcomes, applies its proposed changes, evaluates the result, and extends the archive. The selected agent is both modifier and modification target. Utility combines performance p with clipped cost and time rewards:

U=0.5p+0.25[1−min(1,cost/$10)]+0.25[1−min(1,time/300s)].

Timeouts halve utility. The initial implementation already includes file/shell tools, coding and reasoning subagents, archive analysis, and an asynchronous overseer. File-context and cache management are editable implementation choices. The fixed outer selection/evaluation procedure remains outside this demonstrated recursion. See [§3](https://arxiv.org/html/2504.15228v2#S3).

## Key Contributions

SICA demonstrates executable, non-gradient self-modification across tools and orchestration. Its improvement history includes efficient editing, context management, verification, and symbol-location changes. It supplies an inspectable early example of a solver improving the code subsequently used to modify itself.

## Experimental Setup

The main run uses Sonnet 3.5 v2 for most agents and o3-mini for a reasoning subagent. Fifteen improvement iterations cost approximately $7,000 in API usage. The evaluation panel contains a fixed random 50-question SWE-bench Verified subset, 50 LiveCodeBench questions, and synthetic file-editing and symbol-location tasks. The latter are constructed from repositories and commits (§4).

## Benchmarks and Baselines

The primary comparator is the initial agent, with intermediate archived versions showing trajectories. SWE-bench results concern the selected subset, not the full benchmark. Repeated use of this panel guides selection; an untouched final holdout is **Not verified**. The main trajectory does not isolate recursion against a matched-budget frozen-improver baseline.

## Quantitative Results

All values are **author-reported**. Table 1 reports averages over benchmark instances; no independent reproduction was run.

| Metric and condition | Initial, iteration 0 | Peak-SWE iteration 14 | Final iteration 15 | Source |
|---|---:|---:|---:|---|
| SWE-bench subset accuracy | 17% | 53% | 51% | Table 1 |
| LiveCodeBench subset accuracy | 65% | 67% | 71% | Table 1 |
| Mean cost per problem | $1.91 | $2.20 | $1.70 | Table 1 |
| Mean time per problem | 130.2 s | 117.1 s | 114.5 s | Table 1 |

The best SWE result and the final cost/LiveCodeBench results come from different versions and should not be combined into one operating point.

## Limitations

The five-minute timeout makes efficient editing unusually consequential; the authors explicitly attribute much early improvement to this constraint. Idea generation is path-dependent, and bad early proposals can shape later search. One main trajectory cannot establish repeatability, causal improvement of the improver, or accelerating returns. Selection on a small reused panel permits benchmark adaptation and checkpoint-selection effects.

## Reproducibility

The repository provides Docker-based setup, model-provider configuration, evaluation entry points, and interactive traces. Proprietary APIs, exact data sampling, and the substantial reported budget remain dependencies. Successful installation or reconstruction of the full run is **Not verified**; this review inspected sources only.

## Open Research Questions

Does a later agent improve identical starting agents more effectively than the initial agent at equal search cost? Do tool gains persist with longer timeouts and new repositories? How much variance comes from early proposal choices across complete independent loops?
