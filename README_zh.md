# Awesome DLMs Post-Training

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0-1.0](https://img.shields.io/badge/License-CC0--1.0-lightgrey.svg)](LICENSE)

**扩散语言模型（Diffusion Language Models, dLLM）后训练方向的精选论文、框架与资源列表：SFT、强化学习（GRPO/PPO/RLVR）、偏好优化、安全对齐、蒸馏与高效适配。**

[English](README.md) | [中文](README_zh.md)

## 📢 最新动态

- **[2026-07]** 🎉 本仓库正式发布！已收录 100+ 篇 dLLM 后训练相关论文，欢迎贡献——详见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 📖 收录范围：什么算 dLLM 后训练？

本列表聚焦扩散语言模型的**后训练**阶段，即在基础扩散预训练之后（或对其适配）的一切工作：

- **SFT / 指令微调** —— 面向指令跟随、对话与任务适配的监督微调
- **强化学习** —— GRPO/PPO 类策略优化、RLVR、面向推理的奖励微调
- **偏好优化** —— DPO/KTO 类基于偏好数据的对齐
- **安全对齐** —— dLLM 特有的安全训练、越狱鲁棒性与对齐分析
- **蒸馏与效率适配** —— 少步/一致性蒸馏、引导训练、置信度感知微调、含训练组件的推测解码
- **适配技术** —— AR→DLM 转换、长上下文后训练

收录 **masked/absorbing、block、连续扩散 LM**，包括**多模态**与**代码** dLLM。纯预训练架构论文仅在其奠定了后训练所依赖的训练目标或管线时收录。

## 📑 目录

- [综述（Surveys）](#综述surveys)（3）
- [RL 与推理（RL & Reasoning）](#rl-与推理rl--reasoning)（31）
- [偏好优化（Preference Optimization）](#偏好优化preference-optimization)（2）
- [安全对齐（Safety & Alignment）](#安全对齐safety--alignment)（2）
- [SFT 与指令微调（SFT & Instruction Tuning）](#sft-与指令微调sft--instruction-tuning)（6）
- [训练目标与技术（Training Objectives & Techniques）](#训练目标与技术training-objectives--techniques)（17）
- [效率与蒸馏（Efficiency & Distillation）](#效率与蒸馏efficiency--distillation)（22）
- [多模态与代码 dLLM（Multimodal & Code dLLMs）](#多模态与代码-dllmmultimodal--code-dllms)（21）
- [框架与开源仓库（Frameworks & Open-source Repos）](#框架与开源仓库frameworks--open-source-repos)
- [Star History](#star-history)
- [贡献指南](#贡献指南)
- [许可证](#许可证)

---

## 综述（Surveys）

- [08/14/2025] **[A Survey on Diffusion Language Models](https://arxiv.org/abs/2508.10875)** — 目前最全面的 DLM 综述，系统梳理预训练、SFT、RL 对齐、推理加速与应用，含专门的后训练章节。*Tianyi Li, Mingda Chen, Bowei Guo, Zhiqiang Shen*, arXiv 2025. [[code]](https://github.com/VILA-Lab/Awesome-DLMs)
- [06/2025] **[Discrete Diffusion in Large Language and Multimodal Models: A Survey](https://arxiv.org/abs/2506.13759)** — 聚焦离散扩散在大语言与多模态模型中的公式化、训练与推理，覆盖 LLaDA/Dream/Dimple 等。*Runpeng Yu, Qi Li, Xinchao Wang*, arXiv 2025. [[code]](https://github.com/LiQiiiii/DLLM-Survey)
- [2024] **[Diffusion Models in Text Generation: A Survey](https://doi.org/10.7717/peerj-cs.1905)** — 较早的文本生成扩散模型综述，适合追溯 Diffusion-LM 时代的连续扩散文本工作。*Qiuhua Yi, Xiangfan Chen, et al.*, PeerJ Computer Science 2024.

## RL 与推理（RL & Reasoning）

- [07/16/2026] **[Mask-Aware Policy Gradients for Diffusion Language Models](https://arxiv.org/abs/2607.15200)** — 掩码感知的扩散 LM 策略梯度方法。*Haran Raajesh, Kulin Shah, Adam Klivans, Philipp Krähenbühl*, COLM 2026.
- [06/30/2026] **[SLIM-RL: Risk-Budgeted Random-Masking RL for Diffusion LLMs Without Trajectory Slicing](https://arxiv.org/abs/2607.00208)** — 针对 TraceRL 轨迹切片成本随块大小增长的问题，用 τ-budget 解码器约束提交风险 + 无轨迹随机掩码目标。*Ruikang Zhao, Zhenting Wang, Han Gao, Ligong Han*, arXiv 2026.
- [05/13/2026] **[Beyond Mode-Seeking RL: Trajectory-Balance Post-Training for Diffusion Language Models](https://arxiv.org/abs/2605.13935)** — 引入 trajectory-balance（GFlowNet 式）目标缓解 mode-seeking RL 的多样性坍缩。arXiv 2026.
- [05/11/2026] **[Relative Score Policy Optimization for Diffusion Language Models (RSPO)](https://arxiv.org/abs/2605.10218)** — 用相对得分替代似然做组内策略优化。arXiv 2026.
- [03/13/2026] **[Reinforcement Learning for Diffusion LLMs with Entropy-Guided Step Selection and Stepwise Advantages (EGSPO)](https://arxiv.org/abs/2603.12554)** — 熵引导选择关键去噪步并分配步级优势，降低 dLLM RL 的方差与成本。*Vishnu Teja Kunde, Fatemeh Doudi, et al.*, arXiv 2026. [[code]](https://github.com/vishnutez/egspo-dllm-rl)
- [03/2026] **[LFPO: Likelihood-Free Policy Optimization for Masked Diffusion Models](https://arxiv.org/abs/2603.01563)** — 彻底绕开似然计算的无似然 RLVR 策略优化，规避现有方法的高方差近似问题。 *Chenxing Wei, Jiazhen Kang, et al.*, arXiv 2026. [[code]](https://github.com/kithib/LFPO)
- [02/06/2026] **[Diffusion-State Policy Optimization for Masked Diffusion Language Models (DSPO)](https://arxiv.org/abs/2602.06462)** — 以扩散中间状态为决策状态设计策略优化，而非仅在最终序列上打分。 *Daisuke Oba, Hiroki Furuta, Naoaki Okazaki*, arXiv 2026.
- [01/21/2026] **[The Flexibility Trap: Rethinking the Value of Arbitrary Order in Diffusion Language Models (JustGRPO)](https://arxiv.org/abs/2601.15165)** — 论证任意顺序生成的灵活性并非必要，简单 GRPO 直接移植即可匹敌复杂扩散专用 RL 改造（以 ESPO 为对照基线）。*Zanlin Ni, Shenzhi Wang, Yang Yue, et al.*, ICML 2026 Oral（杰出论文奖）. [[code]](https://github.com/LeapLabTHU/JustGRPO)
- [01/05/2026] **[Progressive Block Scaling for MDMs Through Trajectory-Aware RL (T\*)](https://arxiv.org/abs/2601.11214)** — 基于 TraceRL 的课程式渐进块大小扩展训练方案。 *Hanchen Xia, Baoyou Chen, et al.*, arXiv 2026.
- [12/24/2025] **[dUltra: Ultra-Fast Diffusion Large Language Models via Reinforcement Learning](https://arxiv.org/abs/2512.21446)** — 用 GRPO 学习"路径规划器"（解掩码顺序/并行度），在保持质量的同时大幅加速扩散 LLM 解码。*Shirui Chen, Jiantao Jiao, Lillian J. Ratliff, Banghua Zhu*, arXiv 2025. [[code]](https://github.com/chinsengi/dUltra-os)
- [12/10/2025] **[d-TreeRPO: Towards More Reliable Policy Optimization for Diffusion Language Models](https://arxiv.org/abs/2512.09675)** — 树状分组/rollout 组织方式提升 dLLM 策略优化可靠性。*Leyi Pan, Shuchang Tao, et al.*, ACL 2026 Main. [[code]](https://github.com/THU-BPM/d-TreeRPO)
- [12/09/2025] **[Learning Unmasking Policies for Diffusion Language Models](https://arxiv.org/abs/2512.09106)** — 不同于固定置信度采样，用 RL 学习独立的"解掩码顺序策略"模块，与 DCoLT/UPM 一脉相承。*Metod Jazbec, Theo X. Olausson, Louis Béthune, et al.*, arXiv 2025. [[code]](https://github.com/apple/ml-rl-dllm)
- [12/03/2025] **[Principled RL for Diffusion LLMs Emerges from a Sequence-Level Perspective (ESPO)](https://arxiv.org/abs/2512.03759)** — 把整条序列生成当作单一动作，用 ELBO 作序列级似然代理 + 逐 token 归一化重要性比率，Countdown 上较 token 级基线提升 20–40 点。*Jingyang Ou, Jiaqi Han, Minkai Xu, et al.*, ICLR 2026. [[code]](https://github.com/ML-GSAI/ESPO)
- [10/24/2025] **[MRO: Enhancing Reasoning in Diffusion Language Models via Multi-Reward Optimization](https://arxiv.org/abs/2510.21473)** — 多奖励联合优化提升 dLLM 推理能力。arXiv 2025.
- [10/13/2025] **[Boundary-Guided Policy Optimization for Memory-Efficient RL of Diffusion LLMs (BGPO)](https://arxiv.org/abs/2510.11683)** — 利用块扩散的边界结构最大化 ELBO 线性下界，显著降低 RL 训练显存开销。*Nianyi Lin, Jiajie Zhang, Lei Hou, Juanzi Li*, arXiv 2025. [[code]](https://github.com/THU-KEG/BGPO)
- [10/10/2025] **[SPG: Sandwiched Policy Gradient for Masked Diffusion Language Models](https://arxiv.org/abs/2510.09541)** — 用 log-likelihood 上下界"夹逼"构造三明治目标做策略梯度，显著优于 ELBO 类方法（d1/wd1）。*Chengyu Wang, Paria Rashidinejad, DiJia Su, et al.*, ICLR 2026. [[code]](https://github.com/facebookresearch/SPG)
- [10/09/2025] **[Improving Reasoning for Diffusion Language Models via Group Diffusion Policy Optimization (GDPO)](https://arxiv.org/abs/2510.08554)** — GRPO 的扩散化改造，改进组内相对优势在去噪步上的分配，超越 diffu-GRPO。*Kevin Rojas, Jiahe Lin, Kashif Rasul, et al.*, arXiv 2025.
- [10/09/2025] **[Enhancing Reasoning for Diffusion LLMs via Distribution Matching Policy Optimization (DMPO)](https://arxiv.org/abs/2510.08233)** — 将 RL 表述为分布匹配问题，避免直接估计不可解似然。*Yuchen Zhu, Wei Guo, Jaemoo Choi, et al.*, arXiv 2025.
- [10/05/2025] **[Principled and Tractable RL for Reasoning with Diffusion Language Models](https://arxiv.org/abs/2510.04019)** — 从原则出发推导扩散 LLM 上可处理的 RL 目标，给出更严格的似然近似与更新规则，替代 ELBO/一步估计等偏置代理。*Anthony Zhan*, arXiv 2025.
- [10/03/2025] **[Consolidating Reinforcement Learning for Multimodal Discrete Diffusion Models (MaskGRPO)](https://arxiv.org/abs/2510.02880)** — 统一 LLaDA/MMaDA 的 GRPO 训练框架。*Tianren Ma, Mu Zhang, Yibing Wang, Qixiang Ye*, ICLR 2026. [[code]](https://github.com/martian422/MaskGRPO)
- [10/02/2025] **[Step-Aware Policy Optimization for Reasoning in Diffusion Large Language Models (SAPO)](https://arxiv.org/abs/2510.01544)** — 引入去噪步级的过程奖励，引导 dLLM 沿潜在推理层级逐步取得进展。*Shenghui Xie, Lingjing Kong, Xiangchen Song, et al.*, arXiv 2025.
- [10/02/2025] **[DiFFPO: Training Diffusion LLMs to Reason Fast and Furious via Reinforcement Learning](https://arxiv.org/abs/2510.02212)** — 统一 RL 框架联合训练模型与采样器策略，同时提升推理准确率并降低延迟，改善准确率/计算帕累托前沿。*Hanyang Zhao, Dawen Liang, Wenpin Tang, et al.*, arXiv 2025.
- [09/28/2025] **[Taming Masked Diffusion Language Models via Consistency Trajectory RL with Fewer Decoding Steps (CJ-GRPO)](https://arxiv.org/abs/2509.23924)** — 强调 rollout 与优化轨迹一致性，解决 MDLM 非因果解码与 AR 式 RL 之间的训练-推理不一致。*Jingyi Yang, Guanxu Chen, Xuhao Hu, Jing Shao*, arXiv 2025.
- [09/12/2025] **[Inpainting-Guided Policy Optimization for Diffusion Large Language Models (IGPO)](https://arxiv.org/abs/2509.10396)** — 利用扩散模型部分 inpainting 能力，在 rollout 中注入部分真实答案片段引导探索，缓解稀疏奖励下的探索困难。*Siyan Zhao, Mengchen Liu, Jing Huang, et al.*, arXiv 2025. [[code]](https://github.com/facebookresearch/igpo)
- [09/08/2025] **[Revolutionizing Reinforcement Learning Framework for Diffusion Large Language Models (TraceRL / TraDo)](https://arxiv.org/abs/2509.06949)** — 轨迹感知 RL，将训练目标与模型实际推理轨迹对齐，配合扩散价值模型降方差；衍生 TraDo-4B/8B 及首个长 CoT 扩散模型 TraDo-8B-Thinking；dLLM-RL 是最全面的 dLLM 后训练开源框架。*Yinjie Wang, Ling Yang, Bowen Li, et al.*, ICLR 2026. [[code]](https://github.com/Gen-Verse/dLLM-RL)
- [08/18/2025] **[MDPO: Overcoming the Training-Inference Divide of Masked Diffusion Language Models](https://arxiv.org/abs/2508.13148)** — 按推理时的渐进精炼调度优化策略，弥合 MDLM 训练与推理过程的不一致。*Chaofan Lin et al.*, arXiv 2025. [[code]](https://github.com/autonomousvision/mdpo)
- [07/07/2025] **[wd1: Weighted Policy Optimization for Reasoning in Diffusion Language Models](https://arxiv.org/abs/2507.08838)** — 对低优势样本重新加权而非丢弃，改进 diffu-GRPO 的样本效率与计算开销，GSM8K/MATH/Sudoku/Countdown 上超越 d1。*Xiaohang Tang, Rares Dolga, Sangwoong Yoon, Ilija Bogunovic*, ICLR 2026. [[code]](https://github.com/xiaohangt/wd1)
- [05/14/2025] **[Reinforcing the Diffusion Chain of Lateral Thought with Diffusion Language Models (DCoLT)](https://arxiv.org/abs/2505.10446)** — 把扩散反向采样中间步视为"思考动作"，用结果奖励 RL 优化整条去噪轨迹；LLaDA 上提出 Unmask Policy Module (UPM) 用 Plackett-Luce 建模解掩码顺序。*Zemin Huang, Zhiyang Chen, Zijun Wang, et al.*, arXiv 2025. [[code]](https://github.com/maple-research-lab/LLaDOU)
- [04/16/2025] **[d1: Scaling Reasoning in Diffusion Large Language Models via Reinforcement Learning](https://arxiv.org/abs/2504.12216)** — 提出 diffu-GRPO，用均值场近似 + 随机掩码 prompt 的单次前向估计序列/token 对数概率，SFT+RL 两阶段显著提升 LLaDA 的数学/规划推理能力。**本方向奠基性工作。** *Siyan Zhao, Devaansh Gupta, Qinqing Zheng, Aditya Grover*, NeurIPS 2025. [[code]](https://github.com/dllm-reasoning/d1)
- [02/03/2025] **[Fine-Tuning Discrete Diffusion Models with Policy Gradient Methods (SEPO)](https://arxiv.org/abs/2502.01384)** — 较早将策略梯度方法系统用于离散扩散模型微调的探索性工作。*Oussama Zekri, Nicolas Boullé*, arXiv 2025. [[code]](https://github.com/ozekri/SEPO)
- [10/17/2024] **[DRAKES: Fine-Tuning Discrete Diffusion Models via Reward Optimization with Applications to DNA and Protein Design](https://arxiv.org/abs/2410.13643)** — 将整条反向扩散链纳入奖励反向传播的离散扩散奖励微调框架（生物序列设计，方法直接适用于文本 MDM）。*Chenyu Wang et al.*, ICLR 2025. [[code]](https://github.com/ChenyuWang-Monica/DRAKES)

## 偏好优化（Preference Optimization）

- [10/26/2025] **[Aligning Diffusion Language Models via Unpaired Preference Optimization](https://arxiv.org/abs/2510.23658)** — 将 KTO（unpaired preference optimization）适配到 dLLM，用 ELBO 替代不可解的 log-likelihood，无需成对偏好数据即可对齐。*Vaibhav Jindal et al.*, arXiv 2025. [[code]](https://github.com/vaibhavjindal/elbo-kto)
- [05/25/2025] **[LLaDA 1.5: Variance-Reduced Preference Optimization for Large Language Diffusion Models (VRPO)](https://arxiv.org/abs/2505.19223)** — 首次系统地将 DPO 迁移到 masked diffusion LM，提出 VRPO——无偏蒙特卡洛预算分配 + 对偶采样降低 ELBO 偏好优化方差。**偏好优化方向奠基性工作。** *Fengqi Zhu, Rongzhen Wang, Shen Nie, et al.*, arXiv 2025. [[code]](https://github.com/ML-GSAI/LLaDA-1.5)

## 安全对齐（Safety & Alignment）

- [09/27/2025] **[A2D: Any-Order, Any-Step Safety Alignment for Diffusion Language Models](https://arxiv.org/abs/2509.23286)** — 针对 dLLM 任意顺序、任意步数解码特点的安全对齐方法，缓解 dLLM 独特的越狱脆弱性。*Wonje Jeung et al.*, arXiv 2025.
- [08/17/2025] **[Where to Start Alignment? Diffusion Large Language Model May Demand a Distinct Position](https://arxiv.org/abs/2508.12398)** — 分析性工作，指出 dLLM 的对齐起点/数据位置与 AR 模型本质不同，为 dLLM 对齐提供设计指导。*Zhixin Xie, Xurui Song, Jun Luo*, arXiv 2025.

## SFT 与指令微调（SFT & Instruction Tuning）

- [12/2025] **[LLaDA2.0: Scaling Up Diffusion Language Models to 100B](https://arxiv.org/abs/2512.15745)** — 将扩散语言模型扩展到 100B 并给出完整 post-training（SFT + 对齐）流程。*T. Bie, M. Cao, K. Chen, et al.*, arXiv 2025. [[code]](https://github.com/inclusionAI/LLaDA2.X)
- [09/29/2025] **[LLaDA-MoE: A Sparse MoE Diffusion Language Model](https://arxiv.org/abs/2509.24389)** — 20T token 预训练的 7B-A1B MoE 扩散模型，经 prompt-response 对 SFT 得到 Instruct 版，详细披露数据工程与 MoE 下 SFT 配方。*Fengqi Zhu, Zebin You, Jiamei Wen, et al.*, arXiv 2025. [[code]](https://github.com/ML-GSAI/LLaDA)
- [08/21/2025] **[Dream 7B: Diffusion Large Language Models](https://arxiv.org/abs/2508.15487)** — AR 初始化 + 上下文自适应 token 级噪声重调度；发布 Dream-Base 与 Dream-Instruct（SFT 版），最强开源指令微调扩散模型基线之一。*Jiacheng Ye, Zhihui Xie, Lin Zheng, et al.*, arXiv 2025. [[code]](https://github.com/DreamLM/Dream)
- [02/14/2025] **[Large Language Diffusion Models (LLaDA)](https://arxiv.org/abs/2502.09992)** — 8B masked diffusion LM 从头预训练 + SFT（只对 response 加噪），首次证明扩散范式下 SFT 可获得与 LLaMA3-8B 相当的指令跟随能力。*Shen Nie, Fengqi Zhu, Zebin You, et al.*, NeurIPS 2025. [[code]](https://github.com/ML-GSAI/LLaDA)
- [08/23/2023] **[Diffusion Language Models Can Perform Many Tasks with Scaling and Instruction-Finetuning](https://arxiv.org/abs/2308.12219)** — 最早的 diffusion LM instruction tuning 工作——MLM 预训练 + "diffusive adaptation" 重编程，证明指令微调可赋予扩散 LM zero/few-shot 能力。*Jiasheng Ye, Zaixiang Zheng, Yu Bao, et al.*, ICLR 2024. [[code]](https://github.com/yegcjs/DiffusionLLM)
- [10/2022] **[DiffuSeq: Sequence to Sequence Text Generation with Diffusion Models](https://arxiv.org/abs/2210.08933)** — 将条件 seq2seq 任务作为扩散模型的条件微调，扩散文本模型"任务微调"的早期代表（非 LLM 规模）。*Shansan Gong, Mukai Li, Jiangtao Feng, et al.*, ICLR 2023. [[code]](https://github.com/Shark-NLP/DiffuSeq)

## 训练目标与技术（Training Objectives & Techniques）

- [05/07/2026] **[Don't Retrain—Align: Adapting Autoregressive LMs to Diffusion LMs via Representation Alignment](https://arxiv.org/abs/2605.06885)** — 不重新训练，通过表示对齐微调把 AR LM 适配为扩散 LM，系统综述 DiffuGPT/Dream/Fast-dLLM v2 等转换配方。*Felix Z. Peng et al.*, arXiv 2026.
- [12/2025] **[WeDLM: Reconciling Diffusion Language Models with Standard Causal Attention for Fast Inference](https://arxiv.org/abs/2512.22737)** — 通过拓扑重排序的微调使 dLLM 兼容标准因果注意力/KV cache 的流式并行解码。*Aiwei Liu et al.*, arXiv 2025. [[code]](https://github.com/Tencent/WeDLM)
- [12/2025] **[Efficient-DLM: From Autoregressive to Diffusion Language Models, and Beyond in Speed](https://arxiv.org/abs/2512.14067)** — 系统研究 AR→DLM 转换训练配方（含指令微调阶段）与加速。*Yonggan Fu et al.*, arXiv 2025. [[code]](https://github.com/NVlabs/Fast-dLLM)
- [10/2025] **[UltraLLaDA: Scaling the Context Length to 128K for Diffusion Large Language Models](https://arxiv.org/abs/2510.10481)** — 轻量级后训练（扩散感知 NTK 外推 + 长上下文数据掩码打包）把 dLLM 上下文扩到 128K，无需从头预训练。*Guangxin He, Shen Nie, Fengqi Zhu, et al.*, arXiv 2025. [[code]](https://github.com/Relaxed-System-Lab/UltraLLaDA)
- [10/07/2025] **[SDAR: A Synergistic Diffusion–AutoRegression Paradigm for Scalable Sequence Generation](https://arxiv.org/abs/2510.06303)** — 块级 AR + 块内扩散的统一训练范式，1.7B–30B 规模经 SFT 得到 instruct 模型。*JetAstra Team*, arXiv 2025. [[code]](https://github.com/JetAstra/SDAR)
- [09/30/2025] **[Fast-dLLM v2: Efficient Block-Diffusion LLM](https://arxiv.org/abs/2509.26328)** — 仅用 ~1B token 的块扩散微调（含指令数据）将 AR LLM 转为并行解码 dLLM，数据效率比 Dream 路线高 500×。*Chengyue Wu, Hao Zhang, Shuchen Xue, et al.*, arXiv 2025. [[code]](https://github.com/NVlabs/Fast-dLLM)
- [06/2025] **[LongLLaDA: Unlocking Long Context Capabilities in Diffusion LLMs](https://arxiv.org/abs/2506.14429)** — 首个 dLLM 长度外推研究，NTK-based RoPE 外推（免训练）打通长上下文。*Xiaoran Liu, Zhigeng Liu, Zengfeng Huang, et al.*, AAAI 2026. [[code]](https://github.com/OpenMOSS/LongLLaDA)
- [03/2025] **[Block Diffusion: Interpolating Between Autoregressive and Diffusion Language Models (BD3-LM)](https://arxiv.org/abs/2503.09573)** — 块级自回归 + 块内扩散的混合训练目标，支持任意长度生成与 KV cache，缓解离散扩散固定长度限制。*Marianne Arriola, Aaron Gokaslan, Justin T. Chiu, et al.*, ICLR 2025. [[code]](https://github.com/kuleshov-group/bd3lms)
- [10/23/2024] **[Scaling Diffusion Language Models via Adaptation from Autoregressive Models (DiffuGPT / DiffuLLaMA)](https://arxiv.org/abs/2410.17891)** — attention mask annealing + shift 操作将 GPT-2/LLaMA 持续训练为扩散模型，明确提出后续 instruction tuning 路线并开源模型。**AR→DLM 衔接代表配方。** *Shansan Gong, Shivam Agarwal, Yizhe Zhang, et al.*, ICLR 2025. [[code]](https://github.com/HKUNLP/DiffuLLaMA)
- [10/2024] **[Beyond Autoregression: Discrete Diffusion for Complex Reasoning and Planning](https://arxiv.org/abs/2410.14157)** — 多粒度扩散规划（先规划后生成），展示离散扩散在复杂推理/规划任务上的训练范式。*Jiacheng Ye, Jiahui Gao, Shansan Gong, et al.*, ICLR 2025.
- [09/2024] **[Masked Diffusion Models are Secretly Time-Agnostic Masked Models and Exploit Inaccurate Categorical Sampling](https://arxiv.org/abs/2409.02908)** — 理论分析 MDM 训练目标与采样器的不匹配，指出可改进的训练/推理衔接点。*Kaiwen Zheng, Yongxin Chen, Hanzi Mao, et al.*, arXiv 2024.
- [06/2024] **[Simple and Effective Masked Diffusion Language Models (MDLM)](https://arxiv.org/abs/2406.07524)** — 推导 masked diffusion 的简化 ELBO（Rao-Blackwell 化），建立 SEDD 与 ELBO 的联系，成为 LLaDA 类模型的训练基础。*Subham Sekhar Sahoo, Marianne Arriola, Aaron Gokaslan, et al.*, NeurIPS 2024. [[code]](https://github.com/kuleshov-group/mdlm)
- [06/2024] **[Simplified and Generalized Masked Diffusion for Discrete Data](https://arxiv.org/abs/2406.04329)** — 将 masked diffusion 目标推广并简化为可加权的交叉熵积分，与 MDLM 互为印证。*Jiaxin Shi, Kehan Han, Zhe Wang, et al.*, NeurIPS 2024.
- [02/2024] **[Diffusion of Thoughts: Chain-of-Thought Reasoning in Diffusion Language Models](https://arxiv.org/abs/2402.07754)** — 把 CoT 推理步融入扩散去噪过程（DoT/多遍 DoTMP），"推理轨迹 SFT"方向的开创工作。*Jiacheng Ye, Shanshan Gong, Lin Zheng, et al.*, NeurIPS 2024. [[code]](https://github.com/HKUNLP/diffusion-of-thoughts)
- [02/19/2024] **[Text Diffusion with Reinforced Conditioning (TREC)](https://arxiv.org/abs/2402.14843)** — 最早的文本扩散 reinforced self-conditioning 机制之一，生成时以模型自身前序预测为条件（非 RL 方法）。*Microsoft*, AAAI 2024.
- [10/2023] **[SEDD: Discrete Diffusion Modeling by Estimating the Ratios of the Data Distribution](https://arxiv.org/abs/2310.16834)** — 提出 score entropy（DWDSE）目标替代 ELBO，离散扩散训练的原则性框架，效果可比 GPT-2。*Aaron Lou, Chenlin Meng, Stefano Ermon*, ICML 2024. [[code]](https://github.com/louaaron/Score-Entropy-Discrete-Diffusion)
- [07/2021] **[D3PM: Structured Denoising Diffusion Models in Discrete State-Spaces](https://arxiv.org/abs/2107.03006)** — 离散扩散奠基工作，提出 absorbing-state（mask）转移核与混合 VLB/交叉熵训练目标。*Jacob Austin, Daniel D. Johnson, Jonathan Ho, et al.*, NeurIPS 2021.

## 效率与蒸馏（Efficiency & Distillation）

- [06/01/2026] **[EPIC: Efficient and Parallel Inference under CFG Constraints for Diffusion Language Models](https://arxiv.org/abs/2606.00722)** — 在上下文无关文法（CFG）约束解码下实现高效并行推理（引导 × 效率交叉，偏推理侧）。arXiv 2026.
- [05/22/2026] **[DiLaDiff: Distilled Latent-Augmented Diffusion for Language Modeling](https://arxiv.org/abs/2605.23605)** — 潜空间增强的蒸馏扩散语言模型。arXiv 2026. [[project]](https://jmlemercier.github.io/diladiff/)
- [05/12/2026] **[Self-Distilled Trajectory-Aware Boltzmann Modeling: Bridging the Training-Inference Discrepancy in DLMs](https://arxiv.org/abs/2605.11854)** — 自蒸馏 + 轨迹感知 Boltzmann 建模，弥合 DLM 训练-推理差距。arXiv 2026.
- [05/11/2026] **[Infinite Mask Diffusion for Few-Step Distillation (IMDM)](https://arxiv.org/abs/2605.10518)** — 面向少步采样的无限 mask 扩散蒸馏框架。arXiv 2026. [[code]](https://Ugness.github.io/official_imdm)
- [05/10/2026] **[TAD: Temporal-Aware Trajectory Self-Distillation for Fast and Accurate Diffusion LLM](https://arxiv.org/abs/2605.09536)** — 时间感知的轨迹自蒸馏，加速 dLLM 采样同时保持精度。arXiv 2026. [[code]](https://github.com/BHmingyang/TAD)
- [05/08/2026] **[Guidance Is Not a Hyperparameter: Learning Dynamic Control in Diffusion Language Models](https://arxiv.org/abs/2605.07701)** — 将引导强度从手工超参变为可学习的动态控制量进行训练。arXiv 2026.
- [04/29/2026] **[TIDE: Cross-Architecture Distillation for Diffusion Large Language Models](https://arxiv.org/abs/2604.26951)** — 研究 dLLM 知识蒸馏中教师信号可靠性这一独有问题，做跨架构蒸馏。arXiv 2026. [[code]](https://github.com/PKU-YuanGroup/TIDE)
- [04/06/2026] **[FlowLM: Few-Step Language Modeling via Diffusion-to-Flow Adaptation](https://arxiv.org/abs/2605.20199)** — 将扩散 LM 适配为 flow matching 风格模型以实现少步生成。arXiv 2026.
- [01/12/2026] **[d3LLM: Ultra-Fast Diffusion LLM using Pseudo-Trajectory Distillation](https://arxiv.org/abs/2601.07568)** — 伪轨迹蒸馏教会模型哪些 token 可在早期步自信解码，配合熵基多块解码与 KV cache 刷新，对 LLaDA/Dream 实现最高 10× 加速。*Yu-Yang Qian et al.*, ICML 2026. [[code]](https://github.com/hao-ai-lab/d3LLM)
- [01/05/2026] **[CD4LM: Consistency Distillation and aDaptive Decoding for Diffusion Language Models](https://arxiv.org/abs/2601.02236)** — 离散空间一致性蒸馏（DSCD）训练轨迹不变的学生模型，配合置信度自适应解码跳步，GSM8K 上 5.18× 提速且严格占优精度-效率帕累托前沿。*Yihao Liang et al.*, arXiv 2026. [[code]](https://github.com/yihao-liang/CDLM)
- [05/2026] **[Consistent Diffusion Language Models (Multi-Path Consistency)](https://arxiv.org/abs/2605.00161)** — 提出"多路径一致性"原则训练离散扩散语言模型，实现少步一致生成。*H. Amin et al.*, arXiv (OpenReview).
- [11/24/2025] **[CDLM: Consistency Diffusion Language Models](https://arxiv.org/abs/2511.19269)** — 将 consistency modeling 引入 DLM 训练，蒸馏全双向教师并沿解码轨迹对齐预测，配合块级因果注意力兼容 KV cache，3.6–14.5× 降延迟。*Minseo Kim et al.*, arXiv 2025. [[code]](https://github.com/SqueezeAILab/CDLM)
- [11/04/2025] **[SpecDiff-2: Scaling Diffusion Drafter Alignment for Faster Speculative Decoding](https://arxiv.org/abs/2511.00606)** — 训练低延迟扩散模型作为自回归 LLM 推测解码的 drafter 并对齐草稿分布（前作 SpecDiff：arXiv 2408.05636，NAACL 2025）。*J. Sandler, J. K. Christopher, T. Hartvigsen, N. Fioretto*, arXiv 2025.
- [10/05/2025] **[Self-Speculative Decoding for Diffusion Large Language Models (SSD)](https://arxiv.org/abs/2510.04147)** — dLLM 自身同时充当 drafter 与 verifier，层次验证树单次前向验证多 token，3.46× 无损加速。*Yifeng Gao et al.*, arXiv 2025.（代码尚未发布）
- [09/30/2025] **[dParallel: Learnable Parallel Decoding for dLLMs](https://arxiv.org/abs/2509.26488)** — 提出 certainty-forcing distillation，在自生成轨迹上微调使 masked token 更快并行达到高置信度，GSM8K 上 256→30 步、8.5× 加速。*Zigeng Chen, Gongfan Fang, Xinyin Ma, et al.*, ICLR 2026. [[code]](https://github.com/czg1225/dParallel)
- [09/29/2025] **[Ultra-Fast Language Generation via Discrete Diffusion Divergence Instruct (DiDi-Instruct)](https://arxiv.org/abs/2509.25035)** — 基于积分 KL 散度最小化的分布匹配蒸馏，将 dLLM 教师蒸馏为 8–16 步少步学生模型，64× 加速且超越教师。*Haoyang Zheng, Xinyang Liu, Cindy Xiangrui Kong, et al.*, ICLR 2026. [[code]](https://github.com/haoyangzheng-ai/didi-instruct)
- [09/29/2025] **[Learning to Parallel: Accelerating Diffusion LLMs via Learnable Parallel Decoding (Learn2PD)](https://arxiv.org/abs/2509.25188)** — 后训练轻量过滤器模型预测各位置 token 是否与最终输出一致，逼近 oracle 并行解码策略，LLaDA 上最高 22.58×（配 KV cache 57.51×）无损加速。*Wenrui Bao et al.*, arXiv 2025.
- [09/25/2025] **[WeFT: Weighted Entropy-Driven Fine-Tuning for dLLMs](https://arxiv.org/abs/2509.20863)** — 按 token 熵加权微调 dLLM，重塑置信度动态以支持更激进的并行解码。arXiv 2025.
- [09/22/2025] **[Spiffy: Multiplying Diffusion LLM Acceleration via Lossless Speculative Decoding](https://arxiv.org/abs/2509.18085)** — 为 dLLM 设计的 auto-speculation 推测解码，离线校准有向草稿图 + 块级双向生成，LLaDA/Dream/SDAR 上最高 6.3× 无损加速。*Sudhanshu Agrawal et al.*, arXiv 2025.
- [05/28/2025] **[Fast-dLLM: Training-free Acceleration of Diffusion LLM by Enabling KV Cache and Parallel Decoding](https://arxiv.org/abs/2505.22618)** — 块级近似 KV cache + 置信度感知并行解码，LLaDA/Dream 最高 27.6× 吞吐提升；training-free，是"置信度感知解码"谱系奠基工作。*Chengyue Wu, Hao Zhang, Shuchen Xue, et al.*, ICLR 2026. [[code]](https://github.com/NVlabs/Fast-dLLM)
- [05/26/2025] **[Adaptive Classifier-Free Guidance via Dynamic Low-Confidence Masking (A-CFG)](https://arxiv.org/abs/2505.20199)** — 按低置信度动态加 mask 的自适应 CFG，用于 dLLM 引导解码。arXiv 2025. [[code]](https://github.com/pixeli99/A-CFG)
- [12/13/2024] **[Simple Guidance Mechanisms for Discrete Diffusion Models](https://arxiv.org/abs/2412.10193)** — 首次系统推导离散扩散的 classifier-free / classifier-based guidance，并提出更易引导的 uniform-noise 扩散模型。*Yair Schiff, Subham Sekhar Sahoo, Hao Phung, et al.*, ICLR 2025. [[code]](https://github.com/kuleshov-group/discrete-diffusion-guidance)

## 多模态与代码 dLLM（Multimodal & Code dLLMs）

### 多模态 dLLM

- [02/15/2026] **[LaViDa-R1: Advancing Reasoning for Unified Multimodal Diffusion Language Models](https://arxiv.org/abs/2602.14147)** — 面向多模态扩散 LM 的统一后训练框架，无缝结合 SFT 与多任务 RL（GRPO 类），显著增强跨任务推理能力。*Shufan Li, Yuchen Zhu, Juxiang Gu, et al.*, ICML 2026. [[code]](https://github.com/jacklishufan/LaViDa)
- [12/17/2025] **[DiffusionVL: Translating Any Autoregressive Models into Diffusion Vision Language Models](https://arxiv.org/abs/2512.15713)** — 扩散微调框架，可将任意预训练 AR（视觉）语言模型"转译"为扩散 VLM，仅需少量微调步数。*Linyu Zeng, Jiawei Yao, Bohan Liao, et al.*, ECCV 2026. [[code]](https://github.com/hustvl/DiffusionVL)
- [12/16/2025] **[Sparse-LaViDa: Sparse Multimodal Discrete Diffusion Language Models](https://arxiv.org/abs/2512.14008)** — LaViDa 系列的稀疏化训练与采样优化技术，提升多模态 dLLM 训练/推理效率。*Shufan Li, Juxiang Gu, Kangning Liu, et al.*, arXiv 2025. [[code]](https://github.com/jacklishufan/LaViDa)
- [12/16/2025] **[SDAR-VL: Stable and Efficient Block-wise Diffusion for Vision-Language Understanding](https://arxiv.org/abs/2512.14068)** — 块扩散范式的视觉语言理解模型，通过 AR→block-diffusion 持续训练适配 VLM。*Shuang Cheng, Yuhua Jiang, Zineng Zhou, et al.*, arXiv 2025. [[code]](https://github.com/JetAstra/SDAR-VL)
- [11/10/2025] **[MMaDA-Parallel: Multimodal Large Diffusion Language Models for Thinking-Aware Editing and Generation](https://arxiv.org/abs/2511.09611)** — 并行式"先思考再生成"的文本-图像联合扩散后训练框架，发布评估推理-图像对齐的 ParaBench。*Ling Yang, Ye Tian, et al.*, ICLR 2026. [[code]](https://github.com/tyfeld/MMaDA-Parallel)
- [10/22/2025] **[ReDiff: From Denoising to Refining — A Corrective Framework for Vision-Language Diffusion Model](https://arxiv.org/abs/2510.19871)** — "去噪→修正"的视觉语言扩散后训练/推理框架，用 corrective refinement 提升 dMLLM 输出质量。*Yixin Ji, Tao Wang, Yixiao Ge, et al.*, arXiv 2025. [[project]](https://rediff-hku.github.io/)
- [09/23/2025] **[LaViDa-O: Elastic Large Masked Diffusion Models for Unified Multimodal Understanding and Generation](https://arxiv.org/abs/2509.19244)** — 将 LaViDa 扩展为理解+生成统一模型，支持弹性分辨率/长度配置的统一后训练。*Shufan Li et al.*, arXiv 2025. [[code]](https://github.com/jacklishufan/LaViDa)
- [09/09/2025] **[Lumina-DiMOO: An Omni Diffusion Large Language Model for Multi-Modal Generation and Understanding](https://arxiv.org/abs/2510.06308)** — 纯离散扩散的全模态统一理解+生成基础模型，包含多模态指令微调阶段。*Yi Xin, Qi Qin, Siqi Luo, et al.*, arXiv 2025. [[code]](https://github.com/Alpha-VLLM/Lumina-DiMOO)
- [05/23/2025] **[LaViDa: A Large Diffusion Language Model for Multimodal Understanding](https://arxiv.org/abs/2505.16839)** — 互补掩码训练策略 + 两阶段多模态 SFT，构建基于 LLaDA/Dream 骨干的扩散 VLM。*Shufan Li, Konstantinos Kallidromitis, Hritik Bansal, et al.*, NeurIPS 2025. [[code]](https://github.com/jacklishufan/LaViDa)
- [05/22/2025] **[LLaDA-V: Large Language Diffusion Models with Visual Instruction Tuning](https://arxiv.org/abs/2505.16933)** — 在 LLaDA-8B-Instruct 语言塔上做纯扩散架构的视觉指令微调（含数据 scaling 与注意力掩码消融），多模态指令跟随超过 LLaMA3-V 基线。*Zebin You, Shen Nie, Xiaolu Zhang, et al.*, arXiv 2025. [[code]](https://github.com/ML-GSAI/LLaDA)
- [05/22/2025] **[Dimple: Discrete Diffusion Multimodal Large Language Model with Parallel Decoding](https://arxiv.org/abs/2505.16990)** — 首个离散扩散多模态 LLM 之一，AR-then-diffusion 混合范式 + 结构先验 SFT 与 confident decoding，实现并行解码下的多模态指令跟随。*Runpeng Yu, Xinyin Ma, Xinchao Wang*, arXiv 2025. [[code]](https://github.com/yu-rp/Dimple)
- [05/21/2025] **[MMaDA: Multimodal Large Diffusion Language Models](https://arxiv.org/abs/2505.15809)** — 统一文本推理、多模态理解与文生图的扩散基础模型，混合长 CoT 微调（SFT）+ UniGRPO（面向扩散轨迹的统一策略梯度 RL）三阶段 post-training。*Ling Yang, Ye Tian, Bowen Li, et al.*, NeurIPS 2025. [[code]](https://github.com/Gen-Verse/MMaDA)
- [03/26/2025] **[Unified Multimodal Discrete Diffusion (UniDisc)](https://arxiv.org/abs/2503.20853)** — 单一离散扩散模型统一文本+图像联合建模，支持跨模态 infilling 与指令式编辑的微调。*Alexander Swerdlow, Mihir Prabhudesai, Siddharth Gandhi, et al.*, arXiv 2025. [[code]](https://github.com/alexanderswerdlow/unidisc)

### 代码 dLLM

- [01/22/2026] **[Stable-DiffCoder: Pushing the Frontier of Code Diffusion Large Language Model](https://arxiv.org/abs/2601.15892)** — 复用 Seed-Coder 架构与数据的块扩散代码模型，带 warmup 与 block-wise 裁剪噪声调度的持续预训练 + SFT 管线，同预算下超越 AR 对照。*Chenghao Fan, Wen Heng, Bo Li, et al.*, arXiv 2026. [[code]](https://github.com/ByteDance-Seed/Stable-DiffCoder)
- [07/15/2025] **[DreamOn: Diffusion Language Models For Code Infilling Beyond Fixed-size Canvas](https://arxiv.org/abs/2602.01326)** — 在 Dream-Coder/DiffuCoder 上训练 [expand]/[delete] 特殊标记，实现可变长代码填充。*Zirui Wu, Lin Zheng, Zhihui Xie, et al.*, ICLR 2026. [[code]](https://github.com/DreamLM/DreamOn)
- [10/2025] **[CoDA: Coding LM via Diffusion Adaptation](https://arxiv.org/abs/2510.03270)** — 通过扩散适配（AR→diffusion 改造）训练的代码 LM，开源全流程。*Salesforce AI Research*, arXiv 2025. [[code]](https://github.com/SalesforceAIResearch/CoDA)
- [09/29/2025] **[DiffTester: Accelerating Unit Test Generation for Diffusion LLMs via Repetitive Pattern](https://arxiv.org/abs/2509.24975)** — 针对扩散 LLM（含 DiffuCoder、Dream-Coder）单元测试生成的加速与适配工作。arXiv 2025.
- [09/01/2025] **[Dream-Coder 7B: An Open Diffusion Language Model for Code](https://arxiv.org/abs/2509.01142)** — 基于 Dream 架构的开源代码扩散 LM，代码数据持续预训练 + 指令微调，展现任意顺序生成与强代码 infilling 能力。*Zhihui Xie, Jiacheng Ye, Lin Zheng, et al.*, arXiv 2025. [[code]](https://github.com/DreamLM/Dream-Coder)
- [08/14/2025] **[Diffusion is a Code Repair Operator and Generator](https://arxiv.org/abs/2508.11110)** — 将代码扩散模型用作"修复算子"，探讨扩散后训练/迭代去噪在代码修复与合成数据生成中的作用。*Mukul Singh et al.*, arXiv 2025.
- [06/25/2025] **[DiffuCoder: Understanding and Improving Masked Diffusion Models for Code Generation](https://arxiv.org/abs/2506.20639)** — 130B 代码 token 训练 7B 掩码扩散模型，系统分析解码行为；提出 Coupled-GRPO（互补掩码对 t 与 T−t 耦合采样降方差），代码 dLLM + RL 代表作。*Shansan Gong, Ruixiang Zhang, Huangjie Zheng, et al.*, arXiv preprint. [[code]](https://github.com/apple/ml-diffucoder)
- [10/26/2023] **[CodeFusion: A Pre-trained Diffusion Model for Code Generation](https://arxiv.org/abs/2310.17680)** — 连续扩散代码生成模型（75M 级），早期代码扩散代表作，非 LLM 规模、无 RL 后训练。*Mukul Singh, José Cambronero, Sumit Gulwani, et al.*, EMNLP 2023. [[code]](https://github.com/microsoft/prose-benchmarks/tree/main/CodeFusion)

## 框架与开源仓库（Frameworks & Open-source Repos）

### 后训练框架 / 基准

| 名称 | 链接 | 说明 |
|---|---|---|
| Gen-Verse/dLLM-RL (TraceRL) | [GitHub](https://github.com/Gen-Verse/dLLM-RL) | 最全面的 dLLM RL 后训练框架，TraDo 系列模型 |
| ZHZisZZ/dllm | [GitHub](https://github.com/ZHZisZZ/dllm) | 统一 dLLM 训练/评测/推理库，支持 LLaDA/Dream 的 SFT（arXiv 2602.22661） |
| Block-R1 | [GitHub](https://github.com/YanJiangJerry/Block-R1) | 多领域 dLLM RL 后训练基准，复现 d1/WD1 等算法 |
| DiRL | [GitHub](https://github.com/OpenMOSS/DiRL) | 高效 dLLM RL 后训练框架（arXiv 2512.22234），提出 DiPO（无偏 GRPO） |
| DARE | [GitHub](https://github.com/yjyddq/DARE) | dLLM 对齐与 RL 统一评测执行框架（arXiv 2604.04215），基于 verl + OpenCompass |

### 基础模型官方仓库

| 仓库 | 简介 |
|---|---|
| [ML-GSAI/LLaDA](https://github.com/ML-GSAI/LLaDA) | LLaDA 官方实现，含预训练+SFT 指南 |
| [Gen-Verse/MMaDA](https://github.com/Gen-Verse/MMaDA) | MMaDA 官方仓库，CoT 微调 + UniGRPO |
| [DreamLM/Dream](https://github.com/DreamLM/Dream) | Dream 7B 官方仓库 |
| [NVlabs/Fast-dLLM](https://github.com/NVlabs/Fast-dLLM) | 免训练 KV Cache + 并行解码加速 |
| [apple/ml-diffucoder](https://github.com/apple/ml-diffucoder) | DiffuCoder 官方实现，含 Coupled-GRPO |
| [dllm-reasoning/d1](https://github.com/dllm-reasoning/d1) | d1 官方实现：masked SFT + diffu-GRPO |
| [ML-GSAI/LLaDA-V](https://github.com/ML-GSAI/LLaDA-V) | LLaDA-V 视觉指令微调官方代码 |
| [DreamLM/Dream-Coder](https://github.com/DreamLM/Dream-Coder) | Dream-Coder 7B，adaptation→SFT 全流程 |
| [SalesforceAIResearch/CoDA](https://github.com/SalesforceAIResearch/CoDA) | Salesforce 扩散代码语言模型 |
| [facebookresearch/SPG](https://github.com/facebookresearch/SPG) | SPG 官方代码（Meta） |
| [martian422/MaskGRPO](https://github.com/martian422/MaskGRPO) | MaskGRPO 官方实现（ICLR 2026） |

### 相关 Awesome 列表

- [VILA-Lab/Awesome-DLMs](https://github.com/VILA-Lab/Awesome-DLMs) — 综述《A Survey on Diffusion Language Models》官方列表，Training Strategies / RL 板块可直接交叉核对。
- [piesauce/awesome-dLLM-resources](https://github.com/piesauce/awesome-dLLM-resources) — 高频更新的 dLLM 论文/模型/库列表。
- [AIDASLab/Awesome-Diffusion-LLM](https://github.com/AIDASLab/Awesome-Diffusion-LLM) — 含 Alignment & RL、多模态 dLLM 分类。

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hasson827/Awesome-DLMs-post-training&type=Date)](https://star-history.com/#hasson827/Awesome-DLMs-post-training&Date)

## 贡献指南

欢迎贡献！提交前请阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 了解收录范围、条目格式与 PR 流程。

## 许可证

本作品采用 [CC0-1.0](LICENSE) 许可——可自由使用、分享与二次创作。
