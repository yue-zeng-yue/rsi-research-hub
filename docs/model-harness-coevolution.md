# Model–Harness Co-Evolution

## The coupled objective

Model and harness jointly define behavior:

$$
\max_{\theta,h}\ J_D(\theta,h;b)-\lambda C_{\mathrm{deploy}}(\theta,h)
\quad\text{subject to}\quad C_{\mathrm{search}}+C_{\mathrm{training}}\le B.
$$

Changing $h$ changes what the model observes, which actions it can take, and which trajectories training collects. Changing $\theta$ changes whether the model understands and uses the harness. Consequently, two individually useful updates may interact negatively. A universal claim that a better model always benefits from a better harness is not warranted.

## Alternating and simultaneous optimization

Alternating optimization holds one component fixed while modifying the other. It makes attribution easier but can over-specialize each component to a stale partner. Simultaneous optimization permits coordinated adaptation but creates moving targets and more difficult credit assignment. [SIA](https://arxiv.org/abs/2605.27276), [HarnessForge](https://arxiv.org/abs/2606.01779), [WHALE](https://arxiv.org/abs/2609.00196), [HarnessAdapt-RL](https://arxiv.org/abs/2610.28069), and [JoMoHa](https://arxiv.org/abs/2611.11499) already occupy substantial parts of this design space. Merely combining harness evolution and fine-tuning is not a credible novelty claim.

## Measure compatibility with crossed interventions

For old/new model indices $i\in\{0,1\}$ and old/new harness indices $j\in\{0,1\}$, evaluate all four cells $J_{ij}=J(\theta_i,h_j)$. The interaction is

$$
\mathcal I=J_{11}-J_{10}-J_{01}+J_{00}.
$$

A negative $\mathcal I$ means the combined effect is subadditive on the chosen score scale. It does **not** necessarily mean absolute regression: $J_{11}$ can remain above $J_{00}$. Report both $\mathcal I$ and $J_{11}-J_{00}$, with paired uncertainty and per-family effects. For probabilities near zero or one, add a logistic-scale sensitivity analysis; interaction depends on scale.

[On-policy correction](https://arxiv.org/abs/2609.09134) documents a specific failure of full expert imitation after harness specialization. Its localized correction strategy is a close baseline for any compatibility-aware method. The [teacher-free co-evolution study](https://arxiv.org/abs/2611.15268) provides another relevant factorial design separating skills from trained weights.

## Credit assignment and stable updates

[CoEvoBench](../papers/2026/coevobench.md), reviewed November 25, evaluates researcher-driven choices between model and harness changes and includes component swaps. It is a close evaluation reference for the questions above. Its current public implementation has documented acceptance and provenance gaps, so the protocol and the readiness of the released executor must be assessed separately.

An increase in skill usage can follow both a harness edit and a model update. Counting usage does not determine which caused task success. Randomized component availability and crossed evaluations are more informative. For model learning, log the harness that produced each trajectory and the harness under which a likelihood is evaluated. A new tool interface can invalidate old trajectories even if token importance weights appear well behaved.

Use a candidate pool of compatible pairs rather than independently selecting the highest-scoring model and harness. A conservative acceptance rule can require a lower confidence bound on total gain and an upper bound on regression risk on a prespecified validation family. Such a rule provides an empirical guardrail, not a guarantee on arbitrary future tasks. Reusing the same validation set indefinitely also invalidates naive fixed-sample confidence claims.

Preserve a stable incumbent, immutable evaluation code, and versioned rollback artifacts. A failure of one component should be attributable to its change set. If rollback depends on test outcomes, those outcomes become development evidence; the final audit must be fresh.

## Generalization and negative transfer

Evaluate a matrix of executor families and harness sources, with task families held out from both training and harness search. Match permitted context and tool interfaces before comparing pairs. Test whether skills written by a large model are interpretable by smaller models and whether training transfers domain rules into weights or merely improves compliance with external rules.

Important regression categories include instruction-following failures, invalid tool schemas, lost context, overlong plans, failure to stop, and reliance on inaccessible tools. Stable average score can hide concentrated losses on a minority task family. The [compatibility proposal](../research/model-harness-compatibility.md) specifies risk-sensitive pair selection, crossover controls, and its overlap with existing methods.
