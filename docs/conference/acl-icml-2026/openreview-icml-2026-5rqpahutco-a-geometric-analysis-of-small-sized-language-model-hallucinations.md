---
title: A Geometric Analysis of Small-sized Language Model Hallucinations
title_zh: 小型语言模型幻觉的几何分析
authors: "Emanuele Ricco, Elia Onofri, Lorenzo Cima, Stefano Cresci, Roberto Di Pietro"
date: 2026-04-30
pdf: "https://openreview.net/pdf/08be045499714a7ce9b36769bf1618f54a011cbd.pdf"
tags: ["query:llm-halluc"]
score: 7.0
evidence: 语言模型幻觉的几何分析
tldr: 现有研究通常将大语言模型的幻觉归因于知识缺失，但本文发现即使相关知识存在，模型仍会产生幻觉，这指向了模型内部的检索不稳定性。基于此，本文提出APORIA几何框架，通过在句子嵌入空间中研究对同一提示的重复响应来分析幻觉，揭示了检索不稳定性而非单纯的知识缺失是幻觉产生的核心原因，为理解和缓解幻觉提供了全新视角与坚实的理论依据。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有研究多将幻觉归因于知识缺失，忽略了即使知识存在也会发生的检索不稳定性问题。
method: 提出APORIA几何框架，在句子嵌入空间中研究对同一提示的重复响应以分析检索不稳定性。
result: 实验表明幻觉不仅源于知识缺失，更主要由模型内部检索不稳定性引起。
conclusion: 检索不稳定性是导致语言模型幻觉的关键因素，APORIA框架为理解幻觉提供了新的几何视角。
---

## Abstract
Hallucinations—plausible but factually incorrect responses—pose a major challenge to the reliability of Large Language Models (LLMs), especially in multi-step or agentic settings.  
Existing work largely frames hallucinations as a consequence of missing knowledge; we show instead that, even when the relevant factual knowledge is present, models still produce hallucinated answers, pointing to retrieval instability rather than knowledge gaps.  
Building on this observation, we introduce APORIA (*Aggregate Prompt-wise Observation Retrieving Instability via Asymmetry*—the Socratic state of "puzzlement-in-contradiction" that hallucinations embody), a geometric framework that studies repeated responses to the same prompt in sentence-embedding space. Our central hypothesis is that genuine responses cluster more tightly than hallucinated ones; we empirically validate this and show that, after Fisher projection, the two response classes become consistently separable.  
We leverage this asymmetry in geometry via APORIA-LP, an efficient label-propagation method that classifies large collections of responses from as few as 30–50 annotations, achieving F1 scores above 90% across ten small-sized LLMs.  
To support further research, we release SOCRATES-300K, a fully labelled dataset of 300,000 responses, together with the code for both dataset generation and result reproduction.  
Our key finding—framing hallucinations from a geometric perspective in the embedding space—complements traditional knowledge-centric and single-response evaluation paradigms, paving the way for further research.

---

## 论文详细总结（自动生成）

# 小型语言模型幻觉的几何分析

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：语言模型（尤其是小型LLM）为何会产生幻觉（即合理但事实上不正确的回答）？
- **研究背景**：现有研究普遍将幻觉归因于模型内部的“知识缺失”，即模型本身没有掌握相关信息。
- **研究动机**：本文作者观察到，即使模型内部存在相关的事实知识，依然会产生幻觉。这表明幻觉的根源不仅仅是“不知道”，更在于模型内部存在“检索不稳定性”。因此，需要一种新的视角来量化并解释这种检索不稳定性导致的幻觉。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程
- **核心思想**：提出APORIA（Aggregate Prompt-wise Observation Retrieving Instability via Asymmetry）几何框架，从句子嵌入空间的几何视角分析幻觉，将幻觉视为一种“矛盾中的困惑”状态。
- **关键假设**：对于同一个提示的重复响应，真实响应在嵌入空间中的聚类比幻觉响应更加紧密（即存在几何不对称性）。
- **技术细节与流程**：
  1. **重复采样**：对同一提示进行多次推理，获取多个响应。
  2. **嵌入映射**：将响应映射到句子嵌入空间中。
  3. **Fisher投影**：使用Fisher投影技术对嵌入数据进行降维处理，经验证在投影后真实响应与幻觉响应两类集群实现了持续可分。
  4. **APORIA-LP分类**：基于上述几何不对称性，提出一种高效的标签传播方法。该方法仅需极少量的标注（30-50个）即可对大量未标注的响应集合进行幻觉分类。

## 3. 实验设计：数据集、场景、benchmark与对比方法
- **数据集**：自建并发布了SOCRATES-300K数据集，包含30万个完全标记的响应。
- **实验场景**：针对10个不同的小型语言模型进行幻觉分析与分类。
- **评估指标**：F1分数。
- **对比方法**：基于现有摘要信息，核心对比基线未详细展开，但实验重点在于验证APORIA-LP在极少标注（30-50个）下的分类性能，并在10个模型上均达到了90%以上的F1分数。

## 4. 资源与算力
- **算力说明**：提供的论文摘要与元数据中**未明确说明**所使用的GPU型号、数量及训练时长等算力细节。

## 5. 实验数量与充分性
- **实验规模**：在10个小型LLM上进行了实验验证，并构建了30万条响应的大规模数据集。
- **充分性与客观性评估**：
  - **充分性**：通过10个模型的跨模型验证和大规模数据集测试，证明了几何不对称性现象的普遍性以及APORIA-LP方法的有效性，实验具有一定充分性。
  - **客观性**：实验仅局限于“小型”语言模型，未在主流的大型模型（如Llama-7B/13B及以上、GPT系列等）上进行验证，实验覆盖面存在局限，客观性有待在更大规模模型上进一步确认。

## 6. 论文的主要结论与发现
- 幻觉的产生不仅源于知识的缺失，更主要由模型内部的检索不稳定性引起。
- 在句子嵌入空间中，真实响应与幻觉响应存在显著的几何不对称性（真实响应更紧凑），且通过Fisher投影后两者可实现线性可分。
- 基于几何不对称性的APORIA-LP方法能够以极低的标注成本（30-50个样本）高效识别幻觉（F1>90%）。

## 7. 优点：方法或实验设计上的亮点
- **视角创新**：突破了传统“知识缺失”的单一归因，从“检索不稳定”和“几何视角”解释幻觉，为该领域提供了全新的理论依据。
- **极高的标注效率**：APORIA-LP方法仅需30-50个标注即可完成大规模分类，极大降低了幻觉检测的实际应用成本。
- **开源贡献**：发布了SOCRATES-300K大规模标注数据集及代码，为后续几何视角的幻觉研究提供了宝贵资源。

## 8. 不足与局限
- **模型规模局限**：实验仅在小型语言模型上验证，该方法在大型语言模型（LLM）的嵌入空间中是否依然保持相同的几何不对称性尚属未知。
- **应用场景限制**：该方法依赖于对同一提示的“重复响应”进行聚类分析，这意味着在实际推理应用中需要多次调用模型，会增加推理延迟和计算成本，不适合对实时性要求极高的场景。
- **潜在偏差风险**：几何不对称性假设可能在某些极端复杂或高度开放性的生成任务中不成立，存在一定的偏差风险。

（完）
