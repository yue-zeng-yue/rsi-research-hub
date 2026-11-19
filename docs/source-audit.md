# Source Audit and Verification Boundaries

**Inspection date and literature cutoff:** 2026-11-19, Asia/Shanghai. First submission dates determine eligibility; revisions inspected must also precede the cutoff. This curated snapshot does not claim exhaustive retrieval of all papers published by the end of that day.

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

The final initialization validation record is [data/repository-validation.json](../data/repository-validation.json). It contains file and paper counts, English-script and path checks, local-link checks, review-field checks, and sensitive-content screening results. The URL audit is [data/link-audit.json](../data/link-audit.json); failures identify transport or source-access gaps and do not silently disappear from the record. Markdown validation runs through the pinned npm lockfile and GitHub Actions.

These are documentation and provenance checks. They must never be cited as experimental confirmation of any algorithm in this repository.
