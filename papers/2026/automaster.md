# AutoMaster

**Reviewed:** 2026-11-25. **Evidence:** Primary-reviewed; results are author-reported. No independent run.

## Full Paper Title

AutoMaster: Autonomous Post-Training by Making the Same Model a Better Teacher

## Authors and Affiliations

Guoxin Chen, Shuang Sun, Fanzhe Meng, Xinyu Tang, Ruihua Song, and Wayne Xin Zhao; Gaoling School of Artificial Intelligence, Renmin University of China.

## Publication Date

First submission: 2026-11-19, 17:57:59 UTC, corresponding to November 20 in Asia/Shanghai. Reviewed v2: 2026-11-20, 11:55:50 UTC. The catalog retains the arXiv first-submission date; this is a newly admitted review, not a newly first-published November 20 paper in UTC.

## Venue or Preprint Status

arXiv preprint; peer-reviewed acceptance **Not verified**.

## Paper URL / DOI

[Canonical record](https://arxiv.org/abs/2611.26510) · [Reviewed v2](https://arxiv.org/html/2611.26510v2). arXiv-listed DOI: `10.48550/arXiv.2611.26510`.

## Official GitHub Repository

[RUCAIBox/AutoMaster](https://github.com/RUCAIBox/AutoMaster), linked by the paper. Inspected commit `116c295dfdb7729e8f8684d85dea867c5fd9806e`, including the [README](https://github.com/RUCAIBox/AutoMaster/blob/116c295dfdb7729e8f8684d85dea867c5fd9806e/README.md) and file inventory. The release provides nine skills, inference recipes, and a pinned AweAgent submodule. It links checkpoints and data; those downloads were not inspected. A complete autonomous training controller was not found in the inspected tree. Label this a **partial artifact release**, not a verified end-to-end reproduction package.

## Research Problem

Improve what a fixed teacher demonstrates, beyond filtering trajectories by successful outcomes.

## Methodology and Algorithm

An agent revises teacher skills and selects demonstrations using rollout and student-evaluation feedback. Skill-FT retains skill text in the SFT input but removes generated skills at evaluation. Every round trains from the same initial student checkpoint; experiment history persists. See Section 3.

## Key Contributions

**Review assessment:** the distinction between demonstration generation and selection makes the method relevant to [model RSI](../../docs/model-rsi.md). The teacher is fixed; this is not a sequence in which a better student automatically becomes the next teacher. Skill internalization should be compared with existing distillation methods before claiming a new general RSI mechanism.

## Experimental Setup

GPT-6 Astra proposes interventions; DeepSeek-V4-Pro-Preview teaches Qwen3.5-4B/9B students. Five outer rounds; each SFT run uses 512 trajectories. Three repeated evaluations per checkpoint measure evaluation variability, not independent optimization seeds. See Section 4 and Appendix A.

## Benchmarks and Baselines

Terminal-Bench 2.1, BrowseComp-Lite-185, and Doc2Repo; base, Vanilla SFT, task-matched SFT, and component ablations. Matching demonstrations and the SFT recipe does not equalize the whole discovery cost.

## Quantitative Results

Table 1: Terminal-Bench 2.1, 9B, mean ± SD: Vanilla SFT **26.59 ± 1.30%**, AutoMaster **35.58 ± 1.30%**. Appendix A.6 gives the **+8.99 percentage-point** paired interval **[2.25, 16.10]**. The 4B BrowseComp and Doc2Repo intervals include zero.

## Limitations

**Review analysis:** Appendix A.4 feeds benchmark scores and trajectories into later experimentation and final checkpoint choice. These evaluations cannot simultaneously function as an untouched final audit. A separate task-family test is needed to estimate transfer without adaptive selection.

The reported intervals concern tasks for selected checkpoints. They do not cover the variability of rerunning the full agent-driven search, dataset construction, and training. Positive mean changes in every setting should not be restated as statistically established gains everywhere.

Keeping skills in the input also changes conditioning. The controlled removal ablation is useful, but it does not by itself isolate a unique cognitive explanation for internalization. A next study should compare semantically equivalent paraphrases, irrelevant instructions, and length-matched context.

## Reproducibility

Read Sections 3–5 and Appendices A.1–A.6; inspected the official release scope and immutable repository snapshot. No model training, checkpoint evaluation, or artifact download was performed. Full-loop cost equivalence and independent search replication are **Not verified**.

## Open Research Questions

Does skill-guided data construction still win with equal proposer, teacher, and training budgets on a sealed audit? Compare generation-only, selection-only, and joint interventions using paired tasks, then repeat the entire search. Test student-to-teacher succession separately instead of inferring it from repeated SFT.
