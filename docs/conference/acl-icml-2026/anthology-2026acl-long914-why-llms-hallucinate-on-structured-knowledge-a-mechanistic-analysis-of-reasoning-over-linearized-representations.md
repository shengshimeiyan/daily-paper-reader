---
title: "Why LLMs Hallucinate on Structured Knowledge: A Mechanistic Analysis of Reasoning over Linearized Representations"
title_zh: 为什么大语言模型在结构化知识上产生幻觉：线性化表示推理的机制分析
authors: "Shanghao Li, Jinda Han, Yibo Wang, Yuanjie Zhu, Zihe Song, Langzhou He, Kenan Kamel A Alghythee, Philip S. Yu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.914.pdf"
tags: ["query:llm-halluc"]
score: 8.0
evidence: 结构化知识幻觉的机制分析
tldr: 针对大语言模型在处理线性化结构化知识时产生幻觉的机制进行了深入分析。研究发现幻觉并非源于随机噪声，而是由系统性的内部动态引起：注意力过度集中于捷径式结构线索，且前馈表示未能有效锚定提供的知识。该研究揭示了结构化知识推理中幻觉产生的内在机理。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.914/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1655, \"height\": 630, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.914/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 793, \"height\": 363, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.914/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 795, \"height\": 363, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.914/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 794, \"height\": 558, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.914/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 785, \"height\": 700, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.914/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 811, \"height\": 265, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.914/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 816, \"height\": 628, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.914/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1647, \"height\": 767, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.914/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 762, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.914/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 710, \"height\": 407, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.914/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 722, \"height\": 262, \"label\": \"Table\"}]"
motivation: 大语言模型在处理线性化结构化知识时仍会产生幻觉，其背后的机制尚不清楚。
method: 对模型处理线性化结构化知识时的内部动态进行机制分析，考察注意力和前馈表示。
result: 发现幻觉源于系统性内部动态，如注意力集中于捷径线索及前馈表示未能锚定知识。
conclusion: 揭示了结构化知识推理中幻觉产生的内在机理，为后续缓解幻觉提供了理论依据。
---

## Abstract
In many reasoning tasks, large language models (LLMs) rely on structured external knowledge, such as graphs and tables, which is typically linearized into sequential token representations. However, even when sufficient knowledge is available, LLMs can still produce hallucinated outputs, and the underlying mechanisms behind such failures remain poorly understood. We investigate these mechanisms and find that hallucinations arise from systematic internal dynamics rather than random noise. First, attention disproportionately concentrates toward shortcut-like structural cues rather than distributing across the full context. Second, feed-forward representations fail to ground the provided knowledge, causing the model to revert to parametric memory. Moreover, our results indicate that hallucination is consistently associated with failures in semantic grounding within feed-forward layers, while attention allocation exhibits greater task-dependent variability. Finally, we show that these mechanistic patterns generalize beyond single-hop graphs to multi-hop and tabular settings, enabling effective hallucination detection across structured knowledge formats.

---

## 论文详细总结（自动生成）

# 论文总结：为什么大语言模型在结构化知识上产生幻觉

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）在处理线性化的结构化知识（如知识图谱、表格）进行推理时，即使输入中包含了充足且准确的知识，依然会产生幻觉。目前对这种失败背后的内在机制知之甚少。
- **整体含义**：本文旨在打破黑盒观察，从Transformer内部机制（注意力头和前馈网络）出发，探究线性化结构知识与模型归纳偏置之间的固有张力如何导致系统性的内部失败，从而揭示幻觉产生的深层机理。

