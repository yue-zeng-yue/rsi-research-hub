# Gödel Machines

Evidence cutoff: **2026-11-19**. This is a theoretical foundation, not an empirical demonstration of modern LLM recursive self-improvement. No experiment was reproduced for this note.

## 1. Full Paper Title

*Gödel Machines: Self-Referential Universal Problem Solvers Making Provably Optimal Self-Improvements*. The arXiv title spells the name “Goedel”; related published variants have different titles.

## 2. Authors and Affiliations

Jürgen Schmidhuber; IDSIA, Manno-Lugano, Switzerland, and TU München, Germany, as printed in the v5 manuscript. These are paper-time affiliations, not a claim about current employment.

## 3. Publication Date

First arXiv submission: **2003-09-25**. Version inspected: **v5, 2006-12-17**. The early proposal and later revised treatment should not be assigned the same date.

## 4. Venue or Preprint Status

Technical report IDSIA-19-03. The author-submitted record lists variants in *Adaptive Agents and Multi-Agent Systems II* (2005), ICANN 2005, and *Artificial General Intelligence* (2006). It is not merely an unpublished 2026 preprint. [Bibliographic record](https://arxiv.org/abs/cs/0309048)

## 5. Paper URL / DOI

[Versioned full text](https://arxiv.org/pdf/cs/0309048v5); [arXiv DOI](https://doi.org/10.48550/arXiv.cs/0309048).

## 6. Official GitHub Repository

**Not verified.** The inspected paper does not establish an official GitHub implementation. A project using “Gödel” in its name should not automatically be presented as the author's implementation or as a realization of the theorem.

## 7. Research Problem

When can a system justify rewriting its own problem solver and improvement procedure, accounting for the opportunity cost of continued search?

## 8. Methodology and Algorithm

An initial program contains an environment policy and proof searcher. Axioms encode hardware, software, environment assumptions, and utility. Search proposes a rewrite plus proof that switching now exceeds continuing the current search. A representative utility is expected remaining reward, `u(s,e) = E[sum_{τ=t}^T r(τ) | s,e]`. Proof-producing programs receive computational budgets; an accepted rewrite can replace the searcher itself.

## 9. Key Contributions

Theorem 4.1 formalizes the switch-versus-continue guarantee under a consistent formal system. It does not assert that arbitrary heuristic rewrites are optimal. This is a useful conceptual boundary between proof-authorized self-modification and benchmark-selected agent edits. [Sections 2–5](https://arxiv.org/pdf/cs/0309048v5)

## 10. Experimental Setup

Not applicable: the contribution is a formal machine and proofs. GPU counts, training datasets, and empirical runtime measurements are **not reported as an experimental evaluation**.

## 11. Benchmarks and Baselines

Conceptual comparisons include universal search, HSEARCH, and AIXI-related approaches. No benchmark win rate or contemporary coding-agent baseline is supplied.

## 12. Quantitative Results

No empirical numerical performance result. Asymptotic search statements are mathematical claims, not measured speedups. [Sections 4–6](https://arxiv.org/pdf/cs/0309048v5)

## 13. Limitations

Useful changes can be unprovable or too expensive to prove. A guarantee remains relative to axioms and formalized utility. [Section 2.4](https://arxiv.org/pdf/cs/0309048v5) Research implication: correctness of the proof checker alone does not establish that a real deployment matches its modeled environment or that its objective captures user intent.

## 14. Reproducibility

A meaningful reproduction would first specify a bounded machine, machine-readable axioms, trusted checker, utility, and executable search procedure. It should publish accepted and rejected proofs, resource accounting, and a fixed baseline searcher. Merely prompting an LLM to “prove” an edit beneficial is insufficient. Artifact availability, implementation license, executable full-system reproduction, and realistic compute budget: **Not verified**. No claim of practical tractability is made here.

## 15. Open Research Questions

Research questions proposed for this hub: Can a proof-producing optimizer improve a narrowly specified compiler pass or verifier while charging proof cost? Which environment assumptions can be checked at runtime? Can empirical candidate generation be combined with proof-checked acceptance without silently weakening the guarantee? How should unsuccessful proof search be reported so that a few accepted examples do not conceal prohibitive search costs? These are proposed experiments, not results from the paper.
