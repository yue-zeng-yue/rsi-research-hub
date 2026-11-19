# Rethinking Evaluation of Harness Evolution

## Full Paper Title

Rethinking the Evaluation of Harness Evolution for Agents.

## Authors and Affiliations

Yike Wang (Allen Institute for AI/Ai2; University of Washington); Huaisheng Zhu (Independent); Zhengyu Hu, Yige Yuan (University of Washington); Zhengyu Chen (Independent); Shakti Senthil, Hannaneh Hajishirzi, Yulia Tsvetkov (University of Washington); Noah A. Smith (Ai2; University of Washington); Pradeep Dasigi and Teng Xiao (Ai2). Mapping follows the PDF title page.

## Publication Date

First arXiv submission: 14 July 2026. Reviewed revision: v4, 5 October 2026. Evidence cutoff: 19 November 2026.

## Venue or Preprint Status

arXiv preprint. Conference/workshop acceptance: **Not verified** from an official venue record during this review.

## Paper URL / DOI

[Version-pinned paper](https://arxiv.org/html/2607.12227v4); [arXiv DOI](https://doi.org/10.48550/arXiv.2607.12227).

## Official GitHub Repository

[rethinking-harness-evolution/code](https://github.com/rethinking-harness-evolution/code). The paper links the owning account; the repository explicitly names and links this paper. Inspected revision: `be1507aba4d424344a4548d58bc9cb6b2679fb03`.

## Research Problem

Does optimizing a reusable harness outperform spending comparable feedback and inference on solving tasks directly? Does the resulting harness transfer beyond the tasks that supplied its optimization feedback?

## Methodology and Algorithm

The unified framework distinguishes parallel independent trajectories, sequential trajectory refinement, cross-task harness evolution, and task-specific harness scaling. The latter two modify orchestration rather than only candidate solutions. All start from the same AHE scaffold; its exploration agent is disabled to prevent retrieval of outside benchmark-specific harnesses. Terminal-Bench uses K=5 and one rollout per task per harness. Without tests, outputs use self-selection or the final revision; with tests, oracle success selection and pass@k measure a different information regime. Held-out evaluation uses 45 training, 10 validation, and 34 test tasks. See [§§3–4](https://arxiv.org/html/2607.12227v4#S3).

## Key Contributions

The study separates reusable optimization from instance-level search, introduces explicit feedback controls, and identifies long-horizon games as a setting where task-specific harness editing helps. The positive game results do not establish transfer of a reusable solver or improver.

## Experimental Setup

Terminal-Bench 2.1 contains 89 tasks, including 28 repairs relative to 2.0. Claude Opus 4.6, GPT-5.4, and GPT-5.4 mini use high reasoning settings, up to 128k generated tokens, and two independent runs. ARC-AGI-3 uses 2,000 actions; EdgeBench uses 12-hour windows and periodic harness updates (§§4–5).

## Benchmarks and Baselines

Terminal-Bench compares four methods with direct execution. ARC-AGI-3 compares fixed VISTA* against memory-only/full-harness adaptation over 25 public games. Five EdgeBench games compare sequential refinement with harness scaling from Claude Code/Codex scaffolds; the metric is the best score reached during exploration.

## Quantitative Results

All scores are **author-reported**; no reproduction was performed.

| Condition and comparator | Scores | Source |
|---|---|---|
| Terminal, no tests, three-model mean: direct / parallel / evolution | 68.2 / 72.3 / 67.4 | Table 1 |
| Terminal, tests, mean pass@1: parallel / evolution | 82.0 / 69.7 | Table 2 |
| Terminal held-out mean: initial → evolved | 63.2 → 63.2 | Table 3 |
| ARC, Opus 4.8 RHAE: VISTA* → full harness | 43.3 → 77.5 | Table 4 |
| EdgeBench, Opus 4.8 mean: refinement → scaling | 48.3 → 54.7 | Table 5 |

## Limitations

Equal rollout counts do not establish identical dollar expenditure. Appendix A excludes harness-modification cost; including it would strengthen the negative Terminal comparison but should not be silently generalized to other budgets. Two repetitions provide limited uncertainty characterization. Public games and within-task best-score selection test adaptive discovery, not broad transfer. Offline evolution could amortize across deployment volume, which these comparisons do not fully quantify.

## Reproducibility

Public scripts implement the four methods and configuration/selection workflows; the README requires Python 3.13+, API credentials, and benchmark paths. Full experiment replication, game artifact completeness, and exact contemporary API behavior are **Not verified**. No execution was attempted.

## Open Research Questions

Which task properties predict when editable harnesses outperform trajectory search? Can gains persist under fresh task generators? What deployment volume amortizes search cost, and do conclusions survive matched total dollars, latency, and verification access?
