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
- [SFT & Instruction Tuning](#sft--instruction-tuning) (3)
- [Preference Optimization](#preference-optimization)
- [RL & Reasoning](#rl--reasoning)
- [Safety & Alignment](#safety--alignment)
- [Distillation](#distillation) (1)
- [Inference Acceleration](#inference-acceleration) (2)
- [Training Objectives & Foundations](#training-objectives--foundations) (2)
- [Adaptation Techniques](#adaptation-techniques) (8)
- [Multimodal dLLMs](#multimodal-dllms) (21)
- [Code dLLMs](#code-dllms) (13)
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

- <details>
  <summary>
    <b>[08/2023] Diffusion Language Models Can Perform Many Tasks with Scaling and Instruction-Finetuning</b>
    <a href="https://arxiv.org/abs/2308.12219"><img src="https://img.shields.io/badge/arXiv-2308.12219-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2308.12219"><img src="https://img.shields.io/badge/AlphaXiv-2308.12219-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/yegcjs/DiffusionLLM"><img src="https://img.shields.io/github/stars/yegcjs/DiffusionLLM?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Jiasheng Ye, Zaixiang Zheng, Yu Bao, Lihua Qian, Quanquan Gu

  **TL;DR:** Scales diffusion language models via masked-language-model pretraining and diffusive adaptation, then unlocks general task solving through task-specific and instruction finetuning, eliciting zero/few-shot in-context learning. arXiv 2023.
  </details>

## Preference Optimization

*This section is currently being curated. Entries will be added here after review.*

## RL & Reasoning

*This section is currently being curated. Entries will be added here after review.*

## Safety & Alignment

*This section is currently being curated. Entries will be added here after review.*

## Distillation

- <details>
  <summary>
    <b>[04/2026] Turning the TIDE: Cross-Architecture Distillation for Diffusion Large Language Models</b>
    <a href="https://arxiv.org/abs/2604.26951"><img src="https://img.shields.io/badge/arXiv-2604.26951-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2604.26951"><img src="https://img.shields.io/badge/AlphaXiv-2604.26951-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/PKU-YuanGroup/TIDE"><img src="https://img.shields.io/github/stars/PKU-YuanGroup/TIDE?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Gongbo Zhang, Wen Wang, Ye Tian, Li Yuan

  **TL;DR:** Cross-architecture distillation framework compressing 8B dense / 16B MoE dLLM teachers into a 0.6B student via TIDAL, CompDemo, and Reverse CALM. arXiv 2026.
  </details>

## Inference Acceleration

- <details>
  <summary>
    <b>[05/2026] Elastic-dLLM: Position Preserving Context Compression and Augmentation of Diffusion LLMs</b>
    <a href="https://arxiv.org/abs/2605.18165"><img src="https://img.shields.io/badge/arXiv-2605.18165-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.18165"><img src="https://img.shields.io/badge/AlphaXiv-2605.18165-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Junyi Wu, Tianchen Zhao, Shaoqiu Zhang, Linfeng Zhang, Guohao Dai, Yu Wang

  **TL;DR:** Training-free position-preserving [MASK]-token compression and terminal-aware augmentation that speeds up dLLM decoding and enables longer-context scaling. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[09/2025] Fast-dLLM v2: Efficient Block-Diffusion LLM</b>
    <a href="https://arxiv.org/abs/2509.26328"><img src="https://img.shields.io/badge/arXiv-2509.26328-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.26328"><img src="https://img.shields.io/badge/AlphaXiv-2509.26328-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/NVlabs/Fast-dLLM"><img src="https://img.shields.io/github/stars/NVlabs/Fast-dLLM?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Chengyue Wu, Hao Zhang, Shuchen Xue, Shizhe Diao, Yonggan Fu, Zhijian Liu, Pavlo Molchanov, Ping Luo, Song Han, Enze Xie

  **TL;DR:** Adapts pretrained AR models into a block-diffusion dLLM with hierarchical KV caches and parallel decoding, achieving ~2.5× speedup over AR baselines. arXiv 2025.
  </details>

## Training Objectives & Foundations

- <details>
  <summary>
    <b>[06/2026] Adaptive Block Diffusion: Resolving Training-Inference Mismatch in Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2606.29275"><img src="https://img.shields.io/badge/arXiv-2606.29275-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2606.29275"><img src="https://img.shields.io/badge/AlphaXiv-2606.29275-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Gagan Jain

  **TL;DR:** Trains a single DLM over a distribution of prefix-window configurations so it generalizes across arbitrary inference block sizes without off-grid degradation. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[01/2026] Mechanism Shift During Post-training from Autoregressive to Masked Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2601.14758"><img src="https://img.shields.io/badge/arXiv-2601.14758-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2601.14758"><img src="https://img.shields.io/badge/AlphaXiv-2601.14758-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Injin Kong, Hyoungjoon Lee, Yohan Jo

  **TL;DR:** Circuit analysis showing AR→MDM post-training reorganizes internal computation in a task-dependent way rather than merely repackaging AR inference. arXiv 2026.
  </details>

## Adaptation Techniques

- <details>
  <summary>
    <b>[06/2026] Data-Efficient Autoregressive-to-Diffusion Language Models via On-Policy Distillation</b>
    <a href="https://arxiv.org/abs/2606.06712"><img src="https://img.shields.io/badge/arXiv-2606.06712-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2606.06712"><img src="https://img.shields.io/badge/AlphaXiv-2606.06712-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/divelab/OPDLM"><img src="https://img.shields.io/github/stars/divelab/OPDLM?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Xingyu Su, Jacob Helwig, Shubham Parashar, Atharv Chagi, Lakshmi Jotsna, Degui Zhi, James Caverlee, Dileep Kalathil, Shuiwang Ji

  **TL;DR:** Converts pretrained AR LMs into block-diffusion DLMs with 15×–7,000× fewer tokens by distilling on the model's own decoding trajectories. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[05/2026] NaRA: Noise-Aware LoRA for Parameter-Efficient Fine-Tuning of Diffusion LLMs</b>
    <a href="https://arxiv.org/abs/2605.29716"><img src="https://img.shields.io/badge/arXiv-2605.29716-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.29716"><img src="https://img.shields.io/badge/AlphaXiv-2605.29716-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/generaldi/NaRA"><img src="https://img.shields.io/github/stars/generaldi/NaRA?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shuaidi Wang, Zhan Zhuang, Ruping Huang, Yu Zhang

  **TL;DR:** Noise-level-conditioned LoRA variant that uses a shared hypernetwork to generate dynamic low-rank updates along the dLLM denoising trajectory. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[05/2026] Don't Retrain, Align: Adapting Autoregressive LMs to Diffusion LMs via Representation Alignment</b>
    <a href="https://arxiv.org/abs/2605.06885"><img src="https://img.shields.io/badge/arXiv-2605.06885-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.06885"><img src="https://img.shields.io/badge/AlphaXiv-2605.06885-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/pengzhangzhi/Open-dLLM"><img src="https://img.shields.io/github/stars/pengzhangzhi/Open-dLLM?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Fred Zhangzhi Peng, Alexis Fox, Anru R. Zhang, Alexander Tong

  **TL;DR:** Adapts AR LMs to diffusion LMs by aligning hidden states to a frozen AR teacher, accelerating training up to 4× and improving low-data adaptation. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[12/2025] Efficient-DLM: From Autoregressive to Diffusion Language Models, and Beyond in Speed</b>
    <a href="https://arxiv.org/abs/2512.14067"><img src="https://img.shields.io/badge/arXiv-2512.14067-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2512.14067"><img src="https://img.shields.io/badge/AlphaXiv-2512.14067-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Yonggan Fu, Lexington Whalen, Zhifan Ye, Xin Dong, Shizhe Diao, Jingyu Liu, Chengyue Wu, Hao Zhang, Enze Xie, Song Han, Maksim Khadkevich, Jan Kautz, Yingyan Celine Lin, Pavlo Molchanov

  **TL;DR:** Proposes a block-wise attention training recipe and position-dependent masking strategy for converting pretrained AR models into fast, KV-cacheable dLMs. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[12/2025] From Next-Token to Next-Block: A Principled Adaptation Path for Diffusion LLMs</b>
    <a href="https://arxiv.org/abs/2512.06776"><img src="https://img.shields.io/badge/arXiv-2512.06776-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2512.06776"><img src="https://img.shields.io/badge/AlphaXiv-2512.06776-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/YuchuanTian/NBDiff"><img src="https://img.shields.io/github/stars/YuchuanTian/NBDiff?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Yuchuan Tian, Yuchen Liang, Shuo Zhang, Yingte Shu, Guangwen Yang, Wei He, Sibo Fang, Tianyu Guo, Kai Han, Chao Xu, Hanting Chen, Xinghao Chen, Yunhe Wang

  **TL;DR:** Reframes AR→DLM conversion as a smooth block-size growth path with context-causal prefixes and AR guidance, yielding the NBDiff-7B model. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[10/2025] UltraLLaDA: Scaling the Context Length to 128K for Diffusion Large Language Models</b>
    <a href="https://arxiv.org/abs/2510.10481"><img src="https://img.shields.io/badge/arXiv-2510.10481-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.10481"><img src="https://img.shields.io/badge/AlphaXiv-2510.10481-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/Relaxed-System-Lab/UltraLLaDA"><img src="https://img.shields.io/github/stars/Relaxed-System-Lab/UltraLLaDA?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Guangxin He, Shen Nie, Fengqi Zhu, Yuankang Zhao, Tianyi Bai, Ran Yan, Jie Fu, Chongxuan Li, Binhang Yuan

  **TL;DR:** Lightweight post-training extension of LLaDA to 128K tokens using a diffusion-aware RoPE/NTK extension and tailored masking strategies. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[06/2025] LongLLaDA: Unlocking Long Context Capabilities in Diffusion LLMs</b>
    <a href="https://arxiv.org/abs/2506.14429"><img src="https://img.shields.io/badge/arXiv-2506.14429-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2506.14429"><img src="https://img.shields.io/badge/AlphaXiv-2506.14429-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/OpenMOSS/LongLLaDA"><img src="https://img.shields.io/github/stars/OpenMOSS/LongLLaDA?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Xiaoran Liu, Yuerong Song, Zhigeng Liu, Zengfeng Huang, Qipeng Guo, Ziwei He, Xipeng Qiu

  **TL;DR:** Training-free NTK-based RoPE extrapolation that exploits diffusion LMs' stable length extrapolation for long-context tasks. AAAI 2026.
  </details>

- <details>
  <summary>
    <b>[10/2024] Scaling Diffusion Language Models via Adaptation from Autoregressive Models</b>
    <a href="https://arxiv.org/abs/2410.17891"><img src="https://img.shields.io/badge/arXiv-2410.17891-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2410.17891"><img src="https://img.shields.io/badge/AlphaXiv-2410.17891-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/HKUNLP/DiffuLLaMA"><img src="https://img.shields.io/github/stars/HKUNLP/DiffuLLaMA?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shansan Gong, Shivam Agarwal, Yizhe Zhang, Jiacheng Ye, Lin Zheng, Mukai Li, Chenxin An, Peilin Zhao, Wei Bi, Jiawei Han, Hao Peng, Lingpeng Kong

  **TL;DR:** Converts pretrained AR models (GPT-2/LLaMA) into diffusion LMs via continual pretraining, releasing DiffuGPT/DiffuLLaMA up to 7B. ICLR 2025.
  </details>

## Multimodal dLLMs

- <details>
  <summary>
    <b>[06/2026] dVLA-RL: Reinforcement Learning over Denoising Trajectories for Discrete Diffusion Vision-Language-Action Models</b>
    <a href="https://arxiv.org/abs/2606.23623"><img src="https://img.shields.io/badge/arXiv-2606.23623-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2606.23623"><img src="https://img.shields.io/badge/AlphaXiv-2606.23623-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Yuhao Wu, Yitian Liu, Weijie Shen, Mishuo Han, Wenjie Xu, Haotian Liang, Zhongshan Liu, Yinan Mao, Lei Xu, Xinping Guan, Ru Ying, Ran Zheng, Wei Sui, Xiaokang Yang, Wenbo Ding, Yao Mu

  **TL;DR:** Proposes RL over denoising trajectories for discrete diffusion Vision-Language-Action models by modeling the denoising process as an MDP and optimizing the joint path probability. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[07/2026] Reinforcing the Generation Order of Multimodal Masked Diffusion Models</b>
    <a href="https://arxiv.org/abs/2607.08056"><img src="https://img.shields.io/badge/arXiv-2607.08056-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2607.08056"><img src="https://img.shields.io/badge/AlphaXiv-2607.08056-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Yidong Ouyang, Zhe Wang, Sourav Bhabesh, Dmitriy Bespalov

  **TL;DR:** Uses a learnable control module trained with GRPO to optimize generation order for both text-to-image synthesis and multimodal understanding in masked diffusion models. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[06/2026] Efficient Reinforcement for Visual-Textual Thinking with Discrete Diffusion Model</b>
    <a href="https://arxiv.org/abs/2606.14792"><img src="https://img.shields.io/badge/arXiv-2606.14792-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2606.14792"><img src="https://img.shields.io/badge/AlphaXiv-2606.14792-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Yoonjeon Kim, Yuhta Takida, Chieh-Hsin Lai, Eunho Yang, Yuki Mitsufuji

  **TL;DR:** Demonstrates that multimodal discrete diffusion models enable efficient visual rollouts for RL in interleaved visual-textual reasoning, with factorized reward assignment to mitigate cross-modal interference. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[02/2026] The Design Space of Tri-Modal Masked Diffusion Models</b>
    <a href="https://arxiv.org/abs/2602.21472"><img src="https://img.shields.io/badge/arXiv-2602.21472-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2602.21472"><img src="https://img.shields.io/badge/AlphaXiv-2602.21472-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Louis Bethune, Victor Turrisi, Bruno Kacper Mlodozeniec, Pau Rodriguez Lopez, Lokesh Boominathan, Nikhil Bhendawade, Amitis Shidani, Joris Pelemans, Theo X. Olausson, Devon Hjelm, Paul Dixon, Joao Monteiro, Pierre Ablin, Vishnu Banna, Arno Blaas, Nick Henderson, Kari Noriy, Dan Busbridge, Josh Susskind, Marco Cuturi, Irina Belousova, Luca Zappella, Russ Webb, Jason Ramapuram

  **TL;DR:** Introduces the first tri-modal masked diffusion model pretrained from scratch on text, image-text, and audio-text data, with systematic analysis of multimodal scaling laws and an SDE-based batch-size reparameterization. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[12/2025] DiffusionVL: Translating Any Autoregressive Models into Diffusion Vision Language Models</b>
    <a href="https://arxiv.org/abs/2512.15713"><img src="https://img.shields.io/badge/arXiv-2512.15713-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2512.15713"><img src="https://img.shields.io/badge/AlphaXiv-2512.15713-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/hustvl/DiffusionVL"><img src="https://img.shields.io/github/stars/hustvl/DiffusionVL?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Lunbin Zeng, Jingfeng Yao, Bencheng Liao, Hongyuan Tao, Wenyu Liu, Xinggang Wang

  **TL;DR:** Translates pretrained autoregressive vision-language models into the diffusion paradigm via efficient diffusion finetuning, keeping the backbone architecture intact and supporting block decoding with KV-cache reuse. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[03/2026] Omni-Diffusion: Unified Multimodal Understanding and Generation with Masked Discrete Diffusion</b>
    <a href="https://arxiv.org/abs/2603.06577"><img src="https://img.shields.io/badge/arXiv-2603.06577-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2603.06577"><img src="https://img.shields.io/badge/AlphaXiv-2603.06577-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/VITA-MLLM/Omni-Diffusion"><img src="https://img.shields.io/github/stars/VITA-MLLM/Omni-Diffusion?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Lijiang Li, Zuwei Long, Yunhang Shen, Heting Gao, Haoyu Cao, Xing Sun, Caifeng Shan, Ran He, Chaoyou Fu

  **TL;DR:** The first any-to-any multimodal language model built entirely on mask-based discrete diffusion, unifying understanding and generation across text, speech, and images. ICML 2026.
  </details>

- <details>
  <summary>
    <b>[06/2026] PerceptionDLM: Parallel Region Perception with Multimodal Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2606.19534"><img src="https://img.shields.io/badge/arXiv-2606.19534-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2606.19534"><img src="https://img.shields.io/badge/AlphaXiv-2606.19534-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/MSALab-PKU/PerceptionDLM"><img src="https://img.shields.io/github/stars/MSALab-PKU/PerceptionDLM?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Yueyi Sun, Yuhao Wang, Jason Li, Ye Tian, Tao Zhang, Jacky Mai, Yihan Wang, Haochen Wang, Jinbin Bai, Ling Yang, Yunhai Tong

  **TL;DR:** A multimodal diffusion language model optimized for efficient parallel region perception, enabling simultaneous captioning of multiple masked regions at both sequence and token levels. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[04/2026] Thinking Diffusion: Penalize and Guide Visual-Grounded Reasoning in Diffusion Multimodal Language Models</b>
    <a href="https://arxiv.org/abs/2604.05497"><img src="https://img.shields.io/badge/arXiv-2604.05497-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2604.05497"><img src="https://img.shields.io/badge/AlphaXiv-2604.05497-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Keuntae Kim, Mingyu Kang, Yong Suk Choi

  **TL;DR:** Identifies premature answer generation and weak visual grounding in dMLLM CoT reasoning, proposing Position and Step Penalty (PSP) and Visual Reasoning Guidance (VRG) to delay answers and amplify visual signals. CVPR 2026.
  </details>

- <details>
  <summary>
    <b>[02/2026] LaViDa-R1: Advancing Reasoning for Unified Multimodal Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2602.14147"><img src="https://img.shields.io/badge/arXiv-2602.14147-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2602.14147"><img src="https://img.shields.io/badge/AlphaXiv-2602.14147-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/jacklishufan/LaViDa"><img src="https://img.shields.io/github/stars/jacklishufan/LaViDa?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shufan Li, Yuchen Zhu, Jiuxiang Gu, Kangning Liu, Zhe Lin, Yongxin Chen, Molei Tao, Aditya Grover, Jason Kuen

  **TL;DR:** A multimodal general-purpose reasoning dLLM built with a unified post-training framework integrating SFT and multi-task RL, with techniques such as answer-forcing and tree search. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[04/2026] LLaDA2.0-Uni: Unifying Multimodal Understanding and Generation with Diffusion Large Language Model</b>
    <a href="https://arxiv.org/abs/2604.20796"><img src="https://img.shields.io/badge/arXiv-2604.20796-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2604.20796"><img src="https://img.shields.io/badge/AlphaXiv-2604.20796-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/inclusionAI/LLaDA2.0-Uni"><img src="https://img.shields.io/github/stars/inclusionAI/LLaDA2.0-Uni?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Inclusion AI, Tiwei Bie, Haoxing Chen, Tieyuan Chen, Zhenglin Cheng, Long Cui, Kai Gan, Zhicheng Huang, Zhenzhong Lan, Haoquan Li, Jianguo Li, Tao Lin, Qi Qin, Hongjun Wang, Xiaomei Wang, Haoyuan Wu, Yi Xin, Junbo Zhao

  **TL;DR:** A unified discrete diffusion large language model supporting multimodal understanding and generation within a natively integrated framework, using a semantic discrete tokenizer, MoE backbone, and diffusion decoder. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[05/2025] LaViDa: A Large Diffusion Language Model for Multimodal Understanding</b>
    <a href="https://arxiv.org/abs/2505.16839"><img src="https://img.shields.io/badge/arXiv-2505.16839-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2505.16839"><img src="https://img.shields.io/badge/AlphaXiv-2505.16839-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/jacklishufan/LaViDa"><img src="https://img.shields.io/github/stars/jacklishufan/LaViDa?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shufan Li, Konstantinos Kallidromitis, Hritik Bansal, Akash Gokul, Yusuke Kato, Kazuki Kozuka, Jason Kuen, Zhe Lin, Kai-Wei Chang, Aditya Grover

  **TL;DR:** A family of vision-language models built on discrete diffusion, jointly fine-tuned for multimodal instruction following with complementary masking, prefix KV cache, and timestep shifting for efficient inference and controllable generation. NeurIPS 2025.
  </details>

- <details>
  <summary>
    <b>[03/2025] Unified Multimodal Discrete Diffusion</b>
    <a href="https://arxiv.org/abs/2503.20853"><img src="https://img.shields.io/badge/arXiv-2503.20853-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2503.20853"><img src="https://img.shields.io/badge/AlphaXiv-2503.20853-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/alexanderswerdlow/unidisc"><img src="https://img.shields.io/github/stars/alexanderswerdlow/unidisc?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Alexander Swerdlow, Mihir Prabhudesai, Siddharth Gandhi, Deepak Pathak, Katerina Fragkiadaki

  **TL;DR:** Presents the first unified multimodal discrete diffusion model that jointly understands and generates text and images, with controllable quality–diversity trade-offs, inpainting, and editing. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[05/2025] MMaDA: Multimodal Large Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2505.15809"><img src="https://img.shields.io/badge/arXiv-2505.15809-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2505.15809"><img src="https://img.shields.io/badge/AlphaXiv-2505.15809-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/Gen-Verse/MMaDA"><img src="https://img.shields.io/github/stars/Gen-Verse/MMaDA?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Ling Yang, Ye Tian, Bowen Li, Xinchen Zhang, Ke Shen, Yunhai Tong, Mengdi Wang

  **TL;DR:** Introduces a unified modality-agnostic diffusion foundation model with mixed chain-of-thought fine-tuning and UniGRPO reinforcement learning, achieving strong results in textual reasoning, multimodal understanding, and text-to-image generation. NeurIPS 2025.
  </details>

- <details>
  <summary>
    <b>[05/2025] LLaDA-V: Large Language Diffusion Models with Visual Instruction Tuning</b>
    <a href="https://arxiv.org/abs/2505.16933"><img src="https://img.shields.io/badge/arXiv-2505.16933-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2505.16933"><img src="https://img.shields.io/badge/AlphaXiv-2505.16933-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/ML-GSAI/LLaDA-V"><img src="https://img.shields.io/github/stars/ML-GSAI/LLaDA-V?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Zebin You, Shen Nie, Xiaolu Zhang, Jun Hu, Jun Zhou, Zhiwu Lu, Ji-Rong Wen, Chongxuan Li

  **TL;DR:** Extends LLaDA into a purely diffusion-based multimodal large language model via visual instruction tuning, showing competitive multimodal understanding and favorable data scalability. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[05/2025] Dimple: Discrete Diffusion Multimodal Large Language Model with Parallel Decoding</b>
    <a href="https://arxiv.org/abs/2505.16990"><img src="https://img.shields.io/badge/arXiv-2505.16990-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2505.16990"><img src="https://img.shields.io/badge/AlphaXiv-2505.16990-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/yu-rp/Dimple"><img src="https://img.shields.io/github/stars/yu-rp/Dimple?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Runpeng Yu, Xinyin Ma, Xinchao Wang

  **TL;DR:** Proposes the first discrete diffusion MLLM with an autoregressive-to-diffusion training paradigm and confident parallel decoding, matching or exceeding LLaVA-NEXT while reducing generation iterations. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[09/2025] LaViDa-O: Elastic Large Masked Diffusion Models for Unified Multimodal Understanding and Generation</b>
    <a href="https://arxiv.org/abs/2509.19244"><img src="https://img.shields.io/badge/arXiv-2509.19244-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.19244"><img src="https://img.shields.io/badge/AlphaXiv-2509.19244-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/jacklishufan/LaViDa"><img src="https://img.shields.io/github/stars/jacklishufan/LaViDa?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shufan Li, Jiuxiang Gu, Kangning Liu, Zhe Lin, Zijun Wei, Aditya Grover, Jason Kuen

  **TL;DR:** A unified masked diffusion model with an Elastic Mixture-of-Transformers architecture that supports object grounding, editing, and high-resolution text-to-image generation with planning and self-reflection. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[10/2025] Lumina-DiMOO: An Omni Diffusion Large Language Model for Multi-Modal Generation and Understanding</b>
    <a href="https://arxiv.org/abs/2510.06308"><img src="https://img.shields.io/badge/arXiv-2510.06308-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.06308"><img src="https://img.shields.io/badge/AlphaXiv-2510.06308-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/Alpha-VLLM/Lumina-DiMOO"><img src="https://img.shields.io/github/stars/Alpha-VLLM/Lumina-DiMOO?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Yi Xin, Qi Qin, Siqi Luo, Kaiwen Zhu, Juncheng Yan, Yan Tai, Jiayi Lei, Yuewen Cao, Keqi Wang, Yibin Wang, Jinbin Bai, Qian Yu, Dengyang Jiang, Yuandong Pu, Haoxing Chen, Le Zhuo, Junjun He, Gen Luo, Tianbin Li, Ming Hu, Jin Ye, Shenglong Ye, Bo Zhang, Chang Xu, Wenhai Wang, Hongsheng Li, Guangtao Zhai, Tianfan Xue, Bin Fu, Xiaohong Liu, Yu Qiao, Yihao Liu

  **TL;DR:** An open-source omni discrete diffusion model that handles text-to-image, image-to-image, and image understanding in a fully diffusion paradigm with higher sampling efficiency. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[10/2025] From Denoising to Refining: A Corrective Framework for Vision-Language Diffusion Model</b>
    <a href="https://arxiv.org/abs/2510.19871"><img src="https://img.shields.io/badge/arXiv-2510.19871-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.19871"><img src="https://img.shields.io/badge/AlphaXiv-2510.19871-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/jiyt17/ReDiff"><img src="https://img.shields.io/github/stars/jiyt17/ReDiff?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Yatai Ji, Teng Wang, Yuying Ge, Zhiheng Liu, Sidi Yang, Ying Shan, Ping Luo

  **TL;DR:** Reframes vision-language diffusion generation as active refining via synthetic-error revision and online self-correction, breaking error cascades in parallel decoding. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[11/2025] MMaDA-Parallel: Multimodal Large Diffusion Language Models for Thinking-Aware Editing and Generation</b>
    <a href="https://arxiv.org/abs/2511.09611"><img src="https://img.shields.io/badge/arXiv-2511.09611-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2511.09611"><img src="https://img.shields.io/badge/AlphaXiv-2511.09611-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/tyfeld/MMaDA-Parallel"><img src="https://img.shields.io/github/stars/tyfeld/MMaDA-Parallel?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Ye Tian, Ling Yang, Jiongfan Yang, Anran Wang, Yu Tian, Jiani Zheng, Haochen Wang, Zhiyang Teng, Zhuochen Wang, Yinjie Wang, Yunhai Tong, Mengdi Wang, Xiangtai Li

  **TL;DR:** Proposes a parallel multimodal diffusion framework with bidirectional text-image interaction and Parallel Reinforcement Learning for thinking-aware editing and generation, introducing the ParaBench benchmark. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[12/2025] Sparse-LaViDa: Sparse Multimodal Discrete Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2512.14008"><img src="https://img.shields.io/badge/arXiv-2512.14008-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2512.14008"><img src="https://img.shields.io/badge/AlphaXiv-2512.14008-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/jacklishufan/LaViDa"><img src="https://img.shields.io/github/stars/jacklishufan/LaViDa?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shufan Li, Jiuxiang Gu, Kangning Liu, Zhe Lin, Zijun Wei, Aditya Grover, Jason Kuen

  **TL;DR:** Accelerates masked diffusion sampling by dynamically truncating redundant masked tokens with register tokens and a matching training attention mask, built on LaViDa-O. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[12/2025] SDAR-VL: Stable and Efficient Block-wise Diffusion for Vision-Language Understanding</b>
    <a href="https://arxiv.org/abs/2512.14068"><img src="https://img.shields.io/badge/arXiv-2512.14068-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2512.14068"><img src="https://img.shields.io/badge/AlphaXiv-2512.14068-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/JetAstra/SDAR-VL"><img src="https://img.shields.io/github/stars/JetAstra/SDAR-VL?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shuang Cheng, Yuhua Jiang, Zineng Zhou, Dawei Liu, Wang Tao, Linfeng Zhang, Biqing Qi, Bowen Zhou

  **TL;DR:** Introduces the first large-scale block-wise discrete diffusion framework for vision-language understanding, with asynchronous noise scheduling, mask-ratio scaling, and a beta curriculum for stable training. arXiv 2025.
  </details>

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

- <details>
  <summary>
    <b>[10/2023] CodeFusion: A Pre-trained Diffusion Model for Code Generation</b>
    <a href="https://arxiv.org/abs/2310.17680"><img src="https://img.shields.io/badge/arXiv-2310.17680-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2310.17680"><img src="https://img.shields.io/badge/AlphaXiv-2310.17680-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/microsoft/prose-benchmarks/tree/main/CodeFusion"><img src="https://img.shields.io/github/stars/microsoft/prose-benchmarks?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Mukul Singh, José Cambronero, Sumit Gulwani, Vu Le, Carina Negreanu, Gust Verbruggen

  **TL;DR:** Introduces CodeFusion, a 75M-parameter diffusion model for natural-language-to-code generation that iteratively denoises a full program conditioned on the encoded prompt, outperforming much larger autoregressive models in top-3/top-5 accuracy on Bash, Python, and Excel conditional-formatting rules. EMNLP 2023.
  </details>

- <details>
  <summary>
    <b>[08/2025] Diffusion is a code repair operator and generator</b>
    <a href="https://arxiv.org/abs/2508.11110"><img src="https://img.shields.io/badge/arXiv-2508.11110-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2508.11110"><img src="https://img.shields.io/badge/AlphaXiv-2508.11110-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Mukul Singh, Gust Verbruggen, Vu Le, Sumit Gulwani

  **TL;DR:** Shows that the late steps of a code diffusion process resemble last-mile repairs, and leverages pretrained code diffusion models for repair by noising broken snippets and by generating synthetic repair training pairs. NeurIPS 2025.
  </details>

- <details>
  <summary>
    <b>[09/2025] Dream-Coder 7B: An Open Diffusion Language Model for Code</b>
    <a href="https://arxiv.org/abs/2509.01142"><img src="https://img.shields.io/badge/arXiv-2509.01142-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.01142"><img src="https://img.shields.io/badge/AlphaXiv-2509.01142-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/DreamLM/Dream-Coder"><img src="https://img.shields.io/github/stars/DreamLM/Dream-Coder?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Zhihui Xie, Jiacheng Ye, Lin Zheng, Jiahui Gao, Jingwei Dong, Zirui Wu, Xueliang Zhao, Shansan Gong, Xin Jiang, Zhenguo Li, Lingpeng Kong

  **TL;DR:** Presents an open 7B discrete diffusion language model for code that adapts an autoregressive checkpoint with continuous-time weighted cross-entropy and RL with verifiable rewards, showing strong pass@1 on LiveCodeBench and competitive results on HumanEval, MBPP, BigCodeBench, and CRUXEval. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[09/2025] DiffuTester: Accelerating Unit Test Generation for Diffusion LLMs via Mining Structural Pattern</b>
    <a href="https://arxiv.org/abs/2509.24975"><img src="https://img.shields.io/badge/arXiv-2509.24975-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.24975"><img src="https://img.shields.io/badge/AlphaXiv-2509.24975-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/THU-Agent/DiffuTester"><img src="https://img.shields.io/github/stars/THU-Agent/DiffuTester?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Lekang Yang, Yuetong Liu, Yitong Zhang, Jia Li

  **TL;DR:** Proposes a decoding acceleration framework for diffusion LLM-based unit test generation that mines shared structural patterns across abstract syntax trees to decode repetitive tokens without sacrificing test coverage. ISSTA 2026.
  </details>

- <details>
  <summary>
    <b>[09/2025] CoDA: Coding LM via Diffusion Adaptation</b>
    <a href="https://arxiv.org/abs/2510.03270"><img src="https://img.shields.io/badge/arXiv-2510.03270-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.03270"><img src="https://img.shields.io/badge/AlphaXiv-2510.03270-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/SalesforceAIResearch/CoDA"><img src="https://img.shields.io/github/stars/SalesforceAIResearch/CoDA?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Haolin Chen, Shiyu Wang, Can Qin, Bo Pang, Zuxin Liu, Jielin Qiu, Jianguo Zhang, Yingbo Zhou, Zeyuan Chen, Ran Xu, Shelby Heinecke, Silvio Savarese, Caiming Xiong, Huan Wang, Weiran Yao

  **TL;DR:** Introduces CoDA-1.7B, a lightweight diffusion coder trained via large-scale diffusion pre-training, code-centric mid-training, and instruction tuning with confidence-guided sampling, matching or surpassing 7B diffusion baselines on HumanEval, MBPP, and EvalPlus. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[02/2026] DreamOn: Diffusion Language Models For Code Infilling Beyond Fixed-size Canvas</b>
    <a href="https://arxiv.org/abs/2602.01326"><img src="https://img.shields.io/badge/arXiv-2602.01326-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2602.01326"><img src="https://img.shields.io/badge/AlphaXiv-2602.01326-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/DreamLM/DreamOn"><img src="https://img.shields.io/github/stars/DreamLM/DreamOn?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Zirui Wu, Lin Zheng, Zhihui Xie, Jiacheng Ye, Jiahui Gao, Shansan Gong, Yansong Feng, Zhenguo Li, Wei Bi, Guorui Zhou, Lingpeng Kong

  **TL;DR:** Introduces dynamic length-control states that let code diffusion models autonomously expand or contract the generation canvas, removing the fixed-size-mask limitation and matching oracle-length and autoregressive infilling performance on HumanEval-Infilling and SantaCoder-FIM. ICLR 2026.
  </details>

## Star History

<a href="https://www.star-history.com/?type=date&repos=hasson827%2FAwesome-DLMs-post-training">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=hasson827/Awesome-DLMs-post-training&type=date&theme=dark&legend=top-left&sealed_token=GeI_ZQNY1cDuNBKausNmolsk8mknDemK-I3HQqnimSM7OEDTTIgGKBAGyi04la4onWvP17Kl1lSztgHTXb_Z_jDI-WKFiR4PGD0C_Ow7jaPgrNbzqChD6g" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=hasson827/Awesome-DLMs-post-training&type=date&legend=top-left&sealed_token=GeI_ZQNY1cDuNBKausNmolsk8mknDemK-I3HQqnimSM7OEDTTIgGKBAGyi04la4onWvP17Kl1lSztgHTXb_Z_jDI-WKFiR4PGD0C_Ow7jaPgrNbzqChD6g" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=hasson827/Awesome-DLMs-post-training&type=date&legend=top-left&sealed_token=GeI_ZQNY1cDuNBKausNmolsk8mknDemK-I3HQqnimSM7OEDTTIgGKBAGyi04la4onWvP17Kl1lSztgHTXb_Z_jDI-WKFiR4PGD0C_Ow7jaPgrNbzqChD6g" />
 </picture>
</a>

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for the scope, entry format, and PR process before submitting.

## License

This work is licensed under [CC0-1.0](LICENSE) — free to use, share, and build upon.
