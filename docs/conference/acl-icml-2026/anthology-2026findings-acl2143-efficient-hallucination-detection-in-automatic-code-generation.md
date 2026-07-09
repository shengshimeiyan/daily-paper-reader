---
title: Efficient Hallucination Detection in Automatic Code Generation
title_zh: 自动代码生成中的高效幻觉检测
authors: "Georgy Andryushchenko, Roman Garaev, Lyudmila Rvanova, Artem Shelmanov, Vladimir V. Ivanov"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.2143.pdf"
tags: ["query:llm-halluc"]
score: 6.0
evidence: 自动代码生成中的幻觉检测
tldr: 针对大语言模型自动生成代码中常包含看似正确却导致下游测试失败的幻觉元素问题，提出一种基于差异的流水线构建行级幻觉代码数据集。基于此数据集，训练了一个利用LLM内部表示识别幻觉的轻量级Transformer检测器。实验表明该检测器在多个代码生成领域显著优于现有不确定性量化方法，并展现出赋能LLM编码智能体自我纠错的巨大潜力。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 768, \"height\": 314, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1646, \"height\": 942, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 780, \"height\": 762, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 777, \"height\": 512, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 794, \"height\": 820, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 784, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 789, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 655, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 651, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 518, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 506, \"height\": 398, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1440, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1443, \"height\": 1610, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1632, \"height\": 540, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1646, \"height\": 708, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1581, \"height\": 1829, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1642, \"height\": 772, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2143/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1640, \"height\": 558, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2143/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1648, \"height\": 666, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2143/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1645, \"height\": 920, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2143/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 794, \"height\": 166, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2143/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 798, \"height\": 300, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2143/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 642, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2143/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 731, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2143/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 785, \"height\": 416, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2143/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 797, \"height\": 924, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2143/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 657, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2143/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1643, \"height\": 1417, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2143/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1657, \"height\": 721, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2143/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1654, \"height\": 916, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2143/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1350, \"height\": 559, \"label\": \"Table\"}]"
motivation: 大语言模型生成的代码常包含看似正确但导致测试失败的幻觉元素，亟需有效的检测方法。
method: 引入基于差异的流水线构建行级幻觉代码数据集，并训练利用LLM内部表示的轻量级Transformer检测器。
result: 所提检测器在多个代码生成领域显著超越现有方法，并展现出赋能编码智能体自我纠错的潜力。
conclusion: 利用模型内部表示的轻量级检测器能有效识别代码生成中的幻觉，促进代码智能体的自我纠错。
---

## Abstract
Large language models (LLMs) frequently produce source code that seems correct and well-formed, yet includes hallucinated elements that cause downstream test failures. In this study, we benchmark state-of-the-art uncertainty quantification methods and existing baselines for the task of hallucination detection in source code and introduce a diff-based pipeline to construct a code dataset annotated with line-level hallucinations. Building on this, we train a lightweight Transformer-based detector that uses LLM internal representations to identify hallucinations, substantially outperforming existing methods across several code generation domains. The detector also shows particular promise for enabling self-correction in LLM-based coding agents. We release the first publicly available dataset of line-level code hallucinations, along with the corresponding source code and trained hallucination detectors https://github.com/datapaf/CodeHallucinationDetection

---

## 论文详细总结（自动生成）

# 自动代码生成中的高效幻觉检测：论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）在代码生成中常产生看似语法正确、流畅，但实际包含逻辑错误或捏造元素的“幻觉”代码，导致下游测试失败。
- **现有痛点**：现有的代码幻觉检测多在代码片段级别进行，或依赖执行信号（如运行报错），无法提供细粒度（如行级）的定位；而不确定性量化（UQ）方法在自然语言中应用广泛，但在源代码生成领域的细粒度幻觉检测上仍处于空白。
- **整体含义**：亟需一种高效、细粒度的幻觉检测方法，不仅能判断代码是否正确，还能精准定位到具体哪一行出现了幻觉，从而为开发者的调试及 LLM 编码智能体的自我纠错提供支持。

## 2. 论文提出的方法论
### 核心思想
提出一种基于差异的流水线构建行级幻觉代码数据集，并训练一个轻量级的 Transformer 检测器，利用 LLM 的内部表示来识别生成代码中的行级幻觉。

### 关键技术细节与流程
- **数据标注流水线**：
  1. 将生成代码和真实代码按行切分；
  2. 使用 `diff` 工具对比两者；
  3. 将生成代码中需删除的行（`diff` 中标记为 `-`）标记为幻觉；
  4. 将添加行（标记为 `+`）之后的首行标记为幻觉（若添加前有删除，则首行标记为正确）。
