---
title: "MultiHal: Multilingual Dataset for Knowledge-Graph Grounded Evaluation of LLM Hallucinations"
title_zh: MultiHal：基于知识图谱接地的大语言模型幻觉评估多语言数据集
authors: "Ernests Lavrinovics, Russa Biswas, Katja Hose, Johannes Bjerva"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f92b6f1240a48b7ece72366d685e062d0b99598b.pdf"
tags: ["query:llm-halluc"]
score: 8.0
evidence: 评估大模型幻觉的多语言数据集
tldr: 针对现有大语言模型幻觉评估基准多局限于英语且依赖非结构化文本，忽略了知识图谱等结构化事实资源的问题，提出MultiHal多语言数据集。该数据集融合知识图谱路径，为事实性语言建模提供了结构化事实与多语言支持的评估平台。实验表明知识图谱能有效辅助幻觉缓解，MultiHal填补了现有评估资源在多语言和结构化事实方面的空白。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有幻觉评估基准多为英语中心且依赖非结构化文本，忽略了知识图谱等结构化事实资源。
method: 构建MultiHal多语言数据集，融合知识图谱路径，提供结构化事实和多语言支持的幻觉评估基准。
result: 知识图谱为幻觉缓解提供了有效辅助，MultiHal填补了多语言和结构化事实评估的空白。
conclusion: 结合知识图谱的多语言评估数据集能有效促进大语言模型事实性与幻觉缓解的研究。
---

## Abstract
Large Language Models (LLMs) have inherent limitations of faithfulness and factuality, commonly referred to as hallucinations. Several benchmarks have been developed that provide a test bed for factuality evaluation within the context of English-centric datasets, while relying on supplementary informative context like web links or text passages but ignoring the available structured factual resources. To this end, Knowledge Graphs (KGs) have been identified as a useful aid for hallucination mitigation, as they provide a structured way to represent the facts about entities and their relations with minimal linguistic overhead. We bridge the lack of KG paths and multilinguality for factual language modeling within the existing hallucination evaluation benchmarks and propose a KG-based multilingual, multihop benchmark called MultiHal framed for generative text evaluation. As part of our data collection pipeline, we mined 140k KG-paths from open-domain KGs, from which we pruned noisy KG-paths, curating a high-quality subset of 25.9k. Our baseline evaluation shows an absolute scale improvement by approximately 0.12 to 0.36 points for the semantic similarity score, 0.16 to 0.36 for NLI entailment and 0.29 to 0.42 for hallucination detection in KG-RAG over vanilla QA across multiple languages and multiple models, demonstrating the potential of KG integration. We anticipate MultiHal will foster future research towards several graph-based hallucination mitigation and fact-checking tasks.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）存在固有的忠实度和事实性局限，即“幻觉”问题。现有的幻觉评估基准大多以英语为中心，且主要依赖非结构化的补充上下文（如网页链接或文本段落）来辅助评估，忽略了知识图谱（KG）等结构化事实资源的潜力。
- **整体含义**：知识图谱能够以结构化方式表示实体及其关系，且语言开销极小，是缓解幻觉的理想工具。本研究旨在填补现有评估基准在多语言支持和结构化事实（KG路径）方面的空白，推动基于图结构的幻觉缓解和事实核查研究。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：构建一个基于知识图谱的、多语言、多跳的幻觉评估基准数据集，为生成式文本的事实性评估提供结构化事实与多语言支持的平台。
- **关键技术细节/算法流程**：
  1. **KG路径挖掘**：从开放域知识图谱中挖掘提取了14万条KG路径。
  2. **数据清洗与剪枝**：对挖掘出的原始KG路径进行去噪和剪枝处理，过滤掉低质量或噪声数据。
  3. **高质量子集策划**：最终筛选并策划出包含2.59万条高质量KG路径的子集，构成MultiHal数据集。
  4. **基准框架构建**：将数据集构建为面向生成式文本评估的基准，支持结合KG-RAG（知识图谱检索增强生成）等范式进行测试。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法
- **数据集/场景**：使用本文提出的MultiHal数据集，涵盖多语言和多跳推理的生成式问答场景。
- **Benchmark（评估指标）**：
  - 语义相似度得分
  - 自然语言推理（NLI）蕴含得分
  - 幻觉检测准确率
- **对比方法**：对比了**KG-RAG**（结合知识图谱检索增强的生成方法）与**Vanilla QA**（无外部结构化知识辅助的纯问答方法），并在多种语言和多个模型上进行了对比评估。

### 4. 资源与算力
- 根据提供的论文摘要和元数据，文中**未明确说明**所使用的算力资源（如GPU型号、数量、训练时长等）。

### 5. 实验数量与充分性
- **实验数量**：基线评估涵盖了多种语言、多个模型，并在三个不同的评估维度（语义相似度、NLI蕴含、幻觉检测）上进行了量化对比。
- **充分性与客观性**：实验从多个维度和跨语言/跨模型的设置下验证了KG集成的有效性，证明了方法的泛化能力，具备一定的客观性和充分性。但由于摘要信息有限，缺乏对数据剪枝策略、不同KG规模影响的消融实验描述，无法完全判断其实验设计的全面性。

### 6. 论文的主要结论与发现
- **知识图谱集成显著缓解幻觉**：在多语言和多模型设置下，KG-RAG相比Vanilla QA取得了显著提升，语义相似度绝对提升0.12至0.36，NLI蕴含提升0.16至0.36，幻觉检测提升0.29至0.42。
- **填补研究空白**：MultiHal成功填补了现有幻觉评估资源在多语言和结构化事实（KG路径）方面的空白，证明了结合知识图谱的多语言评估数据集能有效促进大语言模型事实性与幻觉缓解的研究。

### 7. 优点：方法或实验设计上有哪些亮点
- **创新的数据集构建**：首次将多语言、多跳推理与知识图谱路径深度结合，构建了针对幻觉评估的生成式基准，具有鲜明的场景针对性。
- **严格的数据质量控制**：从14万条原始KG路径通过去噪剪枝筛选至2.59万条高质量数据，保证了评估基准的可靠性和信噪比。
- **多维度的评估体系**：不仅关注幻觉检测，还引入了语义相似度和NLI蕴含得分，对生成内容的事实性评估更为全面。
- **显著的实证效果**：明确量化了KG-RAG带来的绝对提升，有力证明了结构化知识在多语言场景下缓解幻觉的巨大潜力。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **数据规模限制**：最终保留的高质量KG路径仅2.59万条，相较于大语言模型庞大的预训练语料，规模偏小，可能限制评估的覆盖广度。
- **信息缺失与覆盖度未知**：摘要中未提及具体支持的语言种类和数量，以及测试的具体LLM模型名称，难以评估其在极低资源语言或特定类型模型上的泛化能力。
- **偏差风险**：数据来源于开放域KG，可能继承知识图谱本身存在的结构偏差或实体分布不均（如偏向西方或高频实体），从而影响评估的公平性。
- **应用限制**：依赖KG路径的生成与检索，在实际应用中可能面临开放域KG更新滞后、特定领域KG缺失或构建成本高昂的挑战。

（完）
