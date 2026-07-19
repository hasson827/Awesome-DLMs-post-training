# 复核结果（2026-07-19，6 个复核子代理交叉验证，所有链接已实际访问确认）

## RL 方向
1. **Mask-Aware Policy Gradients for Diffusion Language Models** — arXiv 2607.15200（2026-07-16），Haran Raajesh, Kulin Shah, Adam Klivans, Philipp Krähenbühl (UT Austin)，COLM 2026，无官方仓库。收录。
2. **SAPO = Step-Aware Policy Optimization** — "Step-Aware Policy Optimization for Reasoning in Diffusion Large Language Models"，arXiv 2510.01544（2025-10-02），Shenghui Xie, Lingjing Kong, Xiangchen Song, Xinshi Dong, Guangyi Chen, Eric P. Xing, Kun Zhang (CMU 等)，无官方仓库。
3. **AWM (Advantage Weighted Matching)** — arXiv 2509.25050，属**图像扩散**（SD3.5/FLUX）论文，**从 dLLM 清单删除**。
4. **Learning Unmasking Policies for Diffusion Language Models** — arXiv 2512.09106（2025-12-09），Metod Jazbec, Theo X. Olausson, Louis Béthune, Pierre Ablin, Michael Kirchhof, … Marco Cuturi (Apple)，GitHub: https://github.com/apple/ml-rl-dllm
5. **d-TreeRPO** — arXiv 2512.09675（2025-12-10），Leyi Pan, Shuchang Tao, … Aiwei Liu, Lijie Wen（清华 THU-BPM/阿里），ACL 2026 Main，GitHub: https://github.com/THU-BPM/d-TreeRPO
6. **dUltra** — 正确编号 arXiv **2512.21446**（2025-12-24），Shirui Chen, Jiantao Jiao, Lillian J. Ratliff, Banghua Zhu (UW/UC Berkeley)，GitHub: https://github.com/chinsengi/dUltra-os
7. **MaskGRPO** — 标题 "Consolidating Reinforcement Learning for Multimodal Discrete Diffusion Models"，arXiv 2510.02880（2025-10-03），Tianren Ma, Mu Zhang, Yibing Wang, Qixiang Ye (UCAS)，ICLR 2026，GitHub: https://github.com/martian422/MaskGRPO
8. **wd1** — 作者为 **Xiaohang Tang**（非 Xiaoyu），arXiv 2507.08838，Rares Dolga, Sangwoong Yoon, Ilija Bogunovic (UCL)，ICLR 2026。
9. **JustGRPO** — 论文标题 "The Flexibility Trap: Rethinking the Value of Arbitrary Order in Diffusion Language Models"，arXiv **2601.15165**（2026-01-21），Zanlin Ni, Shenzhi Wang, Yang Yue, … Gao Huang（清华 LeapLab/阿里），**ICML 2026 Oral（杰出论文奖）**，GitHub: https://github.com/LeapLabTHU/JustGRPO
10. **EGSPO** — "Reinforcement Learning for Diffusion LLMs with Entropy-Guided Step Selection and Stepwise Advantages"，arXiv **2603.12554**（2026-03-13），Vishnu Teja Kunde, Fatemeh Doudi, … Jean-Francois Chamberland (Texas A&M)，GitHub: https://github.com/vishnutez/egspo-dllm-rl。注意与同名 AR-LLM 论文区分。
11. **Text Diffusion with Reinforced Conditioning (TREC)** — arXiv 2402.14843，AAAI 2024，Microsoft；**与 RL 无关**（reinforced self-conditioning），移出 RL 板块或删除。
12. **"Any-Order RL" 不存在** — 用 JustGRPO (The Flexibility Trap) 替代。

## 偏好优化 / SFT / 训练技术
13. **A2D** — "A2D: Any-Order, Any-Step Safety Alignment for Diffusion Language Models"，arXiv 2509.23286（2025-09-27），Wonje Jeung 等。**是安全对齐论文，非偏好优化**，改归安全对齐类。
14. **Where to Start Alignment? Diffusion Large Language Model May Demand a Distinct Position** — arXiv 2508.12398（2025-08-17），Zhixin Xie, Xurui Song, Jun Luo (NTU)，安全对齐类。
15. **LLaDA-MoE** — arXiv 2509.24389，代码并入 https://github.com/ML-GSAI/LLaDA（无独立仓库；inclusionAI/LLaDA-MoE 为 404），权重 HF inclusionAI/LLaDA-MoE-7B-A1B-*。
16. **Efficient-DLM** — arXiv 2512.14067（NVIDIA 等），NVlabs/Efficient-DLM 为 404，代码很可能合入 https://github.com/NVlabs/Fast-dLLM，链接指向该仓库并注明。
17. **WeDLM** — arXiv 2512.22737（腾讯微信 AI 等），GitHub: https://github.com/Tencent/WeDLM ✅
18. **Don't Retrain, Align (REPR-ALIGN)** — arXiv 2605.06885（2026-05-07），Felix Z. Peng 等，无官方代码。
19. **Shi et al. 2024** = "Simplified and Generalized Masked Diffusion for Discrete Data"，arXiv **2406.04329**，NeurIPS 2024（注意勿与 MDLM 2406.07524 混淆）。
20. **"Diffusion Language Models Can Perform Many Tasks with Scaling and Instruction-Finetuning"** — arXiv 2308.12219，venue 是 **ICLR 2024**（非 AAAI 2025），GitHub: https://github.com/yegcjs/DiffusionLLM
21. **DiffuCoder** — arXiv 2506.20639，Apple+HKU，GitHub: https://github.com/apple/ml-diffucoder；**无 NeurIPS 收录证据**，venue 标 arXiv preprint。

