---
title: "Logical Consistency as a Bridge: Improving LLM Hallucination Detection via Label Constraint Modeling between Responses and Self-Judgments"
title_zh: 逻辑一致性作为桥梁：通过响应与自我判断间的标签约束建模改进LLM幻觉检测
authors: "Hao Mi, Qiang Sheng, Shaofei Wang, Beizhe Hu, Yifan Sun, Zhengjia Wang, Hengqi Zeng, Yang Li, Danding Wang, Juan Cao"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.286.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 改进LLM幻觉检测
tldr: 现有大语言模型幻觉检测方法要么仅关注微观层面的隐式神经不确定性，要么仅依赖宏观层面的显式符号推理，未能有效利用两者之间固有的相互依赖性。本文提出LaaB框架，通过建模响应与自我判断之间的标签约束和逻辑一致性，成功将神经特征与符号推理桥接起来，为幻觉检测提供了更全面的整体视角，显著提升了检测性能与可靠性。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.286/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 805, \"height\": 880, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.286/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1642, \"height\": 812, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.286/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 783, \"height\": 633, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.286/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 798, \"height\": 796, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.286/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1604, \"height\": 562, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.286/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 794, \"height\": 725, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.286/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 819, \"height\": 379, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.286/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1638, \"height\": 1487, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.286/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 806, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.286/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1601, \"height\": 507, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.286/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 812, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.286/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 786, \"height\": 455, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.286/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 752, \"height\": 757, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.286/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 797, \"height\": 588, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.286/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1681, \"height\": 308, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.286/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 804, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.286/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1670, \"height\": 774, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.286/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1641, \"height\": 1825, \"label\": \"Table\"}]"
motivation: 现有幻觉检测方法孤立地处理隐式神经不确定性和显式符号推理，未能利用两者的相互依赖性。
method: 提出LaaB框架，通过建模响应与自我判断之间的标签约束和逻辑一致性，桥接神经特征与符号推理。
result: 实验表明LaaB有效结合了神经和符号特征，显著提升了大语言模型的幻觉检测性能。
conclusion: 桥接神经特征与符号推理的逻辑一致性为LLM幻觉检测提供了更全面有效的解决方案。
---

## Abstract
Large Language Models (LLMs) are prone to factual hallucinations, risking their reliability in real-world applications. Existing hallucination detectors mainly extract micro-level intrinsic patterns for uncertainty quantification or elicit macro-level self-judgments through verbalized prompts. However, these methods address only a single facet of the hallucination, focusing either on implicit neural uncertainty or explicit symbolic reasoning, thereby treating these inherently coupled behaviors in isolation and failing to exploit their interdependence for a holistic view. In this paper, we propose LaaB (Logical Consistency-as-a-Bridge), a framework that bridges neural features and symbolic judgments for hallucination detection. LaaB introduces a "meta-judgment" process to map symbolic labels back into the feature space. By leveraging the inherent logical bridge where response and meta-judgment labels are either the same or opposite based on the self-judgment’s semantics, LaaB aligns and integrates dual-view signals via mutual learning and enhances the hallucination detection. Extensive experiments on 4 public datasets, across 4 LLMs, against 8 baselines demonstrate the superiority of LaaB.

---

## 论文详细总结（自动生成）

# 论文总结：Logical Consistency as a Bridge: Improving LLM Hallucination Detection via Label Constraint Modeling between Responses and Self-Judgments

## 1. 核心问题与整体含义
- **核心问题**：大语言模型（LLM）容易产生事实性幻觉，现有幻觉检测方法通常只关注单一视角——要么提取微观层面的内在模式（如隐状态、logits等隐式神经不确定性），要么依赖宏观层面的自我判断（如提示模型自评的显式符号推理）。这两种视角本质上是耦合的，但现有方法将其孤立处理，未能利用其相互依赖性。
- **整体含义**：本文旨在打破微观神经特征与宏观符号推理之间的壁垒，通过挖掘模型“响应”与“自我判断”之间固有的逻辑约束关系，构建一个双视角互学习的整体框架，从而更全面、准确地检测LLM幻觉。

