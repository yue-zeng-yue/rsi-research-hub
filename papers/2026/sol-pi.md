# SoL-Pi: Recursively Scaling Auto-Research Loops for Efficient Agent Harness

## Full Paper Title

SoL-Pi: Recursively Scaling Auto-Research Loops for Efficient Agent Harness

## Authors and Affiliations

Haozhe Liu; Tian Ye; Sensen Gao; Qihang Cao; Yitong Li; Mingchen Zhuge; Duomin Wang; Ruihua Zhang; Ping Luo; Jiawang Bian; Lei Zhu; Ligeng Zhu; Enze Xie; Song Han. The paper lists NVIDIA, NTU, and MIT. Individual author-to-institution assignments are not verified because the consulted HTML provides a collective institutional line.

## Publication Date

First submitted 2026-09-17; reviewed arXiv v1, the only version listed as of the 2026-11-19 cutoff.

## Venue or Preprint Status

arXiv preprint; peer-reviewed publication status not verified.

## Paper URL / DOI

[Paper, v1](https://arxiv.org/html/2609.20519v1); [arXiv DOI](https://doi.org/10.48550/arXiv.2609.20519).

## Official GitHub Repository

[NVlabs/SoL-Pi](https://github.com/NVlabs/SoL-Pi), directly linked in the paper; [official project](https://nvlabs.github.io/SoL-Pi/).

## Research Problem

Can automated research discover reusable reductions in long-horizon agent token expenditure while keeping task capability within declared tolerances?

## Methodology and Algorithm

The search explores 152 directions through independent development lineages over 535 environments. Fixed capability gates precede efficiency gates; nondominated survivors are integrated and frozen. Four retained mechanisms act at distinct boundaries: Action Fusion combines edits with follow-up commands; Online Context Compact compares projected future input savings against cache-rewrite cost; ObservationPack replaces large repeated outputs with handles and excerpts after two requests; Evidence-Preserving Reducer asks a cheaper model to extract log evidence and verifies hashes, exact quotes, exit status, schema, and size, falling back to originals. This is automated harness research, while recursive reuse of the improved harness in later research cycles remains future work. See §2.

## Key Contributions

The useful artifact is a concrete four-mechanism extension to Pi. Search/evaluation isolation is stronger than same-benchmark tuning. Exact evidence retention and deterministic fallback are practical contributions; broad search counts alone do not establish a scaling law.

## Experimental Setup

Search includes 495 repository issue/patch environments and 40 verifier-driven synthetic tasks, with over 3,000 runs and 60,000 interactions. EdgeBench’s 51 public tasks split into 11 one-way acceptance tasks and 40 final generalization tasks. The full stack is frozen before evaluation; GPT-5.6 Sol is the search backend, Opus 5 a transfer backend, and GPT-5.6 Luna performs reduction. Pricing is fixed to 2026-08-17.

## Benchmarks and Baselines

Pi, native Codex/Claude Code, OpenCode and other harnesses on EdgeBench; additional Terminal-Bench 4, IMO 2026, and kernel-swarm evaluations. Efficiency denotes cost per aggregate score. Backend-specific “Performance” points select the best single mechanism, whereas “Efficiency” is the full fixed stack.

## Quantitative Results

Author-reported; no independent reproduction.

| EdgeBench condition | Score | Recorded tokens, B | API cost | Source |
|---|---:|---:|---:|---|
| GPT-5.6 Sol / Pi | 44.833 | 2.1538 | $1,339 | Tables 1–2 |
| GPT-5.6 Sol / full SoL-Pi | 42.003 | 1.0990 | $894 | Tables 1–2 |
| Opus 5 / Pi | 44.756 | 2.3697 | $1,741 | Table 2 |
| Opus 5 / full SoL-Pi | 42.224 | 1.3101 | $1,158 | Table 2 |
| Sol / ObservationPack-only | 47.208 | 2.0224 | $1,271 | Tables 1, 4 |

Full-stack savings accompany lower mean scores; these data do not establish strict quality equivalence.

## Limitations

Only 40 tasks are the final untouched generalization partition, while headline tables summarize all 51 public tasks. Performance configurations are selected separately by backend, so their transfer claim is weaker than that of the preselected full stack. Token traffic includes cache traffic and is not equivalent to FLOPs. The compaction gate omits separate pricing of its summarization call. No controlled equal-budget breadth/depth scaling law or demonstrated multi-generation efficiency compounding is provided.

## Reproducibility

The MIT repository releases opt-in Pi extensions and compatibility/configuration checks. The current README records tested Pi versions and warns about dependency incompatibilities. Its deployable extension release should not be presumed to reproduce the entire 535-environment search. Source accessibility was verified; installation and benchmark outcomes were not tested.

## Open Research Questions

What is net savings after amortizing search, integration, and auxiliary-model calls? Do savings persist at a prespecified noninferiority margin with repeated seeds? Can a second research generation use the first generation’s savings to produce a better Pareto frontier under fixed total compute?
