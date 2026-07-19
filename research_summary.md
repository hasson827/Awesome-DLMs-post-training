# Awesome-DLMs-post-training · 调研汇总（research_summary）

> ⚠️ **说明**：本文档为中间调研产物，修正结论见 `verification_results.md`；正式列表以 `README.md` / `README_zh.md` 为准。
>
> 本文档由 8 个调研子代理（RL/GRPO、DPO/偏好优化、SFT、综述与训练技术、蒸馏与效率、多模态与代码 dLLM、GitHub 仓库验证、Awesome 规范）的结果去重整合而成。**所有条目均来自子代理调研输出，未新造论文**；标注 **[待核实]** 的字段为子代理未能完全确认的信息（作者、venue、arXiv 编号、GitHub 链接等），收录前建议逐条到 arXiv / GitHub 复核。

## 领域简介

扩散语言模型（Diffusion Language Models, DLM）以迭代去噪替代自回归逐 token 生成，2025 年 LLaDA、Dream 等 7–8B 级开源模型出现后，"后训练"（post-training）迅速成为核心研究方向：如何用 SFT 赋予指令跟随能力、用 GRPO/DPO 类方法做推理与对齐、用蒸馏/引导/推测解码训练实现少步高效生成，以及向多模态与代码领域扩展。本仓库聚焦 **DLM 的后训练**：SFT / RL / 偏好优化 / 蒸馏 / 高效适配，兼收奠基性训练目标与综述。

## 建议分类体系

