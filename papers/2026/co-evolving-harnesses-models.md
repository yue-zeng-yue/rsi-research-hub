# Co-Evolving Harnesses and Models

Evidence cutoff: 2026-11-19. Results below are author-reported, not independently reproduced.

## 1. Full Paper Title

Co-Evolving Harnesses and Models: On-Policy Correction Helps Weaker Models Catch Up Where Imitation Fails.

## 2. Authors and Affiliations

Zhou Yu, Bin Bi, Shiva Kumar Pentyala, Shubham Mehrotra, Sougata Chaudhuri, Shilpa Bhagavath, Zeyuan Chen, Ran Xu, Phil Mui, James Zhu, and Sitaram Asur; all Salesforce AI, as listed in the [v1 title block](https://arxiv.org/html/2609.09134v1).

## 3. Publication Date

First submission: 2026-09-08; this review covers v1. [Submission history](https://arxiv.org/abs/2609.09134).

## 4. Venue or Preprint Status

arXiv preprint. Peer-reviewed acceptance: Not verified.

## 5. Paper URL / DOI

[Full paper](https://arxiv.org/html/2609.09134v1); [DOI](https://doi.org/10.48550/arXiv.2609.09134).

## 6. Official GitHub Repository

Not verified. The inspected primary paper does not identify an official implementation repository.

## 7. Research Problem

Does improving an agent's harness compose with improving its weights? A harness optimized around a weak executor may become incompatible with the planning style learned through stronger-model imitation. The paper studies that interference rather than assuming the two improvements add together.

## 8. Methodology and Algorithm

First, a Gemini meta-agent evolves prompts, tools, hooks, context management, and subagent configuration using execution failures and validation feedback. The weaker executor remains fixed during this phase. Next, ordinary supervised imitation trains on complete expert trajectories under that evolved harness.

The proposed alternative keeps the student's own rollout and replaces only a localized failing turn. A meta-level MLE agent diagnoses the failure; the expert proposes corrections, with quality selection among three candidates. Supervised learning on these corrected trajectories aims to preserve the student's broader planning distribution while repairing the specific mistake. This is localized expert supervision, not teacher-free learning or a proof of monotonic improvement. [Sections 3.1–3.4](https://arxiv.org/html/2609.09134v1).

## 9. Key Contributions

The main contribution is a negative result: better expert execution does not imply useful full-trajectory distillation after harness evolution. The correction pipeline provides a concrete compatibility-preserving alternative. Failure categorization and examples support the proposed model–harness mismatch explanation, although they do not establish a uniquely causal mechanism.

## 10. Experimental Setup

Executors include Qwen3-Coder-30B-A3B-Instruct and Gemma-4-26B-A4B-IT; Gemini-3.1-Pro-Preview supplies expert/meta-agent capability. Correction training uses approximately 500 rows, mostly repaired student failures plus successful student trajectories. LoRA uses ranks 16 or 64, two epochs, learning rate 1e-4, effective batch size eight, and long contexts. The appendix reports the better rank setting; H100/H200 hardware and H200 serving are involved. [Appendix B](https://arxiv.org/html/2609.09134v1).

## 11. Benchmarks and Baselines

Seven enterprise tasks cover payroll, budgets, stocks, IoT anomalies, browser automation, website management, and code refactoring. Comparisons include base/evolved harnesses, stronger-expert execution, complete expert-trajectory imitation, and student-trajectory correction. Restrictions requiring designated MCP tools and revised error visibility mean these results should not be treated as directly interchangeable with the earlier suite's scores.

## 12. Quantitative Results

Table 1 reports Qwen mean success over three runs: 29.2% with the base harness, 78.0% with the evolved harness, 63.1% after complete expert imitation, and 79.7% after correction. Expert execution reaches 93.6% under the evolved harness. Imitation declines on all seven tasks. Correction improves five task means, but payroll falls 81.7→81.3 and budgets 87.6→87.0; the small decreases prevent a literal taskwise no-regression claim. [Table 1](https://arxiv.org/html/2609.09134v1).

## 13. Limitations

Seven specialized domains, expert dependence, rank selection, and limited runs constrain generalization. LLM-based failure analysis is interpretive evidence. The study does not establish sustained improvement across many alternating generations or improved capability of the optimizer itself.

## 14. Reproducibility

Read sections 3.1–3.4, Table 1, and appendices B–D. Training settings and examples are documented, but official runnable artifacts remain Not verified. Full reproduction needs task environments, evolved harnesses, correction data, model/API snapshots, seeds, and selection rules. No experiments were run for this review.

## 15. Open Research Questions

Can compatibility be measured before fine-tuning? Would matched-budget student-only reinforcement learning recover the same gains? Do local corrections retain their advantage through repeated harness/weight updates and on genuinely new task families?
