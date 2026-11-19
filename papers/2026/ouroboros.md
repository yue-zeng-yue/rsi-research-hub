# Ouroboros: A Self-Developing Frontier Coding Agent with Reviewed Core Evolution

Reviewed against primary sources on 2026-11-19. Quantitative findings below are author-reported, not independently reproduced.

## Full Paper Title

Ouroboros: A Self-Developing Frontier Coding Agent with Reviewed Core Evolution

## Authors and Affiliations

Anton Razzhigaev; Andrei Gritsaev; Andrei Kaznacheev; Nikita Dragunov; Roman Yampolskiy; Andrei Kuznetsov

PDF page 1: Razzhigaev—Lomonosov Moscow State University, Skoltech, FusionBrain; Gritsaev—FusionBrain and HSE University; Kaznacheev and Dragunov—Lomonosov Moscow State University; Yampolskiy—Joi Lab; Kuznetsov—Skoltech and FusionBrain. Both PDF and HTML print “FusionBrain Lab at AXXX Institute”; the parent institute is Not verified beyond that printed label. Hope is a system contributor, not a formal author.

## Publication Date

2026-08-08; revised 2026-08-31; reviewed v3.

## Venue or Preprint Status

arXiv preprint; no conference acceptance independently verified.

## Paper URL / DOI

[arXiv](https://arxiv.org/abs/2608.08311) · [Full text](https://arxiv.org/html/2608.08311v3) · [arXiv DOI](https://doi.org/10.48550/arXiv.2608.08311).

## Official GitHub Repository

[Official repository](https://github.com/razzant/ouroboros) and [project](https://ouroboros-agent.ai/), both linked from the paper. README/source project exists, but its live state has advanced beyond benchmark snapshots.

## Research Problem

A persistent agent encounters bugs and context failures that a frozen runtime cannot correct itself. Ouroboros studies how such observations become reviewed code changes used by later work, while keeping operator authority outside ordinary self-editing.

## Methodology and Algorithm

A launcher/supervisor surrounds a mutable agent repository. Free evolution makes improvement a scheduled task; experience-driven evolution turns ordinary failures or human suggestions into maintenance proposals. Adoption passes deterministic preflight, staged-diff fingerprinting, blocking model review, and a fresh fingerprint check. Review evidence binds to the exact staged state. Child agents return isolated patches; the parent integrates them. Protected governance files, an external spend limit, rollback, and supervisor-level halt bound mutation.

## Key Contributions

The contribution is an integrated long-running system and audit trail, not a proof that unrestricted self-modification improves an optimizer. It distinguishes live deployment lineage from frozen benchmark snapshots and documents actual failure classes, including contamination, weak verifiers, and isolation mistakes.

## Experimental Setup

Hope’s public deployment spans 161 days to an August 6 cutoff and reports $110.6K model spend and 79.7B processed tokens. Benchmark campaigns use frozen seeds with disclosed model/provider/effort settings and official verifiers. Terminal-Bench has five trials over 89 tasks; OSWorld uses a 100-turn budget on the standard non-Google-Drive set. CL-Bench disables core evolution and task delegation.

## Benchmarks and Baselines

Terminal-Bench 2.1, OSWorld-Verified, CL-Bench, SWE-bench Pro, and GAIA; comparison harnesses include Claude Code, Codex, Cursor, and Hermes. Some headline leaderboard comparisons use different models, whereas the SWE comparison is explicitly model-matched.

## Quantitative Results

Table 2 and Section 5: Opus 5 terminal performance is 387/445=86.97% raw and 386/445=86.74% after removing one shortcut success. OSWorld reports 327.39/361=90.69%. Sonnet 4.6 CL-Bench normalized reward is 0.2301 versus 0.1960 ICL; this measures memory carry with core evolution disabled. After symmetric contamination filtering, SWE-bench Pro is 58.2% versus Codex 59.4% on 655 paired tasks, McNemar p=0.40.

## Limitations

One living lineage cannot isolate causal benefit from self-evolution, human input, changing models, or substantial spend. Reviewer models may share blind spots. Low context mode omits whole-repository review. Frozen benchmark success does not show that recursive evolution caused the score, and public-reference leakage materially changes comparison interpretation.

## Reproducibility

Primary architecture, score/audit sections, limitations, and official README were inspected. Independent reruns were not performed. Reproduction requires the frozen seed, runtime mode, provider route, attempt ledger, and audit exclusions rather than simply installing the latest repository.

## Open Research Questions

How much performance gain is attributable to reviewed core edits under fixed models and equal budgets? Can the review boundary remain effective over multiple independent evolving lineages and changing external environments?

Primary reading: Sections 3–7; Table 2; Limitations; Appendix C.
