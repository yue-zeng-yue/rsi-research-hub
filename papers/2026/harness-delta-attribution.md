# Harness-Delta Attribution

## Full Paper Title

Harness-Delta Attribution: Dissecting Gains From Harness Evolution.

## Authors and Affiliations

Wenxuan Ding (Amazon; New York University); Qin Lu, Changlong Yu, Sha Li, Shuowei Jin, Xin Liu, and Zhenyu Shi (Amazon); Greg Durrett (New York University). Affiliations follow the paper's title page.

## Publication Date

First publication and reviewed version: 15 October 2026, arXiv v1. Evidence cutoff: 19 November 2026.

## Venue or Preprint Status

arXiv preprint. Peer-reviewed acceptance: **Not verified**; the consulted primary record identifies no venue.

## Paper URL / DOI

[Version-pinned paper](https://arxiv.org/html/2610.22466v1). DOI 10.48550/arXiv.2610.22466 is displayed by arXiv as **pending registration**; resolution is not verified.

## Official GitHub Repository

[Wenwen-D/HarnessDeltaAttribution](https://github.com/Wenwen-D/HarnessDeltaAttribution), linked directly in the paper; the README reciprocally cites it. Inspected revision: `cc4119a678b070e324e6d6d94adea1acfcc86acb`.

## Research Problem

An evolved harness can improve benchmark scores by exploiting dataset regularities, purchasing additional inference, or discovering reusable design. Aggregate improvement and even same-benchmark held-out performance do not identify these mechanisms.

## Methodology and Algorithm

For baseline B, evolved E, compute-matched baseline Bc, and shortcut-neutralized En, HDA defines T=S(Bc)−S(B), O=S(E)−S(En), and G=S(En)−S(Bc). Therefore ΔS=O+T+G exactly for raw signed scores. Bc retains the original scaffold while matching average inference expenditure; En minimally disables detected benchmark-specific mechanisms. An analysis agent proposes interventions, with human review of compute matching and neutralization. A paired-bootstrap significance gate excludes statistically insignificant gains from attribution. Displayed percentages are clipped, so they should not be confused with unrestricted causal effect estimates. Crucially, O estimates detected overfitting conservatively; G is a **residual upper bound**, not demonstrated transfer. See [§3](https://arxiv.org/html/2610.22466v1#S3).

## Key Contributions

The paper supplies an operational audit, controlled harness variants, and evidence that repeated task artifacts can survive ordinary train/test splitting. Examples include deterministic ALFWorld controllers eliminating model calls and a recurring correct meta-option in LiveMath.

## Experimental Setup

Twenty-five model–benchmark–framework settings cover eleven Qwen/Claude executors. Meta-Harness and SkillOpt use Opus 4.8 as proposer; AHE uses it as both proposer and executor. Meta-Harness additionally receives aggregate validation scores, while individual validation trajectories remain hidden. Search-selected and validation-selected checkpoints are evaluated on held-out tasks (§4; Appendix B).

## Benchmarks and Baselines

LiveMath, SWE-bench Verified, CREATE, and ALFWorld span reasoning, coding, creativity, and interactive planning. Each evolved harness is compared with its initial scaffold, a compute-scaled scaffold, and the neutralized intervention. The scaling policy must itself be appropriate to available deployment feedback; extra samples and oracle selection are different resources.

## Quantitative Results

All values are **author-reported**, not independently reproduced.

| Comparison / condition | Result | Source |
|---|---|---|
| 21 statistically significant settings, average attribution | O 54%; T 14%; O+T exceeds 50% in 14/21 | §5; Table 1 |
| Meta-Harness, ALFWorld, Qwen3.5-0.8B | +100 percentage points; O/T/G = 100/0/0% | Table 1 |
| Meta-Harness, CREATE, Haiku 4.5 | +37.9 Creativity Utility; O/T/G = 0/49/51% | Table 1 |
| Non-ALFWorld held-out tests versus search gains | Smaller in 13/15 settings; four regress below baseline | §5 |

## Limitations

Shortcut classification and surgical removal require judgment; entangled mechanisms can remain. The ordered decomposition is not a unique factorial causal attribution. Matching mean calls or tokens need not match latency or useful compute. Shared benchmark artifacts limit even held-out evidence. Selecting significant positive gains also prevents interpreting the averages as field-wide prevalence.

## Reproducibility

The repository includes splits, evolved harnesses, candidate summaries, configurations, and attribution tooling, but explicitly omits raw per-item logs and full trajectories. Model availability and human intervention choices remain reproduction dependencies. No experiments were run for this review.

## Open Research Questions

Can independent annotators agree on neutralization? Do positive residuals survive new task generators and artifact removal? How do conclusions change under equal dollars, latency, and deployment-available verification, rather than mean inference counts?
