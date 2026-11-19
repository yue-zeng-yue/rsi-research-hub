# DeepSeekMath and GRPO

Evidence cutoff: **2026-11-19**. Results are author-reported, not reproduced. Classification: model-weight adaptation with externally defined tasks and rewards; a bridge to self-generated trajectory learning.

## 1. Full Paper Title

*DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models*.

## 2. Authors and Affiliations

Zhihong Shao, Peiyi Wang, Qihao Zhu, Runxin Xu, Junxiao Song, Xiao Bi, Haowei Zhang, Mingchuan Zhang, Y.K. Li, Y. Wu, Daya Guo. All list DeepSeek-AI; Shao additionally lists Tsinghua University, and Wang and Zhu Peking University. The university-affiliated authors performed the work as DeepSeek interns. [Title page](https://arxiv.org/html/2402.03300v3)

## 3. Publication Date

First submission **2024-02-05**; inspected version **v3, 2024-04-27**.

## 4. Venue or Preprint Status

arXiv technical report; peer-reviewed venue acceptance **Not verified** from the inspected primary record. [Record](https://arxiv.org/abs/2402.03300)

## 5. Paper URL / DOI

[Full text v3](https://arxiv.org/html/2402.03300v3); [DOI](https://doi.org/10.48550/arXiv.2402.03300).

## 6. Official GitHub Repository

[deepseek-ai/DeepSeek-Math](https://github.com/deepseek-ai/DeepSeek-Math), explicitly linked by the paper. It releases Base, Instruct, and RL checkpoints and inference examples. **Code is MIT; model weights use the separate DeepSeek Model License**. A permissive code license must not be substituted for the weight terms. Repository accessible/unarchived; observed last push 2024-04-15. [Repository and licenses](https://github.com/deepseek-ai/DeepSeek-Math#6-license)

## 7. Research Problem

Improve open-model mathematical reasoning through data selection, supervised tuning, and a less memory-demanding policy optimization method.

## 8. Methodology and Algorithm

GRPO samples a response group per question and uses `A_i = (r_i - mean(r))/std(r)` instead of a learned critic. It combines clipped policy-ratio updates with a reference-policy KL term. The paper distinguishes outcome, process, and iterative reward-model supervision.

## 9. Key Contributions

A math-data pipeline and 7B model family accompany GRPO. Removing the critic changes training infrastructure; it does not remove the need for reliable rewards.

## 10. Experimental Setup

RL starts from DeepSeekMath-Instruct 7B, with roughly 144K GSM8K/MATH-related questions, 64 samples per question, maximum length 1,024, and KL coefficient 0.04.

## 11. Benchmarks and Baselines

Compare Base, Instruct, and RL; English/Chinese math evaluations include GSM8K, MATH, and CMATH. Tool-assisted and chain-of-thought protocols are separate.

## 12. Quantitative Results

Instruct-to-RL chain-of-thought accuracy improves **82.9→88.2% GSM8K**, **46.8→51.7% MATH**, and **84.6→88.8% CMATH**. **60.9% MATH** uses 64-sample self-consistency and is not the single-response score. [Sections 3–4 and Table 5](https://arxiv.org/html/2402.03300v3)

## 13. Limitations

The model/data/reward pipeline is broader than an isolated optimizer experiment. [Sections 5–6](https://arxiv.org/html/2402.03300v3) Research implication: do not attribute the entire Base-to-RL gain to GRPO, or infer equivalent reward quality across domains. Group normalization also needs explicit handling when all sampled rewards are identical; an implementation choice here changes practical behavior.

## 14. Reproducibility

Official inference and checkpoint availability is stronger evidence than a promise of complete training reproducibility. The inspected README does not provide the complete pretraining corpus and end-to-end training recipe; their availability is **Not verified**. Independent TRL/verl implementations should be identified as subsequent implementations, with their loss normalization, clipping, reward scaling, and rollout reuse documented. Current GPU-hours and full reproduction dollar cost: **Not verified**. No training was run. A fair study should account for rollout generation, reference/reward models, optimizer state, and total tokens, rather than reporting only the removed critic's memory.

## 15. Open Research Questions

Proposed studies: At fixed rollout budget, when do richer textual feedback and GRPO complement each other? Does self-generated task selection improve held-out reasoning rather than exploit a reward shortcut? Which part of the gain survives equal data and compute comparisons with rejection-sampling fine-tuning or PPO? Evaluate mathematical validity independently of the training reward and report uncertainty over training seeds.
