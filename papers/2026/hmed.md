# Learning from Revision Consequences: Hindsight Meta-Experience Distillation for Self-Improving Agents

Reviewed against primary sources on 2026-11-19. Quantitative findings below are author-reported, not independently reproduced.

## Full Paper Title

Learning from Revision Consequences: Hindsight Meta-Experience Distillation for Self-Improving Agents

## Authors and Affiliations

Qianhan Feng; Zhongzhen Huang; Yakun Zhu; Xiaofan Zhang; Qi Dou

Verified from PDF page 1: Qianhan Feng and Qi Dou: The Chinese University of Hong Kong. Zhongzhen Huang and Xiaofan Zhang: Shanghai Jiao Tong University. Yakun Zhu: Shanghai Jiao Tong University and Shanghai Innovation Institute.

## Publication Date

2026-10-06; reviewed v1.

## Venue or Preprint Status

arXiv preprint; no conference acceptance independently verified.

## Paper URL / DOI

[arXiv](https://arxiv.org/abs/2610.07979) · [Full text](https://arxiv.org/html/2610.07979v1) · [arXiv DOI](https://doi.org/10.48550/arXiv.2610.07979).

## Official GitHub Repository

Not verified: no author-linked repository was found in the primary full text or exact-title code search.

## Research Problem

A successful search branch can reflect a favorable starting skill library rather than an improved search procedure. HMED targets credit assignment for revisions to Meta-Skills—the textual instructions governing skill discovery—rather than treating final branch scores as direct evidence that an improver became better.

## Methodology and Algorithm

A revision is bound to a completed discovery event. Restore its initial library, history, and task context; run incumbent and revised Meta-Skills from that same state and a supplementary coverage state. Compute Δ as the average difference in best-so-far utility gains. Adopt the revision only if Δ>0 and both continuations complete normally, the new text is delivered throughout its arm, and the text actually changed. Distill the event, edit, process changes, and outcome changes into a reusable Meta-Experience record. Rejected revisions also provide future learning signals.

## Key Contributions

The contribution is revision-centered evidence, with a controlled distinction between using paired replay merely to select a candidate and feeding its consequences into future proposals. Meta-Skill editing remains inside a preserved discovery framework; HMED does not freely rewrite all orchestration code.

## Experimental Setup

Qwen3-32B and DeepSeek-v4-Flash are evaluated with reasoning modes disabled and identical inference configurations. Skill evolution accesses training tasks; resulting skills and Meta-Skills freeze before test evaluation. Unless otherwise specified, means use three independent runs. A separate reuse experiment freezes the learned Meta-Skill and resets the Task-Skill library.

## Benchmarks and Baselines

ALFWorld and ScienceWorld report environment success rates; BiomniBench-DA reports a DeepSeek-v4-Flash judge score out of 100. Baselines include No Skill, Static Skill, SkillEvolver, and MetaSkill-Evolve. Ablations remove consequence feedback, process detail, or hindsight grounding while preserving matched comparison.

## Quantitative Results

Table 1: Qwen HMED scores 54.11/22.56/20.78, versus MetaSkill-Evolve 51.49/20.84/17.80 across the three benchmarks. DeepSeek HMED scores 80.60/32.47/43.19. Table 2 gives ALFWorld 54.11 versus 49.25 for comparison-only. Table 4’s fresh-origin reuse gains over MetaSkill-Evolve are 1.16 and 0.55 points; discovery and final evaluation use disjoint halves of held-out tasks.

## Limitations

Restored starts reduce one confound but do not eliminate stochastic variation or establish population-level causal effects from a few continuations. Replay itself adds cost; an all-in compute advantage is not demonstrated. Biomedical scoring shares the DeepSeek model family with one tested agent, and the transfer margins are modest. No separate comprehensive limitations section was located.

## Reproducibility

Full methods, main tables, and detailed accepted/rejected-record examples were inspected. Independent reruns were not performed. Exact state restoration, coverage-state selection, matching budgets, and record delivery must be reproduced; storing a record alone is insufficient evidence it influenced later decisions.

## Open Research Questions

Can confidence-aware paired replay reduce false acceptance at lower cost? How well do Meta-Experience records transfer when the underlying discovery framework or model changes, and when should old negative evidence expire?

Primary reading: Sections 3–5; Tables 1–4; Appendix A comparison-record case studies.
