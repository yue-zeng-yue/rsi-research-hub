# Idea 2: Generalizable Meta-RSI

**Status:** Unimplemented research hypothesis. **Novelty status:** Requires comparison with HMED, Hyperagents, and recent generalization benchmarks.

## Problem Statement

Learn an improvement policy that remains useful when the initial solver, task family, or improvement budget differs from those used during meta-training. The target is improvement quality from a common start, not simply the quality of a transferred final solver.

## Motivation

A meta-skill can memorize solutions or diagnostic templates specific to its training distribution. Such memory may raise benchmark scores while failing to improve a new agent. Generalizable improvement should identify transferable failure mechanisms and select useful editing actions under resource constraints.

## Related Work

| Work | What it already contributes | Consequence for this proposal |
| --- | --- | --- |
| [STOP](https://arxiv.org/abs/2310.02304) | Executable self-improving optimization scaffolds | Self-editing an improver is not new |
| [Hyperagents](https://arxiv.org/abs/2603.19461) | Editable meta-agent and transfer experiments | Include its transfer and frozen-meta controls |
| [HMED](https://arxiv.org/abs/2610.07979) | Revision-consequence memory, matched discovery-state replay, and transfer with reset skill libraries | Same-start replay and storing failed edits are already prior art |
| [Self-Improvement Memory](https://arxiv.org/abs/2611.18856) | Optimizer-only structured memory of causes, edits, predicted/observed effects, and provenance across task/model changes | A learned policy must beat structured memory, not only unstructured summaries |
| [Skill∞](https://arxiv.org/abs/2610.35434) | Meta-level skill evolution | Distinguish improvement-policy transfer from accumulated skill content |
| [SelfImprove-Bench](https://arxiv.org/abs/2611.02797) | Multiple generalization levels | Evaluate beyond new instances of old templates |
| [Auditing the Product](https://arxiv.org/abs/2610.27610) | Claim-specific evidence and same-start comparisons | Process claims require a crossed intervention |

## Limitations of Existing Methods

Transfer evidence varies in task coverage, retained state, and search budget. A successful transfer run does not imply calibrated action selection across novel budgets or failure distributions. HMED already performs matched-origin comparisons; this proposal must add an algorithmic contribution beyond recommending that control.

## Research Hypothesis

An improvement policy trained over **mechanisms and resource regimes**, with task-family holdouts and an explicit uncertainty-sensitive exploration rule, will achieve better clean-start transfer than a growing library of unstructured revision summaries at the same total cost.

## Proposed Algorithm

Represent each improvement episode by a task-invariant diagnostic state: failure categories, tool-interface complexity, context pressure, uncertainty, prior edit effects, and remaining budget. Let actions select an operator family and evaluation fidelity, such as context repair, tool validation, skill retrieval change, rollback, or stop. Existing code-editing models instantiate the selected operator.

Train the selection policy across diverse development families using outer-loop improvement rewards. Store raw evidence behind summaries to avoid uncheckable abstractions. Randomize operator and task order where feasible and keep a limited random-exploration component. During transfer, freeze the learned meta-policy first; evaluate online meta-adaptation as a separate arm. Restore task libraries, caches, and solver weights for every same-start comparison.

## Mathematical Formulation

For family $k$, let $G_k(\phi,B)=J_{T_k}(I_\phi^B(s_0,D_k);b)-J_{T_k}(s_0;b)$, where outer-loop training uses validation $T_k$ and final testing uses entirely separate families. A proposed robust objective is

$$
\max_\phi\ \min_{q\in\mathcal Q}\sum_k q_k\mathbb{E}_{B\sim P_B}[G_k(\phi,B)]-\lambda C_{\mathrm{meta}}(\phi),
$$

where $\mathcal Q$ is a prespecified neighborhood of development-family weights. This distributionally robust objective is a design choice, not a guarantee on arbitrary tasks. During an episode, operator selection can optimize an uncertainty-aware estimate of future gain per cost, while respecting a fixed budget. Evaluate the policy against the simpler non-robust objective to establish whether this complexity helps.

## Experimental Design

Build family-level splits across interactive tool tasks, structured reasoning, and coding or terminal tasks. Hold out complete task generators and evaluate difficulty extrapolation. Use a distinct executor family for an additional shift. Run a $2\times2$ transfer design: early/late improver crossed with base/improved solver. The primary contrast fixes the base solver, resets all domain memory, and transfers only the improver.

Measure curves at several budgets chosen before experiments. Use at least five independent meta-training/search seeds if the pilot supports that allocation; repeated execution of a single learned improver is an additional variance component, not a substitute. Include leave-one-family-out analyses and report failures, not just the best family. A separate stream experiment can test adaptation after distribution changes, using pre-update scoring.

## Baseline Methods

Fixed improver; random operator policy; budget-aware fixed schedule; unstructured retrieval memory; HMED-style revision-consequence memory with matched-state replay; SIM-style structured optimizer memory with its root-cause-only ablation; Hyperagents with meta-editing enabled and frozen; the same learned policy without robust training; and a fresh strong external proposer with identical feedback and budget. Porting deviations must be documented. SIM retains selected edits and their outcomes; do not misdescribe it as an archive of all rejected candidates.

## Evaluation Metrics

Same-start improvement $\Delta_Q$, improvement-curve area over a prespecified budget interval, success gain per total cost, transfer gap, task-family worst case, operator calibration, edit diversity, and negative-transfer frequency. Plot source performance against transfer performance to reveal specialization. Account for amortized and unamortized meta-training cost separately.

## Expected Challenges

Diagnostic features can leak task identity, reward noise can obscure operator value, and a powerful shared editor may dominate the selection policy. Meta-training itself can be more expensive than the savings obtained. An apparent robust objective benefit may result from greater data diversity; control dataset size and distribution.

## Novelty Assessment

The prospective contribution is a transferable **budget-conditioned improvement policy with demonstrated robustness across generators and executors**. The evaluation protocol alone is insufficient algorithmic novelty. If a static library or HMED matches the result at equal cost, reject the stronger claim. A new benchmark is justified only if it reveals behavior existing generalization ladders cannot measure.

## Potential Publication Venues

ICLR, ICML, or NeurIPS for transferable meta-optimization; TMLR for a reproducible empirical or methodological contribution; ACL/EMNLP if the primary advances concern language-agent adaptation. Venue suitability depends on results and positioning, not terminology.
