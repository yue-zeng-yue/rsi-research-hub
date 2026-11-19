# Evaluation-Free Recursive Self-Improvement for Coding Agents

Evidence cutoff: 2026-11-19. Results below are author-reported, not independently reproduced.

## 1. Full Paper Title

Evaluation-Free Recursive Self-Improvement for Coding Agents.

## 2. Authors and Affiliations

Zhe Ren and Guowei Rong: School of Artificial Intelligence, Jilin University. Yimeng Chen, Nanbo Li, Piotr Piękos, Mateusz Ostaszewski, and Jürgen Schmidhuber: KAUST. Dandan Guo: Jilin University and KAUST. Names follow the [arXiv record](https://arxiv.org/abs/2611.21056); affiliations follow the [v1 title block](https://arxiv.org/html/2611.21056v1).

## 3. Publication Date

First submission: 2026-11-16; reviewed version: v1.

## 4. Venue or Preprint Status

arXiv preprint, 32 pages. Peer-reviewed acceptance: Not verified.

## 5. Paper URL / DOI

[Full paper](https://arxiv.org/html/2611.21056v1); [arXiv record](https://arxiv.org/abs/2611.21056). The record lists DOI 10.48550/arXiv.2611.21056 as pending registration at verification.

## 6. Official GitHub Repository

Not verified. The paper references mini-swe-agent as a dependency; that repository should not be labeled an official ELITE release.

## 7. Research Problem

Repeatedly running every modified coding agent on downstream tasks makes evolutionary search expensive and encourages adaptation to its evaluation distribution. Can executable agent scaffolds improve without downstream candidate-task scores guiding their evolution?

## 8. Methodology and Algorithm

ELITE, Explore-then-Integrate, fixes model weights θ and changes executable scaffold Σ in `Aₜ = (θ, Σₜ)`. Each generation proposes seven focused improvement hypotheses; every child is independently implemented from the same parent. Deterministic exploration gates check structural and operational validity.

An LLM integrator inspects code, edit intentions, and gate results, identifies complementary or conflicting mechanisms, and reimplements a compatible subset as one coherent descendant. It neither concatenates patches mechanically nor selects a single child by task reward. Stronger acceptance checks cover protocol and main-flow operation; failure retains the parent. Downstream candidate results and task-solving trajectories are excluded from this update loop. Final benchmark tests and structural smoke tests still occur: evaluation-free is narrowly about downstream candidate-task evaluation. [Sections 3–4](https://arxiv.org/html/2611.21056v1).

## 9. Key Contributions

The paper replaces evaluate-and-select with mechanism integration, demonstrates a bounded improvement trajectory, and audits validity gates and transfer. It establishes feasibility in this setting, not a theorem that code inspection predicts performance or guarantees monotonic improvement.

## 10. Experimental Setup

DeepSeek-V4-Flash and Qwen-3.7-Plus each perform modification and task solving. ELITE runs ten generations, seven children per generation, with an eight-worker pool and 1,800-second exploration/integration timeouts. DeepSeek comparisons use three independent evolution runs per method; Qwen uses three ELITE runs but one each for DGM/HGM. Baseline worker allocations and evaluation budgets differ, so comparisons are not compute-matched. [Section 5; appendices A.4–A.5](https://arxiv.org/html/2611.21056v1).

## 11. Benchmarks and Baselines

The main experiment uses a fixed 60-task SWE-bench Pro subset. Transfer uses 50 SWE-bench Verified tasks, split equally between Django and Sphinx, and 50 Polyglot tasks. Baselines are the initial agent, Darwin Gödel Machine (DGM), and Huxley-Gödel Machine (HGM). These numbers must not be presented as full-benchmark leaderboard scores.

## 12. Quantitative Results

For DeepSeek, Pro success increases 60.0→85.6%; DGM reaches 86.7%, HGM 88.3%. ELITE transfers at 73.3% Verified and 69.3% Polyglot, versus DGM 63.3/62.7 and HGM 65.3/64.7. Reported evolution times are 4.90 hours for ELITE, 43.15 for DGM, and 15.66 for HGM: approximately 8.8× and 3.2× wall-time reductions under these configurations. ELITE uses zero downstream candidate-task evaluations, while generation, integration, and validity checks still consume resources. [Tables 1–2](https://arxiv.org/html/2611.21056v1).

## 13. Limitations

Small selected task subsets, limited seeds, asymmetric Qwen replication, differing concurrency, and one continuing lineage constrain causal and scalability claims. Accepted agents can fluctuate in downstream ability. Removing task feedback also removes direct evidence that an accepted modification helps.

## 14. Reproducibility

Read method, experimental, limitation, and appendix protocol sections. Prompts, task subsets, and gate descriptions help reconstruct the procedure; an official code release remains Not verified. Reproduction requires archived descendants, edits, model snapshots, timing boundaries, and strict exclusion of final task outcomes from search. No experiments were run here.

## 15. Open Research Questions

Can the result survive complete benchmark sets and equalized token/worker budgets? Which validity checks predict later failures? Does integration remain effective after many generations or require occasional independent task feedback to control drift?
