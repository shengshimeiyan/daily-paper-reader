---
title: Mitigating Hallucinations in Large Vision-Language Models without Performance Degradation
title_zh: 在不降低性能的情况下缓解大型视觉语言模型中的幻觉
authors: "Xingyu Zhu, Junfeng Fang, Shuo Wang, Beier Zhu, Zhicai Wang, Yonghui Yang, Xiangnan He"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.89.pdf"
tags: ["query:llm-halluc"]
score: 7.0
evidence: 缓解视觉语言模型中的幻觉
tldr: 现有基于表示的视觉语言模型幻觉缓解方法常因提取不完全和非选择性参数更新，导致通用生成能力下降。本文提出双阶段框架MPD，在不降低性能的情况下选择性缓解幻觉成分。实验表明，MPD能有效缓解视觉语言模型幻觉，同时保持通用生成能力不下降，其选择性缓解思路对大语言模型幻觉缓解亦具有重要借鉴意义。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.89/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1646, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.89/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 646, \"height\": 381, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.89/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1411, \"height\": 799, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.89/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 759, \"height\": 453, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.89/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 536, \"height\": 388, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.89/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 537, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.89/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 535, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.89/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 535, \"height\": 388, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.89/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1454, \"height\": 538, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.89/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1328, \"height\": 1132, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.89/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 833, \"height\": 472, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.89/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 764, \"height\": 378, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.89/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 637, \"height\": 457, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.89/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1436, \"height\": 468, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.89/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1225, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.89/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1246, \"height\": 358, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.89/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 693, \"height\": 408, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.89/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 824, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.89/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 781, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.89/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 798, \"height\": 318, \"label\": \"Table\"}]"
motivation: 现有基于表示的视觉语言模型幻觉缓解方法常因提取不完全和非选择性更新导致通用能力下降。
method: 提出双阶段框架MPD，在不降低性能的情况下选择性缓解幻觉成分。
result: 实验表明MPD能有效缓解视觉语言模型幻觉，同时保持通用生成能力不下降。
conclusion: 选择性地提取和缓解幻觉成分可以在不牺牲模型通用能力的前提下有效缓解幻觉。
---

## Abstract
Large Vision-Language Models (LVLMs) exhibit powerful generative capabilities but frequently produce hallucinations that compromise output reliability. Fine tuning on annotated data devoid of hallucinations offers the most direct solution, while its high computational cost motivates recent representation-based methods, which focus on mitigating hallucinatory components within hidden representations. Though efficient, we empirically observe that these methods degrade general generation capacity due to incomplete extraction of hallucination components and non-selective parameter updates. To address these limitations, we propose MPD, a dual-stage framework for mitigating hallucinations without performance degradation. Specifically, our MPD relies on two essential factors: (1) semantic-aware component disentanglement to extract pure hallucination components, and (2) interpretable parameter updates that selectively modify parameters most relevant to hallucination. Extensive experiments demonstrate that MPD achieves state-of-the-art performance, reducing hallucinations by 23.4% while maintaining 97.4% of general generative capability as evaluated on LLaVA-Bench and MME, with no additional computational cost.

---

## 论文详细总结（自动生成）

# 论文总结：在不降低性能的情况下缓解大型视觉语言模型中的幻觉

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：大型视觉语言模型（LVLMs）在生成过程中频繁产生“幻觉”（如虚构不存在的物体、错误属性等），严重影响输出的可靠性。
- **现有方法的痛点**：当前基于表示干预的无训练方法（如Nullu）虽然高效，但会导致模型的通用生成能力下降（表现为语义不连贯、词汇重复率上升）。
- **痛点归因**：
  - **提取不完全**：幻觉成分与通用语义成分高度耦合，现有方法在提取时未解耦，导致通用语义被误伤移除。
  - **非选择性参数更新**：现有方法对目标层的所有权重进行大规模更新，严重破坏了原始参数分布，导致过拟合。
- **整体含义**：亟需一种能够在精准剥离并抑制幻觉成分的同时，最小化对模型原有参数和通用能力干扰的缓解框架。

## 2. 方法论：核心思想、关键技术细节与算法流程
- **核心思想**：提出双阶段框架 **MPD**（Mitigating hallucinations without Performance Degradation），通过“语义感知的成分解耦”提取纯净幻觉成分，并通过“可解释的选择性参数更新”仅修改与幻觉最相关的参数。
- **阶段一：语义感知的成分解耦（提取纯净幻觉成分）**
  - **构建对比对**：利用辅助LLM构建对比查询对（包含诱导幻觉的提示 $X^-$ 和语义等价且忠实的提示 $X^+$）。
  - **正交投影提取**：
    - 对忠实表示 $X^+$ 进行SVD分解，得到忠实语义子空间的投影矩阵 $P_\ell$。
    - 将幻觉表示 $X^-$ 投影到忠实子空间的正交补空间上，提取出与通用语义正交的纯净幻觉成分：$\tilde{X}_\ell = (I - P_\ell)X^-_\ell$。
