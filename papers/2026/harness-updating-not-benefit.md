# Harness Updating Is Not Harness Benefit: Disentangling Evolution Capabilities in Self-Evolving LLM Agents

Reviewed against primary sources on 2026-11-19. Quantitative findings below are author-reported, not independently reproduced.

## Full Paper Title

Harness Updating Is Not Harness Benefit: Disentangling Evolution Capabilities in Self-Evolving LLM Agents

## Authors and Affiliations

Minhua Lin; Juncheng Wu; Zijun Wang; Zhan Shi; Yisi Sang; Bing He; Zewen Liu; Tianxin Wei; Zongyu Wu; Zhiwei Zhang; Dakuo Wang; Xiang Zhang; Benoit Dumoulin; Cihang Xie; Yuyin Zhou; Suhang Wang; Hanqing Lu

PDF page 1 maps Lin, Zongyu Wu, Zhiwei Zhang, Xiang Zhang, and Suhang Wang to Pennsylvania State University; Juncheng Wu, Zijun Wang, Cihang Xie, and Yuyin Zhou to UC Santa Cruz; Shi, Sang, Bing He, Dumoulin, and Lu to Amazon; Liu to Emory; Wei to UIUC; Dakuo Wang to Northeastern University.

## Publication Date

2026-05-28; revised 2026-11-04; reviewed v2.

## Venue or Preprint Status

arXiv preprint; no conference acceptance independently verified.

## Paper URL / DOI

[arXiv](https://arxiv.org/abs/2605.30621) · [Full text](https://arxiv.org/html/2605.30621v2) · [arXiv DOI](https://doi.org/10.48550/arXiv.2605.30621).

## Official GitHub Repository

[Official release branch](https://github.com/A-EVO-Lab/a-evolve/tree/release/harness-evolution); the paper links this branch, and its README identifies the same paper. The repository default branch describes a broader agent-evolution project.

## Research Problem

End-to-end harness improvement scores conflate the ability to write useful guidance with the ability to execute it. The paper asks whether ordinary task-solving strength predicts either capability, and whether a costly frontier evolver is necessary.

## Methodology and Algorithm

Freeze model weights and iterate a common solve–evolve protocol. For solver a and evolver e, define gain Δ(a,e) against the initial harness. Harness-updating averages this gain over fixed anchor solvers; harness-benefit takes the maximum over fixed anchor evolvers. The latter is an empirical best-over-anchors statistic, not a model-intrinsic constant. Independent variation of solver and editor is the central experimental intervention.

## Key Contributions

The contribution is an attribution protocol and diagnostics for skill activation and sustained adherence. It separates a poor update from a useful update that the receiving model cannot load or follow; this distinction directly informs where training or inference budget should go.

## Experimental Setup

Seven evolver models and six solvers span Claude, Qwen, and GPT-OSS families. Anchor solvers/evolvers are Opus 4.6, Sonnet 4.6, and Qwen3-235B. Prompt templates, trajectory windows, task streams, evolution budget, and turn limits are held fixed within each benchmark. Tasks are scored before their evidence enters the next update: this is streaming evaluation.

## Benchmarks and Baselines

SWE-bench Verified, MCP-Atlas, and SkillsBench. The primary control is no evolution with the same solver; cross-model editor pairings diagnose attribution. Skills are editable on SWE/SkillsBench; skills, prompts, and memory on MCP-Atlas.

## Quantitative Results

Table 1 reports SWE base/gain pairs of 3.6%/+4.4 points for Qwen3-32B, 20.7%/+19.3 for Qwen3-235B, and 74.2%/+2.6 for Opus 4.6. Section 4.2 reports at most 3.1 points between editor-averaged gains on any benchmark. Table 2 gives skill-load rates 0.251 versus 0.957, and conditional harness-following rates 0.142 versus 0.757, for Qwen3-32B versus Opus. These are different metrics, not accuracy deltas.

## Limitations

Fixed-weight, mostly textual-artifact results do not establish the same scaling law for executable code search or co-training. The model grid is limited, adherence uses an LLM judge, and maxima over anchor editors can be selection-sensitive. A narrow editor spread is not proof that stronger editors never help.

## Reproducibility

Primary methods, tables, limitations, and the official branch README were inspected. Independent reruns were not performed. Reproduction requires exact model versions, ordered streams, and judge settings; aggregate post-evolution scores alone cannot reproduce the decomposition.

## Open Research Questions

Can activation and adherence training improve benefit without increasing editor strength? Does the same solver–editor matrix remain stable under distribution shift, executable harnesses, and total-cost matching?

Primary reading: Sections 3–4 and 6; Tables 1–3; Appendices 9–11.