- **检测器架构**：
  - **输入特征**：提取 LLM 生成代码时的隐藏状态（HS）、注意力权重（AW）和词元概率（TP）。
  - **特征投影**：将每个词元的特征向量通过全连接层投影。
  - **位置编码注入**：将投影后的特征与可训练的行位置嵌入相加，获取上下文特征。
  - **Transformer 编码**：将特征输入 Transformer 编码器，并对同一行内的词元特征进行平均池化，得到该行的上下文向量表示 $h_s$。
  - **不确定性估计**：通过多层感知机（MLP）和 Sigmoid 激活函数，输出该行代码的不确定性得分 $U(s) \in [0, 1]$，得分越高表示幻觉可能性越大。

## 3. 实验设计
- **数据集**：基于 Collu-Bench 构建，包含代码合成（Python：MBPP, HumanEval）和代码修复（Java：HumanEval Java, Defects4J）两个领域。
- **LLM 骨干**：DeepSeek-Coder (1.3B, 6.7B, 33B), CodeLlama 7B, Llama-3-8B-Instruct。
- **评估指标**：由于幻觉行占比少（类别不平衡），主要采用 PR-AUC（精确率-召回率曲线下面积）作为核心指标。
- **对比方法**：
  - **无监督基线**：MSP、Perplexity、Attention Score、最大词元熵（MTE）。
  - **有监督基线**：线性分类器、Lookback lens、SAPLMA (MLP)。
  - **其他基线**：CodeBERT 分类器、提示法（Zero-shot, One-shot, CoT）、随机估计器。

## 4. 资源与算力
- **硬件**：单张 A100 80GB GPU。
- **显存消耗（上限）**：DeepSeek-Coder 1.3B 需 10GB，6.7B 需 20GB，33B 需 58GB。
- **训练时长**：1.3B 模型约 20 分钟，6.7B 约 18 分钟，33B 约 43 分钟。
- **推理开销**：检测器增加 100M-300M 参数，端到端推理时间增加 10%-30%。

## 5. 实验数量与充分性
- **实验规模**：进行了大量实验，涵盖 4 种不同规模/架构的 LLM、2 个代码生成领域、多种特征组合的消融实验、超参数重要性分析，以及针对标注噪声的鲁棒性验证（对比 GPT-5.2 标注与 diff 标注）。
- **充分性与客观性**：实验设计非常充分且客观。不仅横向对比了各类基线，还深入探究了特征贡献度、模型大小对检测难度的影响、跨域泛化能力，并手动进行了错误分析。针对 diff 标注可能引入语法噪声的质疑，补充了 GPT 语义标注的对比实验，证明了结论的稳健性。

## 6. 论文的主要结论与发现
- **模型性能**：提出的 Transformer 检测器（结合 HS+AW+TP 特征）在所有 LLM 和领域上显著优于现有无监督和有监督基线。
- **特征重要性**：隐藏状态（HS）对检测贡献最大，注意力权重（AW）次之，词元概率（TP）单独使用效果很差。
- **模型规模影响**：LLM 越大，产生的幻觉越隐蔽，检测难度越高（PR-AUC 随模型规模增大而下降）。
- **功能正确性关联**：行级最大不确定性得分与整个代码片段的功能错误高度相关，是判断代码是否正确的强指标。
- **跨域泛化**：混合领域训练的检测器泛化能力优于单一领域训练的检测器。
- **潜在应用**：错误分析发现，检测器对“不够优雅/需重构的代码”容易产生误报（假阳性），这表明该检测器未来可能用于代码重构提示。

## 7. 优点
- **首创性**：发布了首个公开的行级代码幻觉数据集及标注流水线。
- **高效性**：检测器轻量级，训练耗时极短（不到1小时），推理开销小（10-30%）。
- **实用性**：行级定位贴合开发者调试习惯，且为 LLM 智能体的自我纠错提供了可能。
- **分析深入**：详尽的消融实验、超参数重要性分析和错误分析，增强了结果的可信度。

## 8. 不足与局限
- **标注噪声**：基于 diff 的自动标注对语法差异（如变量命名、格式化）敏感，容易将语义相同但写法不同的行误标为幻觉（尽管补充实验证明不影响整体结论）。
- **模型特异性**：检测器与特定 LLM 绑定，换用不同 LLM 需重新训练，无法直接跨模型通用。
- **黑盒限制**：依赖 LLM 的内部状态（隐藏层和注意力），无法直接应用于不开放内部表示的闭源商业 LLM（如 GPT-4）。
- **领域局限**：实验主要覆盖 Python 和 Java，对其他编程语言及更复杂场景的泛化能力未经验证。

（完）
