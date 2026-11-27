# Language Models Can Rewrite Their Own Weights

**Reviewed:** 2026-11-27. **Evidence:** Primary-reviewed; results are author-reported. No independent result verified.

## Full Paper Title

Language Models Can Rewrite Their Own Weights

## Authors and Affiliations

Jiajun Fan (UIUC), Neil He (UIUC and Yale), Changyi Yang (CMU), Andy Mao (UIUC), Xi Zhu (Rutgers), Chaoran Cheng (UIUC), Kaiqu Liang (Princeton), Shuaike Shen (CMU), Zetian Li (Stanford), Ruihan Guo (UIUC), and Ge Liu (UIUC), according to the v2 PDF title page.

## Publication Date

First arXiv submission: 2026-11-16, 20:55:08 UTC. Reviewed v2 submitted 2026-11-18, 08:57:59 UTC. The version dates follow the arXiv record rather than the print date in the PDF.

## Venue or Preprint Status

arXiv preprint. Peer-reviewed acceptance: **Not verified**; no proceedings record was identified.

## Paper URL / DOI

[Canonical record](https://arxiv.org/abs/2611.21885) · [Reviewed v2](https://arxiv.org/html/2611.21885v2) · [PDF](https://arxiv.org/pdf/2611.21885v2) · [arXiv DOI](https://doi.org/10.48550/arXiv.2611.21885).

## Official GitHub Repository

**Not verified:** the [first author's project page](https://www.jiajunfan.com/projects/self-rewriting/) provides demonstrations and the paper, but no author-linked runnable implementation was located there or in the versioned paper. The third-party [rank-one LoRA notebook](https://github.com/cpuchip/self-rewrite-lora) is a related attempt, not verified reproduction of the headline protocol.

## Research Problem

Can a model diagnose a behavioral failure, write a persistent edit to a copy of its own checkpoint without gradient updates, and select an edit that helps on unseen items? A second task tests repair of intentionally corrupted weights.

## Methodology and Algorithm

Sections 2 and 3 and Appendix C distinguish the fixed editor from the candidate checkpoint. With graded practice responses, the editor alternates CPU tensor-edit code, forward generation, and hidden-state reads. The environment forbids gradients and optimizer calls and supplies a directional projection primitive. Candidate and base share questions and sampling seeds. In protocol two, the framework evaluates a candidate once on reserved practice questions and returns an aggregate check before the editor decides whether to submit. Every session starts from base weights; no accepted patch becomes the next editor (Appendix E.9).

## Key Contributions

**Review assessment:** the contribution is an empirical diagnosis, editing, and selection workflow using the same base model as editor and target, not a new projection operation. Protocol two supplies evidence of repeated independent proposals and selection. In contrast, [SelfWrite](selfwrite.md) explicitly promotes an edited checkpoint to the next editor; neither paper's final accuracy alone measures editor improvement.

## Experimental Setup

Section 3.1 and Appendices D.1, D.3, and E.9: Qwen3.5 models at 2B, 4B, 9B, and 27B are studied; the headline protocol uses Qwen3.5-27B. Eight reported sessions of that protocol vary editor-turn seeds. Each has up to 20 batched forward requests, 200 Python executions, and a three-hour window excluding the confirmation check. That check uses 256 of 300 reserved practice problems, two samples at up to 4,096 new tokens. This is separate from the final paired 490-problem test with eight samples each at up to 16,384 new tokens.

## Benchmarks and Baselines

The 490 questions are held out from the same DeepScaleR-derived source as development. Compare against the original checkpoint under matching seeds and decoding settings. The metric averages individual answer correctness, not pass@8. Before the final test, submitted edits undergo an initial 200-item held-out comparison using two seed sets. Same-budget scripted parameter search and decoding-only stopping controls for the headline result: **Not verified** in the reported comparison.

## Quantitative Results

Table 13 and Appendix E.9: session 8 raises the time-step bias in all 48 linear-attention layers by 0.5. The final paired metric moves from 57.2% to 63.8% (+6.6 percentage points; question-level 95% interval +5.0 to +8.1; one-sided permutation test against base, p < 0.00001). The token-limit rate drops from 33.6% to 26.1%; 439 answers flip to correct and 182 to incorrect. Session 2 reaches 61.3%; session 1 is not significant against base; five sessions withdraw. The first-protocol early-layer projection is a separate result (Table 8).

## Limitations

Appendix A treats succession of the edited model as future work. **Review analysis:** the result does not isolate model diagnosis from a simple search over a shared bias or improved answer termination. The test is same-source mathematics, the sessions are not recursive generations, and the selected peak is not the expected gain of a fresh session. The image transfer demonstration is for repair of a synthetic fault, not generalization of the successful mathematics edit. Aggregate compute including rejected proposals, confirmation, and final evaluation is not a matched-cost comparison.

## Reproducibility

Inspected Sections 2–4, Figure 1, Tables 1, 8, and 13, and Appendices A, C, D, and E.9. The paper describes intervention and evaluation mechanics; exact runnable author code and independently reproduced headline outcomes remain **Not verified**. No run was performed for this review.

## Open Research Questions

Match a hand-written time-step bias sweep and a stopping-aware decoding baseline to the search and output budgets. Then cross editor identity (base or edited) with fixed target checkpoint and feedback, and evaluate proposal quality on new task families under a fresh audit.
