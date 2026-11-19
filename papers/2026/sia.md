# SIA: Self Improving AI with Harness & Weight Updates

Reviewed against primary sources on 2026-11-19. Quantitative findings below are author-reported, not independently reproduced.

## Full Paper Title

SIA: Self Improving AI with Harness & Weight Updates

## Authors and Affiliations

Prannay Hebbar; Yogendra Manawat; Samuel Verboomen; Alesia Ivanova; Selvam Palanimalai; Kunal Bhatia; Vignesh Baskaran

Not verified: the inspected primary HTML front matter lists authors without institutional affiliations. Hexo Labs maintains the official repository and links the paper, which does not establish every author’s affiliation.

## Publication Date

2026-05-26; revised 2026-05-28; reviewed v2.

## Venue or Preprint Status

arXiv preprint; no conference acceptance independently verified.

## Paper URL / DOI

[arXiv](https://arxiv.org/abs/2605.27276) · [Full text](https://arxiv.org/html/2605.27276v2) · [arXiv DOI](https://doi.org/10.48550/arXiv.2605.27276).

## Official GitHub Repository

[Official SIA repository](https://github.com/hexo-ai/sia); its README links arXiv 2605.27276 and documents the same framework.

## Research Problem

Scaffold search and model training can each saturate while the other component remains a bottleneck. SIA proposes a single feedback-driven loop able to modify the task agent’s runtime or invoke a weight-update procedure.

## Methodology and Algorithm

A Meta-Agent initializes a task-specific scaffold. The Feedback-Agent reads source, full execution trajectories, and verifier outcomes, then selects a harness edit or training action. Claude Sonnet 4.6 fills meta/feedback roles; GPT-OSS-120B is the task model with LoRA rank 32, learning rate 4×10^-5 on H100 infrastructure. The reported experiments first iterate scaffolds and switch after stagnation. Observed training recipes differ: PPO/GAE for legal classification, reward-exponentiated weighting for kernels, and GRPO for denoising. The selector remains a frozen-model prior.

## Key Contributions

The contribution is an operational interface combining two adaptation levers across three different task types. It produces an evolved scaffold and adapted model. The paper’s discussion of richer algorithm selection extends beyond its three main experiments and should not be treated as a comprehensive controlled ablation.

## Experimental Setup

LawBench has 5,332 training and 913 nominal test samples for 191-class criminal-charge classification. TriMul optimizes a fixed GPU-kernel input shape on H100. Denoising tunes and modifies a MAGIC-based pipeline for pancreas scRNA-seq data. Metrics and verifiers differ by domain, so the results are not a common accuracy scale.

## Benchmarks and Baselines

The main comparisons are initial meta-agent scaffold, harness-only best (SIA-H), and harness-plus-weight best (SIA-W+H), with reported prior best task references. A matched-cost weight-only baseline and extensive independent seeds are not established by the inspected results.

## Quantitative Results

Table 3 gives LawBench accuracy 13.5% initial, 50.0% harness-only, 70.1% combined. TriMul reward 1500/runtime rises 0.105→0.120→1.475, with harness-only 12,483 microseconds versus combined 1,017. Denoising’s higher-is-better normalized score is 0.048→0.241→0.289. The legal increase over prior 45.0% is 25.1 percentage points; it should not be described as a 25.1% relative improvement.

## Limitations

A material evaluation issue is explicit in Section 6.3.1: generated scripts are executed against the LawBench test split to produce PPO rewards, although the same split is called held-out. Thus 70.1% is not demonstrated untouched final generalization. Fixed-shape kernel and one-dataset denoising results are narrow. The paper acknowledges coupled optimization against one verifier can overfit. No theorem establishes its stated equilibrium interpretation.

## Reproducibility

Full methods/results/limitations and official README were inspected; independent reruns were not performed. Exact scripts, verifier access, training traces, and budgets would need auditing before using the headline gains as a clean held-out comparison. Repository existence alone does not resolve the feedback/test boundary.

## Open Research Questions

Can a learned selector outperform fixed stagnation-triggered switching under a shared budget and untouched holdout? Which gains survive new kernel shapes, new biological datasets, or a fresh legal evaluation set?

Primary reading: Sections 3, 5–9; Tables 2–3; Figures 4–6.