## 2. 论文提出的方法论
- **核心思想**：通过机制可解释性方法，解耦模型对外部证据的利用和内部记忆的依赖。提出两个互补的诊断指标，分别量化注意力层面的“结构捷径依赖”和前馈网络层面的“语义对齐漂移”。
- **关键技术细节与公式**：
  - **结构捷径依赖**：
    - **定义**：衡量模型注意力是否过度集中在连接查询与答案的最小化“核心结构线索”（如最短路径三元组），而忽略了提供关系验证的“上下文结构线索”。
    - **公式**：计算生成答案token对核心线索的注意力质量（$\alpha_{S}$）与对上下文线索的注意力质量（$\alpha_{\bar{S}}$）之差，并在所有层、头和答案token上求平均。即 $SSR = \frac{1}{L \cdot H \cdot |A|} \sum (\alpha_{l,h,i,S} - \alpha_{l,h,i,\bar{S}})$。SSR越高，说明越依赖捷径。
  - **语义对齐分数**：
    - **定义**：衡量模型内部表示是否在语义上锚定于输入提供的支持上下文集（SCS，核心线索的结构邻居扩展），评估前馈层是否发生向参数记忆的漂移。
    - **公式**：提取答案token在倒数第二层的隐藏表示$h_t$，计算其与支持上下文集中各单元编码的参考嵌入$g_i$的最大余弦相似度，并在所有答案token上求平均。即 $SAS(y_t) = \max_{U_i \in E} \cos(h_t, g_i)$。SAS越低，说明语义漂移越严重。

## 3. 实验设计
- **数据集/场景**：
  - 单跳图谱推理：MetaQA-1hop（主实验，5000样本）
  - 多跳图谱推理：MetaQA-2hop, MetaQA-3hop, ComplexWebQuestions (CWQ)
  - 表格问答：WikiTableQuestions (2000样本)
- **Benchmark**：幻觉检测任务。将模型输出与金标答案对比（EM或F1≥0.3为非幻觉），统计SSR和SAS在幻觉与非幻觉样本中的分布差异，并基于此构建检测器。
- **对比方法**：
  - **模型内部置信度**：Perplexity, Token Confidence, Max Token Probability
  - **语义一致性**：BERTScore, Embedding Divergence, NLI Contradiction

## 4. 资源与算力
- **说明**：论文正文中**未明确说明**所使用的GPU型号、数量及训练时长等算力细节。

## 5. 实验数量与充分性
- **实验数量**：实验覆盖面广，包含：
  - 分布差异与统计显著性检验（t检验）
  - 联合特征行为与互补性分析（皮尔逊相关）
  - 象限分析（基于SSR和SAS中位数划分4个象限）
  - 跨数据集泛化实验（多跳、表格）
  - 鲁棒性分析（跨模型规模Qwen3-8B/14B、跨推理深度、线性化顺序敏感性、支持集定义敏感性）
  - 消融实验（SSR-only vs SAS-only vs SSR+SAS）
- **充分性与客观性**：实验设计**非常充分且客观**。通过控制检索噪声（使用oracle子图）、采用确定性解码、验证指标不受序列位置偏置和浅层词汇重叠影响等方式，严格隔离了变量，证明了结论的鲁棒性。

## 6. 论文的主要结论与发现
- 幻觉并非随机噪声，而是源于系统性的内部动态：**注意力过度集中于捷径式结构线索（高SSR）**，且**前馈表示未能锚定提供的知识导致向参数记忆回退（低SAS）**。
- SSR和SAS捕获了互补的失败机制，两者呈弱负相关。
- **语义锚定失败（低SAS）是幻觉最稳定的预测因子**，无论任务复杂度如何，低SAS象限的幻觉率始终最高；而注意力分配（SSR）更多随任务结构变化，调节失败的具体模式。
- 基于SSR+SAS构建的轻量级幻觉检测器，在无需微调模型的情况下，AUC和F1显著优于所有基于置信度和语义一致性的基线方法。

## 7. 优点
- **视角深刻**：从机制可解释性角度切入，将宏观的幻觉现象归因于注意力路由和FFN表示融合的具体故障，超越了输入/输出层面的黑盒分析。
- **指标设计精巧**：SSR和SAS分别精准对应了Transformer的两个核心组件，且具有明确的几何和概率意义，计算轻量（单次推理即可获取）。
- **兼具理论与应用**：不仅揭示了机理，还成功将机理信号转化为即插即用、性能优越的幻觉检测工具，实用价值高。

## 8. 不足与局限
- **架构局限**：仅研究了Decoder-only的Transformer架构，其他架构（如Encoder-Decoder）可能表现出不同的内部动态。
- **表示局限**：仅探讨了线性化文本表示，未涉及图感知编码或专用提示策略等替代表示方法。
- **因果性局限**：当前分析主要是观察性和相关性的，缺乏基于干预的因果验证来进一步明确语义锚定动态的因果方向。
- **规模局限**：受限于算力，实验最大仅验证到14B参数模型，70B+级别的大模型行为尚待考察。

（完）
