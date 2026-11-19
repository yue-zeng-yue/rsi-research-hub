# Paper Review Guide

The [paper index](paper-index.md) links full reviews and canonical sources. The [machine-readable catalog](../data/papers.json) preserves metadata and inspected sections; the [bibliography](../references.bib) supports manuscript preparation. The review cutoff is 2026-11-19.

Each admitted paper has 15 fields: full title; authors/affiliations; publication date; venue; paper URL/DOI; official code; problem; method; contributions; setup; benchmarks/baselines; quantitative results; limitations; reproducibility; and open questions. Reviews summarize original sources in independent academic prose and add clearly identified critical analysis.

## How to interpret the collection

All indexed scientific results are **author-reported** unless a review explicitly links an independent reproduction. No independent experiment was run during initialization. Full-text review means methods and experiments were inspected; it does not imply that every table was recomputed, every code path audited, or every source claim verified experimentally.

First-publication year determines the folder. A 2025 paper revised in 2026 remains under `2025/`; older foundations live under `foundations/`. Venue status is independent of first arXiv date. Author-reported acceptance is labeled separately from an official proceedings record.

Missing metadata or official code is recorded as `Not verified`, with a reason. A verified paper can still have an unavailable implementation. A claimed release can be a placeholder. Source revisions, mutable APIs, missing trajectories, and incomplete benchmark splits affect reproduction feasibility.

## Recommended reading routes

**Concepts:** Gödel Machines → STaR → STOP → SICA → DGM → Hyperagents. The route distinguishes formal self-rewriting, self-training, persistent code modification, and editable improvement mechanisms.

**Harness methods:** GEPA → Meta-Harness → AHE → Harness² → RRSI → SoL-Pi. Compare edit surfaces, evidence supplied to the proposer, acceptance rules, and total cost.

**Evidence first:** Updating versus Benefit → Rethinking Evaluation → HDA → Auditing the Product → SelfImprove-Bench → The RSI Tax → TRUST. These papers help determine what an improvement claim establishes.

**Co-evolution and meta-learning:** SIA → HarnessForge → WHALE → on-policy correction → HarnessAdapt-RL → JoMoHa → HMED → SIM. Read the [trend report](../docs/research-trends.md) and four research proposals alongside them; this is a conceptual route rather than a publication chronology.

## Search and update policy

The initial search used the supplied candidates, the follow-rsi discovery repository, exact-title queries, and expanded queries for November 2026 harness, meta-improvement, evaluation, and co-evolution research. See [source-audit.md](../docs/source-audit.md) for scope, evidence boundaries, and unresolved items. New leads are not counted until their primary full text is reviewed.
