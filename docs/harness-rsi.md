# Harness RSI: Persistent Adaptation Without Weight Updates

## The optimization object

With frozen model parameters $\theta$, a harness $h$ maps observations and history into prompts, tool interfaces, context windows, actions, and stopping decisions. Search optimizes $h$ using execution evidence. A new prompt is one possible update; persistent memory, executable utilities, dispatch logic, and recovery rules are equally important. A fixed proposer optimizing $h$ is harness optimization. Recursion additionally requires a retained artifact to influence subsequent improvement.

| Surface | Candidate operation | Main failure mode | Required measurement |
| --- | --- | --- | --- |
| Prompts | Rewrite instructions or demonstrations | Longer prompts encode task shortcuts | Held-out score at matched tokens |
| Skills | Generate, retrieve, revise, or delete a reusable procedure | Skill is never read or is misapplied | Exposure, invocation, and randomized utility |
| Tools | Add wrappers, batch calls, or validate arguments | Tool silently supplies benchmark answers | State-based verification and artifact audit |
| Memory | Consolidate trajectories into reusable experience | Contamination, stale facts, harmful retrieval | Clean reset and time-shift evaluation |
| Context | Summarize, rank, evict, or reload observations | Lost constraints or hidden inference cost | Failure categories and full token accounting |
| Workflow | Change branches, subagents, retries, and termination | More attempts masquerade as better reasoning | Equal feedback, calls, and wall-clock comparisons |

## A useful improvement loop

Run a versioned incumbent on development tasks, preserve complete traces, diagnose failures, propose a bounded modification, verify interface compatibility, and compare against the incumbent. Retain both accepted and rejected proposals with their costs. An archive can preserve diversity; a single greedy lineage is simpler but can become trapped by early decisions. [DGM](https://arxiv.org/abs/2505.22954) uses an evolving archive; [Meta-Harness](https://arxiv.org/abs/2603.28052) makes candidate code, results, and traces accessible through a filesystem; [AHE](https://arxiv.org/abs/2604.25850) emphasizes observable components and falsifiable change predictions.

Trajectory analysis should distinguish a wrong plan, an invalid tool call, missing information, a context failure, and a failure to terminate. The same terminal reward can arise from different causes. A proposal justified by the wrong diagnosis may improve the development score while transferring poorly. Structured failure labels are hypotheses to validate, not privileged ground truth.

[AHE-Beta](https://arxiv.org/abs/2611.24924), submitted on November 18, adds requirement-driven development and simulated-user review. Its acceptance checks bind a reviewed change to requirements and tests; they do not statistically certify utility. Its reported executor-token reduction excludes user-simulation cost, and the paper identifies incomplete evolution-token coverage. Requirement satisfaction and economic improvement therefore need separate measurements.

## Offline search versus online adaptation

Offline search can inspect development labels and then deploy a frozen artifact. Online adaptation has only the feedback allowed during deployment. [Harness²](https://arxiv.org/abs/2610.14224) uses behavioral contrasts between candidate executions and a persistent experience library. Its setting must not be compared directly with a label-access baseline without accounting for feedback differences.

For an online stream, record the score **before** adapting to each task and the score after any permitted adaptation. Report both cumulative reward and the cost of adaptation. Evaluate order sensitivity and reset the experience library between independent seeds. Never describe a task as held out if its reward was used to revise the harness before its reported final score.

## Updating, utilizing, and benefiting are different quantities

Let $a$ denote enabling a candidate update and let $Y(a)$ be the task outcome. The quantity of interest is $\mathbb{E}[Y(1)-Y(0)]$ at fixed resource constraints. Update count, lines of code, retrieval frequency, and skill invocation are intermediate variables. They can help explain behavior but do not identify this effect.

[Harness Updating Is Not Harness Benefit](https://arxiv.org/abs/2605.30621) separates the ability to create a useful modification from the executor's ability to exploit it. This motivates an updater-by-executor evaluation matrix. An update created by a stronger model may be inappropriate for a weaker executor, and a correct skill can be too complex, too late, or too expensive to use. Post-treatment comparisons restricted to runs that invoked the skill introduce selection bias.

## Attribution and costs

[HDA](https://arxiv.org/abs/2610.22466) compares an evolved harness with a scaled baseline and a version with detected shortcuts removed. Its residual is an **upper bound on potential generalizable gain**, conditional on the intervention, not proof of generalization. [Rethinking Evaluation](https://arxiv.org/abs/2607.12227) shows that the relative value of harness evolution depends on feedback, baseline strength, and domain; its terminal-task findings and long-horizon game findings should be read together.

Track $C_{\mathrm{total}}=C_{\mathrm{proposal}}+C_{\mathrm{evaluation}}+C_{\mathrm{integration}}+C_{\mathrm{deployment}}$, including rejected edits. [RRSI](https://arxiv.org/abs/2609.24972) regularizes editing and prunes unnecessary modifications; [SoL-Pi](https://arxiv.org/abs/2609.20519) studies efficiency-oriented mechanisms. Saving inference tokens can be valuable even when score decreases slightly, but that is a measured tradeoff requiring a prespecified tolerance.

The next research step is a utility estimator that predicts when a concrete update helps a particular executor on a new task family, with calibrated uncertainty and an abstention option. The [utility-aware proposal](../research/harness-benefit.md) specifies the randomized data and transfer tests needed to evaluate it.
