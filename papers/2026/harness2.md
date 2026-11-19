# Harness²: Recursive Agent Harnessing for an Open World

## Full Paper Title

Harness²: Recursive Agent Harnessing for an Open World

## Authors and Affiliations

Ruiyao Xu (Northwestern University; work during a Google Cloud AI Research internship); Yanfei Chen, Zhongying CuiZhu, Bhavana Dalvi Mishra, Yifei Ming, Han Yu, Rujun Han, Chen-Yu Lee, Tomas Pfister (Google Cloud AI Research).

## Publication Date

arXiv v1 submitted 2026-10-09. The PDF cover displays 2026-10-12; the submission-history date defines first public release. Reviewed v1 before the 2026-11-19 cutoff.

## Venue or Preprint Status

arXiv preprint; a peer-reviewed conference or journal venue was not verified.

## Paper URL / DOI

[Paper, v1](https://arxiv.org/html/2610.14224v1); [arXiv DOI](https://doi.org/10.48550/arXiv.2610.14224).

## Official GitHub Repository

[google-research/harness2](https://github.com/google-research/harness2), directly linked in the paper and mirrored by the [official project](https://harness2.github.io).

## Research Problem

How can harness adaptation proceed on newly arriving professional tasks without ground-truth feedback, while experience from one adaptation improves later adaptations?

## Methodology and Algorithm

Task-level Propose–Probe–Compose compares two candidate scopes: invariant engineering improvements and domain-specific edits. Each runs under matched model/environment settings; a composer may merge, revise, select, or reject changes using behavioral evidence. Parallel recursion expands candidates and compositions with width k; sequential recursion chains k updates. After completing a task, a separate improvement library stores adopted harnesses and evidence-linked EXPERIENCE.md lessons. Every new task starts from common H0 rather than inheriting the previous execution harness wholesale. Thus H′ = Φ(q,H,E;R), followed by R_next = Update(R,H*,D). Model weights, stage instructions, and decision rule stay fixed. See §2.

## Key Contributions

The contribution is coupled task adaptation and cross-task improvement memory with executable probes. This is narrower than a system rewriting every part of its optimizer. Contrasts supply behavioral evidence, not a correctness oracle or formal causal proof.

## Experimental Setup

WorkBuddy-Bench, JobBench, and Harvey LAB are evaluated with GLM-5 and Gemini 3.5 Flash under both OpenCode and Codex. Claude Opus 4.8 is the default editor. Results average three shuffled task streams; each benchmark’s library starts empty. Main comparisons use k=1 and additional parallel recursion k=5. Same-model editor/executor ablations address dependence on a stronger editor.

## Benchmarks and Baselines

Base harness, ReasoningBank, offline Meta-Harness, and per-instance Harness Scaling. LAB Partial is criterion pass rate, not whole-task success. Figure 6 includes all execution and improvement tokens; the main tables’ #Steps measure executor-session turns and must not be read as total adaptation expenditure.

## Quantitative Results

All results below are author-reported; no independent reproduction.

| WorkBuddy macro-score / configuration | Base | k=1 | k=5 | Source |
|---|---:|---:|---:|---|
| Gemini 3.5 Flash + OpenCode | 72.4 ± 0.9 | 77.5 ± 2.5 | 80.8 | Table 1 |
| GLM-5 + OpenCode | 64.2 ± 1.4 | 75.7 ± 2.2 | 79.6 | Table 1 |
| GLM-5 + Codex | 64.4 ± 1.2 | 75.3 ± 1.3 | 78.3 | Table 1 |

k=5 values are base k=1 means plus the table’s reported recursion deltas; SDs are not supplied for those derived entries. In the Gemini/OpenCode row, Meta-Harness scores 76.4 ± 0.7.

## Limitations

Unlabeled task adaptation still uses a learned preference signal, with shared model biases and stochastic trajectories. Stream-order effects and mutable library contents complicate evaluation independence. A better final answer may partly reflect additional attempts rather than reusable harness improvement; Figure 6 improves the cost accounting but does not establish a universal advantage. Library usefulness on shifted domains is finite evidence, not perpetual recursive acceleration.

## Reproducibility

The official Apache-2.0 release supports parallel/sequential runs, OpenCode/Codex, setup/judge commands, and library artifacts. README requirements include Linux, Python 3.12, Node.js, render dependencies, model credentials, and Docker for WorkBuddy. Availability and documentation were verified, but installation, credentials, benchmark access, and scores were not tested.

## Open Research Questions

Can a frozen library improve a fully novel stream under the same total token budget as independent resampling? Which retained lessons generalize causally, and how should stale or contradictory lessons be retired? How robust is composition to systematically wrong proxy judgments?
