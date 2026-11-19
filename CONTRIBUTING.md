# Contributing to RSI Research Hub

Contributions should improve the accuracy, explanatory depth, or reproducibility of the research record. All filenames, prose, comments, templates, and commit messages must be written in professional academic English. Preserve author names and official titles accurately.

## Paper admission

Use a primary paper, official proceedings record, or author-linked project to resolve identity. Search results, aggregators, and curated lists are discovery tools. An acronym match is insufficient. Check first publication date separately from revisions and recommendation dates. Do not infer conference acceptance from an arXiv identifier, a nearby bibliography entry, or a third-party list.

Read methods, experimental setup, results, and limitations. Use the [paper template](templates/paper-review.md) with all 15 fields. Cite a section, page, figure, or table for material claims. Record the exact paper revision in [data/papers.json](data/papers.json). Use `Not verified` with the missing evidence and reason; do not leave an unexplained empty field.

For a numerical comparison, identify the benchmark version, task subset, executor and proposer, comparator, metric, budget/feedback conditions, and repetition count when available. Distinguish percentage points from relative percentages. Do not present a selected peak as a final checkpoint or a single task as a benchmark aggregate. Report uncertainty and known split overlap.

## Evidence labels

- **Primary-reviewed:** source identity and substantive sections were inspected; results remain author-reported.
- **Code available:** the paper or author project links a repository whose relevant code was inspected. A placeholder is not an implementation.
- **Independently reproduced:** an actual run with versioned configurations, raw outcomes, and analysis exists in this repository or an explicitly cited independent artifact.
- **Research hypothesis:** a proposed mechanism or prediction has not been validated.
- **Discovery-only:** a lead has not completed full-text review and is excluded from the reviewed-paper count.

Repository initialization contains no independently reproduced scientific result. Documentation CI is not a benchmark reproduction.

## Updating the catalog

Add the review under the first-publication year, or `papers/foundations/` for pre-2025 work. Add a unique stable ID to `data/papers.json`, including title, authors, affiliations, first date, venue status, paper URL, reviewed-version URL, official code or null, note path, inspected sections, review date, and reproduction status. Preserve source-specific metadata such as repository commits or venue-verification caveats.

Update [paper-index.md](papers/paper-index.md), [references.bib](references.bib), and affected synthesis documents. Do not silently replace a reviewed version with a newer one. Identify changes to title, authors, experimental setup, or conclusions. Explain consequential corrections in the pull request.

## Homepage and visual maintenance

Keep the homepage concise and preserve its navigation, research map, and evidence labels. When admitting papers, update the reviewed-paper count in the homepage, paper index, and review guide together. Refresh the homepage's four recent entries from admitted records in `data/papers.json`, ordered by first publication date; do not present an old paper's revision date as a new publication. Advance the review cutoff only after completing the corresponding source review. Discovery-only leads do not belong in the recent-reviewed table.

The banners in `assets/` are self-contained SVGs with a dark navy, cyan, blue, and violet palette. Keep changing paper counts and dates in selectable Markdown rather than in illustrations. Preserve image descriptions and text equivalents for diagrams. Use GitHub-supported Markdown and HTML; avoid external font, script, and image-service dependencies. Check image paths, heading anchors, collapsed sections, and the rendered homepage when changing layout.

## Research and experiment contributions

Research ideas require a nearest-work comparison and a falsifiable distinction. Avoid claiming originality before literature review and controlled results. Follow the [evaluation protocol](experiments/evaluation-protocol.md), use the [experiment report](templates/experiment-report.md), and distinguish planned, smoke-tested, executed, analyzed, and independently reproduced stages.

Keep evaluators and audit tasks outside the improver's editable surface. Log rejected candidates and resource costs. Publish null and negative results with the same artifact standard as positive ones. Do not replace a failed run silently or tune on the final audit.

## Validation before a pull request

Run:

```bash
npm ci --ignore-scripts
npm run lint
git diff --check
git status --short
```

Then inspect relative links and heading anchors, compare metadata with primary sources, audit all reported numbers, and review staged filenames and content. Do not commit credentials, private datasets, API responses containing secrets, model weights, raw paper downloads, or machine-specific paths. Prefer a source link and artifact hash when redistribution is not established.

Use focused English commits, such as `docs: review a new harness-evolution paper` or `docs: correct evaluation split interpretation`. The issue templates support paper submissions, evidence corrections, and experiment proposals. Include a source locator and explain the effect of every substantive correction.

## Interpretation standards

GitHub stars do not establish algorithmic quality. A single benchmark does not establish general RSI. A non-significant difference does not prove equivalence. A better final agent does not prove a better improver. A theoretical guarantee applies only under its stated assumptions. A source's claim of code release must be checked against the actual release state.
