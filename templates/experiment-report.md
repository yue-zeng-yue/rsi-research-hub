# Experiment Report Template

This is an unfilled reporting specification, not a record of a completed experiment. Replace instructions with evidence before adding a report to `experiments/reports/`.

## Identity and Status

Give a stable experiment ID, date, responsible contributors, source commit, and stage: preregistered, smoke-tested, running, executed, analyzed, or independently reproduced. Link the relevant research proposal.

## Claim and Falsification Criterion

State one primary hypothesis, estimand, practical improvement threshold, and outcome that would reject or weaken the claim. Distinguish product improvement, improved improver, transfer, and efficiency.

## Closest Work and Baselines

Link primary reviews, explain how baselines were implemented, and disclose deviations, inherited numbers, and different feedback access. Include a strong fixed-system extra-compute control where applicable.

## Artifacts and Environment

Record model revisions, harness and improver hashes, adapter configuration, evaluator commit, dataset/task-generator version, container digest, dependency lockfile, hardware, provider, API dates, reasoning settings, and decoding parameters. Include exact reproduction commands once verified.

## Data Boundaries

List train/proposal, development, validation, and sealed-test manifests. Explain task-family splits, source-code or solution contamination checks, simulator state resets, and which feedback each method can inspect. Record every audit access.

## Protocol and Randomization

Specify candidate generation, treatment assignment, update acceptance, search iterations, stopping rule, independent search seeds, execution repetitions, task order, failure retry policy, and checkpoint selection. For meta-RSI, specify the identical starting artifacts. For co-evolution, include the four crossed component conditions.

## Resource Budget and Accounting

Separate planned caps from observed costs. Count proposal, judge, teacher, training, execution, environment, rejected-candidate, retry, and validation costs. Report raw tokens/calls/GPU-hours/wall time, provider prices, and both development and audit totals. State the deployment horizon used for amortization.

## Results and Uncertainty

Publish raw per-task and per-search-seed outcomes and denominators. Report the primary contrast with confidence interval, variance across whole-loop reruns, task-family changes, failures, and cost. Explain bootstrap clusters or statistical-model assumptions. Do not insert synthetic example scores into a completed report.

## Ablations and Diagnostics

Identify which components causally differ between arms. Include relevant frozen-improver, memory reset, compute-matched, skill availability, or model–harness swap controls. Report negative interactions and failed candidates.

## Deviations and Limitations

List departures from preregistration, infrastructure failures, missing logs, unstable APIs, and excluded tasks. Explain the impact on inference. If test feedback caused redesign, mark the later result as a new development stage requiring a fresh audit.

## Reproduction and Decision

Link configuration, data manifests, raw artifacts, and analysis code. State exactly what an independent reviewer reproduced. Conclude whether the hypothesis is supported, rejected, or inconclusive within the tested scope, and record the next decision without extending the claim beyond its evidence.
