---
title: "Stable-RAG: Mitigating Retrieval-Permutation-Induced Hallucinations in Retrieval-Augmented Generation"
title_zh: Stable-RAG：缓解检索增强生成中检索排列引起的幻觉
authors: "Qianchi Zhang, Hainan Zhang, Liang Pang (庞亮), Hong-Wei Zheng, Zhiming Zheng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1188.pdf"
tags: ["query:llm-halluc"]
score: 8.0
evidence: 缓解检索增强生成中的幻觉
tldr: 检索增强生成虽能减少事实幻觉，但对检索文档的排列顺序高度敏感，导致答案大幅变化并引发幻觉。本文提出Stable-RAG方法，旨在缓解由检索排列引起的幻觉，增强模型对文档顺序的鲁棒性。实验表明，Stable-RAG能有效缓解检索排列引起的幻觉，提升生成事实一致性，解决了影响生成可靠性的一个被忽视的关键因素。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 370, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 807, \"height\": 338, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 765, \"height\": 855, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1570, \"height\": 314, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1583, \"height\": 296, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1630, \"height\": 373, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 803, \"height\": 780, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 670, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 769, \"height\": 792, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 805, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1656, \"height\": 688, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 639, \"height\": 420, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1661, \"height\": 1671, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1188/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1659, \"height\": 1807, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1188/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 761, \"height\": 415, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1188/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 828, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1188/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 805, \"height\": 299, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1188/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 798, \"height\": 193, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1188/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1188/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1468, \"height\": 437, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1188/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 775, \"height\": 217, \"label\": \"Table\"}]"
motivation: 检索增强生成中，检索文档的排列顺序会导致模型答案大幅变化，引发未被充分探索的幻觉。
method: 提出Stable-RAG方法，缓解检索排列引起的幻觉，增强模型对文档顺序的鲁棒性。
result: 实验表明Stable-RAG能有效缓解检索排列引起的幻觉，提升生成事实一致性。
conclusion: 解决检索排列敏感性是缓解检索增强生成中幻觉、提升事实一致性的关键。
---

## Abstract
Retrieval-Augmented Generation (RAG) has become a key paradigm for reducing factual hallucinations in Large Language Models (LLMs), yet little is known about how the order of retrieved documents affects model behavior. We empirically show that under a Top-5 retrieval setting with the gold document included, LLM answers vary substantially across permutations of the retrieved set, even when the gold document is fixed in the first position. This reveals a previously underexplored sensitivity to retrieval permutations. Although existing robust RAG methods focus primarily on enhancing LLM robustness to low-quality retrieval and mitigating positional bias to distribute attention fairly over long contexts, neither approach directly addresses permutation sensitivity. In this paper, we propose Stable-RAG, which exploits permutation sensitivity estimation to mitigate permutation-induced hallucinations. Stable-RAG runs the generator under multiple retrieval orders, clusters hidden states, and decodes from a cluster-center representation that captures the dominant reasoning pattern. It then uses these reasoning results to align hallucinated outputs toward the correct answer, encouraging the model to produce consistent and accurate predictions across document permutations. Experiments on three QA datasets show that Stable-RAG improves answer accuracy, reasoning consistency, and generalization across datasets, retrievers, and input lengths compared with strong baselines.

---

## 论文详细总结（自动生成）

# 论文总结：Stable-RAG

## 1. 核心问题与整体含义（研究动机和背景）
*   **核心问题**：检索增强生成（RAG）系统对检索文档的排列顺序高度敏感。即使检索集包含金标准文档且固定在首位，仅改变其他文档的顺序也会导致大语言模型（LLM）产生截然不同的推理路径和答案，这种现象被称为“排列引起的幻觉”。
*   **现有方法的不足**：现有的鲁棒RAG方法主要关注提升对低质量检索（噪声）的鲁棒性或缓解长上下文中的位置偏差，但均未直接解决由文档排列顺序引起的推理不一致问题。
*   **深层原因**：通过逐层分析隐藏状态发现，排列敏感性源于LLM内部推理动力学的结构不稳定性。浅层推理轨迹较集中，而中高层出现显著分歧，导致幻觉风险增加。

