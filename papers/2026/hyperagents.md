# Hyperagents (typeset as HyperAgents in the PDF)

## Full Paper Title

Hyperagents (typeset as HyperAgents in the PDF)

## Authors and Affiliations

Jenny Zhang (University of British Columbia; Vector Institute); Bingchen Zhao (University of Edinburgh); Wannan Yang (New York University); Jakob Foerster (FAIR at Meta); Jeff Clune (University of British Columbia; Vector Institute; Canada CIFAR AI Chair); Minqi Jiang (work done at Meta; no numbered institutional affiliation); Sam Devlin (Meta Superintelligence Labs); Tatiana Shavrina (FAIR at Meta).

## Publication Date

First submission 2026-03-19. Reviewed v2: arXiv submission history says 2026-11-01; its PDF cover says 2026-11-03. These are distinct source date fields, not interchangeable release dates.

## Venue or Preprint Status

arXiv preprint. Conference acceptance was not verified from an official proceedings record; third-party NeurIPS labels are not adopted.

## Paper URL / DOI

[Paper, v2 PDF](https://arxiv.org/pdf/2603.19461v2); [arXiv DOI](https://doi.org/10.48550/arXiv.2603.19461).

## Official GitHub Repository

[facebookresearch/Hyperagents](https://github.com/facebookresearch/Hyperagents), linked by the paper; repository title uses HyperAgents.

## Research Problem

DGM couples task competence and self-modification competence through coding. Hyperagents asks whether the procedure producing improvements can itself evolve when target tasks are paper review, reward design, or mathematical grading rather than coding.

## Methodology and Algorithm

A hyperagent combines task agent and meta-agent in one editable Python program. DGM-H samples from an archive; the selected meta-agent may rewrite both parts, with empirical evaluation controlling retention. Main experiments keep outer parent selection and evaluation fixed. To isolate improvement skill, improvement@k freezes a chosen meta-agent, permits k task-agent proposals, and measures the test-score gain of the validation-selected best candidate. Transfer-agent selection uses descendant performance gains discounted by lineage depth. See §3, §5.2 and Appendix D.3–D.4.

## Key Contributions

The distinctive evidence is transfer of an evolved improvement procedure, not merely transfer of a good task solver. Persistent memory and performance tracking appear as evolved mechanisms. Frozen-meta controls partially separate improved search behavior from continued adaptation during the transfer test.

## Experimental Setup

Paper-review/reward-design experiments use five runs and report bootstrap intervals; source runs last 100 iterations. Modification uses Claude 4.5 Sonnet outside Polyglot; evaluators include GPT-4o for review and o4-mini for grading. Appendix D.2 estimates 83.6 million total tokens per 100-iteration joint review/robotics run, including 33 million modification tokens.

## Benchmarks and Baselines

Polyglot, paper acceptance prediction, Genesis robot reward design, and IMO-GradingBench. Controls include DGM, manually adapted DGM-custom, fixed-meta DGM-H, no-archive DGM-H, and ProofAutoGrader. An initially malformed output interface contributes to zero-score starting points.

## Quantitative Results

Author-reported results; no independent reproduction.

| Condition / score | Comparator | DGM-H | Source |
|---|---:|---:|---|
| Held-out paper review | Initial 0; DGM-custom 0.590 | 0.710, CI 0.590–0.750 | §5.1, Fig. 2 |
| Math grading, imp@50, fixed meta-agent | Initial meta 0.000 | Transferred meta 0.630, CI 0.540–0.630 | §5.2, Fig. 3 |
| Grading after 200 iterations | Fresh 0.610 | Transfer 0.640 | §5.3, Fig. 4 |
| Full IMO-GradingBench accuracy | ProofAutoGrader 0.561 | 0.601 | §5.3; Appendix E.4 |

The 0.640 versus 0.610 comparison is explicitly not significant (p > 0.05).

## Limitations

Large gains from zero partly measure learning required formatting rather than newly acquired domain expertise. DGM-H versus DGM-custom is also not statistically significant in the principal noncoding domains. Fixed task distributions, fixed selection, finite budgets, and foundation-model dependence constrain recursion. Improvement@k equalizes proposal counts, not necessarily token expenditure; transfer nodes also benefit from prior search investment. These experiments do not establish an accelerating capability-growth rate.

## Reproducibility

Official code documents Python 3.12, Docker, domain configuration, and generate_loop.py. Its CC BY-NC-SA 4.0 license imposes noncommercial terms. Code availability and author links were verified; environment execution, complete artifact matching, and scores were not. Reproduction should report both source-run costs and target-run costs.

## Open Research Questions

Can transfer remain beneficial from a fully functional, strong initial interface under equal total cost? Does improved meta-agent quality persist when task-agent code and memory are separately reset? Which evolved mechanisms causally change improvement efficiency across multiple independently selected target domains?
