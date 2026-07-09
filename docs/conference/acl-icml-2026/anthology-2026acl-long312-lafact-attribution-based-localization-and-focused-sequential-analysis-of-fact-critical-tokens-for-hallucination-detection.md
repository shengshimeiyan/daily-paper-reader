---
title: "LAFaCT: Attribution-based Localization and Focused Sequential Analysis of Fact-Critical Tokens for Hallucination Detection"
title_zh: LAFaCT：基于归因的定位与事实关键标记聚焦序列分析用于幻觉检测
authors: "Xin Wang, Jiahao Li, Licheng Zhang, Zhendong Mao"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.312.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 大模型幻觉检测
tldr: 大语言模型存在的幻觉问题严重削弱了其可靠性。现有利用隐藏状态的白盒幻觉检测方法在分析标记序列时，未能识别并聚焦于事实关键信息。本文提出LAFaCT框架，采用先定位后分析的策略，首先利用基于特征归因的事实关键性指标定位关键标记，随后对其隐藏状态进行聚焦序列分析。在八个基准和多个模型家族上的广泛实验证实，LAFaCT达到了新的最先进幻觉检测性能，显著提升了检测的准确性与鲁棒性。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.312/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 786, \"height\": 630, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.312/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1628, \"height\": 664, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.312/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 730, \"height\": 431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.312/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 793, \"height\": 280, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.312/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 795, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.312/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 795, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.312/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 791, \"height\": 591, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.312/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 785, \"height\": 566, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1661, \"height\": 1548, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 815, \"height\": 525, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 814, \"height\": 489, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 810, \"height\": 582, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 813, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 812, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1657, \"height\": 571, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 810, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1689, \"height\": 1298, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1419, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 814, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 775, \"height\": 431, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 778, \"height\": 470, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 575, \"height\": 265, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 811, \"height\": 584, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 814, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.312/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1655, \"height\": 623, \"label\": \"Table\"}]"
motivation: 现有白盒幻觉检测方法利用隐藏状态时未能识别并聚焦于序列中的事实关键信息。
method: 提出LAFaCT框架，先通过特征归因定位事实关键标记，再对其隐藏状态进行聚焦分析。
result: 在八个基准和多个模型家族上的实验证实LAFaCT达到了新的最先进幻觉检测性能。
conclusion: 聚焦事实关键标记的定位与分析策略显著提升了大语言模型幻觉检测的准确性。
---

## Abstract
Large Language Models (LLMs) suffer from hallucinations, severely undermining their reliability. While white-box hallucination detection methods that leverage hidden states prevail, they fail to identify and focus on fact-critical information when analyzing token sequences. To address this, we propose LAFaCT, a Localize-then-Analyze detection framework. It first localizes fact-critical tokens using Factual Criticality, a novel metric derived from feature attribution. A subsequent stage then performs a focused sequential analysis on their hidden states. Extensive experiments on eight benchmarks and multiple model families confirm LAFaCT as the new state-of-the-art, with in-depth analyses validating the effectiveness of its core token-localization strategy.

---

## 论文详细总结（自动生成）

# LAFaCT：基于归因的定位与事实关键标记聚焦序列分析用于幻觉检测

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）的幻觉问题严重削弱了其可靠性。现有的白盒幻觉检测方法在利用模型隐藏状态时面临两难困境：单标记探测仅分析固定位置（如最后一个标记）的隐藏状态，视角受限且不完整；全局聚合则无差别地融合所有标记的隐藏状态，引入了大量事实无关的噪声，稀释了关键信号。
- **整体含义**：为了突破上述瓶颈，幻觉检测必须从“无差别分析”转向“聚焦分析”，即精准识别出对事实性起决定性作用的“事实关键标记”，并仅对这些标记的隐藏状态进行深度分析。

## 2. 方法论：核心思想、关键技术细节与流程
- **核心思想**：提出 LAFaCT 框架，采用“先定位后分析”的策略。首先基于特征归因定位事实关键标记，随后对这些标记的隐藏状态进行聚焦序列分析。
- **定位阶段**：
  - **代理分类器**：在LLM中间层最后一个标记的隐藏状态上训练一个两层MLP分类器，输出事实性概率 $o_p$。
  - **事实关键性度量**：利用 DeepLIFT 算法将 $o_p$ 归因回输入标记的嵌入层（以 `<pad>` 序列为基线），计算每个标记的归因得分为其各维度归因向量的 L2 范数，再通过 softmax 归一化得到事实关键性得分 $C(x_i)$。
  - **Top-p 选择**：根据 $C(x_i)$ 得分，应用 Top-p 策略筛选出事实关键标记子集。
