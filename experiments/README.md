# Experiments and Reproducibility

No large training, benchmark, or API-agent experiment was run during initialization. This directory contains executable-study specifications in prose, not completed experimental results or installed benchmark environments.

Start with the [benchmark catalog](benchmarks.md), adopt the [evaluation protocol](evaluation-protocol.md), and select an [experiment idea](experiment-ideas.md). The four research proposals specify algorithms and nearest baselines. Before launching, pin concrete model checkpoints, dataset revisions, a dependency lockfile, hardware, and a resource budget. No generic launch command is supplied because those choices materially change what an experiment measures.

## Planned sequence

| Stage | Work | Exit evidence |
| --- | --- | --- |
| Environment validation | Install one pinned benchmark, check task manifests, run evaluator/oracle validation | Environment and verifier logs; no agent performance claim |
| Fixed-system baseline | Execute a fixed model/harness with repeated trials | Per-task scores, cost ledger, variance estimate |
| Direct controlled comparison | Run update versus no-update or four-cell component swaps | Matched feedback/budget and paired effects |
| Full-loop comparison | Compare search procedures with independent search seeds | Search cost and final sealed outcome distribution |
| Transfer study | Hold out task families and executor models | Clean-start, no-adaptation and adaptation results separated |

Use [experiment-report.md](../templates/experiment-report.md) for each run. Preserve model, harness, improver, and evaluator identities separately. A result table with no raw denominators, versions, or failed runs is not ready for inclusion in a research claim.

## Artifact policy

Future reports belong in `experiments/reports/` only when a real run exists. Large raw traces, checkpoints, and environments belong in an approved artifact store, with access-controlled references where necessary. Empty result directories and invented sample measurements are intentionally absent.
