# The Resolution Hypothesis: Agent Evolution's Key Is Identifying Improvements

Reviewed on 2026-11-19 against arXiv v1. Results below are author-reported; no independent experiment or scientific reproduction was performed.

## Full Paper Title

The Resolution Hypothesis: Agent Evolution's Key Is Identifying Improvements

## Authors and Affiliations

Author order: Yuanhao Zeng; Shaocheng Lan; Ao Lu; Kuang Yan; Heng Lin; Xinang Xu; Yuan Luo; Yueting Wang; Yexin Li; Ruo Shan; Kan Ren.

The PDF title page maps Yuanhao Zeng to ShanghaiTech University, ByteDance (China), and BIGAI; Shaocheng Lan and Ao Lu to ShanghaiTech University and ByteDance; Kuang Yan, Heng Lin, Xinang Xu, and Ruo Shan to ByteDance; Yuan Luo to SUSTech; Yueting Wang and Kan Ren to ShanghaiTech University; and Yexin Li to BIGAI. The first three authors share equal contribution; Kan Ren is corresponding author. This mapping was checked in the PDF because the HTML flattens affiliation markers.

## Publication Date

First submission and reviewed revision: **2026-11-17 16:57:03 UTC, v1**. The canonical record listed only v1 when inspected on 2026-11-19. This is a newly cataloged paper, not a new November 19 submission or a revision of an existing catalog entry.

## Venue or Preprint Status

arXiv preprint. Conference or journal acceptance: **Not verified**; the canonical record and bounded exact-title OpenReview search did not establish a venue. Unrelated wearable time-series papers using the phrase “resolution hypothesis” are not publication evidence for this work.

## Paper URL / DOI

