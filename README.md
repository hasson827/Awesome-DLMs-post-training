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
- [SFT & Instruction Tuning](#sft--instruction-tuning) (5)
- [Preference Optimization](#preference-optimization) (3)
- [RL & Reasoning](#rl--reasoning) (32)
- [Safety & Alignment](#safety--alignment) (2)
- [Distillation](#distillation) (14)
- [Inference Acceleration](#inference-acceleration) (11)
- [Training Objectives & Foundations](#training-objectives--foundations) (11)
- [Adaptation Techniques](#adaptation-techniques) (10)
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
    <b>[09/2025] GIFT: Guided Importance-Aware Fine-Tuning for Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2509.20863"><img src="https://img.shields.io/badge/arXiv-2509.20863-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.20863"><img src="https://img.shields.io/badge/AlphaXiv-2509.20863-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Guowei Xu, Wenxin Xu, Jiawang Zhao, Kaisheng Ma

  **TL;DR:** An importance-aware SFT method that identifies and up-weights the key tokens guiding the generation direction, improving fine-tuning consistency of dLLMs that lack precise per-step probability estimates. arXiv 2025.
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

- <details>
  <summary>
    <b>[10/2022] DiffuSeq: Sequence to Sequence Text Generation with Diffusion Models</b>
    <a href="https://arxiv.org/abs/2210.08933"><img src="https://img.shields.io/badge/arXiv-2210.08933-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2210.08933"><img src="https://img.shields.io/badge/AlphaXiv-2210.08933-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/Shark-NLP/DiffuSeq"><img src="https://img.shields.io/github/stars/Shark-NLP/DiffuSeq?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shansan Gong, Mukai Li, Jiangtao Feng, Zhiyong Wu, Lingpeng Kong

  **TL;DR:** Casts conditional seq2seq tasks as conditional fine-tuning of a diffusion model; an early representative of task fine-tuning for text diffusion (pre-LLM scale). ICLR 2023.
  </details>

## Preference Optimization

- <details>
  <summary>
    <b>[10/2025] Aligning Diffusion Language Models via Unpaired Preference Optimization (ELBO-KTO)</b>
    <a href="https://arxiv.org/abs/2510.23658"><img src="https://img.shields.io/badge/arXiv-2510.23658-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.23658"><img src="https://img.shields.io/badge/AlphaXiv-2510.23658-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/vaibhavjindal/elbo-kto"><img src="https://img.shields.io/github/stars/vaibhavjindal/elbo-kto?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Vaibhav Jindal, Hejian Sang, Chun-Mao Lai, Yanning Chen, Zhipeng Wang

  **TL;DR:** Combines an ELBO surrogate for intractable diffusion log-likelihoods with the unpaired, prospect-theoretic KTO objective plus variance-reduction practices, establishing unpaired preference optimization as a viable alternative to pairwise alignment on LLaDA-8B-Instruct. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[05/2025] LLaDA 1.5: Variance-Reduced Preference Optimization for Large Language Diffusion Models (VRPO)</b>
    <a href="https://arxiv.org/abs/2505.19223"><img src="https://img.shields.io/badge/arXiv-2505.19223-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2505.19223"><img src="https://img.shields.io/badge/AlphaXiv-2505.19223-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/ML-GSAI/LLaDA-1.5"><img src="https://img.shields.io/github/stars/ML-GSAI/LLaDA-1.5?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Fengqi Zhu, Rongzhen Wang, Shen Nie, Xiaolu Zhang, Chunwei Wu, Jun Hu, Jun Zhou, Jianfei Chen, Yankai Lin, Ji-Rong Wen, Chongxuan Li

  **TL;DR:** Formally analyzes the variance of ELBO-based likelihood estimates for MDM preference optimization and introduces unbiased variance reduction (optimal Monte Carlo budget allocation, antithetic sampling); the resulting LLaDA 1.5 significantly improves over its SFT-only predecessor on math, code, and alignment benchmarks. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[03/2025] Preference-Based Alignment of Discrete Diffusion Models (D2-DPO)</b>
    <a href="https://arxiv.org/abs/2503.08295"><img src="https://img.shields.io/badge/arXiv-2503.08295-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2503.08295"><img src="https://img.shields.io/badge/AlphaXiv-2503.08295-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Umberto Borso, Davide Paglieri, Jude Wells, Tim Rocktäschel

  **TL;DR:** The first adaptation of DPO to discrete diffusion models formulated as continuous-time Markov chains, deriving a loss that aligns the generative process with preference data while preserving fidelity to a reference distribution, without explicit reward models. arXiv 2025.
  </details>

## RL & Reasoning

- <details>
  <summary>
    <b>[07/2026] Mask-Aware Policy Gradients for Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2607.15200"><img src="https://img.shields.io/badge/arXiv-2607.15200-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2607.15200"><img src="https://img.shields.io/badge/AlphaXiv-2607.15200-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/Haran71/mask-aware-policy-gradients"><img src="https://img.shields.io/github/stars/Haran71/mask-aware-policy-gradients?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Haran Raajesh, Kulin Shah, Adam Klivans, Philipp Krähenbühl

  **TL;DR:** Formalizes MDLM generation as a two-stage action MDP over what tokens to place and which positions to remask, decomposing the policy gradient into token and masking terms; optimizing both yields state-of-the-art results on math reasoning and coding (87.1% GSM8K, 53.4% MBPP). COLM 2026.
  </details>

- <details>
  <summary>
    <b>[07/2026] A Continuous-Time Reinforcement Learning Framework for Fine-Tuning Discrete Diffusion Models</b>
    <a href="https://arxiv.org/abs/2607.14522"><img src="https://img.shields.io/badge/arXiv-2607.14522-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2607.14522"><img src="https://img.shields.io/badge/AlphaXiv-2607.14522-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Zikun Zhang, Jiayuan Sheng, David D. Yao, Wenpin Tang

  **TL;DR:** Formulates RL for discrete diffusion in continuous time via controlled CTMCs, deriving continuous-time PPO/GRPO variants that incorporate intermediate rewards along the denoising trajectory, with tractable policy parameterizations and trajectory subsampling for efficient dLLM post-training on math and code. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[07/2026] SLIM-RL: Risk-Budgeted Random-Masking RL for Diffusion LLMs Without Trajectory Slicing</b>
    <a href="https://arxiv.org/abs/2607.00208"><img src="https://img.shields.io/badge/arXiv-2607.00208-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2607.00208"><img src="https://img.shields.io/badge/AlphaXiv-2607.00208-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Ruikang Zhao, Zhenting Wang, Han Gao, Ligong Han

  **TL;DR:** Addresses TraceRL's trajectory-slicing cost scaling with block size via a τ-budget decoder that bounds commit risk plus a trajectory-free random-masking objective. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[05/2026] Relative Score Policy Optimization for Diffusion Language Models (RSPO)</b>
    <a href="https://arxiv.org/abs/2605.10218"><img src="https://img.shields.io/badge/arXiv-2605.10218-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.10218"><img src="https://img.shields.io/badge/AlphaXiv-2605.10218-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Zichao Yu, Shengze Xu, Bingqing Jiang, Wenyi Zhang, Difan Zou

  **TL;DR:** Replaces intractable likelihoods with relative scores for group-based policy optimization of diffusion language models. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[05/2026] DACA-GRPO: Denoising-Aware Credit Assignment for Reinforcement Learning in Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2605.16342"><img src="https://img.shields.io/badge/arXiv-2605.16342-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.16342"><img src="https://img.shields.io/badge/AlphaXiv-2605.16342-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Amin Karimi Monsefi, Dominic Culver, Nikhil Bhendawade, Lokesh Boominathan, Manuel R. Ciosici, Yizhe Zhang, Irina Belousova

  **TL;DR:** A plug-and-play GRPO enhancement tackling missing temporal credit assignment and mean-field likelihood bias via Denoising Progress Scores and Stratified Masking Likelihood, consistently improving three GRPO base methods across seven math, code, and constraint-satisfaction benchmarks. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[03/2026] Reinforcement Learning for Diffusion LLMs with Entropy-Guided Step Selection and Stepwise Advantages (EGSPO)</b>
    <a href="https://arxiv.org/abs/2603.12554"><img src="https://img.shields.io/badge/arXiv-2603.12554-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2603.12554"><img src="https://img.shields.io/badge/AlphaXiv-2603.12554-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/vishnutez/egspo-dllm-rl"><img src="https://img.shields.io/github/stars/vishnutez/egspo-dllm-rl?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Vishnu Teja Kunde, Fatemeh Doudi, Mahdi Farahbakhsh, Dileep Kalathil, Krishna Narayanan, Jean-Francois Chamberland

  **TL;DR:** Entropy-guided selection of critical denoising steps combined with stepwise advantages, reducing the variance and cost of dLLM RL. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[03/2026] LFPO: Likelihood-Free Policy Optimization for Masked Diffusion Models</b>
    <a href="https://arxiv.org/abs/2603.01563"><img src="https://img.shields.io/badge/arXiv-2603.01563-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2603.01563"><img src="https://img.shields.io/badge/AlphaXiv-2603.01563-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Chenxing Wei, Jiazhen Kang, Hong Wang, Jianqing Zhang, Hao Jiang, Xiaolong Xu, Ningyuan Sun, Ying He, F. Richard Yu, Yao Shu, Bo Jiang

  **TL;DR:** A fully likelihood-free RLVR policy optimization method that sidesteps the high-variance likelihood approximations of prior dLLM RL approaches. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[02/2026] Diffusion-State Policy Optimization for Masked Diffusion Language Models (DiSPO)</b>
    <a href="https://arxiv.org/abs/2602.06462"><img src="https://img.shields.io/badge/arXiv-2602.06462-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2602.06462"><img src="https://img.shields.io/badge/AlphaXiv-2602.06462-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Daisuke Oba, Hiroki Furuta, Naoaki Okazaki

  **TL;DR:** A plug-in credit-assignment layer that branches at intermediate masked states from rollout-cached logits and updates only newly filled tokens, consistently improving terminal-feedback baselines such as diffu-GRPO and SPG on math and planning under matched rollout compute. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[01/2026] The Flexibility Trap: Rethinking the Value of Arbitrary Order in Diffusion Language Models (JustGRPO)</b>
    <a href="https://arxiv.org/abs/2601.15165"><img src="https://img.shields.io/badge/arXiv-2601.15165-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2601.15165"><img src="https://img.shields.io/badge/AlphaXiv-2601.15165-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/LeapLabTHU/JustGRPO"><img src="https://img.shields.io/github/stars/LeapLabTHU/JustGRPO?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Zanlin Ni, Shenzhi Wang, Yang Yue, Tianyu Yu, Weilin Zhao, Yeguo Hua, Tianyi Chen, Jun Song, Cheng Yu, Bo Zheng, Gao Huang

  **TL;DR:** Argues that arbitrary-order flexibility is not necessary: a straightforward GRPO transplant matches complex diffusion-specific RL modifications (using ESPO as the comparison baseline). arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[01/2026] T\*: Progressive Block Scaling for Masked Diffusion Language Models Through Trajectory Aware Reinforcement Learning</b>
    <a href="https://arxiv.org/abs/2601.11214"><img src="https://img.shields.io/badge/arXiv-2601.11214-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2601.11214"><img src="https://img.shields.io/badge/AlphaXiv-2601.11214-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Hanchen Xia, Baoyou Chen, Yutang Ge, Guojiang Zhao, Siyu Zhu

  **TL;DR:** A curriculum-style progressive block-size scaling training scheme built on TraceRL for masked diffusion language models. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[12/2025] dUltra: Ultra-Fast Diffusion Large Language Models via Reinforcement Learning</b>
    <a href="https://arxiv.org/abs/2512.21446"><img src="https://img.shields.io/badge/arXiv-2512.21446-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2512.21446"><img src="https://img.shields.io/badge/AlphaXiv-2512.21446-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/chinsengi/dUltra-os"><img src="https://img.shields.io/github/stars/chinsengi/dUltra-os?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shirui Chen, Jiantao Jiao, Lillian J. Ratliff, Banghua Zhu

  **TL;DR:** Uses GRPO to learn a "path planner" over unmasking order and parallelism, greatly accelerating diffusion LLM decoding while preserving quality. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[12/2025] d-TreeRPO: Towards More Reliable Policy Optimization for Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2512.09675"><img src="https://img.shields.io/badge/arXiv-2512.09675-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2512.09675"><img src="https://img.shields.io/badge/AlphaXiv-2512.09675-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/THU-BPM/d-TreeRPO"><img src="https://img.shields.io/github/stars/THU-BPM/d-TreeRPO?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Leyi Pan, Shuchang Tao, Yunpeng Zhai, Zheyu Fu, Liancheng Fang, Minghua He, Lingzhe Zhang, Zhaoyang Liu, Bolin Ding, Aiwei Liu, Lijie Wen

  **TL;DR:** Tree-structured grouping and rollout organization improves the reliability of dLLM policy optimization. ACL 2026 Main.
  </details>

- <details>
  <summary>
    <b>[12/2025] Learning Unmasking Policies for Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2512.09106"><img src="https://img.shields.io/badge/arXiv-2512.09106-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2512.09106"><img src="https://img.shields.io/badge/AlphaXiv-2512.09106-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/apple/ml-rl-dllm"><img src="https://img.shields.io/github/stars/apple/ml-rl-dllm?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Metod Jazbec, Theo X. Olausson, Louis Béthune, Pierre Ablin, Michael Kirchhof, João Monteiro, Victor Turrisi, Jason Ramapuram, Marco Cuturi

  **TL;DR:** Uses RL to learn a standalone unmasking-order policy module instead of fixed confidence-based sampling, in the lineage of DCoLT/UPM. ICML 2026 (oral spotlight).
  </details>

- <details>
  <summary>
    <b>[12/2025] Principled RL for Diffusion LLMs Emerges from a Sequence-Level Perspective (ESPO)</b>
    <a href="https://arxiv.org/abs/2512.03759"><img src="https://img.shields.io/badge/arXiv-2512.03759-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2512.03759"><img src="https://img.shields.io/badge/AlphaXiv-2512.03759-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/ML-GSAI/ESPO"><img src="https://img.shields.io/github/stars/ML-GSAI/ESPO?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Jingyang Ou, Jiaqi Han, Minkai Xu, Shaoxuan Xu, Jianwen Xie, Stefano Ermon, Yi Wu, Chongxuan Li

  **TL;DR:** Treats the entire sequence generation as a single action, using the ELBO as a sequence-level likelihood surrogate with per-token normalized importance ratios; +20–40 points over token-level baselines on Countdown. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[10/2025] MRO: Enhancing Reasoning in Diffusion Language Models via Multi-Reward Optimization</b>
    <a href="https://arxiv.org/abs/2510.21473"><img src="https://img.shields.io/badge/arXiv-2510.21473-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.21473"><img src="https://img.shields.io/badge/AlphaXiv-2510.21473-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Chenglong Wang, Yang Gan, Hang Zhou, Chi Hu, Yongyu Mu, Kai Song, Murun Yang, Bei Li, Chunliang Zhang, Tongran Liu, Jingbo Zhu, Zhengtao Yu, Tong Xiao

  **TL;DR:** Joint multi-reward optimization to improve dLLM reasoning. NeurIPS 2025.
  </details>

- <details>
  <summary>
    <b>[10/2025] Boundary-Guided Policy Optimization for Memory-Efficient RL of Diffusion Large Language Models (BGPO)</b>
    <a href="https://arxiv.org/abs/2510.11683"><img src="https://img.shields.io/badge/arXiv-2510.11683-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.11683"><img src="https://img.shields.io/badge/AlphaXiv-2510.11683-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/THU-KEG/BGPO"><img src="https://img.shields.io/github/stars/THU-KEG/BGPO?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Nianyi Lin, Jiajie Zhang, Lei Hou, Juanzi Li

  **TL;DR:** Exploits the boundary structure of block diffusion to maximize a linear lower bound of the ELBO, significantly reducing RL training memory. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[10/2025] SPG: Sandwiched Policy Gradient for Masked Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2510.09541"><img src="https://img.shields.io/badge/arXiv-2510.09541-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.09541"><img src="https://img.shields.io/badge/AlphaXiv-2510.09541-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/facebookresearch/SPG"><img src="https://img.shields.io/github/stars/facebookresearch/SPG?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Chenyu Wang, Paria Rashidinejad, DiJia Su, Song Jiang, Sid Wang, Siyan Zhao, Cai Zhou, Shannon Zejiang Shen, Feiyu Chen, Tommi Jaakkola, Yuandong Tian, Bo Liu

  **TL;DR:** Constructs a "sandwich" objective from log-likelihood upper and lower bounds for policy gradients, significantly outperforming ELBO-based methods (d1/wd1). ICLR 2026.
  </details>

- <details>
  <summary>
    <b>[10/2025] Improving Reasoning for Diffusion Language Models via Group Diffusion Policy Optimization (GDPO)</b>
    <a href="https://arxiv.org/abs/2510.08554"><img src="https://img.shields.io/badge/arXiv-2510.08554-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.08554"><img src="https://img.shields.io/badge/AlphaXiv-2510.08554-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Kevin Rojas, Jiahe Lin, Kashif Rasul, Anderson Schneider, Yuriy Nevmyvaka, Molei Tao, Wei Deng

  **TL;DR:** A diffusion adaptation of GRPO that improves how group-relative advantages are assigned across denoising steps, surpassing diffu-GRPO. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[10/2025] Enhancing Reasoning for Diffusion LLMs via Distribution Matching Policy Optimization (DMPO)</b>
    <a href="https://arxiv.org/abs/2510.08233"><img src="https://img.shields.io/badge/arXiv-2510.08233-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.08233"><img src="https://img.shields.io/badge/AlphaXiv-2510.08233-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/yuchen-zhu-zyc/DMPO"><img src="https://img.shields.io/github/stars/yuchen-zhu-zyc/DMPO?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Yuchen Zhu, Wei Guo, Jaemoo Choi, Petr Molodyk, Bo Yuan, Molei Tao, Yongxin Chen

  **TL;DR:** Formulates RL as a distribution matching problem, avoiding direct estimation of intractable likelihoods. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[10/2025] Simple Policy Gradients for Reasoning with Diffusion Language Models (AGRPO)</b>
    <a href="https://arxiv.org/abs/2510.04019"><img src="https://img.shields.io/badge/arXiv-2510.04019-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.04019"><img src="https://img.shields.io/badge/AlphaXiv-2510.04019-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/probablyabot/agrpo"><img src="https://img.shields.io/github/stars/probablyabot/agrpo?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Anthony Zhan

  **TL;DR:** Amortized Group Relative Policy Optimization leverages the Markovian nature of dLLMs, optimizing individual denoising steps rather than full sequences and avoiding biased sequence-level likelihood approximations. ICML 2026.
  </details>

- <details>
  <summary>
    <b>[10/2025] Consolidating Reinforcement Learning for Multimodal Discrete Diffusion Models (MaskGRPO)</b>
    <a href="https://arxiv.org/abs/2510.02880"><img src="https://img.shields.io/badge/arXiv-2510.02880-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.02880"><img src="https://img.shields.io/badge/AlphaXiv-2510.02880-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/martian422/MaskGRPO"><img src="https://img.shields.io/github/stars/martian422/MaskGRPO?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Tianren Ma, Mu Zhang, Yibing Wang, Qixiang Ye

  **TL;DR:** A unified GRPO training framework consolidating RL for LLaDA/MMaDA-style multimodal discrete diffusion models. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[10/2025] Advancing Reasoning in Diffusion Language Models with Denoising Process Rewards</b>
    <a href="https://arxiv.org/abs/2510.01544"><img src="https://img.shields.io/badge/arXiv-2510.01544-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.01544"><img src="https://img.shields.io/badge/AlphaXiv-2510.01544-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Shaoan Xie, Lingjing Kong, Xiangchen Song, Xinshuai Dong, Guangyi Chen, Eric P. Xing, Kun Zhang

  **TL;DR:** Introduces denoising-process rewards that directly supervise intermediate denoising steps, guiding dLLMs toward progressively better-structured reasoning instead of outcome-only rewards. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[10/2025] DiFFPO: Training Diffusion LLMs to Reason Fast and Furious via Reinforcement Learning</b>
    <a href="https://arxiv.org/abs/2510.02212"><img src="https://img.shields.io/badge/arXiv-2510.02212-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.02212"><img src="https://img.shields.io/badge/AlphaXiv-2510.02212-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Hanyang Zhao, Dawen Liang, Wenpin Tang, David Yao, Nathan Kallus

  **TL;DR:** A unified RL framework that jointly trains the model and the sampler policy, improving both reasoning accuracy and latency and pushing the accuracy/compute Pareto frontier. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[09/2025] Taming Masked Diffusion Language Models via Consistency Trajectory Reinforcement Learning with Fewer Decoding Steps (CJ-GRPO)</b>
    <a href="https://arxiv.org/abs/2509.23924"><img src="https://img.shields.io/badge/arXiv-2509.23924-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.23924"><img src="https://img.shields.io/badge/AlphaXiv-2509.23924-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/yjyddq/EOSER-ASS-RL"><img src="https://img.shields.io/github/stars/yjyddq/EOSER-ASS-RL?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Jingyi Yang, Guanxu Chen, Xuhao Hu, Jing Shao

  **TL;DR:** Enforces consistency between rollout and optimization trajectories, resolving the train-inference mismatch between MDLM non-causal decoding and AR-style RL. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[09/2025] Inpainting-Guided Policy Optimization for Diffusion Large Language Models (IGPO)</b>
    <a href="https://arxiv.org/abs/2509.10396"><img src="https://img.shields.io/badge/arXiv-2509.10396-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.10396"><img src="https://img.shields.io/badge/AlphaXiv-2509.10396-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/facebookresearch/igpo"><img src="https://img.shields.io/github/stars/facebookresearch/igpo?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Siyan Zhao, Mengchen Liu, Jing Huang, Miao Liu, Chenyu Wang, Bo Liu, Yuandong Tian, Guan Pang, Sean Bell, Aditya Grover, Feiyu Chen

  **TL;DR:** Leverages the partial inpainting ability of diffusion models to inject partial ground-truth answer fragments into rollouts, easing exploration under sparse rewards. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[09/2025] Revolutionizing Reinforcement Learning Framework for Diffusion Large Language Models (TraceRL / TraDo)</b>
    <a href="https://arxiv.org/abs/2509.06949"><img src="https://img.shields.io/badge/arXiv-2509.06949-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.06949"><img src="https://img.shields.io/badge/AlphaXiv-2509.06949-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/Gen-Verse/dLLM-RL"><img src="https://img.shields.io/github/stars/Gen-Verse/dLLM-RL?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Yinjie Wang, Ling Yang, Bowen Li, Ye Tian, Ke Shen, Mengdi Wang

  **TL;DR:** Trajectory-aware RL aligning the training objective with the model's actual inference trajectory, with a diffusion value model for variance reduction; yields TraDo-4B/8B and the first long-CoT diffusion model TraDo-8B-Thinking. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[08/2025] MDPO: Overcoming the Training-Inference Divide of Masked Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2508.13148"><img src="https://img.shields.io/badge/arXiv-2508.13148-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2508.13148"><img src="https://img.shields.io/badge/AlphaXiv-2508.13148-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/autonomousvision/mdpo"><img src="https://img.shields.io/github/stars/autonomousvision/mdpo?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Haoyu He, Katrin Renz, Yong Cao, Andreas Geiger

  **TL;DR:** Optimizes the policy following the progressive refinement schedule used at inference, bridging the MDLM training-inference gap. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[07/2025] wd1: Weighted Policy Optimization for Reasoning in Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2507.08838"><img src="https://img.shields.io/badge/arXiv-2507.08838-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2507.08838"><img src="https://img.shields.io/badge/AlphaXiv-2507.08838-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/xiaohangt/wd1"><img src="https://img.shields.io/github/stars/xiaohangt/wd1?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Xiaohang Tang, Rares Dolga, Sangwoong Yoon, Ilija Bogunovic

  **TL;DR:** Reweights low-advantage samples instead of discarding them, improving diffu-GRPO's sample efficiency and compute cost; surpasses d1 on GSM8K/MATH/Sudoku/Countdown. ICLR 2026.
  </details>

- <details>
  <summary>
    <b>[05/2025] Reinforcing the Diffusion Chain of Lateral Thought with Diffusion Language Models (DCoLT)</b>
    <a href="https://arxiv.org/abs/2505.10446"><img src="https://img.shields.io/badge/arXiv-2505.10446-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2505.10446"><img src="https://img.shields.io/badge/AlphaXiv-2505.10446-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/maple-research-lab/LLaDOU"><img src="https://img.shields.io/github/stars/maple-research-lab/LLaDOU?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Zemin Huang, Zhiyang Chen, Zijun Wang, Tiancheng Li, Guo-Jun Qi

  **TL;DR:** Treats intermediate reverse-sampling steps as "thinking actions" and optimizes the entire denoising trajectory with outcome-reward RL; proposes the Unmask Policy Module on LLaDA with Plackett-Luce modeling of unmasking order. NeurIPS 2025.
  </details>

- <details>
  <summary>
    <b>[04/2025] d1: Scaling Reasoning in Diffusion Large Language Models via Reinforcement Learning</b>
    <a href="https://arxiv.org/abs/2504.12216"><img src="https://img.shields.io/badge/arXiv-2504.12216-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2504.12216"><img src="https://img.shields.io/badge/AlphaXiv-2504.12216-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/dllm-reasoning/d1"><img src="https://img.shields.io/github/stars/dllm-reasoning/d1?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Siyan Zhao, Devaansh Gupta, Qinqing Zheng, Aditya Grover

  **TL;DR:** Proposes diffu-GRPO, using mean-field approximation and random prompt masking to estimate sequence/token log-probabilities in a single forward pass; a two-stage SFT+RL recipe greatly improves LLaDA's math/planning reasoning — a foundational work of dLLM RL. NeurIPS 2025.
  </details>

- <details>
  <summary>
    <b>[02/2025] Fine-Tuning Discrete Diffusion Models with Policy Gradient Methods (SEPO)</b>
    <a href="https://arxiv.org/abs/2502.01384"><img src="https://img.shields.io/badge/arXiv-2502.01384-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2502.01384"><img src="https://img.shields.io/badge/AlphaXiv-2502.01384-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/ozekri/SEPO"><img src="https://img.shields.io/github/stars/ozekri/SEPO?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Oussama Zekri, Nicolas Boullé

  **TL;DR:** An early systematic application of policy gradient methods to fine-tune discrete diffusion models. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[10/2024] DRAKES: Fine-Tuning Discrete Diffusion Models via Reward Optimization with Applications to DNA and Protein Design</b>
    <a href="https://arxiv.org/abs/2410.13643"><img src="https://img.shields.io/badge/arXiv-2410.13643-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2410.13643"><img src="https://img.shields.io/badge/AlphaXiv-2410.13643-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/ChenyuWang-Monica/DRAKES"><img src="https://img.shields.io/github/stars/ChenyuWang-Monica/DRAKES?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Chenyu Wang, Masatoshi Uehara, Yichun He, Amy Wang, Tommaso Biancalani, Avantika Lal, Tommi Jaakkola, Sergey Levine, Hanchen Wang, Aviv Regev

  **TL;DR:** A reward fine-tuning framework that backpropagates rewards through the entire reverse chain of discrete diffusion, demonstrated on DNA/protein design and directly applicable to text MDMs. ICLR 2025.
  </details>

## Safety & Alignment

- <details>
  <summary>
    <b>[09/2025] A2D: Any-Order, Any-Step Safety Alignment for Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2509.23286"><img src="https://img.shields.io/badge/arXiv-2509.23286-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.23286"><img src="https://img.shields.io/badge/AlphaXiv-2509.23286-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Wonje Jeung, Sangyeon Yoon, Yoonjun Cho, Dongjae Jeon, Sangwoo Shin, Hyesoo Hong, Albert No

  **TL;DR:** A safety alignment method tailored to dLLMs' any-order, any-step decoding, mitigating their unique jailbreak vulnerabilities. ICLR 2026.
  </details>

- <details>
  <summary>
    <b>[08/2025] Where to Start Alignment? Diffusion Large Language Model May Demand a Distinct Position</b>
    <a href="https://arxiv.org/abs/2508.12398"><img src="https://img.shields.io/badge/arXiv-2508.12398-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2508.12398"><img src="https://img.shields.io/badge/AlphaXiv-2508.12398-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Zhixin Xie, Xurui Song, Jun Luo

  **TL;DR:** An analytical work showing that the alignment starting point and data position for dLLMs is fundamentally different from AR models, providing design guidance for dLLM alignment. AAAI 2026 (oral).
  </details>

## Distillation

- <details>
  <summary>
    <b>[07/2026] dOPSD: On-Policy Self-Distillation for Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2607.04428"><img src="https://img.shields.io/badge/arXiv-2607.04428-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2607.04428"><img src="https://img.shields.io/badge/AlphaXiv-2607.04428-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Phuong Tuan Dat, Qi Li, Xinchao Wang

  **TL;DR:** Derives the teacher's privilege signal directly from the student's own denoising trajectory for on-policy self-distillation of dLLMs, addressing SFT's exposure bias and RL's sparse sequence-level rewards. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[06/2026] Learning from the Self-future: On-policy Self-distillation for dLLMs (d-OPSD)</b>
    <a href="https://arxiv.org/abs/2606.18195"><img src="https://img.shields.io/badge/arXiv-2606.18195-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2606.18195"><img src="https://img.shields.io/badge/AlphaXiv-2606.18195-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/xingzhejun/d-opsd-code"><img src="https://img.shields.io/github/stars/xingzhejun/d-opsd-code?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Yifu Luo, Zeyu Chen, Haoyu Wang, Xinhao Hu, Yuxuan Zhang, Zhizhou Sha, Shiwei Liu

  **TL;DR:** The first on-policy self-distillation framework tailored for dLLMs, reframing self-teacher construction via self-generated answers as suffix conditioning so the student learns from its "self future-experience". arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[05/2026] DiLaDiff: Distilled Latent-Augmented Diffusion for Language Modeling</b>
    <a href="https://arxiv.org/abs/2605.23605"><img src="https://img.shields.io/badge/arXiv-2605.23605-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.23605"><img src="https://img.shields.io/badge/AlphaXiv-2605.23605-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Jean-Marie Lemercier, Tomas Geffner, Karsten Kreis, Morteza Mardani, Arash Vahdat, Ante Jukić

  **TL;DR:** A distilled latent-augmented diffusion language model for accelerated generation. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[05/2026] Self-Distilled Trajectory-Aware Boltzmann Modeling: Bridging the Training-Inference Discrepancy in Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2605.11854"><img src="https://img.shields.io/badge/arXiv-2605.11854-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.11854"><img src="https://img.shields.io/badge/AlphaXiv-2605.11854-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Kecheng Chen, Ziru Liu, Xijia Tao, Hui Liu, Yibing Liu, Xinyu Fu, Shi Wu, Suiyun Zhang, Dandan Tu, Lingpeng Kong, Rui Liu, Haoliang Li

  **TL;DR:** Self-distillation plus trajectory-aware Boltzmann modeling to bridge the DLM training-inference discrepancy. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[05/2026] Infinite Mask Diffusion for Few-Step Distillation (IMDM)</b>
    <a href="https://arxiv.org/abs/2605.10518"><img src="https://img.shields.io/badge/arXiv-2605.10518-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.10518"><img src="https://img.shields.io/badge/AlphaXiv-2605.10518-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Jaehoon Yoo, Wonjung Kim, Chanhyuk Lee, Seunghoon Hong

  **TL;DR:** An infinite-mask diffusion distillation framework enabling few-step sampling. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[05/2026] TAD: Temporal-Aware Trajectory Self-Distillation for Fast and Accurate Diffusion LLM</b>
    <a href="https://arxiv.org/abs/2605.09536"><img src="https://img.shields.io/badge/arXiv-2605.09536-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.09536"><img src="https://img.shields.io/badge/AlphaXiv-2605.09536-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/BHmingyang/TAD"><img src="https://img.shields.io/github/stars/BHmingyang/TAD?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Haoyang Zhou, Li Kong, Shijie Ren, Xiting Wang, Shuang Liang, Guowei Wang, Zhenxuan Pan

  **TL;DR:** Temporal-aware trajectory self-distillation that accelerates dLLM sampling while preserving accuracy. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[04/2026] Consistent Diffusion Language Models (Multi-Path Consistency)</b>
    <a href="https://arxiv.org/abs/2605.00161"><img src="https://img.shields.io/badge/arXiv-2605.00161-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.00161"><img src="https://img.shields.io/badge/AlphaXiv-2605.00161-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Hasan Amin, Yuan Gao, Yaser Souri, Subhojit Som, Ming Yin, Rajiv Khanna, Xia Song

  **TL;DR:** Proposes a multi-path consistency principle for training discrete diffusion language models toward consistent few-step generation. ICML 2026.
  </details>

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

- <details>
  <summary>
    <b>[04/2026] FlowLM: Few-Step Language Modeling via Diffusion-to-Flow Adaptation</b>
    <a href="https://arxiv.org/abs/2605.20199"><img src="https://img.shields.io/badge/arXiv-2605.20199-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.20199"><img src="https://img.shields.io/badge/AlphaXiv-2605.20199-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Runzhe Zhang, Letian Chen, Wenpeng Zhang, Zhouhan Lin, Peilin Zhao

  **TL;DR:** Transforms pretrained diffusion LMs into flow-matching models via efficient fine-tuning, re-aligning curved sampling trajectories into straight-line flows for high-quality few-step generation. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[01/2026] d3LLM: Ultra-Fast Diffusion LLM using Pseudo-Trajectory Distillation</b>
    <a href="https://arxiv.org/abs/2601.07568"><img src="https://img.shields.io/badge/arXiv-2601.07568-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2601.07568"><img src="https://img.shields.io/badge/AlphaXiv-2601.07568-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/hao-ai-lab/d3LLM"><img src="https://img.shields.io/github/stars/hao-ai-lab/d3LLM?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Yu-Yang Qian, Junda Su, Lanxiang Hu, Peiyuan Zhang, Zhijie Deng, Peng Zhao, Hao Zhang

  **TL;DR:** Pseudo-trajectory distillation teaches the model which tokens can be confidently decoded at early steps; combined with entropy-based multi-block decoding and KV-cache refresh, up to 10× speedup on LLaDA/Dream. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[01/2026] CD4LM: Consistency Distillation and aDaptive Decoding for Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2601.02236"><img src="https://img.shields.io/badge/arXiv-2601.02236-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2601.02236"><img src="https://img.shields.io/badge/AlphaXiv-2601.02236-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/yihao-liang/CDLM"><img src="https://img.shields.io/github/stars/yihao-liang/CDLM?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Yihao Liang, Ze Wang, Hao Chen, Ximeng Sun, Jialian Wu, Xiaodong Yu, Jiang Liu, Emad Barsoum, Zicheng Liu, Niraj K. Jha

  **TL;DR:** Discrete-space consistency distillation trains a trajectory-invariant student; with confidence-adaptive decoding skips, 5.18× speedup on GSM8K while strictly dominating the accuracy-efficiency Pareto frontier. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[11/2025] CDLM: Consistency Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2511.19269"><img src="https://img.shields.io/badge/arXiv-2511.19269-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2511.19269"><img src="https://img.shields.io/badge/AlphaXiv-2511.19269-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/SqueezeAILab/CDLM"><img src="https://img.shields.io/github/stars/SqueezeAILab/CDLM?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Minseo Kim, Chenfeng Xu, Coleman Hooper, Harman Singh, Ben Athiwaratkun, Ce Zhang, Kurt Keutzer, Amir Gholami

  **TL;DR:** Brings consistency modeling into DLM training, distilling a full bidirectional teacher and aligning predictions along the decoding trajectory; block-wise causal attention enables KV cache, reducing latency 3.6–14.5×. MLSys 2026.
  </details>

- <details>
  <summary>
    <b>[09/2025] dParallel: Learnable Parallel Decoding for dLLMs</b>
    <a href="https://arxiv.org/abs/2509.26488"><img src="https://img.shields.io/badge/arXiv-2509.26488-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.26488"><img src="https://img.shields.io/badge/AlphaXiv-2509.26488-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/czg1225/dParallel"><img src="https://img.shields.io/github/stars/czg1225/dParallel?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Zigeng Chen, Gongfan Fang, Xinyin Ma, Ruonan Yu, Xinchao Wang

  **TL;DR:** Certainty-forcing distillation fine-tunes on self-generated trajectories so masked tokens reach high confidence in parallel faster; 256→30 steps on GSM8K, 8.5× speedup. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[09/2025] Ultra-Fast Language Generation via Discrete Diffusion Divergence Instruct (DiDi-Instruct)</b>
    <a href="https://arxiv.org/abs/2509.25035"><img src="https://img.shields.io/badge/arXiv-2509.25035-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.25035"><img src="https://img.shields.io/badge/AlphaXiv-2509.25035-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/haoyangzheng-ai/didi-instruct"><img src="https://img.shields.io/github/stars/haoyangzheng-ai/didi-instruct?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Haoyang Zheng, Xinyang Liu, Cindy Xiangrui Kong, Nan Jiang, Zheyuan Hu, Weijian Luo, Wei Deng, Guang Lin

  **TL;DR:** Distribution-matching distillation based on integral KL divergence minimization, distilling a dLLM teacher into an 8–16-step few-step student; 64× speedup while surpassing the teacher. ICLR 2026.
  </details>

## Inference Acceleration

- <details>
  <summary>
    <b>[05/2026] Revise, Don't Freeze: Sampler-Matched Training for Self-Correcting Masked Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2606.01026"><img src="https://img.shields.io/badge/arXiv-2606.01026-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2606.01026"><img src="https://img.shields.io/badge/AlphaXiv-2606.01026-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Longxuan Yu, Shaorong Zhang, Yu Fu, Hui Liu, Yue Dong, Greg Ver Steeg

  **TL;DR:** Proposes D3IM, a sampler requiring no additional modules, and SCOPE, a lightweight sampler-matched post-training method for self-correcting MDLMs, improving math and code generation. arXiv 2026.
  </details>

- <details>
  <summary>
    <b>[05/2026] EPIC: Efficient and Parallel Inference under CFG Constraints for Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2606.00722"><img src="https://img.shields.io/badge/arXiv-2606.00722-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2606.00722"><img src="https://img.shields.io/badge/AlphaXiv-2606.00722-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/hyundong98/EPIC-Decoding"><img src="https://img.shields.io/github/stars/hyundong98/EPIC-Decoding?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Hyundong Jin, Yo-Sub Han

  **TL;DR:** Efficient parallel inference under context-free-grammar (CFG) constrained decoding for dLLMs. arXiv 2026.
  </details>

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
    <b>[05/2026] Guidance Is Not a Hyperparameter: Learning Dynamic Control in Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2605.07701"><img src="https://img.shields.io/badge/arXiv-2605.07701-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2605.07701"><img src="https://img.shields.io/badge/AlphaXiv-2605.07701-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Fan Zhou, Tim Van de Cruys

  **TL;DR:** Turns guidance strength from a hand-tuned hyperparameter into a learnable dynamic control signal during training. ICLR 2026 ReALM-GEN Workshop.
  </details>

- <details>
  <summary>
    <b>[10/2025] Self-Speculative Decoding for Diffusion Large Language Models (SSD)</b>
    <a href="https://arxiv.org/abs/2510.04147"><img src="https://img.shields.io/badge/arXiv-2510.04147-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.04147"><img src="https://img.shields.io/badge/AlphaXiv-2510.04147-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Yifeng Gao, Ziang Ji, Yuxuan Wang, Biqing Qi, Hanlin Xu, Linfeng Zhang

  **TL;DR:** The dLLM itself acts as both drafter and verifier; a hierarchical verification tree validates multiple tokens in a single forward pass for 3.46× lossless speedup. arXiv 2025.
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

- <details>
  <summary>
    <b>[09/2025] Learning to Parallel: Accelerating Diffusion Large Language Models via Learnable Parallel Decoding (Learn2PD)</b>
    <a href="https://arxiv.org/abs/2509.25188"><img src="https://img.shields.io/badge/arXiv-2509.25188-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.25188"><img src="https://img.shields.io/badge/AlphaXiv-2509.25188-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/ims-kdks/Learning-to-Parallel-Decoding"><img src="https://img.shields.io/github/stars/ims-kdks/Learning-to-Parallel-Decoding?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Wenrui Bao, Zhiben Chen, Dan Xu, Yuzhang Shang

  **TL;DR:** Post-trains a lightweight filter model to predict whether each position's token matches the final output, approximating an oracle parallel-decoding policy; up to 22.58× lossless speedup on LLaDA (57.51× with KV cache). arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[09/2025] Structuring the Future: Diffusion LLM Speculative Decoding via Calibrated Draft Graphs (Spiffy)</b>
    <a href="https://arxiv.org/abs/2509.18085"><img src="https://img.shields.io/badge/arXiv-2509.18085-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2509.18085"><img src="https://img.shields.io/badge/AlphaXiv-2509.18085-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Sudhanshu Agrawal, Risheek Garrepalli, Raghavv Goel, Christopher Lott, Fatih Porikli, Mingu Lee

  **TL;DR:** Auto-speculation speculative decoding designed for dLLMs: offline-calibrated directed draft graphs plus block-wise bidirectional generation; up to 6.3× lossless speedup on LLaDA/Dream/SDAR. ICML 2026 Workshop.
  </details>

- <details>
  <summary>
    <b>[05/2025] Fast-dLLM: Training-free Acceleration of Diffusion LLM by Enabling KV Cache and Parallel Decoding</b>
    <a href="https://arxiv.org/abs/2505.22618"><img src="https://img.shields.io/badge/arXiv-2505.22618-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2505.22618"><img src="https://img.shields.io/badge/AlphaXiv-2505.22618-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/NVlabs/Fast-dLLM"><img src="https://img.shields.io/github/stars/NVlabs/Fast-dLLM?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Chengyue Wu, Hao Zhang, Shuchen Xue, Zhijian Liu, Shizhe Diao, Ligeng Zhu, Ping Luo, Song Han, Enze Xie

  **TL;DR:** Block-wise approximate KV cache plus confidence-aware parallel decoding, up to 27.6× throughput on LLaDA/Dream; training-free and a foundational work of the confidence-aware decoding lineage. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[05/2025] Adaptive Classifier-Free Guidance via Dynamic Low-Confidence Masking (A-CFG)</b>
    <a href="https://arxiv.org/abs/2505.20199"><img src="https://img.shields.io/badge/arXiv-2505.20199-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2505.20199"><img src="https://img.shields.io/badge/AlphaXiv-2505.20199-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/pixeli99/A-CFG"><img src="https://img.shields.io/github/stars/pixeli99/A-CFG?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Pengxiang Li, Shilin Yan, Joey Tsai, Renrui Zhang, Ruichuan An, Ziyu Guo, Xiaowei Gao

  **TL;DR:** Adaptive classifier-free guidance that dynamically masks low-confidence tokens for guided dLLM decoding. arXiv 2025.
  </details>

- <details>
  <summary>
    <b>[12/2024] Simple Guidance Mechanisms for Discrete Diffusion Models</b>
    <a href="https://arxiv.org/abs/2412.10193"><img src="https://img.shields.io/badge/arXiv-2412.10193-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2412.10193"><img src="https://img.shields.io/badge/AlphaXiv-2412.10193-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/kuleshov-group/discrete-diffusion-guidance"><img src="https://img.shields.io/github/stars/kuleshov-group/discrete-diffusion-guidance?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Yair Schiff, Subham Sekhar Sahoo, Hao Phung, Guanghan Wang, Sam Boshar, Hugo Dalla-torre, Bernardo P. de Almeida, Alexander Rush, Thomas Pierrot, Volodymyr Kuleshov

  **TL;DR:** The first systematic derivation of classifier-free and classifier-based guidance for discrete diffusion, plus a more guidable uniform-noise diffusion model. ICLR 2025.
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

- <details>
  <summary>
    <b>[03/2025] Block Diffusion: Interpolating Between Autoregressive and Diffusion Language Models (BD3-LM)</b>
    <a href="https://arxiv.org/abs/2503.09573"><img src="https://img.shields.io/badge/arXiv-2503.09573-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2503.09573"><img src="https://img.shields.io/badge/AlphaXiv-2503.09573-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/kuleshov-group/bd3lms"><img src="https://img.shields.io/github/stars/kuleshov-group/bd3lms?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Marianne Arriola, Aaron Gokaslan, Justin T. Chiu, Zhihan Yang, Zhixuan Qi, Jiaqi Han, Subham Sekhar Sahoo, Volodymyr Kuleshov

  **TL;DR:** A hybrid training objective of block-level autoregression plus intra-block diffusion, enabling arbitrary-length generation and KV cache, alleviating the fixed-length limit of discrete diffusion. ICLR 2025 Oral.
  </details>

- <details>
  <summary>
    <b>[10/2024] Beyond Autoregression: Discrete Diffusion for Complex Reasoning and Planning</b>
    <a href="https://arxiv.org/abs/2410.14157"><img src="https://img.shields.io/badge/arXiv-2410.14157-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2410.14157"><img src="https://img.shields.io/badge/AlphaXiv-2410.14157-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/HKUNLP/diffusion-vs-ar"><img src="https://img.shields.io/github/stars/HKUNLP/diffusion-vs-ar?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Jiacheng Ye, Jiahui Gao, Shansan Gong, Lin Zheng, Xin Jiang, Zhenguo Li, Lingpeng Kong

  **TL;DR:** Multi-granularity diffusion planning (plan-then-generate), demonstrating a training paradigm for discrete diffusion on complex reasoning and planning tasks. ICLR 2025.
  </details>

- <details>
  <summary>
    <b>[09/2024] Masked Diffusion Models are Secretly Time-Agnostic Masked Models and Exploit Inaccurate Categorical Sampling</b>
    <a href="https://arxiv.org/abs/2409.02908"><img src="https://img.shields.io/badge/arXiv-2409.02908-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2409.02908"><img src="https://img.shields.io/badge/AlphaXiv-2409.02908-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Kaiwen Zheng, Yongxin Chen, Hanzi Mao, Ming-Yu Liu, Jun Zhu, Qinsheng Zhang

  **TL;DR:** A theoretical analysis of the mismatch between MDM training objectives and samplers, pointing out improvable training/inference junctions. ICLR 2025.
  </details>

- <details>
  <summary>
    <b>[06/2024] Simple and Effective Masked Diffusion Language Models (MDLM)</b>
    <a href="https://arxiv.org/abs/2406.07524"><img src="https://img.shields.io/badge/arXiv-2406.07524-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2406.07524"><img src="https://img.shields.io/badge/AlphaXiv-2406.07524-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/kuleshov-group/mdlm"><img src="https://img.shields.io/github/stars/kuleshov-group/mdlm?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Subham Sekhar Sahoo, Marianne Arriola, Yair Schiff, Aaron Gokaslan, Edgar Marroquin, Justin T Chiu, Alexander Rush, Volodymyr Kuleshov

  **TL;DR:** Derives a simplified (Rao-Blackwellized) ELBO for masked diffusion and connects SEDD with the ELBO, becoming the training foundation of LLaDA-style models. NeurIPS 2024.
  </details>

- <details>
  <summary>
    <b>[06/2024] Simplified and Generalized Masked Diffusion for Discrete Data</b>
    <a href="https://arxiv.org/abs/2406.04329"><img src="https://img.shields.io/badge/arXiv-2406.04329-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2406.04329"><img src="https://img.shields.io/badge/AlphaXiv-2406.04329-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/google-deepmind/md4"><img src="https://img.shields.io/github/stars/google-deepmind/md4?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Jiaxin Shi, Kehang Han, Zhe Wang, Arnaud Doucet, Michalis K. Titsias

  **TL;DR:** Generalizes and simplifies the masked diffusion objective into a weighted cross-entropy integral, corroborating MDLM. NeurIPS 2024.
  </details>

- <details>
  <summary>
    <b>[02/2024] Diffusion of Thoughts: Chain-of-Thought Reasoning in Diffusion Language Models</b>
    <a href="https://arxiv.org/abs/2402.07754"><img src="https://img.shields.io/badge/arXiv-2402.07754-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2402.07754"><img src="https://img.shields.io/badge/AlphaXiv-2402.07754-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/HKUNLP/diffusion-of-thoughts"><img src="https://img.shields.io/github/stars/HKUNLP/diffusion-of-thoughts?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Jiacheng Ye, Shansan Gong, Liheng Chen, Lin Zheng, Jiahui Gao, Han Shi, Chuan Wu, Xin Jiang, Zhenguo Li, Wei Bi, Lingpeng Kong

  **TL;DR:** Incorporates CoT reasoning steps into the diffusion denoising process; a pioneering work on reasoning-trajectory training for diffusion LMs. NeurIPS 2024.
  </details>

- <details>
  <summary>
    <b>[02/2024] Text Diffusion with Reinforced Conditioning (TREC)</b>
    <a href="https://arxiv.org/abs/2402.14843"><img src="https://img.shields.io/badge/arXiv-2402.14843-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2402.14843"><img src="https://img.shields.io/badge/AlphaXiv-2402.14843-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Yuxuan Liu, Tianchi Yang, Shaohan Huang, Zihan Zhang, Haizhen Huang, Furu Wei, Weiwei Deng, Feng Sun, Qi Zhang

  **TL;DR:** One of the earliest reinforced self-conditioning mechanisms for text diffusion, where the model conditions on its own previous predictions during generation (not an RL method). arXiv 2024.
  </details>

- <details>
  <summary>
    <b>[10/2023] SEDD: Discrete Diffusion Modeling by Estimating the Ratios of the Data Distribution</b>
    <a href="https://arxiv.org/abs/2310.16834"><img src="https://img.shields.io/badge/arXiv-2310.16834-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2310.16834"><img src="https://img.shields.io/badge/AlphaXiv-2310.16834-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/louaaron/Score-Entropy-Discrete-Diffusion"><img src="https://img.shields.io/github/stars/louaaron/Score-Entropy-Discrete-Diffusion?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Aaron Lou, Chenlin Meng, Stefano Ermon

  **TL;DR:** Proposes the score entropy (DWDSE) objective as a principled alternative to the ELBO for discrete diffusion training, matching GPT-2-level performance. ICML 2024 Oral.
  </details>

- <details>
  <summary>
    <b>[07/2021] D3PM: Structured Denoising Diffusion Models in Discrete State-Spaces</b>
    <a href="https://arxiv.org/abs/2107.03006"><img src="https://img.shields.io/badge/arXiv-2107.03006-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2107.03006"><img src="https://img.shields.io/badge/AlphaXiv-2107.03006-7c3aed.svg" alt="AlphaXiv"></a>
  </summary>

  **Authors:** Jacob Austin, Daniel D. Johnson, Jonathan Ho, Daniel Tarlow, Rianne van den Berg

  **TL;DR:** The foundational discrete diffusion work, proposing absorbing-state (mask) transition kernels and hybrid VLB/cross-entropy training objectives. NeurIPS 2021.
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
    <b>[12/2025] WeDLM: Reconciling Diffusion Language Models with Standard Causal Attention for Fast Inference</b>
    <a href="https://arxiv.org/abs/2512.22737"><img src="https://img.shields.io/badge/arXiv-2512.22737-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2512.22737"><img src="https://img.shields.io/badge/AlphaXiv-2512.22737-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/Tencent/WeDLM"><img src="https://img.shields.io/github/stars/Tencent/WeDLM?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Aiwei Liu, Minghua He, Shaoxun Zeng, Sijun Zhang, Linhao Zhang, Chuhan Wu, Wei Jia, Yuan Liu, Xiao Zhou, Jie Zhou

  **TL;DR:** Fine-tuning with topological reordering makes dLLMs compatible with standard causal attention and KV cache for streaming parallel decoding. arXiv 2025.
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
    <b>[10/2025] SDAR: A Synergistic Diffusion–AutoRegression Paradigm for Scalable Sequence Generation</b>
    <a href="https://arxiv.org/abs/2510.06303"><img src="https://img.shields.io/badge/arXiv-2510.06303-b31b1b.svg" alt="arXiv"></a>
    <a href="https://www.alphaxiv.org/abs/2510.06303"><img src="https://img.shields.io/badge/AlphaXiv-2510.06303-7c3aed.svg" alt="AlphaXiv"></a>
    <a href="https://github.com/JetAstra/SDAR"><img src="https://img.shields.io/github/stars/JetAstra/SDAR?style=social&label=Stars" alt="GitHub Stars"></a>
  </summary>

  **Authors:** Shuang Cheng, Yihan Bian, Dawei Liu, Linfeng Zhang, Qian Yao, Zhongbo Tian, Wenhai Wang, Qipeng Guo, Kai Chen, Biqing Qi, Bowen Zhou

  **TL;DR:** A unified training paradigm of block-level AR plus intra-block diffusion; 1.7B–30B models are SFT'ed into instruct models (technical report). arXiv 2025.
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

## Frameworks & Benchmarks

### Post-training Frameworks

| Name | Link | Description |
|---|---|---|
| Gen-Verse/dLLM-RL (TraceRL) | [GitHub](https://github.com/Gen-Verse/dLLM-RL) | Comprehensive dLLM RL post-training framework; TraDo model family (arXiv [2509.06949](https://arxiv.org/abs/2509.06949)) |
| ZHZisZZ/dllm | [GitHub](https://github.com/ZHZisZZ/dllm) | Unified dLLM training/evaluation/inference library supporting SFT for LLaDA/Dream (arXiv [2602.22661](https://arxiv.org/abs/2602.22661)) |
| Block-R1 | [GitHub](https://github.com/YanJiangJerry/Block-R1) | Multi-domain dLLM RL post-training benchmark, reproducing d1/wd1 and other algorithms |
| OpenMOSS/DiRL | [GitHub](https://github.com/OpenMOSS/DiRL) | Efficient dLLM RL post-training framework proposing DiPO, an unbiased GRPO variant (arXiv [2512.22234](https://arxiv.org/abs/2512.22234)) |
| yjyddq/DARE | [GitHub](https://github.com/yjyddq/DARE) | Unified dLLM alignment & RL evaluation/execution framework built on verl + OpenCompass, covering SFT/PEFT/preference optimization/RL for LLaDA, Dream, SDAR, LLaDA2.x (arXiv [2604.04215](https://arxiv.org/abs/2604.04215)) |

### Related Awesome Lists

- [VILA-Lab/Awesome-DLMs](https://github.com/VILA-Lab/Awesome-DLMs) — Official list of the paper *A Survey on Diffusion Language Models*; its Training Strategies / RL sections are great for cross-checking.
- [piesauce/awesome-dLLM-resources](https://github.com/piesauce/awesome-dLLM-resources) — A frequently updated list of dLLM papers, models, and libraries.
- [AIDASLab/Awesome-Diffusion-LLM](https://github.com/AIDASLab/Awesome-Diffusion-LLM) — Includes Alignment & RL and multimodal dLLM categories.

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
