# RSI-Env: An Open-Ended Environment for Recursive Self-Improvement of Agents

Reviewed against primary sources on 2026-11-19. Quantitative findings below are author-reported, not independently reproduced.

## Full Paper Title

RSI-Env: An Open-Ended Environment for Recursive Self-Improvement of Agents

## Authors and Affiliations

Wanying Qu; Zhiyuan Fan; Jiyao Liu; Jiang Zhou; Jianghan Shen; Yanwei Fu; Dongrui Liu

Qu and Liu (Jiyao): Fudan University. Fan: Hong Kong University of Science and Technology. Zhou: Georgia Institute of Technology. Shen: Nanjing University and Shanghai Artificial Intelligence Laboratory. Fu: Fudan University and Shanghai Innovation Institute. Liu (Dongrui): Shanghai Artificial Intelligence Laboratory.

## Publication Date

2026-11-01; reviewed v1.

## Venue or Preprint Status

arXiv preprint; no conference acceptance independently verified.

## Paper URL / DOI

[arXiv](https://arxiv.org/abs/2611.01736) · [Full text](https://arxiv.org/html/2611.01736v1) · [arXiv DOI](https://doi.org/10.48550/arXiv.2611.01736).

## Official GitHub Repository

Not verified: no official repository was linked in the inspected paper or identified by exact-title repository searches.

## Research Problem

Many self-improvement experiments prescribe an objective and retain a fixed external improver. RSI-Env instead studies persistent research in which an updated model–harness system becomes the improver for the next round, including settings without benchmark targets or feedback.

## Methodology and Algorithm

The system state includes model weights, executable harness, persistent research artifacts, and externally managed resources. An improver chooses model training, harness modification, or both. A Host Controller protects inference/training services, evaluation, and lineage records. Crucially, candidate registration checks validity and executability, not improved capability; capability is measured independently. In Self, the registered successor conducts subsequent research. In Teacher, an external fixed agent continues improving the target.

## Key Contributions

The contribution is infrastructure for recursive handoff, durable research state, and an autonomy spectrum. Open-General leaves direction unspecified; Capability-Directed names a broad capability; Benchmark-Guided exposes a named target and its feedback. This separates independent measurement from the acceptance mechanics.

## Experimental Setup

Qwen3.8-27B starts with a minimal loop, bash, and compaction. Self is compared with Codex using GPT-5.6 Sol or GPT-6 Astra at High effort. Every run is allocated ten three-hour rounds, though teachers often terminate much earlier. Tinker supports SFT and custom RL operations. Hardware includes separate 32-A800-GPU training and inference services.

## Benchmarks and Baselines

Seven improvement tasks span general, reasoning, knowledge, agentic, and three benchmark-guided goals. Independent evaluation uses GPQA Diamond (198), AIME 2026 (30), Terminal-Bench 2.1 (89), and a fixed 500-item SimpleQA subset. The first, second, and fourth use avg@3; terminal evaluation uses pass@3. These metrics must not be merged as if identical.

## Quantitative Results

Table 1: Open-General Self raises GPQA 65.2→73.2% and AIME 53.3→56.7%, but lowers terminal pass@3 12.4→9.0% and SimpleQA 82.0→77.2%. Figure 4’s Knowledge Self sequence improves SimpleQA 82.0→85.0→88.0% via a harness update followed by SFT on 48 constructed examples. Its final Table 1 GPQA is 53.0%, a 12.2-point regression from the base.

## Limitations

Only a few accepted successors and one starting model are studied. Improvement is selective, not broadly monotonic. Equal allocated wall time does not mean equal consumed compute: teachers finish early and the Self loop uses much more of its allowance. The protected controller guarantees an evaluation boundary, not safety or statistical improvement.

## Reproducibility

Primary architecture, evaluation settings, result table, and handoff example were read; independent reruns were not performed. Full runnable code availability is not verified. Research-state snapshots and precise data-generation records would be required to distinguish lasting procedural gains from harness-specific or narrow factual adaptations.

## Open Research Questions

How can successor admission preserve multiple capabilities without turning open-ended discovery into benchmark optimization? Can update quality improve across many generations under a controlled consumed-compute budget, with the external controller remaining fixed?

Primary reading: Sections 3–5; Table 1; Figure 4; Appendix A.