- **阶段二：可解释的选择性参数更新**
  - **参数选择**：计算权重矩阵中各行向量与幻觉成分 $\tilde{X}_\ell$ 的平均余弦相似度，选出相似度最高的 Top-K 权重向量（即最负责幻觉生成的参数）。
  - **参数编辑**：构建幻觉子空间的零空间投影矩阵 $\tilde{Q}_\ell = I - \tilde{X}^\top_\ell(\tilde{X}_\ell\tilde{X}^\top_\ell)^{-1}\tilde{X}_\ell$。
  - 仅对选出的 Top-K 权重进行投影更新：$w^{(i)}_\ell \leftarrow \tilde{Q}_\ell w^{(i)}_\ell$，从而消除该权重中的幻觉方向，保留其他方向。

## 3. 实验设计：数据集、Benchmark与对比方法
- **基础模型**：MiniGPT-4 V2, LLaVA-1.5-7B, mPLUG-Owl2。
- **数据集与Benchmark**：
  - **目标幻觉评估**：MSCOCO（CHAIR, POPE, OPOPE指标）、MME（Existence, Count等子集）、HallusionBench、AMBER、MMHalBench。
  - **通用生成能力评估**：LLaVA-Bench（开放对话）、MME（感知与推理）、V* Bench、MMMU、MathVision（非物体幻觉及多模态推理）。
- **对比方法**：DoLa, OPERA, VCD, LURE, HALC, Nullu。

## 4. 资源与算力
- **算力资源**：文中明确提到所有实验均在**单张 A40 GPU (40G)** 上完成。
- **推理开销**：MPD在推理阶段不引入额外计算成本，与原始模型贪婪解码相比延迟极小（3.7s vs 3.1s）。
- **训练时长**：文中未明确提及参数编辑过程的耗时，但强调其属于轻量级的一次性离线编辑。

## 5. 实验数量与充分性
- **实验数量**：实验非常丰富，包含3个基础模型、9个以上Benchmark数据集/指标、6种基线方法对比，以及针对编辑层范围、样本量、SVD保留维度、Top-K权重数量、辅助LLM选择等多组消融实验，还包含隐藏表示分布的可视化分析与效率对比。
- **充分性与客观性**：
  - **充分**：涵盖了从句子级、实例级到表示级的评估，同时兼顾了物体幻觉与通用生成/推理能力的测试。
  - **客观公平**：严格遵循前人（Nullu等）的数据划分与评估协议，使用相同的数据对进行编辑，并在多个不同架构的LVLM上验证了泛化性。

## 6. 主要结论与发现
- **性能提升**：MPD在大幅缓解幻觉（幻觉率降低23.4%）的同时，保留了97.4%的通用生成能力（LLaVA-Bench和MME评估）。
- **理论保障**：正交投影提取的幻觉成分比简单的差值提取更纯净，数学上证明了其估计误差更小。
- **表示分布保留**：可视化显示MPD编辑后的模型隐藏表示分布与原始模型高度对齐，而现有方法则发生严重偏移。
- **参数高效**：选择性更新使得参数扰动大幅减少（在mPLUG-Owl2上减少42%，MiniGPT4上减少37%），且推理零额外开销。

## 7. 优点
- **精准解耦**：通过正交投影巧妙分离了纠缠的通用语义与幻觉语义，避免了“一刀切”导致的通用能力损失。
- **最小化干预**：基于余弦相似度的选择性参数编辑策略，仅修改“罪魁祸首”的神经元，极大保护了模型原有知识。
- **即插即用且高效**：无需重训模型，推理无额外延迟，具有极高的工程落地价值。
- **理论支撑**：不仅有经验效果，还提供了严谨的数学证明支撑其成分提取的优越性。

## 8. 不足与局限
- **偏差与提示限制**：无法解决由更广泛的数据偏差或提示词本身局限性引起的幻觉。
- **评估局限**：现有的自动化Benchmark可能无法完全捕捉长文本的连贯性或风格的多样性。
- **极端场景未验证**：在高度模糊的视觉输入下的鲁棒性仍有待评估。
- **依赖辅助LLM**：对比对的构建依赖外部LLM（如GPT-3.5/5.1），虽然文中验证了不同LLM的鲁棒性，但仍存在一定的外部依赖和离线构建成本。

（完）