- **分析阶段**：
  - **序列表示建模**：提取筛选出的事实关键标记在中间层的隐藏状态，注入相对位置编码（基于标记间的相对距离计算），通过 MLP 投影后输入 Bi-GRU 编码器，生成统一的事实性表示向量 $e_x$。
  - **角度三元组损失**：摒弃传统的交叉熵损失，提出角度三元组损失。将表示映射到单位超球面，通过优化锚点、正样本和负样本之间的角度余弦及固定边界 $m$，增强类间分离和类内紧凑性，学习更具判别力的事实性表示。
  - **推理**：计算测试样本表示与训练集中 Top-5 最近邻的余弦相似度，将其归入平均相似度更高的类别。

## 3. 实验设计：数据集、Benchmark与对比方法
- **数据集与场景**：涵盖8个基准数据集，横跨3大任务场景：
  - **问答（QA）**：TruthfulQA, TriviaQA, CoQA, GSM8K, MedQuad；
  - **文本摘要**：XSum, FRANK；
  - **传记生成**：WikiBio GPT-3。
- **评估指标**：主要使用 AUROC，在 WikiBio 任务中使用 AUC-PR。
- **对比方法**：
  - **黑盒**：SelfCheckGPT；
  - **灰盒**：Semantic Entropy, SAR；
  - **白盒**：EigenScore, PoLLMgraph, Mind, HaloScope (半监督与监督变体), Factoscope, 以及2025年并发方法 SATMD, LapEigvals。

## 4. 资源与算力
- **硬件配置**：4 块 NVIDIA A40 GPU。
- **算力消耗**：总训练与实验耗时约 300 GPU 小时。

## 5. 实验数量与充分性
- **实验数量**：实验规模庞大且覆盖面广。包括：3个主模型在5个QA数据集上的主实验；跨模型规模（7B至14B）的泛化实验；留一法域外（OOD）泛化实验；2个摘要和1个传记生成的开放域实验；以及大量消融实验（定位策略对比、损失函数、位置编码、序列建模架构、归因细节、层选择、数据效率、低资源设置、标签阈值敏感度、k折交叉验证等）。
- **充分性与客观性**：实验设计非常充分且公平。对所有监督基线均在相同数据集上重新训练，超参数在同一验证集上调优，结果取3次随机种子的平均值。消融实验全面验证了各组件的不可替代性。

## 6. 主要结论与发现
- LAFaCT 在8个基准和多个模型家族上实现了新的 SOTA 幻觉检测性能（如在 Llama2-7B 上平均超越最强基线 3.2 AUROC）。
- 在需要复杂推理的数据集（如 GSM8K, MedQuad）上优势尤为显著。
- 具有极强的域外（OOD）泛化能力，在 leave-one-out 设置下平均领先次优方法 4.1 AUROC，这得益于角度三元组损失的学习机制。
- 基于归因的定位策略（特别是 DeepLIFT）显著优于启发式方法（如熵、概率）和其他归因方法，且计算开销极低（仅增加 5.6%-8.4% 的生成耗时）。

## 7. 优点
- **范式创新**：提出“先定位后分析”范式，成功解决了白盒检测中“单标记视角不全”与“全局聚合噪声多”的两难困境。
- **指标设计巧妙**：利用 DeepLIFT 将代理分类器的事实性预测归因至输入层，提出的“事实关键性”指标既有理论支撑，又能精准定位幻觉源头（定性分析证实其能高亮错误前提或逻辑主干）。
- **损失函数优化**：角度三元组损失有效提升了表示的判别力和跨域泛化性。
- **高效性**：在取得 SOTA 的同时，推理开销极小，且对代理分类器架构的鲁棒性强。

## 8. 不足与局限
- **依赖标注数据**：作为监督方法，LAFaCT 依赖标注数据，在标注稀缺场景下的适用性受限。
- **开放域标签噪声**：在开放域生成任务（如摘要）中，事实性标签依赖启发式合成（如 AlignScore 阈值判定），可能引入标签噪声。
- **特定失败模式**：在算术推理中，大量正确的中间步骤可能稀释单一计算错误的信号；在比较知识中，若模型对错误常识具有极强的内部信念，其隐藏状态可能缺乏典型的捏造模式，导致漏检。

（完）
