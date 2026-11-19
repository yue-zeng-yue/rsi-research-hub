# Knowledge in the Harness, Reliability in the Weights

Evidence cutoff: 2026-11-19. Results below are author-reported, not independently reproduced.

## 1. Full Paper Title

Knowledge in the Harness, Reliability in the Weights: Teacher-Free Co-Evolution of an LLM Agent.

## 2. Authors and Affiliations

Yujia Zhang, Xinqi Ren, Shixiong Zhou, and Jia Meng; Brightendata. Zhang and Ren contributed equally. [Title block](https://arxiv.org/html/2611.15268v1).

## 3. Publication Date

First submission: 2026-11-11; reviewed version: v1. [Submission history](https://arxiv.org/abs/2611.15268).

## 4. Venue or Preprint Status

arXiv preprint; peer-reviewed acceptance: Not verified.

## 5. Paper URL / DOI

[Full paper](https://arxiv.org/html/2611.15268v1); [arXiv record](https://arxiv.org/abs/2611.15268). The record lists DOI 10.48550/arXiv.2611.15268 as pending registration at verification.

## 6. Official GitHub Repository

[Brightendata/knowledge-in-the-harness](https://github.com/Brightendata/knowledge-in-the-harness) is explicitly paper-linked. Its accessible README declares Apache-2.0 for code, generated tasks, plugins, and records; upstream τ² policies and Gemma weights retain separate terms.

## 7. Research Problem

Can a small agent improve both policy knowledge and consistent execution using deployment evidence without a stronger teacher? The paper separates accessible knowledge in skills from reliability learned in weights.

## 8. Methodology and Algorithm

Each round alternates `(H, θ) → (H′, θ) → (H′, θ′)`. A fixed base model diagnoses failures and appends bounded rules to on-demand skills; policy text and routing remain immutable. Evidence includes tool writes, database differences, rewards, and skill loads. Code checks, counterexample review, paired retests, attributed reversions, and a global validation gate control acceptance. Crucially, the editor remains base M0, not the improved adapter: this does not demonstrate an improving improver.

GRPO trains rank-32 LoRA on complete conversations using group-relative rewards, clipped policy updates, no KL penalty, and difficulty-dependent rollout counts. Prefix-tree packing shares repeated context. Validation selects using `100 × (0.8 pass¹ + 0.2 pass⁴)`. Here passᵏ estimates all k trials succeeding, not pass@k's at-least-one success. [Sections 3–4](https://arxiv.org/html/2611.15268v1).

## 9. Key Contributions

A concrete two-layer adaptation pipeline, documented evidence gates, and cross-factorial analysis support complementary roles: rules repair missing policy knowledge; weight training stabilizes execution. These are bounded two-round findings, not evidence of unbounded recursive acceleration.

## 10. Experimental Setup

Gemma 4 12B runs two rounds on four A100/A800 80-GB GPUs. Each domain has 200 generated validation tasks and three 300-task training batches; only the first two batches are used. The generator uses benchmark databases and public knowledge-point coverage, while excluding official task scenarios from optimization. The authors report approximately 84 hours and 50,000 conversations per round across both domains; this is their configuration, not a current cost estimate.

## 11. Benchmarks and Baselines

τ²-bench 1.0.1, commit `4ce7c03`, supplies 114 retail and 50 airline official tasks, four trials each. Baselines include the same model with the whole policy in its prompt, the initial skills harness, and crossed final-harness/base-weights and initial-harness/final-weights systems. DeepSeek-V4.1-Flash simulates users; GPT-4.1 judges retail assertions. Thus teacher-free does not mean no external model calls. Simulator differences also prevent direct public-leaderboard comparisons.

## 12. Quantitative Results

After two rounds, retail pass¹/pass⁴ moves from 72.6/48.2 to 85.1/66.7%; airline moves from 56.0/38.0 to 75.5/60.0%. Retail rules-only and weights-only crossed systems score 77.4/48.2 and 78.3/54.4%; the combined system exceeds both. These crossed ablations are not independently optimized single-layer training controls. [Table 2 and section 5](https://arxiv.org/html/2611.15268v1).

## 13. Limitations

One model, two domains, two rounds, small official test sets, and benchmark-informed coverage limit transfer claims. Individual accepted updates need not be statistically significant. A noise-calibrated gate cannot guarantee no regression.

## 14. Reproducibility

Read sections 3–5 and appendices C–D. The verified [repository README](https://github.com/Brightendata/knowledge-in-the-harness#reproducing-the-paper) documents pinned environments, model revision, generated splits, compact run records, adapters, and table-recomputation scripts. Repository availability is not independent reproduction; no scripts or training were executed here.

## 15. Open Research Questions

Does replacing the fixed editor with improved weights improve subsequent optimization? Can gains survive policy changes and unrelated domains? What matched-budget comparison separates coadaptation from additional rollout and validation expenditure?
