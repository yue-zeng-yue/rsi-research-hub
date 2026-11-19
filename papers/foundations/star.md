# STaR: answer-supervised rationale bootstrapping

Evidence cutoff: **2026-11-19**. Results are author-reported and were not reproduced. Classification: iterative synthetic-rationale training, not autonomous objective invention.

## 1. Full Paper Title

*STaR: Bootstrapping Reasoning With Reasoning*. The proceedings PDF also displays “STaR: Self-Taught Reasoner.”

## 2. Authors and Affiliations

Eric Zelikman, Yuhuai Wu, Jesse Mu, Noah D. Goodman. Stanford University Department of Computer Science; Wu additionally lists Google Research. Zelikman and Wu contributed equally. [Proceedings paper](https://proceedings.neurips.cc/paper_files/paper/2022/file/639a9a172c044fbb64175b5fad42e9a5-Paper-Conference.pdf)

## 3. Publication Date

First arXiv submission: **2022-03-28**. This note uses the NeurIPS 2022 proceedings version.

## 4. Venue or Preprint Status

**NeurIPS 2022**, main conference, volume 35. [Official proceedings record](https://proceedings.neurips.cc/paper_files/paper/2022/hash/639a9a172c044fbb64175b5fad42e9a5-Abstract-Conference.html)

## 5. Paper URL / DOI

[arXiv record](https://arxiv.org/abs/2203.14465); [DOI](https://doi.org/10.48550/arXiv.2203.14465); [proceedings full text](https://proceedings.neurips.cc/paper_files/paper/2022/file/639a9a172c044fbb64175b5fad42e9a5-Paper-Conference.pdf).

## 6. Official GitHub Repository

[ezelikman/STaR](https://github.com/ezelikman/STaR), linked in the paper. It builds on mesh-transformer-jax and masked-training work, with `iteration_train.py` as its entry point. GitHub reports Apache-2.0; README separately identifies Apache-2.0 for GPT-J weights. The repository was unarchived, with observed last push 2023-02-21. [README](https://github.com/ezelikman/STaR)

## 7. Research Problem

How can a few rationale demonstrations produce useful reasoning supervision for many labeled questions?

## 8. Methodology and Algorithm

Generate rationale/answer pairs; retain correct answers. For failures, condition on the gold answer and generate a rationale, then remove the hint from training input. Each iteration fine-tunes the original pretrained model on the refreshed accepted dataset. The objective is likelihood of accepted `(rationale, answer)` sequences; correctness is an external filter.

## 9. Key Contributions

Rationalization supplies training examples for questions the model cannot yet answer unaided. The loop connects generated explanations with ordinary supervised fine-tuning.

## 10. Experimental Setup

GPT-J 6B; synthetic addition, CommonsenseQA, GSM8K. CommonsenseQA uses 9,741 training questions and ten seed rationale examples. Reported training increases inner-loop steps across iterations.

## 11. Benchmarks and Baselines

Direct-answer fine-tuning, few-shot prompting, and STaR without rationalization; a larger GPT-3 result provides contextual comparison.

## 12. Quantitative Results

CommonsenseQA accuracy: **72.5%** with rationalization, **68.8%** without, **60.0%** direct fine-tuning; the cited GPT-3 comparison is **73.0%**. This is a specific benchmark comparison, not a controlled model-size scaling law. [Sections 3–5, Table 1](https://proceedings.neurips.cc/paper_files/paper/2022/file/639a9a172c044fbb64175b5fad42e9a5-Paper-Conference.pdf)

## 13. Limitations

Gold answers remain necessary; correct final answers do not guarantee faithful rationales. [Discussion](https://proceedings.neurips.cc/paper_files/paper/2022/file/639a9a172c044fbb64175b5fad42e9a5-Paper-Conference.pdf) Research implication: distinguish answer contamination, accidental multiple-choice correctness, and useful explanation learning. A model can improve benchmark accuracy without producing dependable accounts of its decision process.

## 14. Reproducibility

The official implementation is TPU-oriented legacy JAX code, and its README warns of specific JAX requirements. Reproducing it requires the checkpoint, tokenizer, prompt templates, label parser, generation settings, accepted-example logs, and reset-from-base training behavior. A modern PyTorch port is a replication variant, not automatically the original experiment. Exact end-to-end current compute cost and modern dependency compatibility: **Not verified**. No training was launched. Keep hint-bearing generation inputs separate from hint-free final evaluation to prevent accidental leakage.

## 15. Open Research Questions

Proposed studies: Can verifier-grounded rationales outperform answer-only acceptance at equal generation cost? Does rationalization introduce spurious explanations that harm transfer? What happens when answer checking is noisy or labels are scarce? Compare resetting from the base checkpoint with continued training under matched optimizer steps, and evaluate on unseen problem structures rather than only new examples from the same dataset.
