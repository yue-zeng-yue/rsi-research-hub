# Research Roadmap

This roadmap tracks evidence milestones rather than promising positive findings or publication dates. The initial literature cutoff is 2026-11-19. Each experimental phase specifies its execution environment and resource budget before launch.

## Phase 1: Establish the research base

**Initialization deliverables:** five technical-area guides, source-grounded paper reviews, a trend report, four research proposals, six benchmark guides, and review/report templates. The machine-readable catalog records inspected versions and independent reproduction status.

**Exit criterion:** citations and versions are traceable; missing fields are explicitly qualified; English, Markdown, links, and sensitive-file checks pass; remote repository contents match the committed local tree. See the [source audit](docs/source-audit.md).

## Phase 2: Reproduce a direct harness-benefit comparison

Select one pinned benchmark, fixed executor, and existing update method. Establish a fixed-harness baseline, paired update/no-update outcomes, complete costs, and search variance. Separate environment/oracle validation from agent results. Use a held-out task-family audit and a matched-budget sampling baseline.

**Exit criterion:** another researcher can rerun the exact configuration from the report and recover results within reported uncertainty. A failed reproduction is a valid outcome if the cause and evidence are documented.

## Phase 3: Test one algorithmic contribution

Prioritize utility-aware adaptation, then compatibility-aware pair selection if training resources justify it. Freeze the primary hypothesis, closest baselines, task splits, budget, and failure criterion. Recheck new literature, especially methods for statistical gates, revision-consequence memory, and joint model–harness learning.

**Exit criterion:** either an independently auditable gain over strong equal-cost baselines across held-out families, or a clear negative result explaining why the proposed mechanism fails. Add complexity only when an ablation justifies it.

## Phase 4: Evaluate meta-level transfer and economics

Compare early and late improvers from common starting states. Separate transfer of the improver from transfer of the task solver and memory. Repeat the full loop across seeds and executor families. Report total-cost frontiers and break-even deployment horizons alongside success and regression.

**Exit criterion:** claims distinguish product performance, process improvement, and generalization. Any efficiency claim includes failed proposals and evaluation costs.

## Phase 5: Prepare a reproducible publication

Develop a manuscript around one concrete contribution, with complete related work, ablations, statistical analysis, resource accounting, limitations, and artifacts. Choose venue based on the contribution and evidence. Verify current submission policies, dates, and artifact requirements when a manuscript exists; none are assumed here.

**Exit criterion:** code and configurations reproduce the central tables, results survive an independent review, and claims match their evaluation scope. Acceptance is an external decision, not a roadmap milestone the repository can guarantee.

## Maintenance cadence

For each literature update, record the search date, queries, source versions, included/excluded leads, and unresolved fields. Revisit numerical tables when revisions change; retain the first submission date separately. Refresh the trend report when evidence changes the agenda rather than merely adding names. Reassess close baselines before each experiment and manuscript submission.
