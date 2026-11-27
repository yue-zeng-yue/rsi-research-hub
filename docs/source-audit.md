# Source Audit and Verification Boundaries

**Initial inspection:** 2026-11-19, Asia/Shanghai. **Latest incremental review:** 2026-11-27. Per-paper records retain their inspected versions and dates; older sources were not all re-audited. This curated collection does not claim exhaustive retrieval through either date. First-submission dates follow source records, separately from revisions and review dates.

## Discovery and admission

The search began with all 19 requested names: Darwin Gödel Machine, Hyperagents, Harness², Meta-Harness, RRSI, SoL-Pi, AHE, Ouroboros, SIA, Evo-Harness, Harness Updating Is Not Harness Benefit, Skill∞, HMED, JoMoHa, HarnessForge, WHALE, RSI-Env, The RSI Tax, and HarnessAdapt-RL. Each resolves to a primary paper and receives a full review. Acronyms were disambiguated rather than assigned to a similarly named result.

[follow-rsi](https://github.com/adongwanai/follow-rsi) was used to discover source identifiers and related work. Its prose, scores, and editorial judgments were not treated as primary evidence or copied into this repository. Exact-title searches and forward/backward references led to additional evaluation, model-training, and meta-improvement papers.

Expanded query families included `recursive self-improvement November 2026`, `agent harness evolution`, `meta-harness`, `harness benefit`, `model harness co-evolution`, `self-improvement cost`, `same-start improver evaluation`, and exact titles for newly discovered candidates. Sources were restricted at the evidence stage to original arXiv full texts, official proceedings, author project pages, and author-linked repositories.

## Source provenance

The authoritative per-paper ledger is [data/papers.json](../data/papers.json). It records canonical paper URLs, reviewed-version URLs, inspected sections, author/affiliation metadata, first publication dates, venue qualifications, official code relationships, and reproduction status. Where available, code commits identify the inspected snapshot. The [paper index](../papers/paper-index.md) and [bibliography](../references.bib) are derived views.

The review includes primary Methods, Experiments, and Limitations sections rather than abstract-only summaries. Every review records quantitative conditions and distinguishes author reporting from independent verification. Public source pages and full texts were read; benchmark installations, full code execution, and numerical replication were not performed.

## Material identity and version decisions

- **HarnessForge** is the joint harness/policy paper, with an [official EMNLP 2026 record](https://aclanthology.org/2026.emnlp-main.1893/); unrelated software-verification projects with the same name were excluded.
- **HarnessAdapt-RL** is the method in *Training the Whole Agent, Not Just the Model*, not a guessed paper title.
- **Ouroboros** uses the current title including *Frontier Coding Agent*. Its version-specific affiliation ambiguity is preserved in the review.
- **Hyperagents** distinguishes arXiv revision date from the PDF's printed date. **AHE**, **GEPA**, and **Updating versus Benefit** use revised author lists or experiments where applicable.
- **Meta-Harness** has a substantive main repository as well as a separate optimized artifact. The author's COLM 2026 report is explicitly distinguished from independently verified proceedings.
- **SICA** has a verified ICLR 2025 SSI-FM workshop version. A submission comment is not evidence of main-conference acceptance.
- **AHE-Beta** was submitted on November 18 and discovered at the November 19 cutoff; its requirement-driven review loop is distinct from the earlier AHE paper.

## Benchmark-version decisions

SkillsBench's current 1.1 registry and paper v4 differ from its first paper snapshot. Terminal-Bench's current 4.1 guide differs from the historical 2.0 and 2.1 configurations in the reviewed papers; an 89-task historical count must not be relabeled as the current inventory. SWE-bench Full, Lite, and Verified use different instance sets. ALFWorld text and embodied protocols are distinct. WebShop small-catalog runs are not full-catalog results. ToolSandbox similarity is not automatically binary success.

The [benchmark catalog](../experiments/benchmarks.md) records source links, setup requirements, licenses where inspected, and missing compute estimates. Live web pages and repository default branches can change after inspection; immutable experiment pins remain necessary.

## Unresolved evidence and availability

Some individual affiliations remain unspecified or ambiguous in the primary source. Official implementations were not located for several papers, including HMED, RSI-Env, and The RSI Tax. Skill∞'s linked repository is an announcement placeholder. AHE's debugger release is partial. HDA's repository omits full raw trajectories. These limits are recorded at paper level rather than hidden behind a generic code badge.

Some arXiv DOI records explicitly show pending registration. Such identifiers are labeled as arXiv identifiers, not conference publication DOIs; resolver failures are reported separately from primary paper availability. An accessible URL confirms availability, not the correctness of the paper's claims.

## Research interpretation audit

The synthesis preserves the following distinctions: search versus held-out performance; absolute regression versus negative interaction; task score versus improver quality; repeated execution versus repeated full search; invocation versus causal benefit; and inference savings versus whole-loop savings. HMED already uses matched discovery states, SIM already structures optimizer memory, and TRUST already provides assumption-dependent sequential statistical admission. The four proposals acknowledge these overlaps and do not claim original results.

## Repository validation

The historical initialization validation record is [data/repository-validation.json](../data/repository-validation.json); the latest incremental record is [data/incremental-review-2026-11-27.json](../data/incremental-review-2026-11-27.json). Records distinguish file and paper counts, English-script and path checks, local-link checks, review-field checks, and sensitive-content screening. The initialization URL audit is [data/link-audit.json](../data/link-audit.json); failures identify transport or source-access gaps and do not silently disappear from the record. Markdown validation is configured through the pinned npm lockfile and GitHub Actions.

Initialization checked 189 public source links: 186 were reachable and three OpenReview PDF endpoints returned HTTP 403 to the automated checker. Primary metadata and alternative full-text sources were used where available; the access limitation remains in the audit. All 76 initialization files were verified against the initial remote tree by blob hash. At the November 19 inspection, hosted documentation jobs could not start because of an account-level restriction; local Markdown validation passed. The historical validation record links that inspection's hosted attempt without presenting it as a passing check.

The homepage refresh preserved the subsequent literature addition, checked 180 local Markdown, HTML, image, and heading links, and passed Markdown validation across 63 files. Both self-contained SVG illustrations were parsed and visually inspected; the published homepage's images, research-map navigation, and expandable section were checked in GitHub's renderer. These presentation checks do not expand the scientific review scope.

These are documentation and provenance checks. They must never be cited as experimental confirmation of any algorithm in this repository.

## Incremental review: 2026-11-27

The [dated update](updates/2026-11-27.md) admits RoboEvo² v1 and the previously queued Language Models Can Rewrite Their Own Weights v2, for 42 reviews. The new ledger records selected primary and artifact sources, coverage limits, and unreviewed leads. No previously admitted revision was changed.

## Incremental review: 2026-11-25

The [dated update](updates/2026-11-25.md) admits four reviews against baseline `75a0be6`, bringing the collection to 40. CoEvoBench v1, AutoMaster v2, SelfWrite v1, and TT-RSI v1 were inspected beyond their abstracts. The report and [update ledger](../data/incremental-review-2026-11-25.json) preserve discovery-only candidates and exact artifact pins. No prior metadata was silently upgraded to a newer paper revision.

Material qualifications include AutoMaster's benchmark-feedback selection and partial release; CoEvoBench's audit sanction, weighted metric, and incomplete implementation acceptance; SelfWrite's four accepted changes across five generations; and TT-RSI's transductive setup and output-token budget. Missing affiliations, code, and independent runs remain explicitly qualified. Initialization audit files remain historical snapshots.

## Incremental review: 2026-11-19, Resolution Hypothesis

Baseline: commit `9fa2597` (November 19, 15:33 Asia/Shanghai). The baseline manifest contains 35 reviewed papers, including SIM; this update adds exactly one distinct paper, bringing the catalog to 36. All prior metadata, bibliography entries, review paths, and the 15-field template were consulted before admission.

The bounded discovery pass considered recent harness, model, meta-improvement, and co-evolution queries; existing AHE-Beta and SIM were excluded as duplicates. BaseRSI (`2611.24578`) appeared as a model/harness-internalization lead but was not fully reviewed or added. The selected addition, [The Resolution Hypothesis](../papers/2026/resolution-hypothesis.md), contributes directly to evaluation reliability, generalization boundaries, improver-versus-product measurement, cost, and negative results. This pass is not an exhaustive update of every taxonomy branch.

Primary evidence: the [arXiv record](https://arxiv.org/abs/2611.23068), [v1 full text](https://arxiv.org/html/2611.23068v1), PDF title-page affiliation mapping, and [author project](https://lineshogan.github.io/resolution-hypothesis/). The record lists only v1, submitted November 17 at 16:57:03 UTC. Exact-title OpenReview results did not establish acceptance; unrelated papers using the same phrase were excluded. No paper-specific official implementation was verified. The project page failed in the search renderer but was readable by direct HTTP retrieval; the paper promises artifacts after acceptance. Third-party code-release badges were not accepted as evidence.

The review preserves candidate-pool versus full-method differences, source-overlapping versus disjoint tasks, posterior uncertainty versus seed variability, differing Mini-SWE-agent starting versions, and non-uniform method budgets. Higher-repetition validation is acknowledged as positive counterevidence, without promoting its numerical result where the local configuration description is incomplete. Existing trend conclusions remain unchanged: this adds evidence, not a demonstrated new algorithm or independent reproduction.

The initialization records in `data/repository-validation.json` and `data/link-audit.json` remain historical snapshots and were not relabeled as current full audits. Increment-specific checks and new source reachability are recorded in [incremental-review-2026-11-19.json](../data/incremental-review-2026-11-19.json). No experiment, commit, or publication was performed as part of this review.
