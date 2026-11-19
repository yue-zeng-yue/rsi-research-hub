# STOP: a scaffold that edits its own optimizer

Evidence cutoff: **2026-11-19**. Numerical results below are author-reported; not reproduced here. Classification: recursive **scaffold-code** improvement with fixed model weights.

## 1. Full Paper Title

*Self-Taught Optimizer (STOP): Recursively Self-Improving Code Generation*.

## 2. Authors and Affiliations

Eric Zelikman, Eliana Lorch, Lester Mackey, Adam Tauman Kalai. The COLM manuscript lists Zelikman at Stanford, Mackey at Microsoft Research, and Kalai at OpenAI; starred authors' work was done at Microsoft Research New England. Lorch has no institutional affiliation printed there; affiliation **Not verified**. [COLM title page](https://openreview.net/pdf?id=46Zgqo4QIU)

## 3. Publication Date

First submission **2023-10-03**; inspected revision **2024-08-16, v3**.

## 4. Venue or Preprint Status

Published as a conference paper at **COLM 2024**, according to the paper and arXiv record. [Record](https://arxiv.org/abs/2310.02304)

## 5. Paper URL / DOI

[Full text v3](https://arxiv.org/pdf/2310.02304v3); [DOI](https://doi.org/10.48550/arXiv.2310.02304).

## 6. Official GitHub Repository

[microsoft/stop](https://github.com/microsoft/stop), explicitly linked by the paper. README distinguishes **MIT code** from **CC BY 4.0 documentation/data**. The repository was accessible and unarchived at inspection; its observed last push was 2024-01-01, so availability does not establish that it fully tracks the later COLM revision. [Repository](https://github.com/microsoft/stop)

## 7. Research Problem

Can an LM-calling program optimizer improve its own code sufficiently to improve subsequent downstream optimization?

## 8. Methodology and Algorithm

The seed improver samples candidate programs and selects using a utility function. Meta-utility measures the resulting improver on downstream tasks; the improver is then applied to its own source. Schematically, `I[t+1] = I[t](I[t], meta_utility)`. Model weights stay fixed.

## 9. Key Contributions

Self-modification occurs in the search scaffold, making this stronger than editing one answer but narrower than full model-level RSI. The paper also probes unsafe generated execution behavior.

## 10. Experimental Setup

Main experiments use `gpt-4-0314`, 10-bit learning parity with noise, 20 utility instances, and 50 held-out instances; five independent STOP runs. Weaker-model comparisons use GPT-3.5 and Mixtral.

## 11. Benchmarks and Baselines

Seed, chain-of-thought, and greedy iterative improvers; transfer to string-grid distance, modified quadratic assignment, 3SAT, Maxcut, and noiseless parity.

## 12. Quantitative Results

A selected improver after four rounds raises transfer 3SAT utility from **21.2% to 75.1%** and Maxcut from **58.7% to 74.2%**. These are task-specific utility scores for a selected optimizer, not aggregate general coding accuracy. [Sections 3–5, Table 1](https://arxiv.org/pdf/2310.02304v3)

## 13. Limitations

Small task family, stochastic selection, and fixed proprietary models constrain generalization. Performance need not increase every round. [Sections 5–8](https://arxiv.org/pdf/2310.02304v3) Research implication: selection over many scaffold variants can overfit the meta-evaluation even when no downstream task text is exposed. Reserve a separate optimizer-selection split and final transfer suite.

## 14. Reproducibility

The official repository supplies code and data under separate licenses, but its short README is not a complete contemporary deployment guide. Reproduction should record the exact commit, initial improver, utility-call budget, task seeds, generated candidates, failures, and API model identifier. Availability of the historical API snapshots today is **Not verified**; substituting a new model is a new experiment. GPU-hours and present dollar cost: **Not verified**. Generated code should execute in an externally enforced sandbox whose rules the candidate cannot edit; a mutable Python flag is not an isolation boundary.

## 15. Open Research Questions

Proposed studies: Does improvement transfer to held-out optimizer objectives rather than nearby algorithmic tasks? What fraction of gain survives matched token and utility-call budgets? Can a better downstream improver also reliably improve the next optimizer generation? Can the validator detect time-budget evasion and test tampering before selection? Report the entire distribution of seeds and all attempted rounds, not only the best final scaffold.
