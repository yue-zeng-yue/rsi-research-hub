# Idea 4: Budget-Efficient Recursive Self-Improvement

**Status:** Proposed algorithm and evaluation plan. No efficiency gain has been independently established. **Novelty status:** Unestablished; several strong 2026 baselines already target this problem.

## Problem Statement

Allocate a fixed development budget among candidate generation, structural validation, task evaluation, integration, and model training so as to maximize final audited utility. Include the cost of failed candidates and the method used to choose evaluations.

## Motivation

An agent that runs more cheaply can still be uneconomical if evolution costs exceed deployment savings. Conversely, an expensive search can be rational when its artifact is reused at scale. The evaluation must state the deployment horizon and quality tolerance rather than treating fewer executor tokens as sufficient evidence.

## Related Work

| Work | Existing cost mechanism | Necessary comparison |
| --- | --- | --- |
| [The RSI Tax](https://arxiv.org/abs/2611.13524) | Full-cycle cost accounting, including unsuccessful verification | Include all discovery and evaluation costs |
| [SoL-Pi](https://arxiv.org/abs/2609.20519) | Efficiency-oriented harness mechanisms and composition | Compare at a specified quality tolerance |
| [RRSI](https://arxiv.org/abs/2609.24972) | Restricts and prunes harness modifications | Test against cheap conservative search |
| [Meta-Harness](https://arxiv.org/abs/2603.28052) | Search over reusable harnesses and cost/performance tradeoffs | Equal-cost search history access |
| [ELITE](https://arxiv.org/abs/2611.21056) | No downstream candidate evaluations inside evolution | Structural reasoning is already a competitive low-evaluation baseline |
| [WHALE](https://arxiv.org/abs/2609.00196) | Switches weight/harness learning based on training behavior | Adaptive scheduling alone is insufficient novelty |
| [TRUST](https://arxiv.org/abs/2611.10787) | Uses historical context to allocate statistical evidence across update gates | Value-of-information scheduling must improve on existing evidence-adaptive admission |
| [AHE-Beta](https://arxiv.org/abs/2611.24924) | Requirement-driven development with review and simulated users | Charge simulation and review costs, not only executor-token savings |
| [TT-RSI](../papers/2026/tt-rsi.md) | Refinement and test-time training with output-token-matched inference comparisons | Include reference-input work, adaptation, latency, and all failed attempts before claiming whole-loop savings |
| [CoEvoBench](../papers/2026/coevobench.md) | Shared GPU/time envelope and separate API-cost accounting | Equal resource caps do not imply equal realized cost |

## Limitations of Existing Methods

Cost measures are not interchangeable: output tokens, cached input tokens, GPU-hours, latency, and dollars can rank methods differently. Evaluating only accepted candidates understates search expense. Multi-fidelity evaluations can favor edits tailored to short tasks. An evaluation-free loop still pays for code generation and validity checking and may silently accept regressions.

## Research Hypothesis

A scheduler that estimates the **value of information** of each evaluation, learns when cheap fidelity is misleading, and reserves a fixed final audit budget can improve the quality–total-cost frontier over uniform evaluation and no-evaluation integration.

## Proposed Algorithm

Maintain a candidate archive with a joint posterior or calibrated predictive distribution over quality, regression, and cost. Define several fidelities: interface checks; representative task batches; full development evaluation; and a fresh validation gate. Structural checks establish executability, never task improvement. Choose the next candidate/fidelity pair by estimated reduction in final selection regret per incremental cost, with minimum coverage across task families.

Candidates with implausible upside are stopped early. Candidates whose low-fidelity predictions are unreliable receive more evaluation rather than automatic rejection. Retain a random evaluation fraction to monitor selection bias. Use the same candidate generator and archive access for the scheduler and uniform baseline. Do not spend the sealed audit budget during search.

## Mathematical Formulation

Let $a=(c,f)$ select candidate $c$ and fidelity $f$, and $\mathcal H$ be observed evidence. A proposed acquisition score is

$$
a^*=\arg\max_a\frac{
\mathbb{E}_{y\mid a,\mathcal H}[\max_c\mathbb{E}[U(c)\mid\mathcal H,(a,y)]]
-\max_c\mathbb{E}[U(c)\mid\mathcal H]
}{\mathbb{E}[\Delta C_a\mid\mathcal H]}.
$$

This is a value-of-information approximation, not a computationally free oracle. Include the cost of fitting and evaluating it. Dependence across task families and systematic low-fidelity bias require explicit modeling or conservative calibration.

For an initial evolution cost $C_{\mathrm{evo}}$ and per-deployment savings $c_0-c_1>0$, the accounting break-even is

$$
N_{\mathrm{break}}=\left\lceil\frac{C_{\mathrm{evo}}}{c_0-c_1}\right\rceil.
$$

The formula assumes a fixed workload, unchanged prices and quality, and no additional maintenance. If $c_1\ge c_0$, there is no cost-only break-even; improved quality may still justify the method under a declared utility function.

## Experimental Design

First evaluate schedulers on a fully measured development candidate pool, charging the true cost of every observation a policy requests. Then run an end-to-end prospective experiment to avoid overfitting to that pool. Cover a cheap interactive environment and a costly terminal or coding environment. Pin exact versions, task families, API snapshots, hardware, and prices.

Use multiple total budgets and deployment horizons, with the primary comparisons declared before inspecting outcomes. Run independent search seeds and preserve timeouts and infrastructure failures. Include shifts in task length and executor model to stress low-fidelity calibration. A pilot estimates variance and sets the confirmatory seed count and minimally important quality difference.

## Baseline Methods

No search plus extra inference; uniform candidate evaluation; successive halving; random budget allocation; fixed cheap/full schedule; RRSI; an applicable SoL-Pi recipe; TRUST-style evidence allocation; and ELITE-style validity-gated integration. Add a scheduler with perfect retrospective candidate scores only as a labeled unattainable diagnostic reference.

## Evaluation Metrics

Audited success at matched total cost; Pareto hypervolume under fixed reference points; time to a prespecified quality target; full evolution cost; amortization horizon; regression rate; rejected-candidate expenditure; and misranking by fidelity. Report raw tokens, calls, GPU-hours, wall time, and price conversions separately. Report all deployed artifacts, not only the cheapest successful run.

## Expected Challenges

Cost prediction drift, API caching, parallelism, heavy-tailed runtimes, delayed failures, and a scheduler that costs more than it saves. Evolving the generator invalidates candidate-pool replay assumptions, so replay alone cannot establish end-to-end gains.

## Novelty Assessment

Candidate screening, multi-fidelity search, and budget-aware scheduling are established ideas. A contribution would require an RSI-specific information model that handles reusable artifacts, biased fidelities, and changing partners, plus superior prospective results against strong low-cost baselines. If uniform evaluation or ELITE matches the frontier, the proposed scheduler has not earned an algorithmic novelty claim.

## Potential Publication Venues

ICML, ICLR, or NeurIPS for a general allocation algorithm; MLSys for measured system-level cost and reproducibility; TMLR or a relevant ML journal for a detailed empirical study. Indexing status and submission windows must be checked separately when preparing a manuscript.