## 2. 方法论：核心思想、关键技术细节与算法流程
*   **核心思想**：提出 **Stable-RAG**，利用排列敏感性估计来缓解排列引起的幻觉。通过在多种检索顺序下运行生成器，聚类隐藏状态以捕获主导推理模式，并利用这些结果通过DPO对齐幻觉输出，鼓励模型在不同排列下产生一致且准确的预测。
*   **算法流程**：分为三个阶段：
    1.  **隐藏状态聚类**：
        *   **状态提取**：对于查询和Top-5文档，枚举所有排列（120种），提取生成前最后一层最后一个token的隐藏状态 $h^{(i)}$。
        *   **谱聚类**：构建相似度矩阵 $A_{ij} = \exp(-\frac{1 - \cos(h^{(i)}, h^{(j)})}{\sigma})$，计算归一化拉普拉斯矩阵 $L = I - D^{-1/2}AD^{-1/2}$。通过特征间隔自适应确定聚类数 $K$。
        *   **代表解码**：计算每个簇的质心 $\mu_k$，选择距离质心最近的隐藏状态作为代表，仅解码这些代表状态以减少计算开销（从 $N!$ 降至 $K$）。
    2.  **偏好数据构建**：根据解码结果与真实答案的对比，构建四类偏好数据对 $(x, y_w, y_l)$：
        *   **FC（完全正确）**：所有排列均正确，不参与训练。
        *   **PC（部分正确）**：$y_w$ 为最高频正确答案，$y_l$ 为最高频错误答案。
        *   **FU（完全错误且不可回答）**：无金文档，$y_w$ 为“我不知道”，$y_l$ 为最高频错误答案。
        *   **FA（完全错误但可回答）**：有金文档，$y_w$ 为金答案，$y_l$ 为“我不知道”。
    3.  **DPO对齐**：使用直接偏好优化（DPO）训练基础模型，最大化偏好答案 $y_w$ 的似然。

## 3. 实验设计
*   **数据集**：
    *   单跳QA：NaturalQuestions (NQ), TriviaQA
    *   多跳QA：HotpotQA
*   **评估指标**：Substring Exact Match (SubEM) 和 F1 分数。
*   **检索器**：DPR 和 Contriever-MS MARCO。
*   **对比方法**：
    *   **Vanilla方法**：Direct Generation, Vanilla RAG, Vanilla SFT。
    *   **鲁棒RAG方法**：RetRobust, ATM, RAAT。
    *   **位置偏差方法**：Pos2Distill, Ms-PoE。

## 4. 资源与算力
*   **硬件**：2 块 NVIDIA RTX PRO 6000 GPU。
*   **训练时长**：每个 epoch 约需 2 小时。
*   **模型**：LLaMA3-8B-Instruct, Qwen3-8B。

## 5. 实验数量与充分性
*   **实验数量**：
    *   主实验：3个数据集 × 2个模型 × 2个检索器。
    *   消融实验：针对PC、FA、FU组件的4组消融。
    *   对比实验：与Standard DPO的对比。
    *   泛化性实验：跨数据集、跨检索器、跨Top-K设置。
    *   分析实验：训练数据量影响、内部模型行为分析（PSR指标）、原始vs打乱顺序对比。
*   **充分性与客观性**：实验设计非常充分且全面。不仅涵盖了不同类型的QA任务和不同规模的模型，还深入分析了跨检索器和跨上下文长度的泛化能力。消融实验细致地验证了每种数据构造类型的贡献，且所有基线方法在相同的检索集和测试集下进行评估，保证了公平性。

## 6. 主要结论与发现
*   **排列敏感性普遍存在**：LLM对文档顺序高度敏感，即使金文档在首位也可能产生幻觉，且这种敏感性随模型深度增加而加剧。
*   **Stable-RAG有效性**：在所有数据集和检索器上，Stable-RAG均优于所有强基线，提升了答案准确性和推理一致性。
*   **鲁棒性与泛化性**：Stable-RAG显著降低了扰动成功率（PSR），对文档位置扰动表现出更强的外部鲁棒性，且在跨数据集、跨检索器和不同Top-K设置下均表现出良好的泛化能力。
*   **机制解释**：DPO训练后，模型减少了高敏感样本的聚类数量，稳定了高敏感表示，同时保留了低敏感样本的多样性。

## 7. 优点
*   **问题新颖**：首次系统性地揭示并定义了RAG中的“排列引起的幻觉”问题，填补了现有研究关注噪声和长文本位置偏差之外的空白。
*   **机制深入**：通过逐层隐藏状态聚类和可视化，从机制上解释了排列敏感性的来源（中高层推理轨迹分歧）。
*   **方法高效**：提出的“代表解码”策略将解码次数从 $N!$ 降至 $K$，大幅降低了计算和标注成本。
*   **策略全面**：数据构建策略（FC/PC/FU/FA）巧妙地结合了正确答案强化、错误答案校准和拒答机制。

## 8. 不足与局限
*   **层级约束缺失**：方法仅在最终层表示层面稳定推理，未对中间层的推理轨迹进行显式正则化约束。
*   **计算开销**：尽管使用了代表解码，但构建数据仍需枚举大量排列并进行谱聚类，相比标准RAG仍有不可忽视的计算和标注开销。
*   **外部依赖**：依赖外部检索文档进行 grounding，如果文档本身包含偏见或错误，模型可能会传播或放大这些错误。
*   **可靠性边界**：虽然减少了排列引起的幻觉，但无法保证输出完全正确，在高风险领域仍需谨慎。

（完）
