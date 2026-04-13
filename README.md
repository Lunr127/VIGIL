<div align="center">

# VIGIL: Part-Grounded Structured Reasoning for Generalizable Deepfake Detection

📄 [Paper](https://arxiv.org/abs/2603.21526) &nbsp;|&nbsp; 🌐 [Project Page](https://vigil.best/) &nbsp;|&nbsp; 💾 [OmniFake Dataset]() &nbsp;|&nbsp; 🤗 [Model Weights]()

</div>

## Overview

**VIGIL** is a part-centric structured forensic framework for interpretable and generalizable deepfake detection. Current MLLM-based detectors combine evidence generation and manipulation localization in a single step, blurring faithful observations and hallucinated explanations. VIGIL decouples them through a **plan-then-examine** pipeline: the model first plans which facial parts to inspect based on global visual cues, then examines each part with independently sourced forensic evidence via **stage-gated injection**. A progressive three-stage training paradigm (SFT → hard-sample self-training → RL with part-aware rewards) ensures genuine evidence reasoning rather than template memorization.

We also introduce **OmniFake**, a hierarchical 5-Level benchmark (200K+ images) for fine-grained generalizability evaluation, where the model is trained on only three foundational generators and progressively tested up to in-the-wild social-media data.

### Highlights

- **Part-Grounded Reasoning** — Every forensic claim is anchored to a specific facial part, decoupling claims from evidence to eliminate hallucination.
- **Stage-Gated Injection** — Part-level forensic signals (frequency-domain + pixel-level) are delivered only during examination, preserving autonomous planning.
- **Reasoning Reversion** — Accumulated part-level evidence can overturn an initially incorrect global judgment.
- **OmniFake Benchmark** — 5-Level hierarchical evaluation from in-domain to in-the-wild social-media data.

## Method

<div align="center">
<img src="assets/framework.png" width="95%">
</div>

| Stage | Description |
|:---:|---|
| **Plan** | Observe global visual cues and select which facial parts to inspect — without exposure to external forensic signals. |
| **Examine** | Inject frequency-domain and pixel-level evidence into each selected part via stage-gated mechanism. |
| **Synthesize** | Aggregate part-level findings into a final verdict, with the ability to overturn initial judgments. |

**Training**: (1) SFT on signal-semantic annotations, (2) hard-sample self-training via rejection sampling, (3) RL with part-aware & evidence-conclusion consistency rewards (GRPO).

## OmniFake Benchmark

| Level | Name | Description |
|:---:|:---:|---|
| L1 | In-Distribution | Same generators as training |
| L2 | Cross-Architecture | Unseen models within related paradigm families |
| L3 | Cross-Model | Entirely unseen generation principles (flow matching, autoregressive, commercial generators, etc.) |
| L4 | Cross-Task | Localized manipulation (inpainting, face restoration) |
| L5 | In-the-Wild | Social media, unknown methods & real-world degradations |

<div align="center">
<img src="assets/omnifake.png" width="95%">
</div>

## Main Results

Accuracy (%) on OmniFake. **Bold** = best, <ins>underline</ins> = second best.

<table>
<thead>
<tr>
  <th align="left" width="220">Method</th>
  <th align="center" width="90">L1</th>
  <th align="center" width="90">L2</th>
  <th align="center" width="90">L3</th>
  <th align="center" width="90">L4</th>
  <th align="center" width="90">L5</th>
  <th align="center" width="90">Avg.</th>
</tr>
</thead>
<tbody>
<tr>
  <td>AIDE <sub>ICLR'25</sub></td>
  <td align="center">72.3</td>
  <td align="center">89.1</td>
  <td align="center">81.6</td>
  <td align="center">67.6</td>
  <td align="center">75.0</td>
  <td align="center">78.9</td>
</tr>
<tr>
  <td>Co-SPY <sub>CVPR'25</sub></td>
  <td align="center">83.5</td>
  <td align="center">89.9</td>
  <td align="center">89.0</td>
  <td align="center">71.3</td>
  <td align="center"><ins>82.5</ins></td>
  <td align="center">84.7</td>
</tr>
<tr>
  <td>DDA <sub>NeurIPS'25</sub></td>
  <td align="center"><ins>97.8</ins></td>
  <td align="center"><ins>94.6</ins></td>
  <td align="center"><ins>91.9</ins></td>
  <td align="center"><ins>81.0</ins></td>
  <td align="center">80.7</td>
  <td align="center"><ins>88.8</ins></td>
</tr>
<tr>
  <td>GPT-5.2</td>
  <td align="center">65.8</td>
  <td align="center">82.7</td>
  <td align="center">73.6</td>
  <td align="center">58.8</td>
  <td align="center">69.0</td>
  <td align="center">71.4</td>
</tr>
<tr>
  <td>Gemini-3-Pro</td>
  <td align="center">72.3</td>
  <td align="center">85.9</td>
  <td align="center">78.5</td>
  <td align="center">61.0</td>
  <td align="center">69.9</td>
  <td align="center">75.0</td>
</tr>
<tr>
  <td>FakeVLM <sub>NeurIPS'25</sub></td>
  <td align="center">83.5</td>
  <td align="center">81.0</td>
  <td align="center">76.8</td>
  <td align="center">74.5</td>
  <td align="center">74.9</td>
  <td align="center">77.1</td>
</tr>
<tr>
  <td>Veritas <sub>ICLR'26</sub></td>
  <td align="center">96.8</td>
  <td align="center">94.9</td>
  <td align="center">89.9</td>
  <td align="center">79.0</td>
  <td align="center">81.1</td>
  <td align="center">87.6</td>
</tr>
<tr>
  <td><b>VIGIL (Ours)</b></td>
  <td align="center"><b>98.6</b></td>
  <td align="center"><b>96.7</b></td>
  <td align="center"><b>95.5</b></td>
  <td align="center"><b>89.5</b></td>
  <td align="center"><b>86.0</b></td>
  <td align="center"><b>93.1</b></td>
</tr>
</tbody>
</table>

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
@article{li2026vigil,
  title={VIGIL: Part-Grounded Structured Reasoning for Generalizable Deepfake Detection},
  author={Li, Xinghan and Xu, Junhao and Chen, Jingjing},
  journal={arXiv preprint arXiv:2603.21526},
  year={2026}
}
```

## License

This project is released under the [Apache 2.0 License](LICENSE).
