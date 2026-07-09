---
title: Faithfulness-Aware Uncertainty Quantification for Fact-Checking the Output of Retrieval-Augmented Generation
title_zh: 忠实度感知的不确定性量化用于检索增强生成输出的事实核查
authors: "Ekaterina Fadeeva, Aleksandr Rubashevskii, Dzianis Piatrashyn, Roman Vashurin, Shehzaad Dhuliawala, Artem Shelmanov, Timothy Baldwin, Preslav Nakov, Mrinmaya Sachan, Maxim Panov"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.338.pdf"
tags: ["query:llm-halluc"]
score: 8.0
evidence: 检索增强生成中的事实核查与幻觉检测
tldr: 检索增强生成通过知识检索增强了大语言模型在开放域问答中的表现，但仍易产生幻觉。现有幻觉缓解方法常将事实性与对检索证据的忠实度混淆，错误地将事实正确但未受检索支持的陈述标记为幻觉。本文提出FRANQ方法，通过忠实度感知的不确定性量化区分事实性与忠实度，更准确地检测RAG输出中的幻觉。该方法有效减少了因混淆两者导致的误判，提升了事实核查的可靠性，为RAG场景下的幻觉检测提供了更精细的解决方案。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.338/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1648, \"height\": 505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.338/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1626, \"height\": 675, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.338/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1629, \"height\": 596, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.338/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 755, \"height\": 552, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.338/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 755, \"height\": 595, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.338/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 755, \"height\": 555, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.338/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 759, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.338/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 762, \"height\": 627, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.338/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1618, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.338/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 805, \"height\": 431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.338/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1311, \"height\": 644, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.338/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1315, \"height\": 612, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.338/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1327, \"height\": 597, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 800, \"height\": 457, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1570, \"height\": 696, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1620, \"height\": 823, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 799, \"height\": 760, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 796, \"height\": 737, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1648, \"height\": 731, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1647, \"height\": 732, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 794, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 787, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 786, \"height\": 748, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1642, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1644, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 821, \"height\": 567, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 757, \"height\": 149, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 792, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 796, \"height\": 520, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 796, \"height\": 633, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 796, \"height\": 521, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 793, \"height\": 634, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 796, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1647, \"height\": 501, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 671, \"height\": 987, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.338/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 773, \"height\": 1038, \"label\": \"Table\"}]"
motivation: 现有RAG幻觉缓解方法常将事实性与对检索证据的忠实度混淆，导致误判。
method: 提出FRANQ方法，通过忠实度感知的不确定性量化区分事实性与忠实度，以检测RAG幻觉。
result: FRANQ有效减少了因混淆事实性与忠实度导致的误判，提升了RAG幻觉检测的准确性。
conclusion: 区分事实性与忠实度是提升检索增强生成模型幻觉检测与事实核查效果的关键。
---

## Abstract
Large Language Models (LLMs) enhanced with knowledge retrieval, an approach known as Retrieval-Augmented Generation (RAG), have achieved strong performance in open-domain question answering. However, RAG remains prone to hallucinations: factually incorrect outputs may arise from inaccuracies in the model’s internal knowledge and the retrieved context. Existing approaches to mitigating hallucinations often conflate factuality with faithfulness to the retrieved evidence, incorrectly labeling factually correct statements as hallucinations if they are not explicitly supported by the retrieval. In this paper, we introduce FRANQ (Faithfulness-aware Retrieval-Augmented UNcertainty Quantification), a new method for hallucination detection in RAG outputs. FRANQ applies distinct uncertainty quantification techniques to estimate factuality, conditioning on whether a statement is faithful to the retrieved context. To evaluate FRANQ and competing uncertainty quantification methods, we construct a new long-form question answering dataset annotated for both factuality and faithfulness, combining automated labeling with manual validation of challenging cases. Extensive experiments across multiple datasets, tasks, and LLMs show that FRANQ achieves more accurate detection of factual errors in RAG-generated responses compared to existing uncertainty quantification and hallucination detection approaches.

---

## 论文详细总结（自动生成）

# 论文总结：忠实度感知的不确定性量化用于检索增强生成输出的事实核查

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：检索增强生成（RAG）系统虽然引入了外部知识，但仍会产生幻觉（事实错误）。现有的幻觉检测方法往往将“事实性”与“忠实度”混为一谈，错误地将那些虽然未被检索上下文支持但客观上正确的内容判定为幻觉。
- **整体含义**：本文指出，在RAG场景下，事实性（内容客观正确）与忠实度（内容被检索上下文蕴含）是两个不同的维度。检测RAG输出中的事实错误比单纯检测对上下文的不忠实更为关键。因此，需要一种能够区分这两种错误来源的量化方法，以更精准地进行事实核查。

## 2. 方法论：核心思想、关键技术细节与算法流程
- **核心思想**：提出 FRANQ（Faithfulness-aware Retrieval-Augmented UNcertainty Quantification）方法。该方法首先评估生成声明对检索上下文的忠实度，然后根据忠实度的不同，应用不同的不确定性量化（UQ）技术来估计其事实性。
- **核心公式**：基于全概率公式分解声明的真实性概率：
  $$P(c \text{ is true}) = P(c \text{ is faithful}) \cdot P(c \text{ is true} | \text{faithful}) + P(c \text{ is unfaithful}) \cdot P(c \text{ is true} | \text{unfaithful})$$
