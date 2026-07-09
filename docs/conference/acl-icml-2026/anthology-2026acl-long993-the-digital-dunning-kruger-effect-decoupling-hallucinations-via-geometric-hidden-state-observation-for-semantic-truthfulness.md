---
title: "The Digital Dunning-Kruger Effect: Decoupling Hallucinations via Geometric Hidden-state Observation for Semantic Truthfulness"
title_zh: 数字达克效应：通过几何隐藏状态观察解耦幻觉以实现语义真实性
authors: "Yueheng Mao, Min Yu, Gengwang Li, Jianguo Jiang, Gang Li, Meng Zhang, Zhen Xu, Weiqing Huang, Ming Liu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.993.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 针对大模型的白盒幻觉检测框架
tldr: 当前幻觉检测范式在计算昂贵的黑盒方法高准确率与白盒方法无法检测顽固幻觉之间存在权衡。为弥合这一差距，本文提出GHOST，一个高效的白盒框架，用于大模型幻觉检测。该框架主要针对内部推理不稳定性引起的困惑幻觉，同时捕捉以过早层收敛为特征的顽固幻觉作为补充信号。通过整合隐藏状态的内部几何特征，实现了准确率与效率的平衡。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.993/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 797, \"height\": 398, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.993/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1557, \"height\": 788, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.993/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1661, \"height\": 329, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.993/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1659, \"height\": 1914, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.993/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1663, \"height\": 625, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.993/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1659, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.993/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 799, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.993/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1490, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.993/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 800, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.993/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 800, \"height\": 259, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.993/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1500, \"height\": 672, \"label\": \"Table\"}]"
motivation: 当前幻觉检测方法在黑盒高准确率和白盒低计算成本间存在权衡，难以检测顽固幻觉。
method: 提出GHOST白盒框架，通过整合隐藏状态的内部几何特征来检测大模型幻觉。
result: 该方法有效捕捉了内部推理不稳定性及过早收敛，平衡了准确率与效率。
conclusion: GHOST框架为高效且准确地检测大模型幻觉提供了新的白盒解决方案。
---

## Abstract
Large Language Models (LLMs) often generate overconfident yet factually incorrect hallucinations. Current detection paradigms suffer from a trade-off between the high accuracy of computationally expensive black-box methods and the inability of white-box methods to detect stubborn hallucinations. To bridge this gap, we propose GHOST (Geometric Hidden-state Observation for Semantic Truthfulness), an efficient white-box framework for hallucination detection in LLMs. We primarily target confused hallucinations marked by internal reasoning instability, while also capturing stubborn hallucinations characterized by premature layer-wise convergence as a complementary signal. By integrating internal geometric dynamics with output probability distributions, GHOST constructs a high-dimensional feature space for non-linear truthfulness classification. Extensive evaluations on FinanceBench, RAGTruth, HaluEval, and PopQA show that GHOST outperforms white-box baselines and achieves competitive black-box performance while reducing computational overhead by over 90%, offering a robust solution for real-time detection.

---

## 论文详细总结（自动生成）

# 论文总结：数字达克效应：通过几何隐藏状态观察解耦幻觉以实现语义真实性

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）经常生成过度自信但事实错误的“幻觉”。现有的幻觉检测范式存在权衡：黑盒方法准确率高但计算成本极其昂贵，难以实时部署；白盒方法计算成本低，但依赖粗粒度指标，无法有效检测模型高度自信的“顽固幻觉”。
- **整体含义**：本文指出LLM的幻觉类似于心理学中的“达克效应”，即模型高估自身能力。作者将幻觉细分为“困惑幻觉”（内部推理不稳定）和“顽固幻觉”（过早收敛于错误先验），并提出需要一种既能捕捉内部推理动态，又能兼顾效率的白盒检测框架，以弥合上述权衡差距。

## 2. 提出的方法论：核心思想、关键技术细节
- **核心思想**：提出GHOST（Geometric Hidden-state Observation for Semantic Truthfulness）框架，将LLM的推理过程视为高维语义流形中的动态潜轨迹。通过量化隐藏状态的内部几何动力学特征与输出概率分布特征，构建多维特征空间进行非线性真实性分类。
- **关键技术细节与特征构建**：
  - **表示湍流（Representation Turbulence, $V_{turb}$）**：计算相邻层隐藏状态之间的平均余弦偏差。该值升高代表模型内部存在认知失调和推理不稳定，是识别“困惑幻觉”的主要信号。
  - **顽固度（Stubbornness, $V_{stub}$）**：计算中间层隐藏状态与最终层表示之间的平均余弦相似度。高顽固度且低湍流度表示模型过早收敛于错误结论，是识别“顽固幻觉”的补充信号。
  - **预测熵（Predictive Entropy, $V_{ent}$）**：计算输出Top-K候选词的香农熵，衡量输出概率的不确定性。
  - **语义散度（Semantic Divergence, $V_{div}$）**：计算Top-K候选词在静态输入嵌入空间中的平均成对余弦距离，用于区分词汇同义词与事实混淆。
