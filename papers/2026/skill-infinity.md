# Skill∞: Recursive Self-Improvement for Agent Skill Optimization

Reviewed against primary sources on 2026-11-19. Quantitative findings below are author-reported, not independently reproduced.

## Full Paper Title

Skill∞: Recursive Self-Improvement for Agent Skill Optimization

## Authors and Affiliations

Wangcheng Tao; Zhanglu Yan; Han Wu; Weng-Fai Wong

Wangcheng Tao, Zhanglu Yan, and Weng-Fai Wong: National University of Singapore. Han Wu: City University of Hong Kong.

## Publication Date

2026-10-26; reviewed v1.

## Venue or Preprint Status

arXiv preprint; no conference acceptance independently verified.

## Paper URL / DOI

[arXiv](https://arxiv.org/abs/2610.35434) · [Full text](https://arxiv.org/html/2610.35434v1) · [arXiv DOI](https://doi.org/10.48550/arXiv.2610.35434).

## Official GitHub Repository

[Official project repository](https://github.com/taowangcheng/Skill-Infinity); the paper and README identify it. The inspected README explicitly says the code will be released soon: this is a verified placeholder, not a verified runnable implementation.

## Research Problem

Skill optimizers often improve task guidance while leaving the improvement procedure fixed. Skill∞ makes that procedure a standard skill package and asks whether refining it improves subsequent task-skill optimization across domains.

## Methodology and Algorithm

A task skill is evaluated by average verifier reward. A Meta-Skill is evaluated by the average improvement its budgeted inner optimizations produce over seed task skills. The same agent-led loop optimizes either object: read history, diagnose traces, generate one or two candidates, evaluate, request isolated review, then select or backtrack. The meta agent allocates candidates and may retain a tied candidate when execution evidence supports progress. Scoring remains outside the editable package. Both task and meta skills load through native discovery from names/descriptions, making activation part of the optimization problem.

## Key Contributions

The contribution combines a recursively editable optimization procedure, cross-domain reuse of the refined Meta-Skill, and deployment-like skill activation. Independent review rejects unchanged, unused, or unusable candidates. This is a procedural learning system with frozen backbone weights; it does not demonstrate indefinite recursive acceleration.

## Experimental Setup

Main experiments use Codex CLI with GPT-6 Luna at high reasoning effort and Harbor trials. Task-skill search is capped at four candidates. SkillsBench covers 83 tasks in eight domains. KernelBench uses three level-3 problems and measures runtime on an NVIDIA A100. Reported results average five runs/trials as described in Section 4.1; optimization budgets are separately documented.

## Benchmarks and Baselines

No skill, human-curated skills, self-generated skills, SkillCreator, SkillEvolver, and a fixed seed-Meta-Skill ablation. Additional settings replace the backbone with GPT-5.6 Luna or the harness with OpenCode.

## Quantitative Results

Table 1 reports SkillsBench avg@5 pass rates: 60.7% full method, 56.4% human-curated, 54.5% SkillEvolver, and 55.9% without Meta-Skill self-improvement. Figure 3 gives correctness-weighted KernelBench speedup 1.62 versus 1.18 for SkillEvolver. Section 4.6 reports 8.7M input/66k output tokens per task-skill optimization; self-improvement costs roughly eleven such optimizations, adding under 15% when spread across 83 skills.

## Limitations

Skill expressiveness and verifier reliability bound the results. Procedure adherence is followed by the language model rather than mechanically enforced. Only three kernel problems are tested; budget-scaling results use a selected subset with remaining headroom. Aggregate gains mask domains where human-curated skills remain stronger, such as natural science and finance.

## Reproducibility

Primary methods, experiments, cost discussion, limitations, and repository status were inspected. Independent reruns were not performed. Paper appendices expose seed packages and prompts, but the current repository placeholder prevents verifying a complete runnable reproduction.

## Open Research Questions

Which Meta-Skill revisions improve optimization on entirely new task distributions under a fixed total budget? Can independent review stay reliable when the procedure that requests and interprets review is itself editable?

Primary reading: Section 3; Section 4; Tables 1–2; Figures 3–5; Limitations; Appendices B, C, E, G.
