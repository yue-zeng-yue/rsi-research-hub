# Auditing Product and Recursion Claims

## Full Paper Title

Auditing the Product, Not the Recursion: The Evaluation Evidence Behind Recursive Self-Improvement Claims.

## Authors and Affiliations

Zihan Chen and Di Zhu: Stevens Institute of Technology, Hoboken, New Jersey, USA. Lei Nico Zheng: University of Massachusetts Boston, Boston, Massachusetts, USA. Verified from the paper's author block.

## Publication Date

First publication and reviewed version: 20 October 2026, arXiv v1. The literature search frame was frozen on 17 October 2026; this review's cutoff is 19 November 2026.

## Venue or Preprint Status

arXiv preprint, 39 pages. Peer-reviewed venue: **Not verified**; no accepted venue is identified in the consulted primary metadata.

## Paper URL / DOI

[Version-pinned paper](https://arxiv.org/html/2610.27610v1). arXiv displays DOI 10.48550/arXiv.2610.27610 as **pending registration**; successful resolution is not verified.

## Official GitHub Repository

**Not verified.** Appendix D promises future release of full item-level codes, locators, and notes. That promise is not evidence of an available repository. Tables and the codebook are included in the paper.

## Research Problem

How often do RSI studies provide evidence for accumulating gains, repeatable improvement loops, or a better improver, rather than only reporting a better final system?

## Methodology and Algorithm

A claim-indexed codebook separates product, accumulation, repeatability, and improver claims. Three propositions explain the identification problem: selection can increase noisy development scores without true gains; shared evaluator bias can survive held-out tasks; and jointly changing solver S and improver I exposes only the diagonal I=φ(S). Such observations cannot isolate the improver's effect. The relevant intervention applies earlier and later improvers to **identical starting artifacts**, at matched budgets, then independently audits their successors. Equal starting scores are insufficient. Frozen-loop comparisons answer a useful total-effect question but generally estimate a different quantity. See [§§3–4](https://arxiv.org/html/2610.27610v1#S3).

## Key Contributions

The paper turns broad methodological concerns into measurable reporting indicators, connects them to formal counterexamples, and proposes a reporting standard tied to the actual claim. Its evidence concerns reported study designs, not independent reruns proving that individual systems fail.

## Experimental Setup

Twelve arXiv title/abstract phrase searches yield 173 records and 114 eligible studies; 90 explicitly describe their systems as RSI. Thirty items per study produce 3,420 initial codes. Coding combines an LLM-assisted pass, a random human-coded reliability sample, adjudication, and separate blind coding of improver comparisons. One sampled exclusion leaves 29 adjudicated eligible papers (§5).

## Benchmarks and Baselines

This is meta-research, not an agent benchmark. Twenty established anchor works provide a complementary comparison set, with only two overlapping the search frame. The strict criterion requires selection-independent evaluation; the broad product criterion also admits partial or unstated separation.

## Quantitative Results

All counts are **author-reported**, not independently recoded here.

| Population and indicator | Result | Source |
|---|---|---|
| 90 RSI studies: strict / broad product evaluation | 54/90 (60%) / 81/90 (90%) | Table 4 |
| 90 RSI studies: audited loop reruns / matched-budget comparator | 20/90 (22%) / 33/90 (37%) | Table 4 |
| 26 improver claimants: related / strict same-start comparison | 23/26 / 4/26 | §6.2 |
| Human-coded subset, 22 RSI studies: strict evaluation / audited reruns | 45% / 14% | §6.3 |

There are six same-start comparisons among all 90 RSI studies; four occur among the 26 improver claimants. These denominators must remain distinct.

## Limitations

Phrase-based arXiv retrieval is not a census of all self-improvement research. Most studies retain first-pass coding with revised rules, rather than complete independent human adjudication. Initial coding agreement and later rule changes create classification uncertainty; Wilson intervals do not capture those errors or missed papers. Absence of a reported control does not demonstrate an absent real capability.

## Reproducibility

Appendices provide search details, decision rules, proofs, and per-study summary codes. The complete promised evidence package is **Not verified** as released. No study was re-executed or independently recoded for this review.

## Open Research Questions

Do the design gaps persist under a broader search and fully independent coding? How sensitive are counts to operational definitions? Can repeated same-start tests establish improvement yield per unit compute over multiple solver states and longer horizons?
