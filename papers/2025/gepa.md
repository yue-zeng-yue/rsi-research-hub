# GEPA: reflection-guided prompt evolution

Evidence cutoff: **2026-11-19**. This note uses the **2026 v2 revision**, not the smaller 2025 v1 study. Results are author-reported; not reproduced. Classification: prompt optimization with frozen model weights.

## 1. Full Paper Title

*GEPA: Reflective Prompt Evolution Can Outperform Reinforcement Learning*.

## 2. Authors and Affiliations

Lakshya A Agrawal, Shangyin Tan, Dilara Soylu, Noah Ziems, Rishi Khare, Krista Opsahl-Ong, Arnav Singhvi, Herumb Shandilya, Michael J Ryan, Meng Jiang, Christopher Potts, Koushik Sen, Alexandros G. Dimakis, Ion Stoica, Dan Klein, Matei Zaharia, Omar Khattab. Listed institutions: UC Berkeley; Stanford; University of Notre Dame; Databricks; BespokeLabs.ai; MIT. Specifically: Agrawal/Tan/Khare/Sen/Stoica/Klein at Berkeley; Soylu/Shandilya/Ryan/Potts at Stanford; Ziems/Jiang at Notre Dame; Opsahl-Ong at Databricks; Singhvi at Stanford/Databricks; Dimakis at Berkeley/BespokeLabs.ai; Zaharia at Berkeley/Databricks; Khattab at MIT. [Title page](https://arxiv.org/html/2507.19457v2)

## 3. Publication Date

First submission **2025-07-25**; inspected revision **2026-02-14, v2**.

## 4. Venue or Preprint Status

**ICLR 2026 Oral**, as declared in the author-submitted arXiv record. [Record](https://arxiv.org/abs/2507.19457)

## 5. Paper URL / DOI

[Full text v2](https://arxiv.org/html/2507.19457v2); [DOI](https://doi.org/10.48550/arXiv.2507.19457).

## 6. Official GitHub Repository

[gepa-ai/gepa](https://github.com/gepa-ai/gepa), linked by the paper, and [gepa-ai/gepa-artifact](https://github.com/gepa-ai/gepa-artifact) for research artifacts. Both inspected repositories report MIT and are unarchived. The library's observed last push was 2026-11-09; this does not establish that HEAD reproduces v2.

## 7. Research Problem

Can execution traces and language feedback adapt compound LM systems with fewer sampled trajectories than scalar-reward training?

## 8. Methodology and Algorithm

Reflect on failures, mutate one prompt, test on a minibatch, and retain improving candidates. Instance-wise Pareto selection preserves complementary candidates rather than only the aggregate winner. Weights remain fixed; final selection maximizes validation performance.

## 9. Key Contributions

Combines reflection, evolutionary search, and candidate diversity; supports multi-prompt systems and closed model APIs.

## 10. Experimental Setup

Six tasks; Qwen3 8B and GPT-4.1 Mini; held-out evaluation. GRPO primarily uses LoRA, with full-finetuning analysis also reported.

## 11. Benchmarks and Baselines

HotpotQA, IFBench, HoVer, PUPA, AIME-2025, LiveBench-Math; GRPO, MIPROv2, TextGrad, and Trace/OptoPrime.

## 12. Quantitative Results

Qwen3 aggregate scores: **54.85 GEPA versus 48.91 GRPO**. AIME reverses that ordering: **32.00 versus 38.00**. IFBench reaches **38.61** versus **35.88**, with best GEPA reached after 678 rollouts versus GRPO's 24,000. Do not confuse best-checkpoint rollout count with the full search budget. [Section 4, Tables 1–2](https://arxiv.org/html/2507.19457v2)

## 13. Limitations

These results do not establish universal superiority to RL. Research implication: richer feedback, model choice, prompt length, optimizer compute, and repeated validation selection can all affect comparisons. No optimizer self-rewrite or autonomous task invention is established by prompt mutation alone.

## 14. Reproducibility

The library exposes adapters for evaluation and reflective datasets and supports installation with `pip install gepa`; the research artifact should be the starting point for paper replication. Pin both repositories, task splits, model snapshots, feedback access, and budgets. Record reflection-model tokens separately from task rollouts: equal rollout counts need not mean equal cost. Current monetary cost and GPU-hours for exact v2 reproduction: **Not verified**. No optimization was executed here. [Official library](https://github.com/gepa-ai/gepa)

## 15. Open Research Questions

Proposed studies: Does prompt evolution transfer to unseen tools and environments? Can validation allocation reduce search cost without increasing selection bias? Under matched feedback and token budgets, when does prompt optimization complement weight updates? How does a verifier detect prompts that exploit its scoring assumptions? Measure gains after removing task-specific feedback and under independently authored holdouts.
