# Agentic Harness Engineering Beta: Requirement-Centered Evolution of Agent Harnesses

Review cutoff: 2026-11-19. Author-reported evidence; no independent reproduction.

## Full Paper Title

Agentic Harness Engineering Beta: Requirement-Centered Evolution of Agent Harnesses

## Authors and Affiliations

Jiahang Lin, Jiahao Chen, Yiding Wang, Shichun Liu, Shihan Dou, Honglin Guo, Changhao Jiang, Qi Zhang, Tao Gui, Xuanjing Huang: Fudan University; Chengjun Pan: Peking University; Yuyang Hu: Renmin University of China; Zhenhua Han, Hang Yan: Shanghai Qiji Zhifeng Co., Ltd. Author order is preserved in the manifest.

## Publication Date

2026-11-18, arXiv v1; inspected 2026-11-19.

## Venue or Preprint Status

arXiv preprint. Conference acceptance or journal publication: Not verified; no primary venue record identified.

## Paper URL / DOI

[Paper](https://arxiv.org/abs/2611.24924); [full HTML](https://arxiv.org/html/2611.24924v1); verified [arXiv DOI](https://doi.org/10.48550/arXiv.2611.24924).

## Official GitHub Repository

[Curry09/AHE-Beta](https://github.com/Curry09/AHE-Beta), linked by the paper. The inspected repository contains experiment orchestration, runtime, evaluation, locked dependencies, and local Docker/Gitea or E2B workflows. It is substantive code, not a placeholder.

## Research Problem

Task verifiers miss user requirements such as interruptibility, understandable progress, and delivery of completed results. The paper asks whether interaction-derived requirements can guide persistent harness changes without selecting candidates on benchmark scores.

## Methodology and Algorithm

With model weights fixed, simulated users file issues during multi-turn sessions. Triage checks evidence; an Architect consolidates shared causes; a PM derives additional requirements; Developers implement reviewed RFCs. Admission excludes hidden tests and graders. Merge requires design review, completed tests, code review, and approval bound to the current PR head. The update is H(t+1)=Merge(Develop(H(t), verified requirements)); its gate establishes requirement compliance, not a statistical guarantee of positive task utility (§3).

## Key Contributions

The useful distinction is the optimization signal and engineering workflow. Requirement satisfaction supplies candidate acceptance evidence beyond scalar benchmark reward. However, this does not isolate which role, simulator behavior, or runtime change causes the final improvement.

## Experimental Setup

One evolution run per configuration; six scheduled rounds comprise five modification rounds and a final session-only round. Main configuration uses 32 task/persona seeds. GLM-5.3-Flash executes and simulates users; GLM-5.3 engineers the harness. Main frozen-artifact evaluation repeats three times; other configurations once (§4.1; Appendix E).

## Benchmarks and Baselines

38 held-out Harbor-index tasks cover coding, optimization, analysis, and tool use. Comparators are Base Harness, Claude Code, and released evolved AHE/Meta-Harness artifacts. These are same-executor deployment comparisons, not matched-budget reruns of competing search algorithms.

## Quantitative Results

Figure 2/Table 10 report pass@1 33.3% versus Base 21.9%, and execution tokens 1.42M versus 2.40M/task. Table 4 transfers improve GLM-5.3 by 15.8 points and DeepSeek-V4.1-Flash by 5.3 points. Table 1 reports human preference 31 versus 7, with 10 tie/neither responses among 48 pairs. Table 12 records 1,924.8M evolution tokens as an incomplete lower bound, not total cost.

## Limitations

Execution-token savings exclude simulated-user costs. Three deployment repetitions do not measure search variance. Human pairs come from 25 participant labels; completion is self-reported without independent patch review. The small task suite and shared simulator family limit generality. A source-model gain cannot establish universally beneficial transfer; GLM-5.3 execution tokens actually increase in Table 4.

## Reproducibility

Independent reruns were not performed. Repository workflows and pinned baseline revisions improve inspectability, but reproducibility still depends on API models, sandbox infrastructure, task materials, and full usage coverage. A serious replication should preserve failed sessions and distinguish evolution cost from deployment cost.

## Open Research Questions

Can requirement admission predict utility before rollout evaluation? Does explicit uncertainty improve the review gate? Compare feedback-matched, equal-total-cost searches; randomize role removal; test real-user transfer and longer lineages. Combining requirements with statistical acceptance is promising only if the combined method outperforms each component under the same information budget.
