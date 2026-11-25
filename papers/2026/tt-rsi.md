# Test-Time Recursive Self-Improvement

**Reviewed:** 2026-11-25. **Evidence:** Primary-reviewed; results are author-reported. No independent run.

## Full Paper Title

Beyond Self-Consistency: Recursive Self-Improvement at Test Time

## Authors and Affiliations

Jianyu Wu, Yizhou Wang, Encheng Su, Jinouwen Zhang, Pengze Li, Lintao Wang, Chen Tang, Aoran Wang, Wanli Ouyang, and Shixiang Tang. The title block lists Shanghai Jiao Tong University, Shanghai Artificial Intelligence Laboratory, The Chinese University of Hong Kong, University of Science and Technology of China, Fudan University, and University of Sydney. Individual mappings are **Not verified** because the HTML affiliation associations are malformed.

## Publication Date

First submission and reviewed v1: 2026-11-23, 16:33:00 UTC, or November 24 in Asia/Shanghai. The index uses the arXiv UTC date.

## Venue or Preprint Status

arXiv preprint; peer-reviewed acceptance **Not verified**.

## Paper URL / DOI

[Canonical record](https://arxiv.org/abs/2611.30965) · [Reviewed v1](https://arxiv.org/html/2611.30965v1). The record lists `10.48550/arXiv.2611.30965` with registration pending.

## Official GitHub Repository

**Not verified:** no paper-specific author-linked repository was identified in the record, full text, or exact-name search.

## Research Problem

Use answer refinement, rather than majority agreement alone, as test-time supervision.

## Methodology and Algorithm

In-Context RSI re-solves using the previous visible solution. In-Weight RSI distills answering and refinement with a frozen initial teacher conditioned on evolving references. Main experiments adapt to the benchmark's unlabeled questions; labels are reserved for scoring. See Sections 3–4.

## Key Contributions

**Review assessment:** improving the reference-generating policy while retaining a fixed distillation teacher is a useful distinction. The exact-backup theory should not be treated as a guarantee for finite neural optimization. Neither answer refinement nor distillation alone establishes an autonomous general-purpose researcher.

## Experimental Setup

Qwen3-1.7B/4B/8B; 100 adaptation updates; rank-64 LoRA; 11 inference attempts; avg@12 evaluation. Appendix C reports seed 42, not multiple independent adaptation seeds.

## Benchmarks and Baselines

Five mathematics benchmarks: AIME 2025/2026, HMMT 2025/2026, and BRUMO 2025. Controls include TTRL, TTPO, OPSD-TTT, CANON, and U-OPSD. Appendix D matches TTPO plus self-consistency by **generated tokens**, excluding reference-input cost.

## Quantitative Results

Table 1, Qwen3-4B benchmark-average accuracy: base **55.76%**, TTPO plus self-consistency **65.76%**, TT-RSI **69.64%**. Thus the latter comparison is **+3.88 percentage points**, under the stated output-token accounting. Table 4 separately evaluates transfer without target adaptation.

## Limitations

**Review analysis:** unlabeled adaptation on the scored questions is a legitimate transductive setting, but it answers a different question from performance on untouched task inputs. The main result and cross-task transfer result must remain separate in summaries and future experiments.

Equal generated tokens are not necessarily equal prefill work, memory consumption, latency, GPU-hours, or monetary cost. Sequential refinement can also have different latency from parallel voting. Count the complete adaptation and inference workload when comparing deployment economics.

The theory assumes exact distributional backups; actual token-level optimization, finite samples, and changing error correlations can violate that idealization. Fixed-point reasoning does not guarantee improvement when refinement breaks correct answers too often. A reliable reproduction should log fix and break transitions and report uncertainty by problem and by independent adaptation run.

## Reproducibility

Inspected Sections 2–4, Tables 1 and 4–6, theoretical assumptions, and Appendices B–D. No training or evaluation was run. A public implementation and variance over independent full adaptation runs are **Not verified**.

## Open Research Questions

Does the gain survive matching total wall time and input-plus-output compute? Freeze the adapted model before an unseen-family audit, and compare frozen versus evolving reference policies from identical states. Separately test whether later policies improve a common starting solver more efficiently, rather than merely refining their own answers better.
