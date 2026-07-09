---
title: "ReFL: Reflective Feedback Learning for Hallucination Detection of Large Language Models"
title_zh: ReFL：用于大语言模型幻觉检测的反思反馈学习
authors: "Cunhang Fan, Jun Zhang, Xue Zhang, Shuai Zhang, Zhao Lv, Jianhua Tao, Zhengqi Wen"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.899.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 通过纠正性上下文学习进行幻觉检测
tldr: 针对现有幻觉检测方法依赖外部知识导致成本高或提取内部状态导致泛化差的问题，提出了ReFL幻觉检测框架。该框架利用纠正性上下文学习，动态引导大语言模型识别自身预测错误并调整内部表示，且无需更新模型权重，在降低计算成本的同时提升了检测的泛化能力。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.899/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1658, \"height\": 908, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.899/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 797, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.899/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1651, \"height\": 992, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1610, \"height\": 849, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1606, \"height\": 846, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1663, \"height\": 441, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 804, \"height\": 401, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 802, \"height\": 235, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 808, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 753, \"height\": 139, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 665, \"height\": 411, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 639, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 804, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1646, \"height\": 440, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1646, \"height\": 441, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1647, \"height\": 445, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 802, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1610, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1649, \"height\": 293, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.899/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 778, \"height\": 233, \"label\": \"Table\"}]"
motivation: 现有幻觉检测方法依赖外部知识成本高，或提取内部状态泛化差，限制了实时应用。
method: 提出ReFL框架，利用纠正性上下文学习动态引导模型识别预测错误并调整内部表示。
result: 无需更新模型权重即可实现幻觉检测，降低了成本并提升了泛化能力。
conclusion: 纠正性上下文学习为大语言模型幻觉检测提供了一种高效且泛化能力强的新方法。
---

## Abstract
Large Language Models (LLMs) often generate factually incorrect content, known as “hallucinations”, which undermine the reliability and safety of their outputs. Existing hallucination detection methods either depend on external knowledge sources, incurring high computational costs and limiting real-time applicability, or extract the model’s internal states, leading to poor generalization. To address these issues, this paper proposes ReFL, a hallucination detection framework. ReFL leverages corrective in-context learning to dynamically guide LLMs to recognize their own prediction errors and adjust internal representations, critically without updating model weights. Specifically, by introducing a corrective in-context learning strategy, where triplets of input text, model prediction, and ground-truth label are embedded into the prompt to make the model explicitly aware of its own errors. The model reflects on prior outputs to adjust its internal states and generate semantically structured representations better aligned with factuality. This feedback mechanism encourages the model to shape a more coherent semantic space and enhances the LLM’s internal sensitivity to hallucinations. Experimental results on two benchmark datasets demonstrate that ReFL consistently outperforms existing methods, achieving state-of-the-art performance.

---

## 论文详细总结（自动生成）

# 论文总结：ReFL: Reflective Feedback Learning for Hallucination Detection of Large Language Models

## 1. 核心问题与整体含义（研究动机和背景）
* **核心问题**：大语言模型（LLMs）经常生成看似合理但事实错误的内容（即“幻觉”），严重影响了其在高风险领域的可靠性与安全性。
* **现有方法的痛点**：
  * **依赖外部知识的方法**：计算成本高，限制了实时应用能力。
  * **基于内部状态探测的方法**：将内部状态视为静态特征，缺乏动态干预和自反馈机制，导致泛化能力差（例如跨领域或跨句法结构时性能骤降）。
* **整体含义与动机**：受人类“反思与反馈”认知机制（从错误中学习）的启发，探讨LLM能否通过“观察自身错误”来调整内部推理模式，从而在不更新模型权重的前提下，动态重塑内部表示空间，提升对幻觉的敏感度。

## 2. 方法论：核心思想、关键技术细节与流程
* **核心思想**：提出ReFL（Reflective Feedback Learning）框架，通过**纠正性上下文学习**，将模型的预测错误作为负反馈信号嵌入提示词中，动态引导LLM调整其内部状态，使其生成更符合事实结构的语义表示。
* **关键技术与流程**：
  1. **纠正性上下文学习生成（CICL）**：
     * 首先使用标准k-shot ICL对测试样本 $x$ 进行预测，得到预测标签 $\hat{y}$。
     * 构建**纠正性三元组** $t_i = (x_i, \hat{y}_i, y_i)$，显式编码模型预测与真实标签的关系。预测错误时作为负反馈，预测正确时作为正对齐信号。
     * 构建CICL输入序列：$Input_{CICL} = C_{CICL} || (x, \hat{y}, ?)$，即将纠正性三元组作为上下文，连同测试输入及其预测标签输入模型，让模型“看到”自己过去的输出并进行反思。
  2. **幻觉分类器训练**：
     * **特征提取**：提取LLM最后一层最后一个Token的隐藏嵌入作为特征向量（视为模型对输入语义的最终理解）。
     * **分类器设计**：使用多层感知机（MLP），包含三个隐藏层（维度分别为256, 128, 64），激活函数为ReLU，输出层使用Sigmoid映射为概率 $P \in [0, 1]$。前向传播公式为：$P = MLP(ReLU(W \cdot H + b))$。
     * **损失函数**：使用二元交叉熵损失（BCE）进行优化，整个过程中**LLM的权重保持冻结**。

