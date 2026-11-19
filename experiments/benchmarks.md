# Benchmarks for evaluating self-improving agents

**Evidence cutoff and inspection date: 2026-11-19.** This catalog distinguishes a benchmark's current release from the historical protocol used in a paper. All quoted scores are author-reported; no benchmark run was performed. A higher score after repeated test-set feedback is not independent evidence of generalization.

## Choosing an evaluation target

| Benchmark | Main capability measured | Feedback / scoring | Best use in an RSI study | Key confound |
|---|---|---|---|---|
| SkillsBench | Applying procedural skill packages to specialized work | Deterministic artifact verifiers; matched with/without-skills conditions | Test whether acquired reusable skills transfer | Skill content, harness, and task snapshot can change together |
| ALFWorld | Sequential household planning with aligned text/embodied environments | Goal-state success | Memory and policy transfer across environments | Text-only success is not embodied success |
| WebShop | Grounded search, navigation, option selection | Product-matching reward and full success | Strategy/skill learning in an interactive fixed catalog | Partial reward and full success can move differently |
| Terminal-Bench | Long-horizon terminal tasks | Task-specific executable verifiers | Scaffold or tool-workflow optimization | Version, resource/time budget, and harness strongly matter |
| SWE-bench | Repairing repository issues | Patch evaluation against regression and issue tests | Held-out software-agent capability | Public solutions, test access, and build failures |
| ToolSandbox | Stateful conversational tool use | Trajectory milestones and forbidden-event minefields | Tool adaptation and state-aware memory | Simulator behavior and live-service dependencies |

These are complementary outcome measures. None alone measures an optimizer's ability to improve its next generation. For recursion, evaluate both the **new agent** and the **new agent's ability to produce a further improvement** on independently held-out development tasks.

## SkillsBench

