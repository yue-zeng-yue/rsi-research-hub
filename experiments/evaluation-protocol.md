# Evaluation Protocol for Self-Improvement Claims

**Protocol status:** Proposed, not executed. No benchmark or training result is produced by this repository's initialization.

## 1. Declare the claim and estimand

Choose product improvement, cross-task transfer, improved improver, cost efficiency, or stable co-evolution. Define the initial artifact, target task distribution, reward, inference cap, development budget, minimum practically important difference, and primary statistical contrast before running search. Do not change the primary endpoint after seeing results.

For product quality use $\Delta=J_D(s_1;b)-J_D(s_0;b)$. For improver quality use outputs of early and late improvers applied to identical starting artifacts at the same development budget. For co-evolution measure all four old/new component combinations. The primary unit of uncertainty for a stochastic search method is an independent search run.

## 2. Seal data and evaluation boundaries

Maintain four roles where feasible: proposal/train tasks, development tasks used for iterative feedback, validation tasks used for prespecified selection, and sealed audit tasks. Any task or grader output that affects prompts, candidate selection, training, or hyperparameters belongs to development. Repeated access to validation makes it adaptive development evidence.

Hold out task generators, templates, repositories, or domains when claiming stronger transfer. Check source-code history, cached traces, solution scripts, demonstrations, and skill contents for leakage. Store task IDs and content hashes. An official benchmark test split becomes a development split if the loop uses its feedback.

For continual adaptation, score each new task before its feedback is incorporated. Publish the stream order, resets, and feedback delay. Distinguish cumulative online reward from final frozen-artifact generalization.

## 3. Match information and budget

Each control receives the same allowed tests, judge feedback, tool access, context limits, execution time, and model snapshots. Compare fixed-harness extra sampling and sequential answer refinement as well as no improvement. Keep pass@1, pass@k, and best-of-k with an oracle clearly separate; oracle selection requires feedback unavailable in many deployments.

Record the resource vector rather than collapsing everything into tokens:

$$
\mathbf C=(\text{input tokens},\text{cached input},\text{output tokens},\text{calls},\text{GPU-hours},\text{CPU-hours},\text{wall time},\text{dollars}).
$$

Include proposer, executor, judge, teacher, training, failed candidates, retries, environment startup, and final validation. Report the sealed scientific audit separately from method development cost and include both in the total research bill. Fix exchange rates and API prices only when converting to dollars; retain raw measurements.

## 4. Repetition and uncertainty

Run independent full-loop seeds, independently initializing archives, task-order randomization, and candidate sampling. Five full-loop seeds are a planning target, not a guarantee of adequate statistical power. Use a pilot to estimate variance and choose the confirmatory count; do not silently promote pilot tasks into the sealed test.

Within each search seed, evaluate paired final artifacts on common tasks with multiple execution repetitions where stochasticity matters. A shared seed does not ensure identical dialogue trajectories, so pairing is by task and reset state, not by assuming matching random draws. Use hierarchical or cluster bootstrap over task families and search seeds, or an explicitly justified mixed-effects analysis. Report 95% intervals and raw per-run results.

For a fixed binary paired comparison, report discordant outcomes and an appropriate paired test. Multiple candidates, endpoints, and repeated gates require a prespecified multiplicity or sequential-testing policy. A fresh batch per gate or an explicitly valid sequential procedure is preferable to repeatedly applying an ordinary confidence interval to the same validation set. Separate a practical non-inferiority margin from a failure to reject the null.

## 5. Regression and attribution

Report gains, losses, and ties by task family, including worst-family changes, invalid actions, timeouts, and premature termination. Count infrastructure failures separately using a fixed retry rule that does not depend on success.

For harness effects, include a compute-matched fixed baseline and audit benchmark-specific shortcuts. A shortcut-neutralized residual is conditional on what was detected and how it was removed; it is not a proof of causal generalization. For co-evolution, report both interaction $J_{11}-J_{10}-J_{01}+J_{00}$ and total change $J_{11}-J_{00}$.

For meta-improvement, restart early and late improvers from identical solver, memory, tools, and caches. Add a factorial transfer experiment if solver artifacts are also transferred. Report improvements over an unchanged improver, not only over no search.

## 6. Reproduction package

Retain an experiment report using the [template](../templates/experiment-report.md), plus:

- Immutable source commits, model revisions, API timestamps, adapter hashes, harness hashes, environment/container digests, dependency lockfiles, and hardware details.
- Split manifests, task-generator versions, prompts, tool schemas, reward/verifier definitions, and allowed feedback.
- All candidate identities, parent relations, acceptance decisions, failure traces, and costs, including rejected changes.
- Per-task outcomes, run seeds, raw metric definitions, analysis scripts, and exact commands.
- Data licenses, dataset availability, and redaction rules for any non-public source.

Do not commit credentials, environment files, model caches, private trajectories, or downloaded copyrighted paper collections. Artifacts requiring redistribution review should be referenced by hashes and source links until authorized.

## 7. Acceptance and reporting

A smoke test checks installation and interfaces. An oracle run checks the evaluator. A single successful model run checks execution. A reproduction requires matching the published configuration and uncertainty. A new result requires the preregistered controls and audit. These statuses must remain distinct in reports.

Report a negative result when the confidence interval excludes the planned useful improvement or when a strong baseline matches the method at equal cost. Report inconclusive when power is insufficient. Do not call non-significant differences equivalence. Freeze final artifacts before opening the audit and log any post-audit changes as a new study.

## Methodological sources

[Rethinking Evaluation](https://arxiv.org/abs/2607.12227), [Harness-Delta Attribution](https://arxiv.org/abs/2610.22466), [Auditing the Product](https://arxiv.org/abs/2610.27610), [SelfImprove-Bench](https://arxiv.org/abs/2611.02797), and [The RSI Tax](https://arxiv.org/abs/2611.13524) motivate the controls. The protocol above is this repository's proposed synthesis, not a claim that these sources prescribe identical procedures.
