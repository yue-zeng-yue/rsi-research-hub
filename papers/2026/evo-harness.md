# Evo-Harness: Context-to-Harness Skill Compilation for Self-Evolving Agents

Reviewed against primary sources on 2026-11-19. Quantitative findings below are author-reported, not independently reproduced.

## Full Paper Title

Evo-Harness: Context-to-Harness Skill Compilation for Self-Evolving Agents

## Authors and Affiliations

Tianxin Wei; Zhan Shi; Minhua Lin; Bing He; Zewen Liu; Yisi Sang; Yuanchen Bei; Xuying Ning; Jiaru Zou; Ting-Wei Li; Xiao Lin; Yanjun Zhao; Chi Wang; Benoit Dumoulin; Dakuo Wang; Jingrui He; Hanqing Lu

University of Illinois Urbana-Champaign: Wei, Bei, Ning, Zou, Li, Lin (Xiao), Zhao, He (Jingrui). Amazon: Shi, He (Bing), Sang, Dumoulin, Lu. Pennsylvania State University: Lin (Minhua). Emory University: Liu. AG2 AI: Wang (Chi). Northeastern University: Wang (Dakuo).

## Publication Date

2026-08-15; revised 2026-08-30; reviewed v2.

## Venue or Preprint Status

arXiv preprint; no conference acceptance independently verified.

## Paper URL / DOI

[arXiv](https://arxiv.org/abs/2608.15071) · [Full text](https://arxiv.org/html/2608.15071v2) · [arXiv DOI](https://doi.org/10.48550/arXiv.2608.15071).

## Official GitHub Repository

[Official release branch](https://github.com/A-EVO-Lab/a-evolve/tree/release/evo-harness); the paper links this branch and its README names the same paper.

## Research Problem

Online agents often get only one execution of a task. Raw context mixes reusable lessons with incidental details. Evo-Harness studies how to convert failure experience into guidance that helps later tasks while keeping solver weights fixed.

## Methodology and Algorithm

After an unsuccessful execution, the solver proposes a structured memory with lesson, trigger, evidence, and scope. A separate evolver compares proposals with the current library and chooses add, merge, revise, or skip. It compiles both cross-task guidance and topic-specific procedures. Selected skills are injected into subsequent execution context under a bounded selection interface. Batch updates let the evolver detect common patterns across failures; this differs from retaining an unfiltered transcript.

## Key Contributions

The work contributes an online harness-learning formulation, a two-stage reflection/compilation pipeline, and analyses separating feedback quality, solver capacity, topic/general skills, and cross-model transfer. Editable artifacts are natural-language guidance, not rewritten executable control flow.

## Experimental Setup

Claude Opus 4.6 is the default solver and evolver. Additional analyses use Opus 4.7/4.5, Kimi-K2.5, and GPT-OSS. Streams span 1,899 CL-Bench, 89 Terminal-Bench, 300 SWE-bench Lite, 165 τ-bench, and 80 WebArena-Infinity tasks. Shared protocols are used for baselines. Online stream scores and frozen train-split transfer are separate experiments.

## Benchmarks and Baselines

AWM, Dynamic Cheatsheet cumulative/retrieval variants, Evo-Memory, ACE, XSkill, and no evolution. Component controls remove solver proposals or retain only general/topic guidance; feedback controls compare self-judgment with environment pass/fail and richer diagnostics.

## Quantitative Results

Table 1, Opus 4.6: CL-Bench rises 29.54→34.02%, Terminal-Bench 62.92→73.03%, SWE-bench Lite 63.67→67.00%, τ-bench 72.73→76.97%, and WebArena-Infinity 72.50→76.25%. Table 4 shows self-generated feedback regresses to 27.96% and 61.67% on CL/SWE. Minimal grounded feedback reaches SWE 67.33%, slightly above richer feedback’s 67.00%, so more detail is not uniformly better.

## Limitations

The main evidence concerns sequential adaptation, not solely a frozen final harness on untouched tasks. Textual skills and single-agent settings limit generalization to executable or multi-agent systems. Category gains are uneven: Opus 4.6 empirical-discovery tasks decline 2.5 points. A strong solver may use guidance that a weaker solver cannot; cross-model transfer is not automatic.

## Reproducibility

Primary algorithms, result tables, feedback analyses, limitations, and the official branch README were inspected. Independent reruns were not performed. Reproduction must retain task order, batching, feedback availability, skill-selection budget, and exact model variants; a five-benchmark average would conceal materially different feedback regimes.

## Open Research Questions

How should online compilers detect harmful or obsolete skills without expensive replay? Can guided training improve skill adherence, and how does a cost-aware selector decide when topic-specific detail becomes overfitting?

Primary reading: Section 3; Section 4; Tables 1–4; Limitations; Appendices A, F, I.
