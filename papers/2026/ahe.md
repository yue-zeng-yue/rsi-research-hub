# Agentic Harness Engineering: Observability-Driven Automatic Evolution of Coding-Agent Harnesses

## Full Paper Title

Agentic Harness Engineering: Observability-Driven Automatic Evolution of Coding-Agent Harnesses

## Authors and Affiliations

Jiahang Lin, Shichun Liu, Shihan Dou, Zhiheng Xi, Xuanjing Huang, Tao Gui, Yu-Gang Jiang (Fudan University); Chengjun Pan (Peking University); Lizhi Lin, Hang Yan, Zhenhua Han (Shanghai Qiji Zhifeng Co., Ltd). Author order: Lin, Liu, Pan, Lin, Dou, Xi, Huang, Yan, Han, Gui, Jiang. The reviewed v4 includes Xi and Jiang, absent from earlier versions.

## Publication Date

First submitted 2026-04-28; reviewed arXiv v4 submitted 2026-05-18; cutoff 2026-11-19.

## Venue or Preprint Status

arXiv preprint; formal conference/journal acceptance not verified.

## Paper URL / DOI

[Paper, v4](https://arxiv.org/html/2604.25850v4); [arXiv DOI](https://doi.org/10.48550/arXiv.2604.25850).

## Official GitHub Repository

[china-qijizhifeng/agentic-harness-engineering](https://github.com/china-qijizhifeng/agentic-harness-engineering), directly named in the paper and described as official by the repository.

## Research Problem

How can an agent reliably modify heterogeneous harness components when useful failure evidence is buried in enormous traces and regressions are difficult to attribute?

## Methodology and Algorithm

AHE exposes seven file-based components through NexAU: prompt, tool descriptions, implementations, middleware, skills, subagents, and memory. Agent Debugger creates a layered evidence corpus while preserving raw traces. An Evolve Agent edits components and records hypotheses, predicted fixes, and predicted regressions. Subsequent task-level outcomes are compared with that manifest and rejected edits can be rolled back; code changes are versioned. Verifiers, model configuration, and run logs are read-only. This is an auditable evaluate–analyze–edit loop, not a differentiable optimizer or unrestricted self-rewriting evaluator. See §3, Algorithm 1.

## Key Contributions

The distinctive contribution is operational observability: edit boundaries, navigable evidence, and falsifiable predictions. Component ablations demonstrate interaction effects; regression forecasting provides a useful negative result about the limits of agent explanations.

## Experimental Setup

One ten-iteration campaign, approximately 32 hours, evolves on all 89 Terminal-Bench 2 tasks with one-hour timeouts. Code, debugger, and evolve roles use GPT-5.4 high. Reported pass@1 is mean binary success across rollouts, not best-of-k. Failed/timed-out trials count as failures; token means exclude infrastructure-aborted or timed-out trials. The frozen artifact is tested on 500 SWE-bench Verified tasks and alternative models.

## Benchmarks and Baselines

OpenCode, Terminus-2, Codex; ACE and Training-Free GRPO share the minimal NexAU0 seed. Transfer includes Qwen 3.6 Plus, Gemini 3.1 Flash Lite preview, DeepSeek V4 Flash, and alternative GPT-5.4 reasoning levels. Component-only swaps test prompt, tools, middleware, and long-term memory.

## Quantitative Results

All numbers are author-reported; no independent reproduction.

| Condition | Comparator | AHE | Source |
|---|---:|---:|---|
| Terminal-Bench 2, full evolution/evaluation panel | Seed 69.7%; Codex 71.9% | 77.0% | Table 1 |
| Terminal-Bench hard tier | Codex 56.7% | 53.3% | Table 1 |
| Unseen SWE-bench Verified success | Seed 75.2% | 75.6% | Table 2 |
| SWE-bench tokens/trial | Seed 526k | 461k | Table 2 |
| Regression prediction precision / recall | Random 5.6% / 5.4% | 11.8% / 11.1% | §4.4.2, Fig. 4 |

The held-out accuracy gain is 0.4 points, substantially smaller than the 7.3-point evolution-panel gain.

## Limitations

Terminal-Bench has no task holdout within the main evolution run. The single campaign does not establish robustness across search seeds. File-level predictions and observed flips are useful diagnostics but cannot identify causation when edits interact and rollouts vary stochastically. Conditional token averages may understate resources spent on failed trials. The timeout/reasoning interaction changes apparent transfer. Most regressions are not forecast; favorable explanations should not substitute for controlled ablations.

## Reproducibility

The official repository provides uv/Python 3.13 instructions, Harbor/E2B integration, configuration snapshots, and NexAU version pinning. Crucially, its README states Agent Debugger is only partially open-sourced, limiting full reconstruction. The surrounding repository advertises MIT, but that does not erase the unreleased dependency boundary. Availability and documentation were checked; installation and result replication were not performed.

## Open Research Questions

Would gains persist with disjoint evolution/validation/test tasks and equal compute? Can randomized component interventions improve causal attribution and regression recall? How much transfer comes from reusable coordination mechanisms versus task-specific rules embedded in memory or middleware?
