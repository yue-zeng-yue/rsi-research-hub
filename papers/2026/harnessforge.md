# HarnessForge: Joint Harness and Policy Evolution for Adaptive Agent Systems

Reviewed against primary sources on 2026-11-19. Quantitative findings below are author-reported, not independently reproduced.

## Full Paper Title

HarnessForge: Joint Harness and Policy Evolution for Adaptive Agent Systems

## Authors and Affiliations

Mingju Chen; Can Lv; Guibin Zhang; Heng Chang; Shiji Zhou

PDF page 1 maps Mingju Chen, Can Lv, and Shiji Zhou to Beijing Advanced Innovation Center for Future Blockchain and Privacy Computing, School of Artificial Intelligence, Beihang University; Heng Chang to Tsinghua University. Guibin Zhang has no affiliation superscript in that source, so his affiliation is Not verified.

## Publication Date

2026-06-01; proceedings October 2026; reviewed v1.

## Venue or Preprint Status

Published in Proceedings of EMNLP 2026, pages 43130–43155, Budapest, October 2026; verified by the [ACL Anthology record](https://aclanthology.org/2026.emnlp-main.1893/). Anthology lists DOI 10.18653/2026.emnlp-main.1893 and a SAC Highlight Award. The reviewed technical body is the arXiv version.

## Paper URL / DOI

[arXiv](https://arxiv.org/abs/2606.01779) · [Full text](https://arxiv.org/html/2606.01779v1) · [arXiv DOI](https://doi.org/10.48550/arXiv.2606.01779).

## Official GitHub Repository

[Official implementation](https://github.com/mingju-c/HarnessForge); the paper links it. README includes generated harnesses, paired manifests, production prompts, benchmark runners, and training utilities.

## Research Problem

An improved runtime and improved policy may still perform poorly together. HarnessForge treats the coupled harness–policy pair as the adaptation unit, seeking task-regime-specific compatibility rather than assuming components improve independently.

## Methodology and Algorithm

The harness has planning, action, and memory modules; the policy is a base reasoner plus a lightweight adapter. A meta-agent diagnoses failures, retrieves relevant archive exemplars, and proposes executable module edits. Smoke tests and successive half-selection filter candidates using a Pareto vector of quality, negative token cost, and negative latency. Survivors inherit their parent policy states and train separately on success-filtered trajectories collected under their own harness. These matched pairs populate the next round; successful rollout evidence is reused rather than requiring a wholly separate alignment collection.

## Key Contributions

The method links fault localization, budgeted multiobjective harness search, lineage-specific policy alignment, and cross-pair compatibility evaluation. It supports SFT by default and studies GRPO/RLOO replacements. The external GPT-5.5 proposer is fixed; it is not itself the learned recursive object.

## Experimental Setup

Qwen3-4B and Qwen3-8B backbones undergo three evolution rounds, with eight proposed harnesses and two retained survivors per round in the main setting. The appendices specify dataset splitting/deduplication, adapters, executable interfaces, and budget conventions. Default policy alignment uses curated successful trajectories.

## Benchmarks and Baselines

ToolHop, HotpotQA, 2WikiMultiHopQA, RestBench-TMDB, and API-Bank. Search baselines include ADAS, AgentSquare, AFlow, MaAS, and MermaidFlow; training baselines include SFT, GRPO, and RLOO. SearchQA is a macro-F1 aggregate, while TMDB and API-Bank include success/path/API metrics.

## Quantitative Results

Table 1: Qwen3-4B TMDB success is 76.00%, versus the strongest baseline GRPO at 64.00%—a 12.00 percentage-point gain, not 12% relative. ToolHop answer correctness is 52.82% versus 49.74% GRPO. Figure 4 reports API-Bank matched final-pair 77.19%, versus 71.93% for the final harness with earlier policies and 71.06% for the final policy with earlier harnesses. Qwen3-8B does not lead every metric: GRPO ToolHop path is 75.62 versus 74.05.

## Limitations

Compatibility evidence is compelling for the studied lineages but does not establish universal co-evolution superiority. The system depends on an external frontier proposer, executable benchmark adapters, and success-filtered data. Rollout budgets are not complete proposer/training costs. The primary main text has no extensive standalone limitations section; broader model scaling and repeated-search uncertainty remain unclear.

## Reproducibility

Primary method, tables, appendix protocol, and official code README were inspected; independent reruns were not performed. README notes shared training toolkit copies without bundled datasets/weights, so manifests alone do not establish complete artifact availability.

## Open Research Questions

How can the population preserve compatibility while sharing useful modules across lineages? Would explicit cross-pair robustness objectives outperform specialization, and what is the full cost of maintaining multiple adapters?

Primary reading: Sections 3–4; Tables 1–3; Figure 4; Appendices B–F; official ACL Anthology record.
