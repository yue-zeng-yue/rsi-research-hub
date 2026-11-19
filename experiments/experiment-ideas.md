# Initial Discriminating Experiments

All studies below are plans. Budgets and exact model choices must be fixed before execution; no result is implied by the predicted outcome.

## E1: Does a skill help its executor?

Use a pinned SkillsBench release and an unchanged executor. Generate edits using development tasks, then randomize enable/disable assignment on fresh task instances. Compare curated skills, generated skills, no skills, and irrelevant but valid skills. Match inference caps and count skill-generation cost. Measure task success, retrieval, invocation, tokens, and latency. Do not condition the primary contrast on observed invocation. Hold out task families for utility-model evaluation.

**Discriminating result:** A learned utility policy beats a direct paired-validation selector at equal total cost on unseen families. A result confined to development tasks rejects the transfer claim. Source context: [Updating versus Benefit](https://arxiv.org/abs/2605.30621).

## E2: Does model adaptation break harness compatibility?

Start from one fixed open-weight model and one harness. Evolve the harness on development tasks; train the model using either full expert imitation, on-policy correction, or a model-only baseline. Evaluate old/new weights crossed with old/new harnesses. Control the teacher budget and include all failed rollouts and training runs. Repeat with an unseen executor family only after the first full comparison is reliable.

**Discriminating result:** Pair-aware selection improves joint utility or regression coverage over separate gates, rather than merely recovering the known advantage of localized correction. Source context: [On-policy correction](https://arxiv.org/abs/2609.09134), [JoMoHa](https://arxiv.org/abs/2611.11499).

## E3: Did the improver itself improve?

Save early and late improvers, reset the solver and skill library, and improve on new task generators with equal budgets. Compare learned meta-policy, HMED-style consequence memory, frozen improver, and shuffled memory. Repeat a second arm that carries solver memory to quantify its contribution separately.

**Discriminating result:** A paired late-versus-early improver gain from common states remains on unseen families. Improvement only when inherited task solutions are present supports solver transfer instead. Source context: [HMED](https://arxiv.org/abs/2610.07979), [Auditing the Product](https://arxiv.org/abs/2610.27610).

## E4: When does search pay for itself?

Compare uniform evaluation, multi-fidelity allocation, RRSI-style regularization, no-evaluation integration, and a fixed harness with extra inference. Run budget curves and price a range of deployment horizons. Hold the candidate generator fixed in a selection-only experiment, then run the complete loop prospectively.

**Discriminating result:** A lower total-cost frontier at a declared quality margin, including proposer/teacher costs. A cheaper deployment artifact with prohibitive discovery cost is a horizon-dependent tradeoff. Source context: [RSI Tax](https://arxiv.org/abs/2611.13524), [ELITE](https://arxiv.org/abs/2611.21056).

## Common launch gate

Before any expensive run, finish the split manifest, fixed baseline, cost ledger, analysis plan, and evaluator validation. Pilot measurements determine the number of full-loop seeds and resource cap. Record the measured budget and exact environment in the study preregistration.