- **分类器**：将上述4个特征组合成向量，输入非线性分类器。经过对比，随机森林因其对高维特征交互的鲁棒性而被选用。

## 3. 实验设计：数据集、Benchmark与对比方法
- **数据集/场景**：
  - **FinanceBench**：专业金融领域，测试高代价场景下的顽固幻觉。
  - **RAGTruth**：检索增强生成（RAG）场景，测试外部知识整合时的困惑幻觉。
  - **HaluEval**：通用知识问答（10,000样本）。
  - **PopQA**：长尾实体知识，测试模型对生僻事实的虚假记忆。
- **评估指标**：AUPRC（核心指标，对类别不平衡更鲁棒）和 F1-score。
- **对比方法**：
  - **白盒方法**：Predictive Entropy, INSIDE, LI, LapEigvals, UTH, HIDE, LoRA probe。
  - **黑盒方法**：SelfCheckGPT（基于多次采样一致性）。
- **基座模型**：Qwen2.5-1.5B, Gemma-3-4B, Mistral-7B, DeepSeek-R1-7B（涵盖小模型、不同架构及推理模型）。

## 4. 资源与算力
- **硬件配置**：4张 NVIDIA GeForce RTX 3090 GPU，双路 Intel Xeon Gold 6326 CPU。
- **计算时长**：在所有4个数据集和4个基座模型上提取几何特征的总GPU时间约为24小时。
- **推理效率**：GHOST的向量化解码提取机制仅增加约0.08s-0.18s的延迟（额外开销约4.3%-4.6%），相比SelfCheckGPT减少超过90%的计算开销。

## 5. 实验数量与充分性
- **实验规模**：
  - 主实验：4个模型 × 4个数据集的全面对比。
  - 消融实验：对4个特征组分别进行剔除测试。
  - 泛化实验：跨数据集和跨模型的OOD（Out-of-Distribution）测试。
  - 其他：分类器对比、错误分析、效率分析。
- **充分性与客观性**：实验设计非常充分，覆盖了多种架构、不同知识领域和RAG场景。消融实验清晰拆解了各特征贡献；OOD实验客观揭示了方法在跨域（特别是金融域）时的性能衰减；标注质量通过人工评估（Cohen’s Kappa = 0.82）进行了验证，确保了评估的公平与客观。

## 6. 论文的主要结论与发现
- GHOST在所有评估的LLM架构和基准测试中均达到了SOTA性能，显著超越白盒基线，并在AUPRC和F1上与昂贵的黑盒方法（SelfCheckGPT）具备竞争力。
- **湍流度是最关键的特征**，移除它导致性能下降最大；而顽固度作为补充信号，能有效识别低不稳定性的过早收敛幻觉。
- GHOST对推理模型（DeepSeek-R1）特别有效，能精准捕捉复杂逻辑推导中的几何不稳定性。
- OOD泛化性能下降是不对称的，从高度专业化的金融数据集迁移时退化最严重，主要归因于幻觉先验概率的偏移和特征分布变化。

## 7. 优点
- **认知视角的创新**：将“达克效应”引入LLM幻觉分析，提出了“困惑”与“顽固”的细粒度分类，为幻觉产生机制提供了理论解释。
- **极高的工程实用价值**：在单次前向传播中提取特征，额外延迟极低（<5%），解决了黑盒方法无法实时部署的痛点。
- **特征设计的合理性**：不仅依赖隐藏状态的几何轨迹，还巧妙融合了输出分布的语义散度，区分了同义词替换与事实错误。

## 8. 不足与局限
- **架构适用性受限**：实验仅验证了Decoder-only Transformer架构，对Encoder-Decoder或非Transformer结构的适用性未知。
- **白盒访问限制**：方法依赖模型内部隐藏状态，无法应用于闭源或仅API访问的模型。
- **顽固幻觉的检测瓶颈**：对于内部推理极其稳定但事实错误的“顽固幻觉”，依然存在较多漏报，且目前缺乏专门针对此类幻觉的数据集进行深入研究。
- **复杂正确推理的误报**：多步正确推理有时也会表现出高内部不稳定性，容易被误判为幻觉（假阳性）。
- **OOD校准问题**：在跨域部署时，决策阈值容易因先验偏移而失准，需结合后处理校准策略。

（完）
