# Awesome DLMs Post-Training

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0-1.0](https://img.shields.io/badge/License-CC0--1.0-lightgrey.svg)](LICENSE)

**A curated list of papers, frameworks, and resources on post-training for Diffusion Language Models (dLLMs): SFT, preference optimization, RL, safety alignment, distillation, inference acceleration, adaptation, and domain models.**

## 📢 News

- **[2026-07]** 🎉 Repository restructured around a method-centric post-training taxonomy. All entries now use arXiv + AlphaXiv badges and collapsible details. Contributions are welcome — see [CONTRIBUTING.md](CONTRIBUTING.md).

## 📖 What Counts as dLLM Post-Training?

This list focuses on the **post-training** stage of Diffusion Language Models, i.e. everything that happens after (or adapts) the base diffusion pre-training:

- **SFT & instruction tuning** — supervised fine-tuning for instruction following, chat, long-CoT, and task adaptation
- **Preference optimization** — DPO/KTO/IPO-style alignment from paired or unpaired preference data
- **RL & reasoning** — GRPO/PPO/RLVR policy optimization, reward modeling, and trajectory-level RL for reasoning
- **Safety & alignment** — safety training, jailbreak robustness, and alignment analysis specific to dLLMs
- **Distillation** — knowledge/self/consistency/few-step distillation for faster or smaller dLLMs
- **Inference acceleration** — learned parallel decoding, speculative decoding, KV-cache training, and guidable decoding
- **Training objectives & foundations** — core discrete-diffusion objectives and training-inference analyses that post-training builds upon
- **Adaptation techniques** — AR→DLM conversion, long-context post-training, and representation alignment
- **Multimodal & code dLLMs** — domain-specific post-training for vision-language and code diffusion LMs

We cover **masked/absorbing, block, and continuous diffusion LMs**, including **multimodal** and **code** dLLMs. Pure pre-training architecture papers are included only when they establish training objectives or pipelines that post-training builds upon.

## 📑 Table of Contents

- [Surveys](#surveys) (4)
- [SFT & Instruction Tuning](#sft--instruction-tuning)
- [Preference Optimization](#preference-optimization)
- [RL & Reasoning](#rl--reasoning)
- [Safety & Alignment](#safety--alignment)
- [Distillation](#distillation)
- [Inference Acceleration](#inference-acceleration)
- [Training Objectives & Foundations](#training-objectives--foundations)
- [Adaptation Techniques](#adaptation-techniques)
- [Multimodal dLLMs](#multimodal-dllms)
- [Code dLLMs](#code-dllms)
- [Frameworks & Benchmarks](#frameworks--benchmarks)
- [Star History](#star-history)
- [Contributing](#contributing)
- [License](#license)

---

## Surveys

- <details>
  <summary>
    <b>[08/14/2025] A Survey on Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2508.10875"><img src="https://img.shields.io/badge/arXiv-2508.10875-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2508.10875"><img src="https://img.shields.io/badge/AlphaXiv-2508.10875-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/VILA-Lab/Awesome-DLMs"><img src="https://img.shields.io/github/stars/VILA-Lab/Awesome-DLMs?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Tianyi Li, Mingda Chen, Bowei Guo, Zhiqiang Shen

  **TL;DR:** The most comprehensive DLM survey to date, systematically covering pre-training, SFT, RL alignment, inference acceleration, and applications, with a dedicated post-training chapter. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[06/2025] Discrete Diffusion in Large Language and Multimodal Models: A Survey</b>
    <a href="https://arxiv.org/abs/2506.13759"><img src="https://img.shields.io/badge/arXiv-2506.13759-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2506.13759"><img src="https://img.shields.io/badge/AlphaXiv-2506.13759-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/LiQiiiii/DLLM-Survey"><img src="https://img.shields.io/github/stars/LiQiiiii/DLLM-Survey?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Runpeng Yu, Qi Li, Xinchao Wang

  **TL;DR:** Focuses on discrete diffusion formulations, training, and inference in large language and multimodal models, covering LLaDA, Dream, Dimple, and more. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[07/2026] Accelerating Masked Diffusion Large Language Models: A Survey of Efficient Inference Techniques</b>
    <a href="https://arxiv.org/abs/2607.12829"><img src="https://img.shields.io/badge/arXiv-2607.12829-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2607.12829"><img src="https://img.shields.io/badge/AlphaXiv-2607.12829-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Daehoon Gwak, Minhyung Lee, Junwoo Park, Jaegul Choo

  **TL;DR:** Introduces a unified latency decomposition framework for dLLMs and surveys efficient inference techniques across algorithms, architectures, and systems, with reproducible benchmarking guidelines. IJCAI-ECAI 2026 Survey Track.
  </details>

- <details>
  <summary>
    <b>[05/2023] A Survey of Diffusion Models in Natural Language Processing</b>
    <a href="https://arxiv.org/abs/2305.14671"><img src="https://img.shields.io/badge/arXiv-2305.14671-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2305.14671"><img src="https://img.shields.io/badge/AlphaXiv-2305.14671-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Hao Zou, Zae Myung Kim, Dongyeop Kang

  **TL;DR:** An earlier survey reviewing diffusion models for NLP tasks including generation, sentiment analysis, topic modeling, and machine translation, with comparisons to autoregressive models. arXiv 2023.
  </details>

## SFT & Instruction Tuning

*This section is currently being curated. Entries will be added here after review.*

## Preference Optimization

*This section is currently being curated. Entries will be added here after review.*

## RL & Reasoning

*This section is currently being curated. Entries will be added here after review.*

## Safety & Alignment

*This section is currently being curated. Entries will be added here after review.*

## Distillation

*This section is currently being curated. Entries will be added here after review.*

## Inference Acceleration

*This section is currently being curated. Entries will be added here after review.*

## Training Objectives & Foundations

*This section is currently being curated. Entries will be added here after review.*

## Adaptation Techniques

*This section is currently being curated. Entries will be added here after review.*

## Multimodal dLLMs

*This section is currently being curated. Entries will be added here after review.*

## Code dLLMs

*This section is currently being curated. Entries will be added here after review.*

## Frameworks & Benchmarks

*This section is currently being curated. Entries will be added here after review.*

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hasson827/Awesome-DLMs-post-training&type=Date)](https://star-history.com/#hasson827/Awesome-DLMs-post-training&Date)

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for the scope, entry format, and PR process before submitting.

## License

This work is licensed under [CC0-1.0](LICENSE) — free to use, share, and build upon.
