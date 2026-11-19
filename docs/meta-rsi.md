# Meta-RSI: Learning a Better Improvement Procedure

## What changes at the meta level?

A meta-improver chooses how to diagnose failures, generate edits, allocate evaluations, combine candidates, preserve memory, and stop. Write its policy as $I_\phi$. Editing an agent's task prompt is a first-order update. Editing a reusable rule for proposing future prompts is a meta-level update. A file's name does not determine its level: a purported meta-skill must actually affect subsequent improvement decisions.

[STOP](https://arxiv.org/abs/2310.02304) targets an improvement program; [Hyperagents](https://arxiv.org/abs/2603.19461) exposes task and meta-agent programs; [HMED](https://arxiv.org/abs/2610.07979) studies experience derived from revision consequences. These mechanisms motivate meta-learning, but a comparison against a fixed starting improver is still needed to identify their value.

## Meta-learning formulation

Let $\mathcal{T}_{\mathrm{train}}$ contain task families, each with inner-loop development data $D_k$ and outer-loop validation data $V_k$. A meta-objective is

$$
\max_\phi\;\mathbb{E}_{k,s_0}\left[J_{V_k}(I_\phi^B(s_0,D_k);b)-J_{V_k}(s_0;b)-\lambda C(I_\phi^B)\right].
$$

Here $I_\phi^B$ denotes the entire budget-limited improvement procedure. The parameters $\phi$ may be model weights, code, an experience library, or a policy over editing operators. Differentiable meta-learning is one option; program search and contextual decision policies are others. An outer validation set used to select $\phi$ cannot also establish final generalization.

## Cross-task generalization

Instance splits preserve task format and can share shortcuts. Distinguish unseen instances, unseen templates, harder instances, unseen domains, unseen environments, and unseen executor models. [SelfImprove-Bench](https://arxiv.org/abs/2611.02797) is directly relevant because it evaluates a generalization ladder; its ranking changes warn against reporting a single universal ordering of improvers.

Transfer the **improver artifact only** in a clean-start experiment. Carrying over the improved task solver or domain memory tests a different intervention. Report both if useful, with a factorial design distinguishing solver transfer, improver transfer, and their combination. Similarly, compare a meta-skill with a content-matched static retrieval baseline so that benefits from extra examples are separated from benefits from a learned improvement policy.

[Self-Improvement Memory](https://arxiv.org/abs/2611.18856) is a close November 2026 baseline: structured causes, edits, predicted and observed effects, and provenance are supplied to the optimizer, not directly to the task solver. This is more informative than an unstructured summary baseline. Its paired coding-search evidence and other single-search transfer settings must retain their different repetition levels.

## Budget-aware meta-optimization

An improver spends resources to obtain information. Candidate generation, evaluation fidelity, retries, and integration compete for the same budget. A useful decision rule selects action $a$ by predicted increase in final held-out utility per incremental cost, rather than immediate development score. The predictions themselves need calibration under distribution shift.

Cheap structural checks can reject invalid changes before expensive task evaluation. [ELITE](https://arxiv.org/abs/2611.21056) takes this further by integrating inspected implementations without downstream candidate task evaluation inside its loop. Its evaluation-free label does not eliminate proposal costs, validity checks, or final scientific assessment. [The RSI Tax](https://arxiv.org/abs/2611.13524) motivates accounting for the entire loop.

## How to establish that the improver improved

1. Save early and late improver snapshots, with code, memory, parameters, and tool versions.
2. Restart each from the same set of initial solvers and unseen task families.
3. Give each the same feedback interface and total development budget.
4. Evaluate outputs using a sealed audit and fixed execution budget.
5. Repeat the **whole** process across independent search seeds; repeated execution of one selected solver is insufficient.
6. Include frozen-improver, random or shuffled guidance, and fixed search controls.

Report the paired contrast $\Delta_Q=Q(I_{\mathrm{late}})-Q(I_{\mathrm{early}})$, its uncertainty, and where it fails. A stronger late improver that carries a better task solver into the experiment does not isolate $\Delta_Q$. [Auditing the Product](https://arxiv.org/abs/2610.27610) provides the central evidence distinction.

## Unresolved questions

Meta-level rewards are sparse and delayed; good exploratory changes can look worse before enabling future improvements. An evolving evaluator can make old and new scores incomparable. Search may compress training-family solutions into a meta-skill, and a new executor can invalidate diagnostic heuristics. There is no established evidence in this repository for unrestricted recursive acceleration.

The [generalizable Meta-RSI proposal](../research/generalizable-meta-rsi.md) focuses on clean-start transfer and controlled improvement operators. It treats a positive result as a bounded statement about a measured family distribution, not universal learning to improve.
