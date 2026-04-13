<div align="center">

# VIGIL: Part-Grounded Structured Reasoning for Generalizable Deepfake Detection

[Paper (PDF)]() &nbsp;|&nbsp; [Project Page]() &nbsp;|&nbsp; [OmniFake Dataset]() &nbsp;|&nbsp; [Model Weights]()

</div>

## Abstract

Multimodal large language models (MLLMs) offer a promising path toward interpretable deepfake detection by generating textual explanations. However, the reasoning process of current MLLM-based methods combines evidence generation and manipulation localization into a unified step. This combination blurs the boundary between faithful observations and hallucinated explanations, leading to unreliable conclusions.

Building on this, we present **VIGIL**, a part-centric structured forensic framework inspired by expert forensic practice through a *plan-then-examine* pipeline: the model first plans which facial parts warrant inspection based on global visual cues, then examines each part with independently sourced forensic evidence. A stage-gated injection mechanism delivers part-level forensic evidence only during examination, ensuring that part selection remains driven by the model's own perception rather than biased by external signals. We further propose a progressive three-stage training paradigm whose reinforcement learning stage employs part-aware rewards to enforce anatomical validity and evidence–conclusion coherence.

To enable rigorous generalizability evaluation, we construct **OmniFake**, a hierarchical 5-Level benchmark where the model, trained on only three foundational generators, is progressively tested up to in-the-wild social-media data. Extensive experiments demonstrate that VIGIL consistently outperforms both expert detectors and concurrent MLLM-based methods across all generalizability levels.

## Highlights

- **Part-Grounded Reasoning** — Forensic evidence is anchored to specific facial parts, decoupling claims from observations to eliminate hallucinated explanations.
- **Plan-then-Examine Pipeline** — The model autonomously selects which regions to inspect, then examines each with independently sourced frequency-domain and pixel-level forensic signals via stage-gated injection.
- **Reasoning Reversion** — Accumulated part-level evidence can overturn an initially incorrect global judgment, enabling self-correcting forensic analysis.
- **OmniFake Benchmark** — A hierarchical 5-Level benchmark with 200K+ images for fine-grained generalizability evaluation, from in-domain to in-the-wild social-media data.

## Method Overview

<div align="center">
<img src="assets/framework.png" width="95%">
</div>

VIGIL adopts a **plan-then-examine** pipeline inspired by expert forensic practice:

| Stage | Description |
|:---:|---|
| **Plan** | The model observes global visual cues and autonomously selects which facial parts to inspect — without exposure to any external forensic signal. |
| **Examine** | A stage-gated mechanism injects frequency-domain and pixel-level features as part-level evidence embeddings, providing each selected region with independently sourced forensic support. |
| **Synthesize** | Part-level findings are synthesized into a final verdict. Accumulated evidence can overturn an initially incorrect judgment (*reasoning reversion*). |

The progressive three-stage training paradigm consists of: (1) supervised fine-tuning, (2) hard-sample self-training via rejection sampling, and (3) reinforcement learning with part-aware & evidence-conclusion consistency rewards.

## OmniFake Benchmark

OmniFake is a hierarchical 5-Level benchmark containing over **200K images** designed for fine-grained generalizability evaluation. The model is trained on only three foundational generators and progressively tested across increasingly challenging levels.

| Level | Name | Description |
|:---:|:---:|---|
| L1 | In-Domain | Same generators as training |
| L2 | Cross-Generator | Different architectures, same paradigm |
| L3 | Cross-Paradigm | Unseen generation paradigms |
| L4 | Cross-Task | Localized manipulation & editing |
| L5 | In-the-Wild | Social media, unknown methods |

<div align="center">
<img src="assets/omnifake.png" width="95%">
</div>

## Main Results

VIGIL consistently outperforms both expert detectors and concurrent MLLM-based methods across all OmniFake levels (Accuracy %):

| Method | L1 | L2 | L3 | L4 | L5 | Avg. |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| AIDE (ICLR'25) | 72.3 | 89.1 | 81.6 | 67.6 | 75.0 | 78.9 |
| Co-SPY (CVPR'25) | 83.5 | 89.9 | 89.0 | 71.3 | 82.5 | 84.7 |
| DDA (NeurIPS'25) | 97.8 | 94.6 | 91.9 | 81.0 | 80.7 | 88.8 |
| GPT-5.2 | 65.8 | 82.7 | 73.6 | 58.8 | 69.0 | 71.4 |
| Gemini-3-Pro | 72.3 | 85.9 | 78.5 | 61.0 | 69.9 | 75.0 |
| FakeVLM (NeurIPS'25) | 83.5 | 81.0 | 76.8 | 74.5 | 74.9 | 77.1 |
| Veritas (ICLR'26) | 96.8 | 94.9 | 89.9 | 79.0 | 81.1 | 87.6 |
| **VIGIL (Ours)** | **98.6** | **96.7** | **95.5** | **89.5** | **86.0** | **93.1** |

## Code & Data

> We are currently organizing the code and data. Stay tuned!

| Resource | Status |
|---|---|
| Training & Inference Code | Coming Soon |
| Model Weights | Coming Soon |
| OmniFake Dataset | Coming Soon |
| Demo | Coming Soon |

## Citation

If you find our work useful, please consider citing:

```bibtex
@article{vigil2026,
  title={VIGIL: Part-Grounded Structured Reasoning for Generalizable Deepfake Detection},
  author={Li, Xinghan and Xu, Junhao and Chen, Jingjing},
  year={2026}
}
```

## License

This project is released under the [Apache 2.0 License](LICENSE).
