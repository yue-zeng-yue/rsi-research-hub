# Self-Improvement Memory Enables Continual Recursive Self-Improvement

Review cutoff: 2026-11-19. Author-reported evidence; no independent reproduction.

## Full Paper Title

Self-Improvement Memory Enables Continual Recursive Self-Improvement

## Authors and Affiliations

Xin Yu: Google Cloud AI and Pennsylvania State University; Fei Xia, Jiaqi Pan, Youbao Tang, Chengzhi Liu, Ting Yu: Google Cloud AI; Adams Yu, Sicong Jiang: Google DeepMind; Yanfei Chen: Google Cloud AI Research; Lingzhou Xue: Pennsylvania State University. Paper author order is preserved in the manifest.

## Publication Date

2026-11-13, arXiv v1; inspected 2026-11-19.

## Venue or Preprint Status

arXiv preprint. The author project describes it as a preprint; peer-reviewed venue: Not verified.

## Paper URL / DOI

[Paper](https://arxiv.org/abs/2611.18856); [full HTML](https://arxiv.org/html/2611.18856v1); verified [arXiv DOI](https://doi.org/10.48550/arXiv.2611.18856).

## Official GitHub Repository

Not verified. The [author project](https://lucasxinyu.github.io/sim/), linked from Xin Yu’s homepage, explicitly says no public implementation is linked. Its interactive record is illustrative, not an exported experimental artifact; unrelated benchmark repositories are not SIM code.

## Research Problem

An evolved harness does not explain why inherited edits were made or which conditions justified them. When tasks or executor models change, an optimizer can discard useful mechanisms or repeat failed reasoning unless improvement experience accompanies the harness.

## Methodology and Algorithm

SIM stores root-cause hypotheses and ordered attempts containing edits, rationale, predicted/observed outcomes, and benchmark/model/round provenance. Proposer and selector consume the full JSON memory; the task-solving policy does not. Formally candidates=P(H,F,history;M), selection=S(candidates,evaluations;M), followed by memory append. Only the chosen accepted edit is recorded, including unmet predictions or regressions; rejected proposals are not appended. Planning/search procedures and model weights stay fixed. Transfer requires a compatible executable harness interface (§3; Appendix D).

## Key Contributions

The central contribution is structured optimizer memory and continuation across setting changes. Its same-harness controls distinguish improvement-process information from a better starting executable artifact. It therefore overlaps directly with proposals for transferable revision memory, although it does not learn a general budget-conditioned operator policy.

## Experimental Setup

Source and target optimization each use ten rounds and five proposed candidates per round. Gemini 3.8 Flash is the main proposer/selector and cross-dataset executor; cross-model experiments transfer Claude Opus 5.5 harnesses to Gemini. Five rollouts per task estimate execution performance. Main comparisons use one search run per condition; a separate coding study has ten independent source runs with paired continuations (§4; Appendix C).

## Benchmarks and Baselines

Four domains: Terminal-Bench 2.1→4; classification suites; Harvey LAB→JobBench/GDPval/APEX; EngDesign→Frontier-Eng. Controls: cold start, evolved-harness-only transfer, root-cause-only memory, full SIM. Transfer arms share the evolved starting harness. Source-overlapping engineering components receive zero credit while remaining in the denominator.

## Quantitative Results

Table 3 reports SIM versus no-SIM paired coding advantage +2.36 points, 95% CI [1.05,3.68], paired p=.003, winning 9/10 pairs. Table 6 workspace cross-model continuation reaches 84.75 versus 73.42 from the same 68.41 start. Table 1’s latest generation reverses the advantage: CRSI 94.8 versus fresh RSI 95.6.

## Limitations

Equal rounds/candidates do not imply equal tokens or runtime; complete-memory prompting adds cost. Full SIM combines inherited records and new target updates, so their separate effects are unidentified. Other-domain single runs support descriptive comparisons, not robust search-level rankings. Compatible-interface transfer is narrower than arbitrary partner or tool changes.

## Reproducibility

Independent reruns were not performed. The paper provides record schemas, splits, settings, and paired statistics; public implementation and complete raw artifacts were not verified. Replication should freeze API versions, separate execution/search variance, report final retained artifacts rather than test-selected maxima, and account for source amortization and memory growth.

## Open Research Questions

Does source-only memory help without target appends? Do rejected-edit histories add value beyond selected-edit memory? Test content/length-matched summaries, shuffled provenance, retrieval versus full context, and changing tool contracts. A new meta-policy should beat SIM under equal total budgets and clean-start interventions, not merely beat an empty or unstructured memory.