## 3. 实验设计：数据集、Benchmark与对比方法
* **数据集/场景**：
  * **True-False**：跨领域事实声明数据集，涵盖动物、城市、公司等6个语义独立的主题，用于评估跨领域泛化能力。
  * **LogicStruct**：包含肯定、否定、合取、析取4种句法结构，用于评估跨句法结构的泛化能力（训练集为肯定句，测试集为其他结构）。
  * **TruthfulQA**：真实世界QA场景，用于评估复杂现实幻觉检测能力。
* **评估指标**：准确率（ACC）、AUC（或AUROC）。
* **对比方法**：
  * 基于概率：LN-PP。
  * 基于内部状态：SAPLMA, MIND, MM。
  * 基于提示引导：PRISM (PRISM-MM, PRISM-SAPLMA)。
  * 基于一致性/不确定性（仅TruthfulQA）：SelfCheckGPT, Semantic Entropy。

## 4. 资源与算力
* 文中明确提到了使用的算力资源：
  * **效率分析实验**：在单张 **NVIDIA H100** GPU 上进行。
  * **主实验及补充实验**：在单张 **NVIDIA A800** GPU 上进行。
* 训练时长方面，文中给出了True-False数据集上LLaMA2-7B的运行时间对比：ReFL的特征提取时间为68.43秒，训练时间为60.48秒，总耗时128.91秒，在所有对比方法中最短。

## 5. 实验数量与充分性
* **实验数量**：
  * 涉及7种不同参数规模和架构的LLM（LLaMA2-7B/13B, LLaMA3-8B, OPT-6.7b, Qwen2.5-3B/7B/14B）。
  * 3个主要数据集评估（True-False, LogicStruct, TruthfulQA）。
  * 7项消融实验与分析：纠正三元组的影响、内部状态探测vs直接生成判断、纠正比例影响、真实QA场景、上下文示例数量k的影响、层选择影响、特征提取策略影响。
  * 内部表示的定量（方差比）与定性（t-SNE可视化）分析。
* **充分性与客观性**：实验设计非常充分且客观。不仅涵盖了多模型、多领域、多句法，还针对现有方法泛化差的痛点（特别是否定句和跨领域）进行了专门验证；所有Baseline均由作者复现以确保公平比较；消融实验详尽地验证了框架各组件的有效性。

## 6. 主要结论与发现
* **性能优越**：ReFL在两个基准数据集上均达到SOTA，在LLaMA3-8B上取得了88.1%的ACC和95.6%的AUC。
* **泛化能力显著提升**：在最具挑战性的“否定”句法结构上，ReFL准确率超过90%，远超其他方法；证明了纠正性反馈迫使模型关注“正确性结构”而非语义捷径。
* **动态重塑内部表示**：定量分析显示ReFL的方差比相比SAPLMA提升了121%，t-SNE可视化也表明幻觉与非幻觉样本的决策边界更清晰，证明反馈机制有效重塑了语义空间。
* **探测优于生成**：基于内部状态的探测（85% ACC）远优于让LLM直接生成判断（61% ACC），表明事实性信号在隐藏状态中更丰富。
* **最优纠正比例**：提示词中纠正样本的比例为50%时效果最佳，过高会引入噪声，过低则缺乏反馈信号。

## 7. 优点
* **无需参数更新**：完全通过提示词引导动态调整内部状态，不修改LLM权重，具有极高的参数效率。
* **主动干预而非被动探测**：打破了以往方法将内部状态视为静态特征的做法，首次引入“自反馈”机制主动重塑表示空间。
* **高效性**：仅需单次前向传播即可提取特征，支持批量推理，运行时间优于现有方法。
* **强泛化性**：有效解决了现有探测方法在跨领域和跨句法（特别是含否定词）上的失效问题。

## 8. 不足与局限
* **应用层级受限**：当前框架主要关注句子级别的事实性评估，尚未拓展到需要更深层次上下文理解的段落级幻觉检测。
* **闭源模型受限**：方法核心依赖提取LLM的内部状态（最后一层隐藏嵌入），因此无法直接应用于GPT-4o、Gemini等闭源商业模型。
* **依赖真实标签**：CICL的构建需要真实标签来形成纠正三元组，这在某些缺乏监督信号的实际场景中可能构成限制。

（完）