## 效率 / 蒸馏
22. **DiLaDiff** — arXiv 2605.23605（2026-05-22，NVIDIA），项目页 https://jmlemercier.github.io/diladiff/，无独立仓库。
23. **TAD** — arXiv 2605.09536，GitHub: https://github.com/BHmingyang/TAD
24. **Infinite Mask (IMDM)** — arXiv 2605.10518，代码 https://Ugness.github.io/official_imdm
25. **TIDE (Cross-Architecture Distillation)** — arXiv 2604.26951（PKU-YuanGroup），GitHub: https://github.com/PKU-YuanGroup/TIDE
26. **FlowLM** — arXiv 2605.20199，无官方代码。
27. **EPIC** — arXiv 2606.00722；CFG 指 context-free grammar 约束解码，非 classifier-free guidance。
28. **Adaptive CFG (A-CFG)** — arXiv 2505.20199（2025-05-26），GitHub: https://github.com/pixeli99/A-CFG
29. **Consistent DLM (Amin et al.)** — arXiv 2605.00161，venue 有歧义，标 "arXiv (OpenReview)"；与 CDLM (Kim et al.) 区分。
30. **d3LLM** — arXiv 2601.07568，**ICML 2026**，GitHub: https://github.com/hao-ai-lab/d3LLM
31. **CDLM** — arXiv 2511.19269（Berkeley/Together AI），GitHub: https://github.com/SqueezeAILab/CDLM
32. **CD4LM** — arXiv 2601.02236，GitHub: https://github.com/yihao-liang/CDLM
33. **SSD (Self Speculative Decoding)** — arXiv 2510.04147，代码承诺公开但尚未发布，标 "code not released"。
34. **Simple Guidance** — arXiv 2412.10193，**ICLR 2025**，GitHub: https://github.com/kuleshov-group/discrete-diffusion-guidance
35. **Fast-dLLM** — arXiv 2505.22618，**ICLR 2026**，GitHub: https://github.com/NVlabs/Fast-dLLM；续作 v2 arXiv 2509.26328。
36. **SpecDiff 前作** — arXiv 2408.05636，**NAACL 2025**；SpecDiff-2 arXiv 2511.00606。

## 多模态 / 代码
37. **Lumina-DiMOO** — arXiv 2510.06308，GitHub: https://github.com/Alpha-VLLM/Lumina-DiMOO
38. **UniDisc** — arXiv 2503.20853 确认（CMU），GitHub: https://github.com/alexanderswerdlow/unidisc；"DUS" 条目统一改名 UniDisc。
39. **LaViDa-R1** — arXiv 2602.14147，ICML 2026（据作者主页），代码在 LaViDa 系列仓库（jacklishufan/LaViDa）。
40. **LaViDa-O** — arXiv 2509.19244，venue 标 arXiv 2025；前作 LaViDa (2505.16839) 为 NeurIPS 2025。
41. **Sparse-LaViDa** — arXiv 2512.14008。
42. **SDAR-VL** — arXiv 2512.14068，GitHub: https://github.com/JetAstra/SDAR-VL
43. **ReDiff (From Denoising to Refining)** — arXiv 2510.19871，项目页 https://rediff-hku.github.io/
44. **RISE —— 未找到 DLM 语境下的该论文，删除该条目。**
45. **DreamOn** — arXiv 2602.01326，**ICLR 2026**，GitHub: https://github.com/DreamLM/DreamOn
46. **CodeFusion** — arXiv 2310.17680，**EMNLP 2023**，代码 https://github.com/microsoft/prose-benchmarks/tree/main/CodeFusion
47. **DiffTester** — arXiv 2509.24975，无官方仓库。
48. **LLaDA-V** — arXiv 2505.16933，venue 改 **arXiv 2025**（ICLR 2026 未证实），代码并入 ML-GSAI/LLaDA。

## 框架
49. **DiRL** — arXiv 2512.22234，复旦/OpenMOSS，GitHub: https://github.com/OpenMOSS/DiRL（正确链接），提出 DiPO（无偏 GRPO），活跃。
50. **DARE** — arXiv 2604.04215，上海 AI Lab/复旦/浙大，GitHub: https://github.com/yjyddq/DARE（官方，~200 stars），基于 verl+OpenCompass 的统一后训练框架，活跃。注意多个同名干扰项勿混淆。
