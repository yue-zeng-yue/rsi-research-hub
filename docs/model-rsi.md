# Model RSI: Training the Policy and the Training Process

## Self-training and synthetic supervision

Self-training alternates generating examples, scoring or filtering them, and updating model weights. [STaR](https://arxiv.org/abs/2203.14465) is an early language-model example: generate rationales, retain successful reasoning, and use answer-conditioned rationalization when initial reasoning fails. A successful trajectory is evidence of an output satisfying a verifier, not evidence that every intermediate explanation is faithful.

For weighted synthetic examples $(x,y,w)$, supervised training minimizes

$$
L_{\mathrm{SFT}}(\theta)=-\mathbb{E}_{(x,y,w)\sim\mathcal{B}}\left[w\sum_t\log\pi_\theta(y_t\mid x,y_{<t},h)\right].
$$

The harness $h$ is part of the data-generating process. Store its exact version with every example. Filtering on success can reduce diversity, erase difficult cases, and favor outputs exploiting a verifier. Preserve the denominator of generated candidates and account for failures, filtering, and teacher calls.

## RL and GRPO

[DeepSeekMath](https://arxiv.org/abs/2402.03300) introduces group-relative policy optimization. For a group of $G$ sampled responses to a prompt, a common outcome-reward implementation forms

$$
\widehat A_i=\frac{r_i-\overline r}{\operatorname{std}(r_1,\ldots,r_G)+\epsilon},\qquad
\rho_{i,t}(\theta)=\frac{\pi_\theta(o_{i,t}\mid x,o_{i,<t},h)}{\pi_{\theta_{\mathrm{old}}}(o_{i,t}\mid x,o_{i,<t},h)}.
$$

One representative clipped objective is

$$
\max_\theta\;\mathbb{E}\left[\frac1G\sum_i\frac1{|o_i|}\sum_t
\min\{\rho_{i,t}\widehat A_i,\operatorname{clip}(\rho_{i,t},1-\delta,1+\delta)\widehat A_i\}
-\beta D_{\mathrm{KL}}(\pi_\theta\Vert\pi_{\mathrm{ref}})\right].
$$

This is an explanatory form, not a claim that every cited implementation uses identical normalization, KL estimator, length weighting, or clipping. In tool-using environments, specify which assistant tokens contribute to the loss; environment responses are observations. The rollout order is generate, execute, score, estimate advantages, update. Same-reward groups supply no relative outcome signal. Adaptive rollout allocation changes the sampling distribution and must be documented.

## Why model updates can damage an evolved harness

Successful expert trajectories may use planning strategies a smaller student cannot execute. [Co-Evolving Harnesses and Models](https://arxiv.org/abs/2609.09134) compares complete expert imitation with local corrections on the student's own trajectories. Its Table 1 reports mean success under an evolved harness falling from 78.0% to 63.1% after imitation and reaching 79.7% with local correction across seven enterprise tasks. These are author-reported results in a specific LoRA setup, not a theorem that imitation is generally harmful.

For RL under an evolving harness, changing tools or observations changes the effective policy and trajectory distribution. A likelihood ratio over model tokens alone does not automatically correct for a changed harness transition mechanism. Freeze the harness within a training epoch, retain its version in the rollout ledger, and define how stale trajectories are discarded or reweighted. [HarnessForge](https://arxiv.org/abs/2606.01779), [HarnessAdapt-RL](https://arxiv.org/abs/2610.28069), and [JoMoHa](https://arxiv.org/abs/2611.11499) are relevant co-optimization baselines.

## Automated post-training versus algorithm improvement

Automation may select a data mixture, verifier, training schedule, adapter rank, or checkpoint. That is useful engineering even if the optimizer remains fixed. To claim improvement of the training algorithm, compare learned or revised update procedures from identical base checkpoints, data access, and total GPU/API budgets. Include the cost of discovering the procedure. A later checkpoint trained longer is not a controlled test of a better optimizer.

The November 2026 [teacher-free co-evolution study](https://arxiv.org/abs/2611.15268) alternates rule edits and multi-turn GRPO, with separate gates and a factorial ablation. Its editor remains the base model, so the study should not be cited as evidence that the editor recursively becomes better. It also distinguishes reliable execution from knowledge stored in external skills.

## Experimental priorities

The [November 25 update](updates/2026-11-25.md) distinguishes three additional cases: [AutoMaster](../papers/2026/automaster.md) improves demonstrations while restarting students, [SelfWrite](../papers/2026/selfwrite.md) lets merged weights author subsequent edits, and [TT-RSI](../papers/2026/tt-rsi.md) adapts on unlabeled target questions using refinement-derived supervision. Compare their feedback access and retained state explicitly. In particular, transductive adaptation is not an untouched-task audit, and gradient-free edits are not cost-free updates.

Compare model-only, harness-only, alternating, and joint updates using a common starting system. Measure held-out success, reliability across repeated runs, regressions by task family, policy drift, tool-format errors, and resource use. Use external correctness checks where possible, evaluate calibration of model judges, and reserve final tests from training and checkpoint selection. Log pretrained model identity, adapter configuration, precision, optimizer settings, model and harness hashes, data lineage, and serving configuration.

No model training was run during repository initialization. Mathematical objectives here are research specifications; implementation and independent results belong in versioned experiment reports.