[Canonical record](https://arxiv.org/abs/2611.23068); [reviewed HTML v1](https://arxiv.org/html/2611.23068v1); [PDF v1](https://arxiv.org/pdf/2611.23068v1). The record lists `10.48550/arXiv.2611.23068` as an arXiv-issued DOI with **registration pending** at inspection, not a conference DOI.

## Official GitHub Repository

**Not verified:** no paper-specific implementation repository was identified in the inspected author-linked [project page](https://lineshogan.github.io/resolution-hypothesis/) or bounded exact-title code search. The paper's introduction promises reproducible materials and trajectory data upon acceptance. An accessible interactive project page is not an implementation release. Third-party implementations or “code released” badges are not counted as author code. No repository commit can therefore be pinned.

## Research Problem

The paper asks whether frozen-model agent evolution is limited by producing useful artifacts or by distinguishing useful artifacts from noisy scores. It separates the quality of a final agent artifact from the reliability of the procedure that chooses and accumulates artifacts. Its objects are prompts, skills, memories, and executable harnesses, not trained model weights (§§1–3).

## Methodology and Algorithm

This is principally a diagnostic study, not a new state-of-the-art evolution algorithm. For artifact A, it models one observed score as its expected quality plus evaluation noise. Total score variance separates into variation between artifacts produced by independent evolution runs and variation between repeated evaluations of one fixed artifact (§3.1; Appendix B). More evaluation repetitions of one artifact do not estimate the former.

The study combines independent evolution runs, repeated held-out testing, audits of evaluation shortcuts, and two fixed candidate pools. The Proposal Pool tests whether generated skills transfer to disjoint tasks. The Selection Pool supplies selectors with limited rollout evidence and estimates candidate quality using other rollouts that those selectors cannot observe. A hierarchical empirical-Bayes estimate and an equal-quality null address the upward bias from selecting a maximum over noisy candidates (§5; Appendices F.1–F.3).

Existing algorithms retain their method-specific acceptance and stopping rules. For example, GEPA uses a three-task training gate and validation Pareto selection; AHE selects among five versions using validation scores. Trace2Skill and ReasoningBank have no score-based rejection in the three non-terminal domains, so they are not ordinary greedy acceptance gates (Appendix C.2).

## Key Contributions

The authors argue that evaluation resolution is a shared bottleneck, and offer separate tests of proposer quality, selector accuracy, and between-run variability. The distinctive evidence is their joint measurement rather than the invention of variance decomposition or best-arm identification. For context, this catalog already reviews [HDA](harness-delta-attribution.md), [Rethinking Evaluation](rethinking-evaluation.md), and [TRUST](trust.md): attribution, matched-budget comparison, and statistical admission are existing lines of work.

The results support scoped negative findings about tested selection procedures. They do not prove that all RSI is ineffective, that every large gain is invalid, or that an evolved final agent measures improvement of its own improver.

## Experimental Setup

The grid uses GPT-5.4 nano, GPT-5.6 Luna and Terra, DeepSeek-V4-Flash-0731, Kimi-K3, and GLM-5.2, with coverage varying by experiment rather than a full Cartesian product. Within a method configuration the solver, reflector, and artifact editor use the same model. Non-terminal tasks use medium reasoning effort and a 16,384-token completion cap; Terminal-Bench uses provider-default effort (Appendix C.1).

Method-level variance uses eight independent evolution runs, or sixteen for text-artifact methods with GPT-5.4 nano, followed by sixteen evaluations per artifact, reduced to eight on Terminal-Bench and for harness methods (§4.1). Candidate-pool experiments use DeepSeek-V4-Flash (Table 5). The Proposal Pool has 100 skills from ten training tasks, tested sixteen times on each of ten disjoint tasks. Its trajectories run with a two-hour cap; shorter timeouts are retrospective cutoffs of the same trajectories, not fresh shorter-budget runs (Appendix F.1).

The Selection Pool has 100 skills sourced from six Terminal-Bench and three DeepSWE tasks; evaluation includes six source tasks and five tasks withheld from generation. Each pair receives eight rollouts, extended to fifteen for the ten highest-scoring artifacts per task. This is not an entirely unseen-task pool. DeepSeek-V4-Flash judges read trajectories without outcome labels; the ACE-style condition adapts a reflector prompt rather than reproducing a full ACE training loop (Appendices C.4, F.1, F.3).

## Benchmarks and Baselines

Table 3 specifies train/validation/test splits: ALFWorld 100/70/67; SpreadsheetBench Verified-400 80/39/281; OfficeQA 49/49/148; Terminal-Bench v2.1 18/18/53. These method-level splits differ from the candidate-pool splits. The terminal baseline and text methods use Mini-SWE-agent 2.4.6, whereas harness methods start from 1.14.4 (Appendix C.3), limiting a pure method-only cross-family comparison.

Methods are SkillOpt-Lite, GEPA, Trace2Skill, ReasoningBank, HarnessLens, Meta-Harness, and AHE, plus unevolved agents. Budgets are held per method across models but are not universally equal between methods: GEPA has metric-call caps, Meta-Harness/AHE use five rounds, and HarnessLens has a training-pass cap (Appendix C.2). This is not a comprehensive equal-dollar ranking. Selection comparators include random choice, execution scores, native SkillOpt-Lite/GEPA operators, and three trajectory-judge variants.

## Quantitative Results

| Finding | Conditions and comparator | Evidence boundary and locator |
| --- | --- | --- |
| More than 60% of configuration-pair differences fall below one single-run comparison standard deviation | Same-model, same-benchmark pairs across the variance grid; 150 configurations and 1,030 independent evolution runs | Descriptive comparison, not proof of equality. §4.1; Figure 2; Appendix D |
| Execution-based pairwise selection accuracy: **49.7% ± 1.9%**, versus random **50%** | DeepSeek-V4-Flash; 100-skill Selection Pool; eleven Terminal-Bench v2.1 tasks; one visible rollout per artifact, remaining rollouts used for quality reference | Posterior mean ± half-width of 95% credible interval, not seed SD. Table 1; Appendices C.4/F.3 |
| Native SkillOpt-Lite and GEPA selection: **48.6% ± 2.6%** each | Same fixed pool and reference; two visible rollouts per artifact | Native selection operators, not complete end-to-end methods. Table 1 |
| Candidate quality exceeds the matched equal-quality null by **3.33 percentage points** at K=100 under original timeouts and **3.41 points** under the two-hour cutoff | DeepSeek-V4-Flash Proposal Pool; ten disjoint test tasks; sixteen rollouts per skill/task; empirical-Bayes estimate with concentration cap 100 | Posterior diagnostic, not achieved deployed-selector gain or equal-cost superiority. Figure 9; Appendix F.1 |

Appendix F.3 also reports better final outcomes when validation averages sixteen rollouts instead of one. This is important counterevidence to a blanket “selection cannot work” reading, but incurs sixteenfold validation-rollout demand. Its local paragraph does not fully restate the model/subset assignment, so this review does not promote its numerical score comparison without that remaining configuration clarification.

## Limitations

The authors restrict claims to frozen weights; candidate-level evidence comes only from Terminal-Bench, and broader program evolution is explicitly outside the demonstrated scope (Limitations). The Selection Pool partly overlaps source tasks, quality is a posterior estimate rather than an exact oracle, and sampling is deeper for top-scoring candidates. Interpret results under that design.

Review analysis: cross-family harness-version differences and unequal method budgets prevent attributing all ranking differences solely to the evolution rule. The one-rule audit establishes that a rule can reproduce a gain, not that it was its unique cause; the paper explicitly acknowledges post-hoc rule construction and genuine residual gains (Appendix E.5). Process diagnostics are promising measurements, not proven general-purpose substitutes for terminal utility. Aggregate consumption exceeds ten million LLM calls and 400,000 CPU core-hours (§3.2); these totals are not the cost of one method or evidence of a cheap replication.

## Reproducibility

Inspected: canonical version history, HTML methods/results/limitations and Appendices B–H, PDF title page and relevant experimental passages, and author project-page links. No code installation, benchmark execution, or numerical reproduction was attempted. The project page was inaccessible through the search renderer but readable through direct HTTP retrieval; this transport distinction is recorded in the incremental audit.

Public implementation, raw trajectories, and a complete pinned reproduction package remain **Not verified**, because release is promised rather than established. Retain author-reported status even where the paper itself reproduces or audits earlier work: those are experiments by these authors, not independent reproductions performed by this repository.

## Open Research Questions

1. Can sequential or paired selection beat repeated validation at equal **total** proposal, rollout, and judging cost? Compare against TRUST and the paper's stronger-validation control; reject an efficiency claim if the gain disappears after budget matching.
2. Do selector results transfer to disjoint non-terminal domains and executable harness edits? Pre-register source-disjoint pools and preserve a final untouched audit; failure outside text skills would limit the proposed generalization.
3. Can process checks identify downstream-useful edits rather than merely changes in behavior? Require prospective prediction of held-out utility and audit process-metric exploitation. Correlation or reduced metric variance alone is insufficient.

These are research hypotheses, not validated recommendations or claims of originality.