1. [Surveys（综述）](#1-surveys)
2. [RL & Reasoning（GRPO/策略梯度/RLVR）](#2-rl--reasoning)
3. [Preference Optimization（DPO/KTO/对齐）](#3-preference-optimization)
4. [SFT & Instruction Tuning](#4-sft--instruction-tuning)
5. [Training Objectives & Techniques（训练目标/适配/长上下文）](#5-training-objectives--techniques)
6. [Efficiency & Distillation（蒸馏/引导/少步/推测解码）](#6-efficiency--distillation)
7. [Multimodal & Code dLLMs](#7-multimodal--code-dllms)
8. [Open-source Frameworks & Repos（开源框架与仓库）](#8-open-source-frameworks--repos)

---

## 1. Surveys

- [08/14/2025] **A Survey on Diffusion Language Models**
  - **Authors:** Tianyi Li, Mingda Chen, Bowei Guo, Zhiqiang Shen · arXiv 2025
  - **TL;DR:** 目前最全面的 DLM 综述，系统梳理预训练、SFT、RL 对齐、推理加速与应用，含专门的后训练章节。
  - [arXiv](https://arxiv.org/abs/2508.10875) · [GitHub](https://github.com/VILA-Lab/Awesome-DLMs)

- [06/2025] **Discrete Diffusion in Large Language and Multimodal Models: A Survey**
  - **Authors:** Runpeng Yu, Qi Li, Xinchao Wang · arXiv 2025
  - **TL;DR:** 聚焦离散扩散在大语言与多模态模型中的公式化、训练与推理，覆盖 LLaDA/Dream/Dimple 等。
  - [arXiv](https://arxiv.org/abs/2506.13759) · [GitHub](https://github.com/LiQiiiii/DLLM-Survey)

- [2024] **Diffusion Models in Text Generation: A Survey** [待核实：具体链接/卷期信息]
  - **Authors:** Qiuhua Yi, Xiangfan Chen, et al. · PeerJ Computer Science 2024
  - **TL;DR:** 较早的文本生成扩散模型综述，适合追溯 Diffusion-LM 时代的连续扩散文本工作（在 2509.26488 参考文献中确认存在：PeerJ Comput. Sci. 10:e1905）。

---

## 2. RL & Reasoning

- [07/16/2026] **Mask-Aware Policy Gradients for Diffusion Language Models** [待核实：日期在未来，可能为预告页]
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 掩码感知的扩散 LM 策略梯度方法。
  - [arXiv](https://arxiv.org/abs/2607.15200)

- [06/30/2026] **SLIM-RL: Risk-Budgeted Random-Masking RL for Diffusion LLMs Without Trajectory Slicing**
  - **Authors:** Ruikang Zhao, Zhenting Wang, Han Gao, Ligong Han · arXiv 2026
  - **TL;DR:** 针对 TraceRL 轨迹切片成本随块大小增长的问题，用 τ-budget 解码器约束提交风险 + 无轨迹随机掩码目标。
  - [arXiv](https://arxiv.org/abs/2607.00208)

- [05/13/2026] **Beyond Mode-Seeking RL: Trajectory-Balance Post-Training for Diffusion Language Models**
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 引入 trajectory-balance（GFlowNet 式）目标缓解 mode-seeking RL 的多样性坍缩。
  - [arXiv](https://arxiv.org/abs/2605.13935)

- [05/11/2026] **Relative Score Policy Optimization for Diffusion Language Models (RSPO)**
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 用相对得分替代似然做组内策略优化。
  - [arXiv](https://arxiv.org/abs/2605.10218)

- [03/13/2026] **RL for Diffusion LLMs with Entropy-Guided Step Selection and Stepwise Advantages (EGSPO)**
  - **Authors:** Vishnu Teja 等 [待核实] · arXiv 2026
  - **TL;DR:** 熵引导选择关键去噪步并分配步级优势，降低 dLLM RL 的方差与成本。
  - [arXiv](https://arxiv.org/abs/2603.12554) · [GitHub](https://github.com/vishnutez/egspo-dllm-rl)

- [03/2026] **LFPO: Likelihood-Free Policy Optimization for Masked Diffusion Models**
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 彻底绕开似然计算的无似然 RLVR 策略优化，规避现有方法的高方差近似问题。
  - [arXiv](https://arxiv.org/abs/2603.01563)

- [02/06/2026] **Diffusion-State Policy Optimization for Masked Diffusion Language Models (DSPO)**
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 以扩散中间状态为决策状态设计策略优化，而非仅在最终序列上打分。
  - [arXiv](https://arxiv.org/abs/2602.06462)

- [01/21/2026] **The Flexibility Trap: Why Arbitrary Order Limits Reasoning Potential in Diffusion Language Models (JustGRPO)**
  - **Authors:** LeapLabTHU（清华）[具体作者待核实] · arXiv 2026
  - **TL;DR:** 论证任意顺序生成的灵活性并非必要，简单 GRPO 直接移植即可匹敌复杂扩散专用 RL 改造（以 ESPO 为对照基线）。
  - [arXiv](https://arxiv.org/abs/2601.15165) · [GitHub](https://github.com/LeapLabTHU/JustGRPO)

- [01/05/2026] **Progressive Block Scaling for MDMs Through Trajectory-Aware RL (T\*)**
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 基于 TraceRL 的课程式渐进块大小扩展训练方案。
  - [arXiv](https://arxiv.org/abs/2601.11214)

- [12/24/2025] **dUltra: Ultra-Fast Diffusion Large Language Models via Reinforcement Learning**
  - **Authors:** [待核实] · arXiv 2025
  - **TL;DR:** 用 GRPO 学习"路径规划器"（解掩码顺序/并行度），在保持质量的同时大幅加速扩散 LLM 解码。
  - arXiv: https://arxiv.org/abs/2512.21446 （编号来自效率子代理；RL 子代理标注 [待核实]，建议复核） · [GitHub](https://github.com/chinsengi/dUltra-os)

- [12/10/2025] **d-TreeRPO: Towards More Reliable Policy Optimization for Diffusion Language Models**
  - **Authors:** [待核实] · arXiv 2025
  - **TL;DR:** 树状分组/rollout 组织方式提升 dLLM 策略优化可靠性。
  - [arXiv](https://arxiv.org/abs/2512.09675)

- [12/09/2025] **Learning Unmasking Policies for Diffusion Language Models**
  - **Authors:** [待核实，见 arXiv 页] · arXiv 2025（v3 2026-03）
  - **TL;DR:** 不同于固定置信度采样，用 RL 学习独立的"解掩码顺序策略"模块，与 DCoLT/UPM 一脉相承。
  - [arXiv](https://arxiv.org/abs/2512.09106)

- [12/03/2025] **Principled RL for Diffusion LLMs Emerges from a Sequence-Level Perspective (ESPO)**
  - **Authors:** Jingyang Ou, Jiaqi Han, Minkai Xu, Shaoxuan Xu, Jianwen Xie, Stefano Ermon, Yi Wu, Chongxuan Li（人大/Stanford/清华）· ICLR 2026
  - **TL;DR:** 把整条序列生成当作单一动作，用 ELBO 作序列级似然代理 + 逐 token 归一化重要性比率，Countdown 上较 token 级基线提升 20–40 点。
  - [arXiv](https://arxiv.org/abs/2512.03759) · [GitHub](https://github.com/ML-GSAI/ESPO)

- [10/24/2025] **MRO: Enhancing Reasoning in Diffusion Language Models via Multi-Reward Optimization**
  - **Authors:** [待核实] · arXiv 2025
  - **TL;DR:** 多奖励联合优化提升 dLLM 推理能力。
  - [arXiv](https://arxiv.org/abs/2510.21473)

- [10/13/2025] **Boundary-Guided Policy Optimization for Memory-Efficient RL of Diffusion LLMs (BGPO)**
  - **Authors:** Nianyi Lin, Jiajie Zhang, Lei Hou, Juanzi Li（清华 KEG）· arXiv 2025
  - **TL;DR:** 利用块扩散的边界结构最大化 ELBO 线性下界，显著降低 RL 训练显存开销。
  - [arXiv](https://arxiv.org/abs/2510.11683) · [GitHub](https://github.com/THU-KEG/BGPO)

- [10/10/2025] **SPG: Sandwiched Policy Gradient for Masked Diffusion Language Models**
  - **Authors:** Chengyu Wang, Paria Rashidinejad, DiJia Su, Song Jiang, Sid Wang, Siyan Zhao, … Tommi Jaakkola, Feiyu Chen 等（Meta/MIT/UCLA）· arXiv 2025（仓库标注 ICLR 2026）
  - **TL;DR:** 用 log-likelihood 上下界"夹逼"构造三明治目标做策略梯度，显著优于 ELBO 类方法（d1/wd1）。
  - [arXiv](https://arxiv.org/abs/2510.09541) · [GitHub](https://github.com/facebookresearch/SPG)

- [10/09/2025] **Improving Reasoning for Diffusion Language Models via Group Diffusion Policy Optimization (GDPO)**
  - **Authors:** Kevin Rojas, Jiahe Lin, Kashif Rasul, Anderson Schneider, Yuriy Nevmyvaka, Molei Tao, Wei Deng（Morgan Stanley 等）· arXiv 2025
  - **TL;DR:** GRPO 的扩散化改造，改进组内相对优势在去噪步上的分配，超越 diffu-GRPO。
  - [arXiv](https://arxiv.org/abs/2510.08554)

- [10/09/2025] **Enhancing Reasoning for Diffusion LLMs via Distribution Matching Policy Optimization (DMPO)**
  - **Authors:** Yuchen Zhu, Wei Guo, Jaemoo Choi, Petr Molodyk, Bo Yuan, Molei Tao, Yongxin Chen（Gatech 等）· arXiv 2025
  - **TL;DR:** 将 RL 表述为分布匹配问题，避免直接估计不可解似然。
  - [arXiv](https://arxiv.org/abs/2510.08233)

- [10/05/2025] **Principled and Tractable RL for Reasoning with Diffusion Language Models**
  - **Authors:** Anthony Zhan（单作者）· arXiv 2025
  - **TL;DR:** 从原则出发推导扩散 LLM 上可处理的 RL 目标，给出更严格的似然近似与更新规则，替代 ELBO/一步估计等偏置代理。
  - [arXiv](https://arxiv.org/abs/2510.04019)

- [10/2025] **MaskGRPO: Consolidating Reinforcement Learning for Multimodal Discrete Diffusion Models**
  - **Authors:** [待核实] · ICLR 2026
  - **TL;DR:** 统一 LLaDA/MMaDA 的 GRPO 训练框架。
  - [arXiv](https://arxiv.org/abs/2510.02880) · [GitHub](https://github.com/martian422/MaskGRPO)

- [10/02/2025] **Step-Aware Policy Optimization for Reasoning in Diffusion Large Language Models (SAPO)** [待核实：缩写/作者]
  - **Authors:** Shangda Xie, Lingdong Kong, Xuan Song, … Eric P. Xing, K. Zhang [待核实] · arXiv 2025
  - **TL;DR:** 引入去噪步级的过程奖励，引导 dLLM 沿潜在推理层级逐步取得进展。
  - [arXiv](https://arxiv.org/abs/2510.01544)

- [10/02/2025] **DiFFPO: Training Diffusion LLMs to Reason Fast and Furious via Reinforcement Learning**
  - **Authors:** Hanyang Zhao, Dawen Liang, Wenpin Tang, David Yao, Nathan Kallus（Netflix/Columbia 等）· arXiv 2025
  - **TL;DR:** 统一 RL 框架联合训练模型与采样器策略，同时提升推理准确率并降低延迟，改善准确率/计算帕累托前沿。
  - [arXiv](https://arxiv.org/abs/2510.02212)

- [09/29/2025] **Advantage Weighted Matching: Aligning RL with Pretraining in Diffusion Models (AWM)**
  - **Authors:** Sanghui Xue, Chao Ge, Shilong Zhang, Yang Li, Zhi-Ming Ma（中科院等）[作者列表待核实] · arXiv 2025
  - **TL;DR:** 将 RL 更新写成与扩散预训练目标同构的优势加权匹配形式，使 RL 微调与预训练目标对齐、稳定高效。
  - [arXiv](https://arxiv.org/abs/2509.25050)

- [09/28/2025] **Taming Masked Diffusion Language Models via Consistency Trajectory RL with Fewer Decoding Steps (CJ-GRPO)**
  - **Authors:** Jingyi Yang, Guanxu Chen, Xuhao Hu, Jing Shao · arXiv 2025
  - **TL;DR:** 强调 rollout 与优化轨迹一致性，解决 MDLM 非因果解码与 AR 式 RL 之间的训练-推理不一致。
  - [arXiv](https://arxiv.org/abs/2509.23924)

- [09/12/2025] **Inpainting-Guided Policy Optimization for Diffusion Large Language Models (IGPO)**
  - **Authors:** Siyan Zhao, Mengchen Liu, Jing Huang, Miao Liu, … Aditya Grover, Feiyu Chen（UCLA/Meta）· arXiv 2025
  - **TL;DR:** 利用扩散模型部分 inpainting 能力，在 rollout 中注入部分真实答案片段引导探索，缓解稀疏奖励下的探索困难。
  - [arXiv](https://arxiv.org/abs/2509.10396) · [GitHub](https://github.com/facebookresearch/igpo)

- [09/08/2025] **Revolutionizing Reinforcement Learning Framework for Diffusion Large Language Models (TraceRL / TraDo)**
  - **Authors:** Yinjie Wang, Ling Yang, Bowen Li, Ye Tian, Ke Shen, Mengdi Wang 等（Princeton/PKU）· ICLR 2026
  - **TL;DR:** 轨迹感知 RL，将训练目标与模型实际推理轨迹对齐，配合扩散价值模型降方差；衍生 TraDo-4B/8B 及首个长 CoT 扩散模型 TraDo-8B-Thinking；dLLM-RL 是最全面的 dLLM 后训练开源框架。
  - [arXiv](https://arxiv.org/abs/2509.06949) · [GitHub](https://github.com/Gen-Verse/dLLM-RL)

- [08/18/2025] **MDPO: Overcoming the Training-Inference Divide of Masked Diffusion Language Models**
  - **Authors:** Chaofan Lin 等（autonomousvision）[部分待核实] · arXiv 2025
  - **TL;DR:** 按推理时的渐进精炼调度优化策略，弥合 MDLM 训练与推理过程的不一致。
  - [arXiv](https://arxiv.org/abs/2508.13148) · [GitHub](https://github.com/autonomousvision/mdpo)

- [07/07/2025] **wd1: Weighted Policy Optimization for Reasoning in Diffusion Language Models**
  - **Authors:** Xiaohang Tang, Rares Dolga, Sangwoong Yoon, Ilija Bogunovic（UCL）[作者名两来源不一致：Xiaohang/Xiaoyu Tang，待核实] · arXiv 2025
  - **TL;DR:** 对低优势样本重新加权而非丢弃，改进 diffu-GRPO 的样本效率与计算开销，GSM8k/MATH/Sudoku/Countdown 上超越 d1。
  - [arXiv](https://arxiv.org/abs/2507.08838) · [GitHub](https://github.com/xiaohangt/wd1)

- [05/14/2025] **Reinforcing the Diffusion Chain of Lateral Thought with Diffusion Language Models (DCoLT)**
  - **Authors:** Zemin Huang, Zhiyang Chen, Zijun Wang, Tiancheng Li, Guo-Jun Qi（Westlake/MAPLE Lab）· arXiv 2025
  - **TL;DR:** 把扩散反向采样中间步视为"思考动作"，用结果奖励 RL 优化整条去噪轨迹；LLaDA 上提出 Unmask Policy Module (UPM) 用 Plackett-Luce 建模解掩码顺序。
  - [arXiv](https://arxiv.org/abs/2505.10446) · [GitHub](https://github.com/maple-research-lab/LLaDOU)

- [04/16/2025] **d1: Scaling Reasoning in Diffusion Large Language Models via Reinforcement Learning**
  - **Authors:** Siyan Zhao, Devaansh Gupta, Qinqing Zheng, Aditya Grover（UCLA）· NeurIPS 2025
  - **TL;DR:** 提出 diffu-GRPO，用均值场近似 + 随机掩码 prompt 的单次前向估计序列/token 对数概率，SFT+RL 两阶段显著提升 LLaDA 的数学/规划推理能力。**本方向奠基性工作。**
  - [arXiv](https://arxiv.org/abs/2504.12216) · [GitHub](https://github.com/dllm-reasoning/d1)

- [02/03/2025] **Fine-Tuning Discrete Diffusion Models with Policy Gradient Methods (SEPO)**
  - **Authors:** Oussama Zekri, Nicolas Boullé · arXiv 2025
  - **TL;DR:** 较早将策略梯度方法系统用于离散扩散模型微调的探索性工作。
  - [arXiv](https://arxiv.org/abs/2502.01384) · [GitHub](https://github.com/ozekri/SEPO)

- [10/17/2024] **DRAKES: Fine-Tuning Discrete Diffusion Models via Reward Optimization with Applications to DNA and Protein Design**
  - **Authors:** Chenyu Wang 等 · ICLR 2025
  - **TL;DR:** 将整条反向扩散链纳入奖励反向传播的离散扩散奖励微调框架（生物序列设计，方法直接适用于文本 MDM）。
  - [arXiv](https://arxiv.org/abs/2410.13643) · [GitHub](https://github.com/ChenyuWang-Monica/DRAKES)

- [02/19/2024] **Text Diffusion with Reinforced Conditioning**
  - **Authors:** [待核实] · arXiv 2024
  - **TL;DR:** 最早的文本扩散 + 强化学习对齐尝试之一，用强化条件机制按奖励微调文本扩散模型。
  - [arXiv](https://arxiv.org/abs/2402.14843)

---

## 3. Preference Optimization

- [10/26/2025] **Aligning Diffusion Language Models via Unpaired Preference Optimization**
  - **Authors:** Vaibhav Jindal 等 · arXiv 2025
  - **TL;DR:** 将 KTO（unpaired preference optimization）适配到 dLLM，用 ELBO 替代不可解的 log-likelihood，无需成对偏好数据即可对齐。
  - [arXiv](https://arxiv.org/abs/2510.23658) · [GitHub](https://github.com/vaibhavjindal/elbo-kto)

- [09/27/2025] **A2D: Any-Order, Any-Step Safety Alignment for Diffusion Language Models**
  - **Authors:** [待核实] · arXiv 2025
  - **TL;DR:** 针对 dLLM 任意顺序、任意步数解码特点的安全对齐方法，缓解 dLLM 独特的越狱脆弱性。
  - [arXiv](https://arxiv.org/abs/2509.23286)

- [08/17/2025] **Where to Start Alignment? Diffusion Large Language Model May Demand a Distinct Position**
  - **Authors:** [待核实] · arXiv 2025
  - **TL;DR:** 分析性工作，指出 dLLM 的对齐起点/数据位置与 AR 模型本质不同，为 dLLM 对齐提供设计指导。
  - [arXiv](https://arxiv.org/abs/2508.12398)

- [05/25/2025] **LLaDA 1.5: Variance-Reduced Preference Optimization for Large Language Diffusion Models (VRPO)**
  - **Authors:** Fengqi Zhu, Rongzhen Wang, Shen Nie, Xiaolu Zhang, … Ji-Rong Wen, Chongxuan Li（人大高瓴/蚂蚁）· arXiv 2025
  - **TL;DR:** 首次系统地将 DPO 迁移到 masked diffusion LM，提出 VRPO——无偏蒙特卡洛预算分配 + 对偶采样降低 ELBO 偏好优化方差。**偏好优化方向奠基性工作。**
  - [arXiv](https://arxiv.org/abs/2505.19223) · [GitHub](https://github.com/ML-GSAI/LLaDA-1.5)

---

## 4. SFT & Instruction Tuning

- [12/2025] **LLaDA2.0: Scaling Up Diffusion Language Models to 100B**
  - **Authors:** T. Bie, M. Cao, K. Chen 等（inclusionAI/蚂蚁）· arXiv 2025
  - **TL;DR:** 将扩散语言模型扩展到 100B 并给出完整 post-training（SFT + 对齐）流程。
  - [arXiv](https://arxiv.org/abs/2512.15745) · [GitHub](https://github.com/inclusionAI/LLaDA2.X)

- [09/29/2025] **LLaDA-MoE: A Sparse MoE Diffusion Language Model**
  - **Authors:** Fengqi Zhu, Zebin You, Jiamei Wen 等（RUC ML-GSAI）· arXiv 2025
  - **TL;DR:** 20T token 预训练的 7B-A1B MoE 扩散模型，经 prompt-response 对 SFT 得到 Instruct 版，详细披露数据工程与 MoE 下 SFT 配方。
  - [arXiv](https://arxiv.org/abs/2509.24389) · GitHub：未找到官方仓库 [待核实]

- [08/21/2025] **Dream 7B: Diffusion Large Language Models**
  - **Authors:** Jiacheng Ye, Zhihui Xie, Lin Zheng, Jiahui Gao, Zirui Wu, Xin Jiang, Zhenguo Li, Lingpeng Kong · arXiv 2025
  - **TL;DR:** AR 初始化 + 上下文自适应 token 级噪声重调度；发布 Dream-Base 与 Dream-Instruct（SFT 版），最强开源指令微调扩散模型基线之一。
  - [arXiv](https://arxiv.org/abs/2508.15487) · [GitHub](https://github.com/DreamLM/Dream)

- [02/14/2025] **Large Language Diffusion Models (LLaDA)**
  - **Authors:** Shen Nie, Fengqi Zhu, Zebin You, Xiaolu Zhang, Jingyang Ou, Jun Hu, Jun Zhou, Yankai Lin, Ji-Rong Wen, Chongxuan Li · NeurIPS 2025
  - **TL;DR:** 8B masked diffusion LM 从头预训练 + SFT（只对 response 加噪），首次证明扩散范式下 SFT 可获得与 LLaMA3-8B 相当的指令跟随能力。
  - [arXiv](https://arxiv.org/abs/2502.09992) · [GitHub](https://github.com/ML-GSAI/LLaDA)

- [08/23/2023] **Diffusion Language Models Can Perform Many Tasks with Scaling and Instruction-Finetuning**
  - **Authors:** Jiasheng Ye, Zaixiang Zheng, Yu Bao, Lihua Qian, Quanquan Gu · arXiv 2023（AAAI 2025 [待核实]）
  - **TL;DR:** 最早的 diffusion LM instruction tuning 工作——MLM 预训练 + "diffusive adaptation" 重编程，证明指令微调可赋予扩散 LM zero/few-shot 能力。
  - [arXiv](https://arxiv.org/abs/2308.12219) · [GitHub](https://github.com/yegcjs/DiffusionLLM)

- [10/2022] **DiffuSeq: Sequence to Sequence Text Generation with Diffusion Models**
  - **Authors:** Shansan Gong, Mukai Li, Jiangtao Feng, Zhiyong Wu, Lingpeng Kong · ICLR 2023
  - **TL;DR:** 将条件 seq2seq 任务作为扩散模型的条件微调，扩散文本模型"任务微调"的早期代表（非 LLM 规模）。
  - [arXiv](https://arxiv.org/abs/2210.08933) · [GitHub](https://github.com/Shark-NLP/DiffuSeq)

---

## 5. Training Objectives & Techniques

- [05/2026] **Don't Retrain—Align: Adapting Autoregressive LMs to Diffusion LMs via Representation Alignment**
  - **Authors:** 见 arXiv · arXiv 2026
  - **TL;DR:** 不重新训练，通过表示对齐微调把 AR LM 适配为扩散 LM，系统综述 DiffuGPT/Dream/Fast-dLLM v2 等转换配方。
  - [arXiv](https://arxiv.org/abs/2605.06885) · 代码未核实 [待核实]

- [12/2025] **WeDLM: Reconciling Diffusion Language Models with Standard Causal Attention for Fast Inference**
  - **Authors:** Aiwei Liu 等 · arXiv 2025
  - **TL;DR:** 通过拓扑重排序的微调使 dLLM 兼容标准因果注意力/KV cache 的流式并行解码。
  - [arXiv](https://arxiv.org/abs/2512.22737) · GitHub [待核实]

- [12/2025] **Efficient-DLM: From Autoregressive to Diffusion Language Models, and Beyond in Speed**
  - **Authors:** Yonggan Fu 等（NVIDIA 系）· arXiv 2025
  - **TL;DR:** 系统研究 AR→DLM 转换训练配方（含指令微调阶段）与加速。
  - [arXiv](https://arxiv.org/abs/2512.14067) · GitHub [待核实]

- [10/2025] **UltraLLaDA: Scaling the Context Length to 128K for Diffusion Large Language Models**
  - **Authors:** Guangxin He, Shen Nie, Fengqi Zhu, Binhang Yuan 等 · arXiv 2025
  - **TL;DR:** 轻量级后训练（扩散感知 NTK 外推 + 长上下文数据掩码打包）把 dLLM 上下文扩到 128K，无需从头预训练。
  - [arXiv](https://arxiv.org/abs/2510.10481) · [GitHub](https://github.com/Relaxed-System-Lab/UltraLLaDA)

- [10/07/2025] **SDAR: A Synergistic Diffusion–AutoRegression Paradigm for Scalable Sequence Generation**
  - **Authors:** JetAstra（智元）团队 · arXiv 2025
  - **TL;DR:** 块级 AR + 块内扩散的统一训练范式，1.7B–30B 规模经 SFT 得到 instruct 模型。
  - [arXiv](https://arxiv.org/abs/2510.06303) · [GitHub](https://github.com/JetAstra/SDAR)

- [09/30/2025] **Fast-dLLM v2: Efficient Block-Diffusion LLM**
  - **Authors:** Chengyue Wu, Hao Zhang, Shuchen Xue, Shizhe Diao, Yonggan Fu, Zhijian Liu, Pavlo Molchanov, Ping Luo, Song Han, Enze Xie · arXiv 2025
  - **TL;DR:** 仅用 ~1B token 的块扩散微调（含指令数据）将 AR LLM 转为并行解码 dLLM，数据效率比 Dream 路线高 500×。
  - [arXiv](https://arxiv.org/abs/2509.26328) · [GitHub](https://github.com/NVlabs/Fast-dLLM)（v2 目录）

- [06/2025] **LongLLaDA: Unlocking Long Context Capabilities in Diffusion LLMs**
  - **Authors:** Xiaoran Liu, Zhigeng Liu, Zengfeng Huang, Qipeng Guo, Ziwei He, Xipeng Qiu · AAAI 2026
  - **TL;DR:** 首个 dLLM 长度外推研究，NTK-based RoPE 外推（免训练）打通长上下文。
  - [arXiv](https://arxiv.org/abs/2506.14429) · [GitHub](https://github.com/OpenMOSS/LongLLaDA)

- [03/2025] **Block Diffusion: Interpolating Between Autoregressive and Diffusion Language Models (BD3-LM)**
  - **Authors:** Marianne Arriola, Aaron Gokaslan, Justin T. Chiu, Zhihan Yang, Volodymyr Kuleshov 等 · ICLR 2025
  - **TL;DR:** 块级自回归 + 块内扩散的混合训练目标，支持任意长度生成与 KV cache，缓解离散扩散固定长度限制。
  - [arXiv](https://arxiv.org/abs/2503.09573) · [GitHub](https://github.com/kuleshov-group/bd3lms)

- [10/23/2024] **Scaling Diffusion Language Models via Adaptation from Autoregressive Models (DiffuGPT / DiffuLLaMA)**
  - **Authors:** Shansan Gong, Shivam Agarwal, Yizhe Zhang, Jiacheng Ye 等 · ICLR 2025
  - **TL;DR:** attention mask annealing + shift 操作将 GPT-2/LLaMA 持续训练为扩散模型，明确提出后续 instruction tuning 路线并开源模型。**AR→DLM 衔接代表配方。**
  - [arXiv](https://arxiv.org/abs/2410.17891) · [GitHub](https://github.com/HKUNLP/DiffuLLaMA)

- [10/2024] **Beyond Autoregression: Discrete Diffusion for Complex Reasoning and Planning**
  - **Authors:** Jiacheng Ye, Jiahui Gao, Shansan Gong, Lingpeng Kong 等 · ICLR 2025
  - **TL;DR:** 多粒度扩散规划（先规划后生成），展示离散扩散在复杂推理/规划任务上的训练范式。
  - [arXiv](https://arxiv.org/abs/2410.14157)

- [09/2024] **Masked Diffusion Models are Secretly Time-Agnostic Masked Models and Exploit Inaccurate Categorical Sampling**
  - **Authors:** Kaiwen Zheng, Yongxin Chen, Hanzi Mao, Ming-Yu Liu, Jun Zhu, Qinsheng Zhang · arXiv 2024
  - **TL;DR:** 理论分析 MDM 训练目标与采样器的不匹配，指出可改进的训练/推理衔接点。
  - [arXiv](https://arxiv.org/abs/2409.02908)

- [06/2024] **Simple and Effective Masked Diffusion Language Models (MDLM)**
  - **Authors:** Subham Sekhar Sahoo, Marianne Arriola, Aaron Gokaslan, Justin T. Chiu, Volodymyr Kuleshov 等 · NeurIPS 2024
  - **TL;DR:** 推导 masked diffusion 的简化 ELBO（Rao-Blackwell 化），建立 SEDD 与 ELBO 的联系，成为 LLaDA 类模型的训练基础。
  - [arXiv](https://arxiv.org/abs/2406.07524) · [GitHub](https://github.com/kuleshov-group/mdlm)

- [06/2024] **Simplified and Generalized Masked Diffusion for Discrete Data**
  - **Authors:** Jiaxin Shi, Kehan Han, Zhe Wang, Arnaud Doucet, Michalis Titsias · NeurIPS 2024
  - **TL;DR:** 将 masked diffusion 目标推广并简化为可加权的交叉熵积分，与 MDLM 互为印证。
  - [arXiv](https://arxiv.org/abs/2406.04329) （编号 [待核实]，建议复核）

- [02/2024] **Diffusion of Thoughts: Chain-of-Thought Reasoning in Diffusion Language Models**
  - **Authors:** Jiacheng Ye, Shanshan Gong, Lin Zheng, Lingpeng Kong 等 · NeurIPS 2024
  - **TL;DR:** 把 CoT 推理步融入扩散去噪过程（DoT/多遍 DoTMP），"推理轨迹 SFT"方向的开创工作。
  - [arXiv](https://arxiv.org/abs/2402.07754) · [GitHub](https://github.com/HKUNLP/diffusion-of-thoughts)

- [10/2023] **SEDD: Discrete Diffusion Modeling by Estimating the Ratios of the Data Distribution**
  - **Authors:** Aaron Lou, Chenlin Meng, Stefano Ermon · ICML 2024
  - **TL;DR:** 提出 score entropy（DWDSE）目标替代 ELBO，离散扩散训练的原则性框架，效果可比 GPT-2。
  - [arXiv](https://arxiv.org/abs/2310.16834) · [GitHub](https://github.com/louaaron/Score-Entropy-Discrete-Diffusion)

- [07/2021] **D3PM: Structured Denoising Diffusion Models in Discrete State-Spaces**
  - **Authors:** Jacob Austin, Daniel D. Johnson, Jonathan Ho, Daniel Tarlow, Rianne van den Berg · NeurIPS 2021
  - **TL;DR:** 离散扩散奠基工作，提出 absorbing-state（mask）转移核与混合 VLB/交叉熵训练目标。
  - [arXiv](https://arxiv.org/abs/2107.03006)

---

## 6. Efficiency & Distillation

- [06/01/2026] **EPIC: Efficient and Parallel Inference under CFG Constraints for Diffusion Language Models** [待核实细节]
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 在 CFG 约束下实现高效并行推理（引导 + 效率交叉，偏推理侧）。
  - [arXiv](https://arxiv.org/abs/2606.00722)

- [05/22/2026] **DiLaDiff: Distilled Latent-Augmented Diffusion for Language Modeling** [待核实细节]
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 潜空间增强的蒸馏扩散语言模型。
  - [arXiv](https://arxiv.org/abs/2605.23605)

- [05/12/2026] **Self-Distilled Trajectory-Aware Boltzmann Modeling: Bridging the Training-Inference Discrepancy in DLMs**
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 自蒸馏 + 轨迹感知 Boltzmann 建模，弥合 DLM 训练-推理差距。
  - [arXiv](https://arxiv.org/abs/2605.11854)

- [05/11/2026] **Infinite Mask Diffusion for Few-Step Distillation** [待核实细节]
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 面向少步采样的无限 mask 扩散蒸馏框架。
  - [arXiv](https://arxiv.org/abs/2605.10518)

- [05/10/2026] **TAD: Temporal-Aware Trajectory Self-Distillation for Fast and Accurate Diffusion LLM** [待核实细节]
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 时间感知的轨迹自蒸馏，加速 dLLM 采样同时保持精度。
  - [arXiv](https://arxiv.org/abs/2605.09536)

- [05/08/2026] **Guidance Is Not a Hyperparameter: Learning Dynamic Control in Diffusion Language Models**
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 将引导强度从手工超参变为可学习的动态控制量进行训练。
  - [arXiv](https://arxiv.org/abs/2605.07701)

- [04/29/2026] **Cross-Architecture Distillation for Diffusion Large Language Models**
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 研究 dLLM 知识蒸馏中教师信号可靠性这一独有问题，做跨架构蒸馏。
  - [arXiv](https://arxiv.org/abs/2604.26951)

- [04/06/2026] **FlowLM: Few-Step Language Modeling via Diffusion-to-Flow Adaptation**
  - **Authors:** [待核实] · arXiv 2026
  - **TL;DR:** 将扩散 LM 适配为 flow matching 风格模型以实现少步生成。
  - [arXiv](https://arxiv.org/abs/2605.20199) （日期/编号组合建议复核）

- [01/12/2026] **d3LLM: Ultra-Fast Diffusion LLM using Pseudo-Trajectory Distillation**
  - **Authors:** Yu-Yang Qian 等 [待核实完整作者] · arXiv 2026
  - **TL;DR:** 伪轨迹蒸馏教会模型哪些 token 可在早期步自信解码，配合熵基多块解码与 KV cache 刷新，对 LLaDA/Dream 实现最高 10× 加速。
  - [arXiv](https://arxiv.org/abs/2601.07568) · 代码开源（链接 [待核实]）

- [01/05/2026] **CD4LM: Consistency Distillation and aDaptive Decoding for Diffusion Language Models**
  - **Authors:** Yihao Liang 等 [待核实完整作者] · arXiv 2026
  - **TL;DR:** 离散空间一致性蒸馏（DSCD）训练轨迹不变的学生模型，配合置信度自适应解码跳步，GSM8K 上 5.18× 提速且严格占优精度-效率帕累托前沿。
  - [arXiv](https://arxiv.org/abs/2601.02236) · 代码开源（链接 [待核实]）

- [~2025-2026] **Consistent Diffusion Language Models (multi-path consistency)** [待核实：日期/作者/venue]
  - **Authors:** H. Amin 等 [待核实] · OpenReview 投稿
  - **TL;DR:** 提出"多路径一致性"原则训练离散扩散语言模型，实现少步一致生成。
  - [OpenReview PDF](https://openreview.net/pdf?id=inXScPz1gT)

- [11/24/2025] **CDLM: Consistency Diffusion Language Models**
  - **Authors:** Minseo Kim 等 [待核实完整作者] · arXiv 2025
  - **TL;DR:** 将 consistency modeling 引入 DLM 训练，蒸馏全双向教师并沿解码轨迹对齐预测，配合块级因果注意力兼容 KV cache，3.6–14.5× 降延迟。
  - [arXiv](https://arxiv.org/abs/2511.19269) · 代码开源（链接 [待核实]）

- [11/04/2025] **SpecDiff-2: Scaling Diffusion Drafter Alignment for Faster Speculative Decoding**
  - **Authors:** J. Sandler, J. K. Christopher, T. Hartvigsen, N. Fioretto · arXiv 2025
  - **TL;DR:** 训练低延迟扩散模型作为自回归 LLM 推测解码的 drafter 并对齐草稿分布。注：目标模型是 AR LLM，属边缘相关（"扩散 drafter"）。
  - [arXiv](https://arxiv.org/abs/2511.00606) （前作 SpecDiff 编号 [待核实]）

- [10/05/2025] **Self-Speculative Decoding for Diffusion Large Language Models (SSD)**
  - **Authors:** Yifeng Gao 等 [待核实完整作者] · arXiv 2025
  - **TL;DR:** dLLM 自身同时充当 drafter 与 verifier，层次验证树单次前向验证多 token，3.46× 无损加速。
  - [arXiv](https://arxiv.org/abs/2510.04147) · 代码承诺开源（链接 [待核实]）

- [09/30/2025] **dParallel: Learnable Parallel Decoding for dLLMs**
  - **Authors:** Zigeng Chen, Gongfan Fang, Xinyin Ma, Ruonan Yu, Xinchao Wang（NUS）· ICLR 2026（据官方 README）
  - **TL;DR:** 提出 certainty-forcing distillation，在自生成轨迹上微调使 masked token 更快并行达到高置信度，GSM8K 上 256→30 步、8.5× 加速。
  - [arXiv](https://arxiv.org/abs/2509.26488) · [GitHub](https://github.com/czg1225/dParallel)

- [09/29/2025] **Ultra-Fast Language Generation via Discrete Diffusion Divergence Instruct (DiDi-Instruct)**
  - **Authors:** Haoyang Zheng, Xinyang Liu, Cindy Xiangrui Kong, Nan Jiang, … Wei Deng, Guang Lin（Purdue/UT Austin/NUS 等）· ICLR 2026（据官方 README）
  - **TL;DR:** 基于积分 KL 散度最小化的分布匹配蒸馏，将 dLLM 教师蒸馏为 8–16 步少步学生模型，64× 加速且超越教师。
  - [arXiv](https://arxiv.org/abs/2509.25035) · [GitHub](https://github.com/haoyangzheng-ai/didi-instruct)

- [09/29/2025] **Learning to Parallel: Accelerating Diffusion LLMs via Learnable Parallel Decoding (Learn2PD)**
  - **Authors:** Wenrui Bao 等 [待核实完整作者] · arXiv 2025
  - **TL;DR:** 后训练轻量过滤器模型预测各位置 token 是否与最终输出一致，逼近 oracle 并行解码策略，LLaDA 上最高 22.58×（配 KV cache 57.51×）无损加速。
  - [arXiv](https://arxiv.org/abs/2509.25188)

- [09/25/2025] **WeFT: Weighted Entropy-Driven Fine-Tuning for dLLMs**
  - **Authors:** [待核实] · arXiv 2025
  - **TL;DR:** 按 token 熵加权微调 dLLM，重塑置信度动态以支持更激进的并行解码。
  - [arXiv](https://arxiv.org/abs/2509.20863)

- [09/22/2025] **Spiffy: Multiplying Diffusion LLM Acceleration via Lossless Speculative Decoding**
  - **Authors:** Sudhanshu Agrawal 等 [待核实完整作者] · arXiv 2025
  - **TL;DR:** 为 dLLM 设计的 auto-speculation 推测解码，离线校准有向草稿图 + 块级双向生成，LLaDA/Dream/SDAR 上最高 6.3× 无损加速。
  - [arXiv](https://arxiv.org/abs/2509.18085)

- [05/28/2025] **Fast-dLLM: Training-free Acceleration of Diffusion LLM by Enabling KV Cache and Parallel Decoding**
  - **Authors:** Chengyue Wu, Hao Zhang, Shuchen Xue, Zhijian Liu, Shizhe Diao, Ligeng Zhu, Ping Luo, Song Han, Enze Xie（HKU/NVIDIA/MIT）· arXiv 2025（venue [待核实]）
  - **TL;DR:** 块级近似 KV cache + 置信度感知并行解码，LLaDA/Dream 最高 27.6× 吞吐提升。注：training-free，是"置信度感知解码"谱系奠基工作。
  - [arXiv](https://arxiv.org/abs/2505.22618) · [GitHub](https://github.com/NVlabs/Fast-dLLM)

- [05/26/2025] **Adaptive Classifier-Free Guidance via Dynamic Low-Confidence Masking** [待核实：arXiv 编号]
  - **Authors:** [待核实] · arXiv 2025（日期据 VILA-Lab/Awesome-DLMs 列表）
  - **TL;DR:** 按低置信度动态加 mask 的自适应 CFG，用于 dLLM 引导解码。

- [12/13/2024] **Simple Guidance Mechanisms for Discrete Diffusion Models**
  - **Authors:** Yair Schiff, Subham Sekhar Sahoo, Hao Phung, Guanghan Wang, Sam Boshar, … Volodymyr Kuleshov [完整列表待核实] · ICLR 2025
  - **TL;DR:** 首次系统推导离散扩散的 classifier-free / classifier-based guidance，并提出更易引导的 uniform-noise 扩散模型。
  - [arXiv](https://arxiv.org/abs/2412.10193) · 代码开源（kuleshov-group 旗下，仓库名 [待核实]）

---

## 7. Multimodal & Code dLLMs

### 多模态 dLLM

- [02/15/2026] **LaViDa-R1: Advancing Reasoning for Unified Multimodal Diffusion Language Models**
  - **Authors:** Shufan Li, Yuchen Zhu, Juxiang Gu, Kangning Liu, Zhe Lin, Yifan Chen, Molei Tao, Aditya Grover, Jason Kuen · arXiv 2026
  - **TL;DR:** 面向多模态扩散 LM 的统一后训练框架，无缝结合 SFT 与多任务 RL（GRPO 类），显著增强跨任务推理能力。
  - [arXiv](https://arxiv.org/abs/2602.14147) · GitHub [待核实]（预期在 LaViDa 仓库发布）

- [12/17/2025] **DiffusionVL: Translating Any Autoregressive Models into Diffusion Vision Language Models**
  - **Authors:** Linyu Zeng, Jiawei Yao, Bohan Liao, Hanjun Tao, Wenbo Liu, Xinchao Wang · ECCV 2026（repo 自述）
  - **TL;DR:** 扩散微调框架，可将任意预训练 AR（视觉）语言模型"转译"为扩散 VLM，仅需少量微调步数。
  - [arXiv](https://arxiv.org/abs/2512.15713) · [GitHub](https://github.com/hustvl/DiffusionVL)

- [12/16/2025] **Sparse-LaViDa: Sparse Multimodal Discrete Diffusion Language Models**
  - **Authors:** Shufan Li, Juxiang Gu, Kangning Liu, Zhe Lin, Zijun Wei, Aditya Grover, Jason Kuen · arXiv 2025
  - **TL;DR:** LaViDa 系列的稀疏化训练与采样优化技术，提升多模态 dLLM 训练/推理效率。
  - [arXiv](https://arxiv.org/abs/2512.14008) · GitHub：jacklishufan/LaViDa 同仓库 [待核实]

- [12/16/2025] **SDAR-VL: Stable and Efficient Block-wise Diffusion for Vision-Language Understanding**
  - **Authors:** Shuang Cheng, Yuhua Jiang, Zineng Zhou, Dawei Liu, Wang Tao, Linfeng Zhang, Biqing Qi, Bowen Zhou · arXiv 2025
  - **TL;DR:** 块扩散范式的视觉语言理解模型，通过 AR→block-diffusion 持续训练适配 VLM。
  - [arXiv](https://arxiv.org/abs/2512.14068) · GitHub [待核实]

- [11/10/2025] **MMaDA-Parallel: Multimodal Large Diffusion Language Models for Thinking-Aware Editing and Generation**
  - **Authors:** Ling Yang, Ye Tian 等 · ICLR 2026（repo 自述）
  - **TL;DR:** 并行式"先思考再生成"的文本-图像联合扩散后训练框架，发布评估推理-图像对齐的 ParaBench。
  - [arXiv](https://arxiv.org/abs/2511.09611) · [GitHub](https://github.com/tyfeld/MMaDA-Parallel)

- [10/22/2025] **From Denoising to Refining: A Corrective Framework for Vision-Language Diffusion Model**
  - **Authors:** Yixin Ji, Tao Wang, Yixiao Ge, Zhengdao Liu, Shuo Yang, Ying Shan, Ping Luo · arXiv 2025
  - **TL;DR:** "去噪→修正"的视觉语言扩散后训练/推理框架，用 corrective refinement 提升 dMLLM 输出质量。
  - [arXiv](https://arxiv.org/abs/2510.19871) · GitHub [待核实]

- [09/29/2025] **Recursive Introspection Mask Diffusion Vision Language Model (RISE)** [待核实：作者/venue]
  - **Authors:** [待核实] · arXiv 2025
  - **TL;DR:** 在掩码扩散 VLM 中引入递归自省机制，通过迭代式自我修正训练提升多模态理解精度。
  - [arXiv](https://arxiv.org/abs/2509.23625) · GitHub [待核实]

- [09/23/2025] **LaViDa-O: Elastic Large Masked Diffusion Models for Unified Multimodal Understanding and Generation**
  - **Authors:** Shufan Li 等 · arXiv 2025
  - **TL;DR:** 将 LaViDa 扩展为理解+生成统一模型，支持弹性分辨率/长度配置的统一后训练。
  - [arXiv](https://arxiv.org/abs/2509.19244) · GitHub：LaViDa 同仓库 [待核实]

- [09/09/2025] **Lumina-DiMOO: An Omni Diffusion Large Language Model for Multi-Modal Generation and Understanding** [待核实：arXiv 编号与仓库]
  - **Authors:** Yi Xin, Qi Qin, Siqi Luo, Kaiwen Zheng 等（Alpha-VLLM 团队）· arXiv 2025
  - **TL;DR:** 纯离散扩散的全模态统一理解+生成基础模型，包含多模态指令微调阶段。
  - arXiv: https://arxiv.org/abs/2510.06308 [待核实，请以 arXiv 检索 "Lumina-DiMOO" 为准] · GitHub: https://github.com/Alpha-VLLM/Lumina-DiMOO [待核实]

- [05/23/2025] **LaViDa: A Large Diffusion Language Model for Multimodal Understanding**
  - **Authors:** Shufan Li, Konstantinos Kallidromitis, Hritik Bansal, Akash Gokul, Yusuke Kato, Kazuki Kozuka, Jason Kuen, Zhe Lin, Kai-Wei Chang, Aditya Grover · NeurIPS 2025
  - **TL;DR:** 互补掩码训练策略 + 两阶段多模态 SFT，构建基于 LLaDA/Dream 骨干的扩散 VLM。
  - [arXiv](https://arxiv.org/abs/2505.16839) · [GitHub](https://github.com/jacklishufan/LaViDa)

- [05/22/2025] **LLaDA-V: Large Language Diffusion Models with Visual Instruction Tuning**
  - **Authors:** Zebin You, Shen Nie, Xiaolu Zhang, Jun Hu, Jun Zhou, Zhiwu Lu, Ji-Rong Wen, Chongxuan Li · arXiv 2025（ICLR 2026 提交 [待核实]）
  - **TL;DR:** 在 LLaDA-8B-Instruct 语言塔上做纯扩散架构的视觉指令微调（含数据 scaling 与注意力掩码消融），多模态指令跟随超过 LLaMA3-V 基线。
  - [arXiv](https://arxiv.org/abs/2505.16933) · [GitHub](https://github.com/ML-GSAI/LLaDA-V)

- [05/22/2025] **Dimple: Discrete Diffusion Multimodal Large Language Model with Parallel Decoding**
  - **Authors:** Runpeng Yu, Xinyin Ma, Xinchao Wang（NUS）· arXiv 2025
  - **TL;DR:** 首个离散扩散多模态 LLM 之一，AR-then-diffusion 混合范式 + 结构先验 SFT 与 confident decoding，实现并行解码下的多模态指令跟随。
  - [arXiv](https://arxiv.org/abs/2505.16990) · [GitHub](https://github.com/yu-rp/Dimple)

- [05/21/2025] **MMaDA: Multimodal Large Diffusion Language Models**
  - **Authors:** Ling Yang, Ye Tian, Bowen Li, Xinchen Zhang, Ke Shen, Yunhai Tong, Mengdi Wang（Princeton/PKU/字节）· NeurIPS 2025
  - **TL;DR:** 统一文本推理、多模态理解与文生图的扩散基础模型，混合长 CoT 微调（SFT）+ UniGRPO（面向扩散轨迹的统一策略梯度 RL）三阶段 post-training。
  - [arXiv](https://arxiv.org/abs/2505.15809) · [GitHub](https://github.com/Gen-Verse/MMaDA)

- [03/26/2025] **Unified Multimodal Discrete Diffusion (UniDisc)**
  - **Authors:** Alexander Swerdlow, Mihir Prabhudesai, Siddharth Gandhi, Deepak Pathak, Katerina Fragkiadaki（CMU）· arXiv 2025
  - **TL;DR:** 单一离散扩散模型统一文本+图像联合建模，支持跨模态 infilling 与指令式编辑的微调。
  - [arXiv](https://arxiv.org/abs/2503.20853) · GitHub: https://github.com/aswerdlow935/unidisc [待核实]

### 代码 dLLM

- [09/29/2025] **DiffTester: Accelerating Unit Test Generation for Diffusion LLMs via Repetitive Pattern** [与后训练相关性较弱，可选收录]
  - **Authors:** [待核实] · arXiv 2025
  - **TL;DR:** 针对扩散 LLM（含 DiffuCoder、Dream-Coder）单元测试生成的加速与适配工作。
  - [arXiv](https://arxiv.org/abs/2509.24975) · GitHub [待核实]

- [01/22/2026] **Stable-DiffCoder: Pushing the Frontier of Code Diffusion Large Language Model**
  - **Authors:** Chenghao Fan, Wen Heng, Bo Li, Sichen Liu, Yuxuan Song, Jing Su, Xiaoye Qu, Kai Shen, Wei Wei（HUST/ByteDance Seed）· arXiv 2026
  - **TL;DR:** 复用 Seed-Coder 架构与数据的块扩散代码模型，带 warmup 与 block-wise 裁剪噪声调度的持续预训练 + SFT 管线，同预算下超越 AR 对照。
  - [arXiv](https://arxiv.org/abs/2601.15892) · [GitHub](https://github.com/ByteDance-Seed/Stable-DiffCoder)

- [07/15/2025] **DreamOn: Diffusion Language Models For Code Infilling Beyond Fixed-size Canvas**
  - **Authors:** Zirui Wu, Lin Zheng, Zhihui Xie, Jiacheng Ye, Jiahui Gao, Yansong Feng, Zhenguo Li, Victoria W., Guorui Zhou, Lingpeng Kong · arXiv（v1 2025-07，2026-02 修订）
  - **TL;DR:** 在 Dream-Coder/DiffuCoder 上训练 [expand]/[delete] 特殊标记，实现可变长代码填充。
  - [arXiv](https://arxiv.org/abs/2602.01326) · 代码仓库 [待核实]（HKU NLP blog: hkunlp.github.io/blog/2025/dreamon）

- [10/2025] **CoDA: Coding LM via Diffusion Adaptation**
  - **Authors:** Salesforce AI Research · arXiv 2025
  - **TL;DR:** 通过扩散适配（AR→diffusion 改造）训练的代码 LM，开源全流程。
  - [arXiv](https://arxiv.org/abs/2510.03270) · [GitHub](https://github.com/SalesforceAIResearch/CoDA)

- [09/01/2025] **Dream-Coder 7B: An Open Diffusion Language Model for Code**
  - **Authors:** Zhihui Xie, Jiacheng Ye, Lin Zheng, Jiahui Gao, Jingwei Dong, Zirui Wu, Xueliang Zhao, Shansan Gong, Xin Jiang, Zhenguo Li, Lingpeng Kong（HKU NLP/华为）· arXiv 2025
  - **TL;DR:** 基于 Dream 架构的开源代码扩散 LM，代码数据持续预训练 + 指令微调，展现任意顺序生成与强代码 infilling 能力。
  - [arXiv](https://arxiv.org/abs/2509.01142) · [GitHub](https://github.com/DreamLM/Dream-Coder)

- [08/14/2025] **Diffusion is a Code Repair Operator and Generator**
  - **Authors:** Mukul Singh 等 · arXiv 2025
  - **TL;DR:** 将代码扩散模型用作"修复算子"，探讨扩散后训练/迭代去噪在代码修复与合成数据生成中的作用。
  - [arXiv](https://arxiv.org/abs/2508.11110) · GitHub [待核实]

- [06/25/2025] **DiffuCoder: Understanding and Improving Masked Diffusion Models for Code Generation**
  - **Authors:** Shansan Gong, Ruixiang Zhang, Huangjie Zheng, Jiatao Gu, Navdeep Jaitly, Lingpeng Kong, Yizhe Zhang（Apple/HKU）· NeurIPS 2025 [待核实最终收录状态]
  - **TL;DR:** 130B 代码 token 训练 7B 掩码扩散模型，系统分析解码行为；提出 Coupled-GRPO（互补掩码对 t 与 T−t 耦合采样降方差），代码 dLLM + RL 代表作。
  - [arXiv](https://arxiv.org/abs/2506.20639) · [GitHub](https://github.com/apple/ml-diffucoder)

- [10/26/2023] **CodeFusion: A Pre-trained Diffusion Model for Code Generation**（早期参考，可酌情剔除）
  - **Authors:** Mukul Singh, José Cambronero, Sumit Gulwani, Vu Le, Carina Negreanu, Gust Verbruggen（Microsoft）· EMNLP 2023
  - **TL;DR:** 连续扩散代码生成模型（75M 级），早期代码扩散代表作，非 LLM 规模、无 RL 后训练。
  - [arXiv](https://arxiv.org/abs/2310.17680) · 无官方开源 [待核实]

---

## 8. Open-source Frameworks & Repos

### 后训练框架 / 基准

| 名称 | 链接 | 说明 |
|---|---|---|
| Gen-Verse/dLLM-RL (TraceRL) | https://github.com/Gen-Verse/dLLM-RL | ⭐ ~511（验证时实测）· 最全面的 dLLM RL 后训练框架，TraDo 系列模型 |
| ZHZisZZ/dllm | https://github.com/ZHZisZZ/dllm | ⭐ ~2649 · 统一 dLLM 训练/评测/推理库，支持 LLaDA/Dream 的 SFT（arXiv 2602.22661） |
| Block-R1 | https://github.com/YanJiangJerry/Block-R1 | 多领域 dLLM RL 后训练基准，复现 d1/WD1 等算法 |
| DiRL | 链接 [待核实] | 2025-11，dLLM RL 后训练高效训练框架 |
| DARE | [待核实]（arXiv 2604.04215，2026-04） | dLLM 对齐与 RL 统一评测执行框架 |

### 基础模型官方仓库（star 数为验证时实测）

| 仓库 | Stars | 简介 |
|---|---|---|
| [ML-GSAI/LLaDA](https://github.com/ML-GSAI/LLaDA) | ~3899 | LLaDA 官方实现，含预训练+SFT 指南 |
| [Gen-Verse/MMaDA](https://github.com/Gen-Verse/MMaDA) | ~1660 | MMaDA 官方仓库，CoT 微调 + UniGRPO |
| [DreamLM/Dream](https://github.com/DreamLM/Dream) | ~1255 | Dream 7B 官方仓库 |
| [NVlabs/Fast-dLLM](https://github.com/NVlabs/Fast-dLLM) | ~1062 | 免训练 KV Cache + 并行解码加速 |
| [apple/ml-diffucoder](https://github.com/apple/ml-diffucoder) | ~830 | DiffuCoder 官方实现，含 Coupled-GRPO |
| [Gen-Verse/dLLM-RL](https://github.com/Gen-Verse/dLLM-RL) | ~511 | TraceRL 官方代码 |
| [dllm-reasoning/d1](https://github.com/dllm-reasoning/d1) | ~454 | d1 官方实现：masked SFT + diffu-GRPO |
| [ML-GSAI/LLaDA-V](https://github.com/ML-GSAI/LLaDA-V) | ~347 | LLaDA-V 视觉指令微调官方代码 |
| [DreamLM/Dream-Coder](https://github.com/DreamLM/Dream-Coder) | ~106 | Dream-Coder 7B，adaptation→SFT 全流程 |
| [SalesforceAIResearch/CoDA](https://github.com/SalesforceAIResearch/CoDA) | ~65 | Salesforce 扩散代码语言模型 |
| [facebookresearch/SPG](https://github.com/facebookresearch/SPG) | ~62 | SPG 官方代码（Meta） |
| [martian422/MaskGRPO](https://github.com/martian422/MaskGRPO) | ~19 | MaskGRPO 官方实现（ICLR 2026） |

### 相关 Awesome 列表（竞品/交叉核对来源）

- [VILA-Lab/Awesome-DLMs](https://github.com/VILA-Lab/Awesome-DLMs) — ⭐ ~1143，综述《A Survey on Diffusion Language Models》官方列表，Training Strategies / RL 板块可直接交叉核对。
- [piesauce/awesome-dLLM-resources](https://github.com/piesauce/awesome-dLLM-resources) — 高频更新的 dLLM 论文/模型/库列表。
- [AIDASLab/Awesome-Diffusion-LLM](https://github.com/AIDASLab/Awesome-Diffusion-LLM) — ⭐ ~89，含 Alignment & RL、多模态 dLLM 分类。

---

## 附：未解决 / 需向用户确认的条目

1. **"Any-Order RL"**（任务简报提及）：未找到以此精确命名的工作；最接近的是 JustGRPO 与 Learning Unmasking Policies / DCoLT。
2. **"DUS"**（任务简报提及）：未能定位确切论文；最接近候选为 UniDisc（2503.20853）。
3. 2026 年 5–6 月新预印本密集（piesauce 列表持续更新），正式发布前建议用 arXiv API 批量复核 [待核实] 条目的编号、作者与日期。
