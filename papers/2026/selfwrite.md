# SelfWrite

**Reviewed:** 2026-11-25. **Evidence:** Primary-reviewed; results are author-reported. No independent run.

## Full Paper Title

Recursive Self-Editing: LLMs Program Their Own Weight Edits for Self-Improvement

## Authors and Affiliations

Linghua Zhang and Yunhe Li. Affiliations: **Not verified**; the inspected arXiv record and HTML title block do not supply institutional affiliations.

## Publication Date

First submission and reviewed v1: 2026-11-22, 14:30:51 UTC.

## Venue or Preprint Status

arXiv preprint. Peer-reviewed acceptance: **Not verified**.

## Paper URL / DOI

[Canonical record](https://arxiv.org/abs/2611.29513) · [Reviewed v1](https://arxiv.org/html/2611.29513v1). The record lists `10.48550/arXiv.2611.29513` with registration pending.

## Official GitHub Repository

**Not verified:** no paper-specific author-linked implementation was identified in the record, full text, or exact-name code search. Do not substitute a similarly named repository.

## Research Problem

Test whether an updated model can author further direct edits to its own weights.

## Methodology and Algorithm

The current model programs low-rank edits using weight and activation tools. Eight sessions propose candidates; a hidden paired gate admits the best positive change. Merged weights become the next editor, with retained history. No gradient tool is used. Sections 3–4 distinguish screen, gate, and test data.

## Key Contributions

**Review assessment:** succession of the edited model is an explicit recursive mechanism. It still needs a separate causal test of whether the later editor is better at editing. Nearby November work includes [Language Models Can Rewrite Their Own Weights](https://arxiv.org/abs/2611.21885) and [BaseRSI](https://arxiv.org/abs/2611.24578); their identities were checked, but their full comparative review is pending. No priority claim is endorsed here.

## Experimental Setup

Qwen3.8-27B on DAPO-Math; five generations; fixed 500-question gate and 500-question test; four samples per question. Eight GPUs support serving and weight tools. Appendix B caps edits at rank 64 and relative Frobenius norm 0.1.

## Benchmarks and Baselines

The main numerical comparator is the starting model. The held-out split remains within one mathematics source. Same-budget random-edit, fixed-editor, and gradient-based controls are **Not verified** in the reported experiment.

## Quantitative Results

Table 2: test avg@4 **76.30 → 77.75%**; pass@4 **82.60 → 84.80%**. Gate avg@4 **73.95 → 76.45%**. Five generations yield **four accepted improvements**; generation five is unchanged. These are distinct metrics and datasets.

## Limitations

**Review analysis:** repeated selection against a fixed gate can adapt to its statistics even when problem content stays hidden. A positive paired mean is not a multiple-testing correction. Small admitted gains require uncertainty that accounts for candidate selection and repeated reuse.

The independent test is useful evidence of within-source transfer. It does not establish cross-domain benefit, absence of capability regression, or sustained acceleration. Four samples per problem do not replace independent full-search seeds, and eight candidate sessions are also not eight complete replications.

A direct parameter edit can be expensive despite using no backpropagation. Measure all proposal calls, diagnostic forwards, unsuccessful candidates, gate evaluations, and checkpoint handling before comparing it with LoRA training. The best follow-up would reuse the exact same edit primitives and budget across learned, frozen, and random proposers.

## Reproducibility

Inspected Sections 3–6, Algorithm 1, Table 2, and Appendices A–B. No execution was attempted. Public runnable artifacts, raw candidate outcomes, complete GPU-hours, and uncertainty across full runs are **Not verified**.

## Open Research Questions

From a common checkpoint and history, does the later editor propose better edits than the original editor? Cross editor identity with target weights and archive access to separate those effects. Audit an unrelated capability suite after every retained edit. These tests would distinguish better answers from a better improvement process.
