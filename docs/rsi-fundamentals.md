# Foundations of Recursive Self-Improvement

Review cutoff: **2026-11-19**. This chapter defines the repository's operational terminology; it does not claim that the literature uses a single agreed definition.

## What counts as improvement?

An agent is a distribution over trajectories, not just a language model checkpoint. Let $\theta$ denote model parameters, $h$ a persistent harness, $m$ persistent memory, and $\tau$ a task. The harness specifies prompts, tools, context assembly, memory access, termination, and control flow. Define

$$
J_D(\theta,h,m;b)=\mathbb{E}_{\tau\sim D,\,z\sim\pi_{\theta,h,m}(\cdot\mid\tau;b)}[R(\tau,z)],
$$

where $b$ is an execution budget and $R$ an independently specified task reward. An improvement claim must identify $D$, $R$, $b$, the initial artifact, and the uncertainty of the estimated difference. Changing the reward, spending more inference compute, or selecting the luckiest run can increase the measured score without establishing a more capable system.

Let $s_t=(\theta_t,h_t,m_t)$ and let an improver $I_{\phi_t}$ produce a candidate from training evidence $E_t$:

$$
\widetilde{s}_{t+1}=I_{\phi_t}(s_t,E_t;B_t),\qquad
s_{t+1}=\operatorname{Gate}(s_t,\widetilde{s}_{t+1};V_t).
$$

The evaluation set $V_t$ is separate from proposal data. Repeatedly querying it makes it part of development; a final sealed audit remains necessary.

## Self-improvement, recursion, and stronger process claims

| Claim | Operational requirement | Insufficient evidence |
| --- | --- | --- |
| Task refinement | A new answer or trajectory improves a current task | No persistent change is required |
| Persistent self-improvement | A retained change improves later task execution | Merely writing a skill file |
| Recursive mechanism | A retained change participates in producing subsequent improvements | Repeating a fixed external optimizer alone |
| Improved improver | A later improver improves a common initial solver more than an earlier one at equal budget | Comparing a late solver with an early solver |
| General RSI | Effective improvement persists across broad task, model, and resource shifts | A finite positive curve on one benchmark |

The repository uses **bounded RSI** when the recursive mechanism is demonstrated in finite experiments but its evaluator, budget, task generator, or other essential components remain fixed. A system may have recursive code while lacking evidence that recursion helps. Conversely, a fixed optimizer can be practically valuable without qualifying as improved-improver evidence. [STOP](https://arxiv.org/abs/2310.02304), [DGM](https://arxiv.org/abs/2505.22954), and [Hyperagents](https://arxiv.org/abs/2603.19461) illustrate progressively broader editable components, not a proven ladder toward unlimited improvement.

## Improving the agent versus improving the improver

For a distribution $P$ over starting states and task families, define the value of an improver as

$$
Q(I;P,B)=\mathbb{E}_{(s,D)\sim P}\left[J_D(I(s;B);b)-J_D(s;b)\right].
$$

This notation suppresses the internal proposal/evaluation loop. To test whether $I_1$ is better than $I_0$, assign both to **identical starting artifacts**, the same task split and search budget $B$, and independently evaluate their outputs at the same execution budget $b$. Their task memories, tools, caches, and solver weights must be reset or explicitly treated as experimental factors. Score equality is not state equality.

An evolving solver and improver create observational confounding: a stronger solver may make the improver appear better. [Auditing the Product, Not the Recursion](https://arxiv.org/abs/2610.27610) formalizes this distinction and audits how often appropriate comparisons are reported. Its counts describe its October 2026 search frame, not every paper ever written about self-improvement.

## RSI versus reinforcement learning

RL optimizes a policy against returns from interaction. With a fixed update operator $U$, conventional training is $\theta_{t+1}=U(\theta_t,\mathcal{B}_t)$, where $\mathcal{B}_t$ is a rollout batch. The learner can generate its own experiences without modifying $U$. This is policy improvement, not by itself evidence that the improvement algorithm improves.

An RSI system may use RL for its model updates, text-space search for its harness, and a learned scheduler for choosing between them. To claim meta-level improvement, it must identify what in the training algorithm, curriculum, evaluator, or proposal policy changed and isolate its contribution. GRPO is an update rule, not a synonym for RSI. See [Model RSI](model-rsi.md) for the objective and [Meta-RSI](meta-rsi.md) for process evaluation.

## Historical development and applications

1. **Formal self-rewriting.** [Gödel Machines](https://arxiv.org/abs/cs/0309048) study self-modification justified by proofs relative to a formal utility function and axioms. The guarantee is conditional on those assumptions and proof search, not an empirical guarantee for modern LLM agents.
2. **Learning from generated reasoning.** [STaR](https://arxiv.org/abs/2203.14465) uses successful generated rationales to improve a model through training. It is a foundation for self-training, while its update procedure remains externally designed.
3. **Executable improvers.** [STOP](https://arxiv.org/abs/2310.02304) makes the program-improvement scaffold itself an optimization target. [SICA](https://arxiv.org/abs/2504.15228) and DGM examine code changes to agents that can perform later modifications.
4. **Harness search and editable meta-agents.** [Meta-Harness](https://arxiv.org/abs/2603.28052), Hyperagents, and [AHE](https://arxiv.org/abs/2604.25850) investigate search history, observability, and modification of improvement behavior.
5. **Attribution, cost, and coupled learning.** The 2026 work represented by [HDA](https://arxiv.org/abs/2610.22466), [the RSI Tax](https://arxiv.org/abs/2611.13524), and [on-policy correction](https://arxiv.org/abs/2609.09134) asks whether gains transfer, amortize, and survive model changes.

Concrete applications include repository repair, terminal workflows, policy-constrained tool use, mathematical reasoning, and scientific optimization. Each has different feedback quality: unit tests can verify a patch but may be incomplete; simulator state can verify tool effects but embed benchmark shortcuts; a model judge can provide rich feedback while sharing errors with the proposer.

## Limits of current evidence

Finite search runs do not establish sustained acceleration, asymptotic convergence, or general intelligence. External frontier models often supply proposals or supervision, so improvement can reflect access to stronger pre-existing capabilities. Closed APIs and mutable model aliases undermine reproducibility. Search may exploit public task artifacts, and an adaptive evaluator can drift from the intended objective. Repeated selection rewards noise unless the audit is independent.

Operational improvement is still useful: a reusable tool can reduce calls across many deployments, and a tailored harness can help a small model complete a domain workflow. The appropriate claim is conditional and measurable. The [evaluation protocol](../experiments/evaluation-protocol.md) specifies the evidence needed before this repository will label any experiment an independently reproduced improvement.