**Purpose and environment.** Tasks pair procedural skills with verifiable outputs. The current repository uses native BenchFlow `task.md` packages, with separate environment, oracle, and verifier directories. Default `tasks/` require no external task credentials; credentialed integrations live in `tasks-extra/`. Agent-model APIs are a separate credential requirement. [Official repository](https://github.com/benchflow-ai/skillsbench)

**Version and protocol.** The inspected registry declares **skillsbench@1.1**, 87 tasks, tag `v1.1`, commit `b63b7b2850226b6aa4fb5929a8c1ac7bc4d9a6af`, BenchFlow `>=0.6.3,<0.7`, and per-task digests. It supersedes registry 1.0. This registry numbering is distinct from the original paper snapshot: paper v1 described 86 inventory tasks, with 84 in its main evaluated figure. Current paper v4 describes 87 tasks across eight domains and 18 model-harness configurations. [Registry](https://github.com/benchflow-ai/skillsbench/blob/main/registry.json), [v4 paper](https://arxiv.org/abs/2602.12670v4)

**Baselines and interpretation.** Match the model, harness, task roster, resources, and trials across no-skills and curated-skills runs. A self-generated-skills arm is useful but its generation tokens and feedback access must count toward budget. The v1.1 release reports **33.9%→50.5%, +16.6 percentage points** in its paper aggregate; these are not the v1 +16.2-point results. [Official release analysis](https://www.skillsbench.ai/blogs/skillsbench-1-1)

**Setup and compute.** Install the release-compatible BenchFlow version, validate tasks, run oracle solutions, then compare skill conditions. The current README demonstrates `bench tasks check tasks/offer-letter-generator` and `bench eval run --tasks-dir tasks/offer-letter-generator --agent oracle --sandbox docker`. Those commands illustrate one task, not a full benchmark result. Modal is the documented default cloud backend. Exact full-run cost: **Not verified**. Use each pinned task's declared limits; do not carry old no-GPU statements over to `tasks-extra/` GPU tasks. [Setup](https://github.com/benchflow-ai/skillsbench#quick-start)

**Limitations.** Human-curated skills can encode substantial expert labor; this differs from an agent acquiring skills by itself. Overlap between skills and held-out solutions can inflate apparent transfer. Curated task coverage and deterministic tests do not guarantee broad professional competence. Code license: Apache-2.0; inspect bundled assets separately.

## ALFWorld

**Purpose and environment.** ALFWorld aligns TextWorld commands with embodied ALFRED/AI2-THOR household tasks. Its six task families include putting objects away, examining them under light, cleaning, heating, cooling, and collecting two objects. The original paper lists **3,553 training, 140 seen-evaluation, and 134 unseen-evaluation tasks**. [Paper, Section 2 and Table 1](https://arxiv.org/pdf/2010.03768)

**Version and protocol.** Pin the package/repository commit, downloaded game files, configuration, environment type, goal-language mode, seed, action validity handling, and maximum steps. No current numeric release was verified here. The frequently cited 134-task unseen split is not the entire dataset. Keep seen and unseen results separate. Report goal success, per-family success, invalid actions, and steps; for embodied evaluation retain the navigation/perception configuration.

**Baselines.** The original BUTLER agent, its ablations, and a fixed prompting baseline provide different comparisons. For a self-improvement experiment, add a frozen agent with identical interaction budget and a memory/skill ablation. Improvements from new memories should be assessed in unseen environments with fresh episode state.

**Setup and compute.** Official setup uses Python 3.9+, `pip install alfworld`, and `alfworld-download`; extras provide visual/full dependencies. `alfworld-download --extra` adds checkpoints and sequence-to-sequence data. The README's historical tested machine is a GTX 1080 Ti, quad-core Xeon, and 16 GB RAM; this is **not a minimum for current text-only API-agent inference**. Docker instructions explicitly warn that they were tested on an older version. Current model-training cost: **Not verified**. [Repository setup and hardware](https://github.com/alfworld/alfworld)

**Limitations.** Abstract commands simplify perception and motor control. Reusing training demonstrations or test trajectories as agent memory changes the evaluation claim. Code is MIT; bundled components have their own licenses, including Fast Downward GPLv3. [License notes](https://github.com/alfworld/alfworld#license)

## WebShop

**Purpose and environment.** A simulated shopping website with a fixed catalog, free-form goals, search actions, product pages, and option selection. It has **1.18 million products and 12,087 instructions**. The original split is **10,587/1,000/500 train/development/test instructions**. Scoring includes a fractional matching reward and binary complete success. [Paper, Sections 3 and 5](https://arxiv.org/pdf/2207.01206)

**Version and protocol.** Pin code, product and attribute files, search index, instruction IDs, observation mode, action limits, and decoding settings. The official setup distinguishes the full catalog from a 1,000-product small download, and `html` from simplified observations. A small-catalog result cannot be presented as full WebShop. No current numbered release was verified.

**Baselines and results.** Original rule, imitation-learning (IL), RL, and IL+RL baselines are useful anchors. The paper reports **29.1% IL success**, while further RL raises mean score to **62.4** but lowers success to **28.7%**; expert-human success is **59.6%**. Thus partial-reward gains alone can conceal worse complete task fulfillment. [Section 5.2](https://arxiv.org/pdf/2207.01206)

**Setup and compute.** Official instructions specify Python 3.8.13, Java, data download, and search-index construction. Use the full-data option `-d all` when claiming the full benchmark and verify the configuration points at full product files. Browser mode additionally requires a compatible ChromeDriver; text-mode evaluation has different dependencies. Optional image features and human demonstrations are separately downloaded. Exact hardware minimum, full-run API cost, and currently working external download availability: **Not verified**. [README](https://github.com/princeton-nlp/WebShop)

**Limitations.** The benchmark is a simulator, not a live commerce reliability test. The i.i.d. instruction split permits catalog overlap, so category-held-out or temporally new catalogs are stronger transfer probes. Repository `LICENSE.md` is MIT; this does not establish blanket rights over all underlying product content. [License](https://github.com/princeton-nlp/WebShop/blob/master/LICENSE.md)

## Terminal-Bench

**Purpose and environment.** Containerized terminal work with task-specific environments and executable outcome checks. Useful for long-horizon editing, debugging, system work, and scientific workflows.

**Version and protocol.** As inspected, the official homepage and run guide identify **4.1**, with explicit dataset argument `terminal-bench/terminal-bench@4.1.0`. The task count and complete 4.1 resource roster were **Not verified** because the linked Hub task listing did not render its inventory. Do not copy the **89-task count from historical 2.0** into a 4.1 entry. [Official current run guide](https://www.tbench.ai/run), [2.0 paper](https://openreview.net/pdf/574281303882f822808ab57ac3a57a2bddfbc7a3.pdf)

**Baselines.** Specify the complete model-and-agent pair. Terminus 2 is a documented 2.0 reference; Claude Code, Codex, and other installed agents are distinct harnesses. Repeated trials, timeout/resource multipliers, network access, and reasoning settings must accompany resolution rate. Historical leaderboard scores are not cross-version comparisons.

**Setup and compute.** For a historical replication, the official 2.0 README supplies `harbor run --dataset terminal-bench@2.0 --agent oracle --n-concurrent 4`. The current 4.1 guide instead installs `harbor[modal]`, uses the fully qualified 4.1.0 dataset identifier, and documents GPU-enabled sandboxes. Its example uses five trials. These are materially different execution requirements. GPU type/count and total expense for a full current run: **Not verified**; inspect task manifests before budgeting. [2.0 repository](https://github.com/harbor-framework/terminal-bench-2), [current guide](https://www.tbench.ai/run)

**Limitations.** Passing tests can miss specification failures and does not prove general job completion. Public tasks invite contamination and repeated-optimizer overfitting. Keep evaluation tasks and solution scripts outside the improvement agent's accessible training material. Harbor and the verified 2.0 repository are Apache-2.0; the complete 4.1 dataset license was **Not verified** here. [Harbor](https://github.com/harbor-framework/harbor)

## SWE-bench

**Purpose and environment.** Resolve real repository issues from a specified base commit, then grade submitted patches in reconstructed environments. The official site distinguishes **Full 2,294**, **Lite 300**, and **Verified 500** instances, plus separate Multilingual and Multimodal sets. These are not interchangeable test sets. [Official benchmark definitions](https://www.swebench.com/)

**Version and protocol.** Choose a named dataset and immutable revision, then pin harness, task repo, container images, architecture, prediction format, and instance list. The current official README describes a v5 CLI, while retaining the old Python-module entry point. Count infrastructure failures separately and state the denominator and retry policy. Resolution requires the issue-relevant tests to pass without regressing the preserved tests; gold patches and hidden tests must not become agent training inputs.

**Baselines.** Original retrieval/SWE-Llama baselines answer a historical question; a fixed mini-SWE-agent model-harness pair is a more useful contemporary controlled baseline. Compare full trajectories and patches, not only aggregate success. An oracle gold-patch run checks that the environment can grade a known solution; it is not an agent baseline.

**Setup and compute.** Documented commands include `swebench eval verified --gold` and `swebench eval verified -p <predictions> --run-id <unique-run-id> -j <workers>`. The README recommends x86_64, **120 GB free disk, 16 GB RAM, eight CPU cores**, and restrained concurrency; ARM support is experimental. It warns that result caching keys on run and instance IDs, so changed patches require a new run ID. These requirements describe evaluation infrastructure, not model inference memory or total experiment cost. [Official README](https://github.com/SWE-bench/SWE-bench)

**Limitations.** Public issue/patch histories, incomplete tests, package drift, and test tampering can distort results. A self-improver tuned repeatedly on Verified needs another held-out suite for its final claim. Harness code is MIT; source repositories and datasets require their own license checks. [Verified data card](https://huggingface.co/datasets/SWE-bench/SWE-bench_Verified)

## ToolSandbox

**Purpose and environment.** Stateful Python tools mutate contacts, messages, reminders, and settings. A user simulator converses with the agent; trajectory milestones assess required events, and minefields invalidate prohibited actions. The paper v2 describes **1,032 scenarios, 34 tools, 11 domains**. State dependency, canonicalization, and insufficient information are explicit categories. [Paper, Sections 2–4](https://arxiv.org/html/2408.04682v2)

**Version and protocol.** Pin repository commit, scenario names, tool-augmentation setting, agent model, user-simulator model, prompt, turn limit, and external service configuration. No semantic benchmark release was verified. Report the paper's **average similarity score** as such; it is not automatically binary task success. Keep per-category results and minefield violations visible.

**Baselines.** The paper compares open and proprietary models with a shared minimal prompt. For self-improvement, retain that prompt as an anchor, then separately report scaffold, tool-description, and memory changes. Hold the simulator constant when comparing agents, and use alternate simulators or human review to test simulator-specific adaptation.

**Setup and compute.** Official setup uses Python 3.9 and `pip install '.[dev]'`; `tool_sandbox --user <user-type> --agent <agent-type> --scenario wifi_off` runs one scenario. Omitting the scenario selection runs all scenarios. Both agent and simulator may consume paid model calls; search scenarios require `RAPID_API_KEY`. Local model serving can use a compatible endpoint and adds model-dependent GPU demand. Current total token, service, and GPU expense: **Not verified**. [Official README](https://github.com/apple-aiml-research/ToolSandbox)

**Limitations.** Simulated users are not real users; live service outputs can change. The scenario family is intentionally constrained, and repeated evaluation can optimize to its milestone definitions. The repository uses a **custom Apple license**, with separately licensed subcomponents, not MIT or Apache-2.0. [Exact license](https://github.com/apple-aiml-research/ToolSandbox/blob/main/LICENSE)

## Minimum evidence to retain

For every study, publish immutable task IDs and versions; train/development/test boundaries; model and harness snapshots; reset policy; verifier access; repetitions and seeds; time, token, and utility-call budgets; successful and failed trajectories; infrastructure failures; and both aggregate and per-task changes. Report the **cost of discovering an improvement** separately from **the cost of using it**. Verify oracle behavior before expensive runs, but do not label oracle-only checks as benchmark replication.
