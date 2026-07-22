# Awesome DLMs Post-Training

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0-1.0](https://img.shields.io/badge/License-CC0--1.0-lightgrey.svg)](LICENSE)

**A curated list of papers, frameworks, and resources on post-training for Diffusion Language Models (dLLMs): SFT, preference optimization, RL, safety alignment, distillation, inference acceleration, adaptation, and domain models.**

## 📢 News

- **[2026-07]** 🎉 Repository restructured around a method-centric post-training taxonomy. All entries now use arXiv + AlphaXiv badges and collapsible details. Contributions are welcome — see [CONTRIBUTING.md](CONTRIBUTING.md).

## 📖 What Counts as dLLM Post-Training?

This list focuses on the **post-training** stage of Diffusion Language Models, i.e. everything that happens after (or adapts) the base diffusion pre-training:

- **Base models** — influential dLLMs whose training pipeline includes a post-training (SFT / alignment) stage and that subsequent post-training work builds upon
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
- [Base Models](#base-models) (6)
- [SFT & Instruction Tuning](#sft--instruction-tuning) (2)
- [Preference Optimization](#preference-optimization)
- [RL & Reasoning](#rl--reasoning)
- [Safety & Alignment](#safety--alignment)
- [Distillation](#distillation)
- [Inference Acceleration](#inference-acceleration)
- [Training Objectives & Foundations](#training-objectives--foundations)
- [Adaptation Techniques](#adaptation-techniques)
- [Multimodal dLLMs](#multimodal-dllms)
- [Code dLLMs](#code-dllms) (7)
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

## Base Models

- <details>
  <summary>
    <b>[02/2025] Large Language Diffusion Models (LLaDA)</b>
    <a href="https://arxiv.org/abs/2502.09992"><img src="https://img.shields.io/badge/arXiv-2502.09992-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2502.09992"><img src="https://img.shields.io/badge/AlphaXiv-2502.09992-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/ML-GSAI/LLaDA"><img src="https://img.shields.io/github/stars/ML-GSAI/LLaDA?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shen Nie, Fengqi Zhu, Zebin You, Xiaolu Zhang, Jingyang Ou, Jun Hu, Jun Zhou, Yankai Lin, Ji-Rong Wen, Chongxuan Li

  **TL;DR:** An 8B masked diffusion LM trained from scratch plus SFT (noise applied to responses only), demonstrating for the first time that SFT in the diffusion paradigm can match LLaMA3-8B-level instruction following. NeurIPS 2025.
  </details>

- <details>
  <summary>
    <b>[08/2025] Dream 7B: Diffusion Large Language Models</b>
    <a href="https://arxiv.org/abs/2508.15487"><img src="https://img.shields.io/badge/arXiv-2508.15487-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2508.15487"><img src="https://img.shields.io/badge/AlphaXiv-2508.15487-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/DreamLM/Dream"><img src="https://img.shields.io/github/stars/DreamLM/Dream?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Jiacheng Ye, Zhihui Xie, Lin Zheng, Jiahui Gao, Zirui Wu, Xin Jiang, Zhenguo Li, Lingpeng Kong

  **TL;DR:** AR initialization plus context-adaptive token-level noise rescaling; releases Dream-Base and Dream-Instruct (SFT), one of the strongest open instruction-tuned diffusion model baselines. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[12/2025] LLaDA2.0: Scaling Up Diffusion Language Models to 100B</b>
    <a href="https://arxiv.org/abs/2512.15745"><img src="https://img.shields.io/badge/arXiv-2512.15745-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2512.15745"><img src="https://img.shields.io/badge/AlphaXiv-2512.15745-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/inclusionAI/LLaDA2.X"><img src="https://img.shields.io/github/stars/inclusionAI/LLaDA2.X?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Tiwei Bie, Maosong Cao, Kun Chen, Lun Du, Mingliang Gong, Zhuochen Gong, Yanmei Gu, Jiaqi Hu, Zenan Huang, Zhenzhong Lan, Chengxi Li, Chongxuan Li, Jianguo Li, Zehuan Li, Huabin Liu, Lin Liu, Guoshan Lu, Xiaocheng Lu, Yuxin Ma, Jianfeng Tan, Lanning Wei, Ji-Rong Wen, Yipeng Xing, Xiaolu Zhang, Junbo Zhao, Da Zheng, Jun Zhou, Junlin Zhou, Zhanchao Zhou, Liwang Zhu, Yihong Zhuang

  **TL;DR:** Scales diffusion language models to 100B via AR→dLLM conversion with a 3-phase block-level WSD training scheme, releasing instruction-tuned MoE variants LLaDA2.0-mini (16B) and LLaDA2.0-flash (100B). arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[09/2025] LLaDA-MoE: A Sparse MoE Diffusion Language Model</b>
    <a href="https://arxiv.org/abs/2509.24389"><img src="https://img.shields.io/badge/arXiv-2509.24389-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.24389"><img src="https://img.shields.io/badge/AlphaXiv-2509.24389-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/ML-GSAI/LLaDA"><img src="https://img.shields.io/github/stars/ML-GSAI/LLaDA?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Fengqi Zhu, Zebin You, Yipeng Xing, Zenan Huang, Lin Liu, Yihong Zhuang, Guoshan Lu, Kangyu Wang, Xudong Wang, Lanning Wei, Hongrui Guo, Jiaqi Hu, Wentao Ye, Tieyuan Chen, Chenchen Li, Chengfu Tang, Haibo Feng, Jun Hu, Jun Zhou, Xiaolu Zhang, Zhenzhong Lan, Junbo Zhao, Da Zheng, Chongxuan Li, Jianguo Li, Ji-Rong Wen

  **TL;DR:** A 7B-A1B MoE diffusion model trained from scratch on ~20T tokens; the Instruct version is obtained via SFT, with strong performance despite fewer active parameters. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[06/2026] Improved Large Language Diffusion Models (iLLaDA)</b>
    <a href="https://arxiv.org/abs/2606.25331"><img src="https://img.shields.io/badge/arXiv-2606.25331-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2606.25331"><img src="https://img.shields.io/badge/AlphaXiv-2606.25331-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/ML-GSAI/LLaDA"><img src="https://img.shields.io/github/stars/ML-GSAI/LLaDA?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shen Nie, Qiyang Min, Shaoxuan Xu, Zihao Huang, Yuxuan Song, Yong Shan, Yankai Lin, Wayne Xin Zhao, Chongxuan Li, Ji-Rong Wen

  **TL;DR:** An 8B masked diffusion language model trained from scratch with fully bidirectional attention, scaling pre-training to 12T tokens and SFT on a 25B-token instruction corpus; strong improvements over LLaDA on general, math, and code benchmarks. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[02/2025] TESS 2: A Large-Scale Generalist Diffusion Language Model</b>
    <a href="https://arxiv.org/abs/2502.13917"><img src="https://img.shields.io/badge/arXiv-2502.13917-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2502.13917"><img src="https://img.shields.io/badge/AlphaXiv-2502.13917-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/hamishivi/tess-2"><img src="https://img.shields.io/github/stars/hamishivi/tess-2?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Jaesung Tae, Hamish Ivison, Sachin Kumar, Arman Cohan

  **TL;DR:** A general instruction-following diffusion language model adapted from a strong AR model via continued pretraining and instruction tuning, introducing modular reward guidance for inference-time alignment. ACL 2025.
  </details>

## SFT & Instruction Tuning

- <details>
  <summary>
    <b>[05/2026] Learnability-Informed Fine-Tuning of Diffusion Language Models (LIFT)</b>
    <a href="https://arxiv.org/abs/2605.22939"><img src="https://img.shields.io/badge/arXiv-2605.22939-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.22939"><img src="https://img.shields.io/badge/AlphaXiv-2605.22939-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/divelab/LIFT"><img src="https://img.shields.io/github/stars/divelab/LIFT?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shubham Parashar, Atharv Chagi, Jacob Helwig, Lakshmi Jotsna, Sushil Vemuri, James Caverlee, Dileep Kalathil, Shuiwang Ji

  **TL;DR:** An SFT-based post-training algorithm that aligns learning difficulty with diffusion time steps, improving reasoning in dLLMs without relying on RL. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[10/2025] Rainbow Padding: Mitigating Early Termination in Instruction-Tuned Diffusion LLMs</b>
    <a href="https://arxiv.org/abs/2510.03680"><img src="https://img.shields.io/badge/arXiv-2510.03680-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.03680"><img src="https://img.shields.io/badge/AlphaXiv-2510.03680-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/quasar529/rainbow-padding"><img src="https://img.shields.io/github/stars/quasar529/rainbow-padding?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Bumjun Kim, Dongjae Jeon, Dueun Kim, Wonje Jeung, Albert No

  **TL;DR:** A simple remedy for `<eos>` overflow in instruction-tuned dLLMs that uses cyclic distinct padding tokens to prevent early termination and improve length robustness. arXiv 2025.
  </details>

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

- <details>
  <summary>
    <b>[06/2025] DiffuCoder: Understanding and Improving Masked Diffusion Models for Code Generation</b>
    <a href="https://arxiv.org/abs/2506.20639"><img src="https://img.shields.io/badge/arXiv-2506.20639-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2506.20639"><img src="https://img.shields.io/badge/AlphaXiv-2506.20639-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/apple/ml-diffucoder"><img src="https://img.shields.io/github/stars/apple/ml-diffucoder?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shansan Gong, Ruixiang Zhang, Huangjie Zheng, Jiatao Gu, Navdeep Jaitly, Lingpeng Kong, Yizhe Zhang

  **TL;DR:** A 7B masked diffusion code model trained on 130B tokens, analyzing dLLM decoding behavior and proposing coupled-GRPO for diffusion-native RL training on code generation benchmarks. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[01/2026] Stable-DiffCoder: Pushing the Frontier of Code Diffusion Large Language Model</b>
    <a href="https://arxiv.org/abs/2601.15892"><img src="https://img.shields.io/badge/arXiv-2601.15892-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2601.15892"><img src="https://img.shields.io/badge/AlphaXiv-2601.15892-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/ByteDance-Seed/Stable-DiffCoder"><img src="https://img.shields.io/github/stars/ByteDance-Seed/Stable-DiffCoder?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Chenghao Fan, Wen Heng, Bo Li, Sichen Liu, Yuxuan Song, Jing Su, Xiaoye Qu, Kai Shen, Wei Wei

  **TL;DR:** A block diffusion code model reusing Seed-Coder's architecture and data, with block diffusion continual pretraining and SFT, outperforming AR counterparts on code benchmarks. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[05/2026] Beyond Mode-Seeking RL: Trajectory-Balance Post-Training for Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2605.13935"><img src="https://img.shields.io/badge/arXiv-2605.13935-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.13935"><img src="https://img.shields.io/badge/AlphaXiv-2605.13935-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Saba Ahmadi, Prasanna Parthasarathi, Yufei Cui

  **TL;DR:** Proposes TraFL, a trajectory-balance objective for diffusion LM post-training that mitigates mode-seeking and improves coverage across math and code generation benchmarks. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[05/2026] Beyond Execution: Static-Analysis Rewards and Hint-Conditioned Diffusion RL for Code Generation</b>
    <a href="https://arxiv.org/abs/2605.17174"><img src="https://img.shields.io/badge/arXiv-2605.17174-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.17174"><img src="https://img.shields.io/badge/AlphaXiv-2605.17174-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Shuyin Ouyang, Zhaozhi Qian, Faroq AL-Tam, Muhammad AL-Qurishi, Jie M. Zhang

  **TL;DR:** A systematic study of RL post-training for diffusion-based code generation using execution-free (static-analysis) rewards and hint-conditioned sampling. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[02/2026] AnCoder: Anchored Code Generation via Discrete Diffusion Models</b>
    <a href="https://arxiv.org/abs/2602.17688"><img src="https://img.shields.io/badge/arXiv-2602.17688-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2602.17688"><img src="https://img.shields.io/badge/AlphaXiv-2602.17688-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Anton Xue, Litu Rout, Constantine Caramanis, Sanjay Shakkottai

  **TL;DR:** Introduces AnchorTree, which uses AST structure to anchor the diffusion process and prioritize syntactically and semantically salient tokens for higher-quality code generation. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[05/2026] Constrained Code Generation with Discrete Diffusion</b>
    <a href="https://arxiv.org/abs/2605.16829"><img src="https://img.shields.io/badge/arXiv-2605.16829-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.16829"><img src="https://img.shields.io/badge/AlphaXiv-2605.16829-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Lize Shao, Michael Cardei, Zichen Xie, Ferdinando Fioretto, Wenxi Wang

  **TL;DR:** Introduces CDC, a training-free neurosymbolic framework that enforces functional and security constraints during discrete diffusion decoding for code generation. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[12/2025] Corrective Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2512.15596"><img src="https://img.shields.io/badge/arXiv-2512.15596-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2512.15596"><img src="https://img.shields.io/badge/AlphaXiv-2512.15596-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/zhangshuibai/CDLM"><img src="https://img.shields.io/github/stars/zhangshuibai/CDLM?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shuibai Zhang, Fred Zhangzhi Peng, Yiheng Zhang, Jin Pan, Grigorios G. Chrysos

  **TL;DR:** Studies corrective behavior in DLMs and proposes a correction-oriented post-training principle that supervises visible incorrect tokens, with a Code Revision Benchmark for evaluation. arXiv 2025.
  </details>

## Frameworks & Benchmarks

*This section is currently being curated. Entries will be added here after review.*

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hasson827/Awesome-DLMs-post-training&type=Date)](https://star-history.com/#hasson827/Awesome-DLMs-post-training&Date)

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for the scope, entry format, and PR process before submitting.

## License

This work is licensed under [CC0-1.0](LICENSE) — free to use, share, and build upon.