## 2. 论文提出的方法论
- **核心思想**：提出 LaaB（Logical Consistency-as-a-Bridge）框架。该框架将LLM的“自我判断”本身视为一种可能带有幻觉的“特殊响应”（即元判断，Meta-judgment），并利用响应标签与元判断标签之间的逻辑一致性作为桥梁，通过互学习将神经特征与符号判断对齐并整合。
- **关键技术细节**：
  - **响应幻觉建模**：使用检测器 $D_r$ 提取原始响应的内在特征 $F_r$（隐状态、logits或注意力分数），预测响应的事实性分布 $S_r$。
  - **自我判断幻觉建模**：使用检测器 $D_j$ 提取模型自我判断生成过程的内在特征 $F_j$，预测判断本身的事实性分布 $S_j$。
  - **逻辑约束**：基于自我判断的语义建立逻辑依赖。若判断为“Yes”（肯定响应），则响应标签与判断标签一致（$L_r = L_j$）；若判断为“No”（否定响应），则两者标签相反（$L_r = 1 - L_j$）。
  - **逻辑约束互学习**：使用 Huber 损失对齐 $D_r$ 和 $D_j$ 的预测概率。为防止弱检测器误导强检测器，引入基于置信度的加权机制（比较同伴与自身在真实标签上的预测置信度），并动态计算梯度范数平衡系数 $\alpha$。
- **算法流程**：
  - **阶段一（异步互学习）**：$D_r$ 和 $D_j$ 轮流训练，当一个收敛后冻结，继续训练另一个。
  - **阶段二（联合微调）**：解冻两个检测器，使用结合交叉熵损失和加权逻辑损失的总损失进行联合优化。
  - **推理阶段**：仅部署 $D_r$，无需生成自我判断，从而不增加额外推理成本。

## 3. 实验设计
- **数据集**：TriviaQA, MMLU, NQ_Open, HaluEval（涵盖问答、多任务、长文本等场景）。
- **LLM模型**：Llama-3.1-8B-Instruct, Llama-3.1-70B-Instruct, Qwen-2.5-32B-Instruct, Mistral-7B-Instruct-v0.3。
- **Benchmark与评估指标**：幻觉检测二分类任务，采用 Macro F1 (macF1) 和 Accuracy (Acc) 作为评估指标。
- **对比方法**：共8种基线，包括自我判断法、基于采样的方法，以及基于内在模式的方法（SAPLMA, Logits Lens, Lookback Lens, LapEigvals, TSV）。

## 4. 资源与算力
- **算力资源**：附录E提及效率测试在配备单张 NVIDIA A800 GPU 的服务器上进行（batch size=128）。
- **未明确信息**：论文未明确说明完整实验所需的总训练时长或GPU数量，但强调推理延迟极低（如基于隐状态的LaaB推理延迟仅约0.0215 ms/instance）。

## 5. 实验数量与充分性
- **实验数量**：
  - 主实验：4个LLM × 4个数据集 × 多种基线及增强版对比。
  - 变体分析：对比仅用 $D_j$、仅用 $D_r$ 和两者结合的推理效果。
  - 泛化实验：留一法跨数据集泛化测试。
  - 深入分析：预测正确性转移分析、不同响应长度下的性能分析。
  - 扩展基线：补充了LapEigvals和TSV两种基线的对比。
- **充分性与客观性**：实验非常充分。覆盖了不同参数规模（7B-70B）和不同架构的模型，验证了方法在多种内在特征（隐状态、logits、注意力）上的普适性；消融实验逻辑清晰，公平对比了有无LaaB框架的性能差异。

## 6. 论文的主要结论与发现
- LaaB 框架能持续提升基于内在模式的基线检测器性能，其中基于隐状态的检测器（SAPLMA）提升最显著且整体表现最好。
- 基于内在模式的检测器普遍优于基于自我判断或采样的方法，说明内部表征包含更丰富的事实性信号。
- 互学习成功将自我判断视角的知识蒸馏到了响应检测器 $D_r$ 中，使得推理时仅需 $D_r$ 即可获得性能提升，且不增加推理负担。
- LaaB 提升了模型跨数据集的泛化能力，且对长文本响应的幻觉检测改善尤为明显。

## 7. 优点
- **视角新颖**：创造性地将“自我判断”视为可能产生幻觉的生成行为（元判断），而非直接作为真实标签，巧妙利用了逻辑一致性作为神经与符号的桥梁。
- **推理高效**：训练时双视角互学习，推理时丢弃判断分支，实现了零额外推理成本的性能提升。
- **设计鲁棒**：引入置信度感知的加权机制和动态梯度平衡系数，有效避免了互学习中弱检测器拖累强检测器的问题。

## 8. 不足与局限
- **提示词约束**：强制LLM以“Yes”或“No”作答，抑制了模型表达“我不知道”的倾向，可能引入噪声影响检测器训练。
- **双重错误的理论极限**：如果内在模式检测器和自我判断同时出错，逻辑约束无法纠正（尽管联合优化对真实标签的学习能挽回极小部分此类样本）。
- **软约束局限**：使用的逻辑约束损失是软约束，不能保证最终模型对每个样本都严格满足逻辑一致性。
- **白盒限制**：方法依赖提取LLM的内部状态（隐状态、logits等），仅适用于LLM服务提供方进行内部监控，第三方黑盒API用户无法使用。

（完）
