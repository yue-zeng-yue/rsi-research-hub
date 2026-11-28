# Paper Review Guide

The [paper index](paper-index.md) links **44 primary-full-text-reviewed papers** and canonical sources. The [machine-readable catalog](../data/papers.json) preserves metadata and inspected sections; the [bibliography](../references.bib) supports manuscript preparation. The latest incremental review is dated 2026-11-28; earlier records retain their own inspection dates. This is a selective update, not exhaustive coverage through that date.

Each admitted paper has 15 fields: full title; authors/affiliations; publication date; venue; paper URL/DOI; official code; problem; method; contributions; setup; benchmarks/baselines; quantitative results; limitations; reproducibility; and open questions. Reviews summarize original sources in independent academic prose and add clearly identified critical analysis.

## How to interpret the collection

All indexed scientific results are **author-reported** unless a review explicitly links an independent reproduction. No independent experiment was run during initialization. Full-text review means methods and experiments were inspected; it does not imply that every table was recomputed, every code path audited, or every source claim verified experimentally.

First-publication year determines the folder. A 2025 paper revised in 2026 remains under `2025/`; older foundations live under `foundations/`. Venue status is independent of first arXiv date. Author-reported acceptance is labeled separately from an official proceedings record.

Missing metadata or official code is recorded as `Not verified`, with a reason. A verified paper can still have an unavailable implementation. A claimed release can be a placeholder. Source revisions, mutable APIs, missing trajectories, and incomplete benchmark splits affect reproduction feasibility.

## Recommended reading routes

### Concepts

[Gödel Machines](foundations/godel-machines.md) → [STaR](foundations/star.md) → [STOP](foundations/stop.md) → [SICA](2025/sica.md) → [DGM](2025/dgm.md) → [Hyperagents](2026/hyperagents.md).

Distinguish formal self-rewriting, self-training, persistent code modification, and editable improvement mechanisms.

### Harness methods

[GEPA](2025/gepa.md) → [Meta-Harness](2026/meta-harness.md) → [AHE](2026/ahe.md) → [Harness²](2026/harness2.md) → [RRSI](2026/rrsi.md) → [SoL-Pi](2026/sol-pi.md).

Compare edit surfaces, evidence supplied to the proposer, acceptance rules, and total cost.

### Evidence first

[Updating versus Benefit](2026/harness-updating-not-benefit.md) → [Rethinking Evaluation](2026/rethinking-evaluation.md) → [HDA](2026/harness-delta-attribution.md) → [Auditing the Product](2026/auditing-product-recursion.md) → [SelfImprove-Bench](2026/selfimprove-bench.md) → [The RSI Tax](2026/rsi-tax.md) → [TRUST](2026/trust.md).

Determine what an improvement claim establishes, and which comparison is still missing.

### Co-evolution and meta-learning

[SIA](2026/sia.md) → [HarnessForge](2026/harnessforge.md) → [WHALE](2026/whale.md) → [On-policy correction](2026/co-evolving-harnesses-models.md) → [HarnessAdapt-RL](2026/harnessadapt-rl.md) → [JoMoHa](2026/jomoha.md) → [HMED](2026/hmed.md) → [SIM](2026/sim.md).

Read the [trend report](../docs/research-trends.md) and four research proposals alongside them; this is a conceptual route rather than a publication chronology.

## Search and update policy

The [November 20–25 update](../docs/updates/2026-11-25.md) adds [CoEvoBench](2026/coevobench.md), [AutoMaster](2026/automaster.md), [SelfWrite](2026/selfwrite.md), and [TT-RSI](2026/tt-rsi.md). Read them together to distinguish research decisions, teacher interventions, editor succession, and transductive adaptation. Their dates follow first arXiv submission in UTC; a revision or local-calendar date is recorded separately.

The initial search used the supplied candidates, the follow-rsi discovery repository, exact-title queries, and expanded queries for November 2026 harness, meta-improvement, evaluation, and co-evolution research. See [source-audit.md](../docs/source-audit.md) for scope, evidence boundaries, and unresolved items. New leads are not counted until their primary full text is reviewed.

The [November 28 review](../docs/updates/2026-11-28.md) adds [TransHarness](2026/transharness.md) and [EvoLink-Bench](2026/evolink-bench.md). Read them together to distinguish transferring a frozen policy from benefiting causally from persistent state.

The [November 27 review](../docs/updates/2026-11-27.md) adds [RoboEvo²](2026/roboevo2.md) and [Language Models Can Rewrite Their Own Weights](2026/self-rewriting.md). Compare the unit of improvement: a motor policy, a harness, an edited language model, or the editor itself.
