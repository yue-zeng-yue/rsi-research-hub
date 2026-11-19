# Open-source projects and research artifacts

Verified **2026-11-19** from official repositories and paper links. “Official” means the paper or its official project explicitly identifies the repository. “Available” means the repository was accessible; it does not mean its complete experiment ran successfully. Last-push dates are observed GitHub metadata, not claims of ongoing support.

## Paper artifacts

| Project | Relation to the research | What is actually available | License and observed status | Main reproduction caveat |
|---|---|---|---|---|
| [microsoft/stop](https://github.com/microsoft/stop) | Official STOP artifact | Code/data for scaffold self-optimization | MIT code; CC BY 4.0 docs/data; unarchived; last push 2024-01-01 | Repository predates paper v3; historical model endpoint availability **Not verified** |
| [ezelikman/STaR](https://github.com/ezelikman/STaR) | Official STaR implementation | Iterative training wrapper over mesh-transformer-jax; GPT-J-oriented tooling | Apache-2.0 repository; unarchived; last push 2023-02-21 | Legacy JAX/TPU dependencies; a current port needs independent validation |
| [deepseek-ai/DeepSeek-Math](https://github.com/deepseek-ai/DeepSeek-Math) | Official model project | Base/Instruct/RL checkpoints and inference examples | MIT code; separate Model License; unarchived; last push 2024-04-15 | Checkpoint access does not establish release of full corpus or complete RL training pipeline |
| [gepa-ai/gepa](https://github.com/gepa-ai/gepa) | Official GEPA library | Optimizer, interfaces, examples, integrations | MIT; unarchived; last push 2026-11-09 | Library evolution can differ from the paper implementation |
| [gepa-ai/gepa-artifact](https://github.com/gepa-ai/gepa-artifact) | Official GEPA reproduction artifact, linked by the library | Configurations, experiment logs via Git LFS, figure notebooks, modified dependency setup | MIT; unarchived; last push 2026-02-08 | Uses modified DSPy/Arbor forks and distinct GRPO configuration; verify correspondence to paper v2 |
| Gödel Machines | Foundational theoretical paper | [Formal specification and proofs](https://arxiv.org/pdf/cs/0309048v5) | Official implementation and implementation license **Not verified** | Name similarity is not proof that another repository realizes the original machine |

## Benchmark and infrastructure projects

| Repository | Verified role | License | Observed state / caution |
|---|---|---|---|
| [benchflow-ai/skillsbench](https://github.com/benchflow-ai/skillsbench) | Skills tasks, oracle solutions, verifiers, and release registry | Apache-2.0 | Unarchived; last push 2026-11-16; current task packaging differs from paper v1 |
| [alfworld/alfworld](https://github.com/alfworld/alfworld) | Text/embodied interactive environment | MIT main project; separate dependency licenses | Unarchived; last push 2026-02-08; historical Docker/hardware notes are not current minimum requirements |
| [princeton-nlp/WebShop](https://github.com/princeton-nlp/WebShop) | Shopping simulator, baseline models, data setup | MIT repository | Unarchived; last push 2024-09-06; catalog downloads and search-index setup are additional dependencies |
| [harbor-framework/terminal-bench-2](https://github.com/harbor-framework/terminal-bench-2) | Historical Terminal-Bench 2.0 tasks | Apache-2.0 | Unarchived; last push 2026-04-30; not the current 4.1 task set |
| [harbor-framework/harbor](https://github.com/harbor-framework/harbor) | Task execution and evaluation infrastructure | Apache-2.0 | Unarchived; last push 2026-11-19; task version and sandbox backend are separate pins |
| [SWE-bench/SWE-bench](https://github.com/SWE-bench/SWE-bench) | Repository-repair evaluation harness | MIT | Unarchived; last push 2026-09-18; current README documents v5 CLI |
| [apple-aiml-research/ToolSandbox](https://github.com/apple-aiml-research/ToolSandbox) | Stateful conversational tool-use scenarios | Custom Apple license; separately licensed subcomponents | Unarchived; last push 2026-09-11; historical `apple/ToolSandbox` URL redirects here |
| [stanfordnlp/dspy](https://github.com/stanfordnlp/dspy) | Modular LM programming and optimization | MIT | Unarchived; last push 2026-11-18 |
| [verl-project/verl](https://github.com/verl-project/verl) | Distributed post-training framework | Apache-2.0 | Unarchived; last push 2026-11-19; historical `volcengine/verl` URL redirects here |
| [huggingface/trl](https://github.com/huggingface/trl) | SFT, preference and RL training library | Apache-2.0 | Unarchived; last push 2026-11-19 |
| [SWE-agent/mini-swe-agent](https://github.com/SWE-agent/mini-swe-agent) | Minimal software-agent baseline | MIT | Unarchived; last push 2026-11-16; current README is v2 |

## How to use this list

For replication, start from the paper-specific artifact and its exact configurations. For a new research system, a maintained library can be preferable, but state that it is a new implementation. Preserve a readable source snapshot, dependency lockfile, generated candidates, and evaluation receipts. Distinguish four statuses in reports: source inspected, environment smoke-tested, partial experiment reproduced, and full claimed result reproduced. This catalog establishes **source inspected** only.

A repository-level license is not a blanket license for downloaded model checkpoints, browser data, task fixtures, or third-party packages. No license conclusion is made where the relevant artifact terms were not verified. No executable project or paper here was automatically judged correct from stars, recent activity, or the presence of a README.