- **关键技术细节**：
  - **忠实度估计 $P(c \text{ is faithful})$**：使用 AlignScore 计算声明与检索上下文的事实一致性，输出连续概率值而非二值判断。
  - **忠实条件下的事实性 $P(c \text{ is true} | \text{faithful})$**：
    - 长文本QA：使用 Max Claim Probability（基于上下文和查询的token对数概率）。
    - 短文本QA：使用 Semantic Entropy（语义熵）。
  - **不忠实条件下的事实性 $P(c \text{ is true} | \text{unfaithful})$**：此时声明来源于模型内部知识。
    - 长文本QA：使用 Parametric Knowledge（移除检索上下文，仅基于查询计算token对数概率）。
    - 短文本QA：使用 Sum of Eigenvalues（特征值和，基于采样多样性）。
- **校准流程**：针对不同条件下的UQ分数分布不一致的问题，采用保序回归进行校准。提出了**条件校准**策略，即分别利用忠实和不忠实的训练子集对 $UQ_{faith}$ 和 $UQ_{unfaith}$ 进行独立校准。

## 3. 实验设计：数据集、Benchmark与对比方法
- **数据集**：
  - **长文本QA**：本文新构建的数据集。包含76个问题，使用4个LLM生成答案，通过GPT-4o提取原子声明并进行自动标注，对困难样本进行人工校验，同时标注了事实性和忠实度。
  - **短文本QA**：4个公开数据集（TriviaQA, SimpleQA, Natural Questions, PopQA），将整个回答视为单一声明，利用金标准答案通过GPT-4o判定事实性。
- **Benchmark指标**：PR-AUC（精确率-召回率曲线下面积，以错误声明为正类）和 PRR（预测拒绝率，衡量拒绝不确定预测同时保留准确预测的能力）。
- **对比方法**：
  - **通用UQ基线**：Max Sequence Prob, Perplexity, Semantic Entropy, P(True) 等。
  - **RAG特定基线**：单独使用 AlignScore 或 Parametric Knowledge。
  - **监督基线**：XGBoost（分别使用全部UQ特征和仅FRANQ特征训练）。
  - **FRANQ变体**：无校准、统一校准、条件校准。

## 4. 资源与算力
- **GPU型号与时长**：使用单块 NVIDIA V100 32GB GPU。长文本QA的完整数据生成与基线评估约需8天；短文本QA不到1天。
- **API开销**：使用 OpenAI API (GPT-4o) 进行声明拆分、匹配和标注，每个模型运行约花费100美元。
- **人工标注**：6名学生标注员，每人贡献约3小时，无财务报酬。

## 5. 实验数量与充分性
- **实验数量**：实验规模较大，涵盖了2种任务形式（长/短文本）、5个数据集、4-5个不同规模/架构的LLM（Llama 3B/8B, Falcon 3B, Gemma 4B/12B），对比了10余种基线方法，并进行了组件消融、检索噪声鲁棒性、训练数据量影响和计算效率等深度分析实验。
- **充分性与客观性**：实验设计非常充分且公平。固定了检索过程和底层LLM，仅对比UQ方法的效果；消融实验详尽地验证了各组件的必要性；针对检索失败（随机打乱、事实污染）的鲁棒性测试增强了结论的可靠性；对短文本QA报告了多数据集平均值和单独结果，减少了特定数据集的偏差。

## 6. 主要结论与发现
- **性能提升**：FRANQ（特别是条件校准版本）在长文本和短文本QA任务中，其事实错误检测能力均优于现有的无监督UQ方法、RAG特定方法和有监督分类器。
- **组件重要性**：对于长文本QA，不忠实分支的UQ方法选择至关重要，Parametric Knowledge 表现最佳；对于短文本QA，各组合差异不大但 Semantic Entropy + Sum of Eigenvalues 最优。
- **鲁棒性**：FRANQ在面对无关检索和包含事实错误的误导性检索时，表现出极强的鲁棒性，性能下降最小。
- **数据效率**：条件校准的FRANQ仅需极少的标注数据（长文本约300条，短文本约120条）即可达到性能饱和，且优于XGBoost基线。
- **轻量级**：推理开销小（增加约1.7s），校准模型极小（仅几百字节）。

## 7. 优点
- **视角新颖**：明确区分了RAG语境下常被混淆的“事实性”与“忠实度”，解决了正确但无依据内容被误判为幻觉的问题。
- **理论优雅**：基于全概率公式的分解逻辑清晰，将复杂的RAG不确定性来源解耦为检索驱动和参数驱动，具有很好的可解释性。
- **实用性强**：条件校准策略简单有效，且对标注数据需求极低；推理开销小，适合实际部署。

## 8. 不足与局限
- **依赖上游信号质量**：FRANQ的性能高度依赖于 AlignScore 评估忠实度的准确性以及底层LLM概率校准的质量。在极端严重的检索错误或模型严重失准情况下，性能可能受损。
- **标注偏差**：长文本评估流程依赖 GPT-4o 进行声明提取和初步标注，尽管有人工校验，但仍可能存在模型固有的偏差。
- **应用限制**：FRANQ仅用于“检测”幻觉，并不能在生成阶段“阻止”幻觉，需依赖下游过滤机制；部分变体仍需少量标注数据用于校准。

（完）
