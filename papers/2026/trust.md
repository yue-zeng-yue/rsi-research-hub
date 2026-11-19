# Trustworthy Recursive Self-Improvement with Statistical Guarantees

Review cutoff: 2026-11-19. Author-reported evidence; no independent reproduction.

## Full Paper Title

Trustworthy Recursive Self-Improvement with Statistical Guarantees

## Authors and Affiliations

Zihe Gao and Yifan Cui: Zhejiang University. Zhengling Qi: George Washington University. The PDF first page verifies the individual affiliation mapping missing from flattened HTML.

## Publication Date

2026-11-07, arXiv v1; inspected 2026-11-19.

## Venue or Preprint Status

arXiv preprint. Conference or journal publication: Not verified; no primary acceptance record found.

## Paper URL / DOI

[Paper](https://arxiv.org/abs/2611.10787); [full HTML](https://arxiv.org/html/2611.10787v1); verified [arXiv DOI](https://doi.org/10.48550/arXiv.2611.10787).

## Official GitHub Repository

Not verified. No author-designated implementation appears in the inspected paper, and exact-title/arXiv-ID searches did not locate one. The similarly named pujiayue/Trustworthy-RSI repository accompanies a different survey and must not be assigned to TRUST.

## Research Problem

Repeated noisy candidate selection can accept harmful harness revisions. Per-round tests do not automatically control errors across an adaptive lineage; strict familywise control can reject nearly everything under small evaluation budgets.

## Methodology and Algorithm

TRUST tests H0: Δt≤−ε using bounded paired outcomes, sequential e-values, and pre-validation contextual error allocation. Accept when evidence reaches 1/αt. Its budget charge is αt/(previous accepts+1). An overlap correction raises the null mean by exposure probability times β. Under Assumption 1, reused observations must satisfy a conditional optimistic-bias bound determined by β; the initial validation pool is iid and independent of initial information, sampling is prescribed, and betting/allocation are predictable. Theorem 2 controls FERε=E[unacceptably harmful accepts/(accepts∨1)]≤q, including bounded outer stopping. This is not a bound on the probability of any regression or every task-family loss (§§3–5).

## Key Contributions

The paper connects contextual online multiple testing to acceptance decisions and explicitly distinguishes tolerated losses from genuine improvement. Consequently, statistical gating or LLM-guided evidence allocation alone is already prior art. A new method needs a distinct estimand, stronger applicable assumptions, or a demonstrated efficiency benefit.

## Experimental Setup

30 rounds and five seeds per setting; 20 initialization examples, a reused 200-example validation pool, up to 40 paired evaluations per round, and 300 reporting-only test examples. Defaults: q=.30, ε=.10, β=.01. Three proposals are screened using prior feedback. Initial harnesses contain prespecified weaknesses (Appendix G).

## Benchmarks and Baselines

HotpotQA joint F1, DROP token F1, and APPS test-case pass rate; DeepSeek-V4-Flash and Qwen-3.8-Flash. Gates: Greedy, PACE, Bernstein SGM-B, Hoeffding SGM-H, and TRUST. These baselines target different error criteria and loss tolerances, so risk-power curves are more informative than a single ranking.

## Quantitative Results

Table 1/§1 report six-setting mean gain 24.84 percentage points, empirical FER0 2.78% versus Greedy 45.59%, and mean maximum drawdown .047 versus 4.963 points. On DeepSeek HotpotQA, TRUST gain is 11.58±1.30 points (standard error). Empirical FER0 counts ties as non-improvement; it is not the theoretical FERε with ε=.10.

## Limitations

Exact β calibration from data is unresolved (§7). Thus observed low FER does not certify Assumption 1. Power consistency additionally fixes the horizon while n,N grow with n/N→0, assumes improving proposals occur, and restricts betting fractions; it is not an indefinite-recursion result. A positive tolerance permits accumulated small losses, and the final-gain lower bound need not be positive.

## Reproducibility

Independent reruns and proof verification were not performed. Algorithms, assumptions, operator menus, and gate settings are supplied. API identities, candidate-screening history, all exposed samples, and full token costs should be logged; early test stopping does not eliminate feedback costs because experiments retain all 40 feedback examples.

## Open Research Questions

Can β be conservatively estimated or avoided with fresh samples? How should false-evolution control extend to drifting distributions and family-specific harms? Evaluate all gates at comparable risk targets, add pristine strong incumbents, and compare prospective total-cost frontiers. Coupled model/harness selection also requires accounting for candidate-pool selection before testing.
