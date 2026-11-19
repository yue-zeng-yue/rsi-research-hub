# Research Gaps and Decision Criteria

This file converts the [trend report](../docs/research-trends.md) into research decisions. Every proposed contribution is unvalidated. A missing experiment in the reviewed corpus is a motivation, not proof of novelty.

| Priority | Question | Minimum discriminating experiment | Nearest prior art | Go / revise decision |
| --- | --- | --- | --- | --- |
| 1 | Can update utility be predicted for a new executor? | Randomize update exposure; hold out task and executor families | Updating versus Benefit, HDA, HMED, GEPA | Proceed only if prediction improves selection over equal-cost paired validation |
| 2 | Can pair-specific risk prevent co-evolution regressions? | Old/new model crossed with old/new harness, plus fresh validation | On-policy correction, HarnessForge, JoMoHa, teacher-free co-evolution | Proceed if risk calibration and useful coverage both improve |
| 3 | Can the improver transfer without solver memory? | Restore common initial solvers; transfer only early/late improvers | Hyperagents, HMED, Skill∞, SelfImprove-Bench | Revise if gains depend on inherited solutions or larger budgets |
| 4 | Can search quality be preserved with fewer expensive evaluations? | Prospective scheduler versus uniform, halving, and ELITE controls | RSI Tax, SoL-Pi, RRSI, ELITE | Proceed only on total-cost gains at declared quality tolerance |

## Evidence hierarchy

An inspected algorithm establishes what is proposed. An author-reported controlled experiment establishes evidence under its conditions. A released implementation improves inspectability. A successful independent run establishes reproduction of that configuration. None of these automatically implies broad transfer. This initialization reaches primary-source review and repository validation only.

For every claim, identify its unit: one selected artifact, the distribution of artifacts from a full search loop, the improver from a fixed start, or the deployed system over a stream. Allocate repetitions at the matching level. Many execution reruns cannot compensate for only one search seed.

## Evidence that would change the agenda

If a new primary paper already implements the proposed utility estimator with the same transfer controls, change the proposal or reproduce it. If most apparent harness benefit is recovered by a stronger fixed baseline, focus on diagnosing missing capabilities rather than adding evolution machinery. If cheap randomized evaluations are too noisy, first improve the measurement protocol and task coverage. If training cost dominates, defer co-evolution until a model-only baseline and resource budget are established.

## Research record requirements

Each selected direction should have a dated preregistration, immutable split manifest, source version ledger, baseline fidelity notes, resource cap, statistical analysis plan, and explicit abandonment criterion. Preserve negative results. A publication-oriented contribution must be stated only after a renewed related-work search and results that distinguish the proposed mechanism from simpler alternatives.

See the [paper index](../papers/paper-index.md) for source identities and the four linked proposal documents in the [README](../README.md) for algorithms, metrics, and venue fit.
