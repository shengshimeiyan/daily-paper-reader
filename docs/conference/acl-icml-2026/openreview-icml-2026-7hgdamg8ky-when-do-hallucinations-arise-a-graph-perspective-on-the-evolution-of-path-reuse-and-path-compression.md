---
title: When Do Hallucinations Arise? A Graph Perspective on the Evolution of Path Reuse and Path Compression
title_zh: 幻觉何时产生？路径复用与路径压缩演化的图视角
authors: "Xinnan Dai, Kai Yang, Cheng Luo, Shenglai Zeng, Kai Guo, Jiliang Tang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/aedc027637e7cca15eb5ee14f5d323b73334c4e6.pdf"
tags: ["query:llm-halluc"]
score: 8.0
evidence: 大模型幻觉的产生机制
tldr: 大语言模型的推理幻觉常表现为流畅但缺乏支撑的结论，违反上下文或事实知识，但其产生机制尚不明确。本文将下一标记预测建模为底层图上的图搜索过程，其中实体对应节点，学习到的转移构成边。从这一视角出发，本文揭示了推理幻觉源于内在推理中的路径复用与外在推理中的路径压缩机制。这一发现不仅深化了对解码器仅Transformer产生幻觉的理解，也为未来从图结构角度缓解大模型推理幻觉提供了理论依据。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大语言模型推理幻觉的产生机制尚不明确，缺乏对解码器仅Transformer的深入理解。
method: 将下一标记预测建模为图搜索过程，从路径复用与路径压缩的演化视角分析幻觉。
result: 揭示了推理幻觉源于内在推理的路径复用与外在推理的路径压缩机制。
conclusion: 图视角下的路径演化分析为理解大语言模型推理幻觉的内在机制提供了理论依据。
---

## Abstract
Reasoning hallucinations in large language models (LLMs) often appear as fluent yet unsupported conclusions that violate either the given context or underlying factual knowledge. Although such failures are widely observed, the mechanisms by which decoder-only Transformers produce them remain poorly understood. We model next-token prediction as a graph search process over an underlying graph, where entities correspond to nodes and learned transitions form edges. From this perspective, contextual reasoning is a constrained search over a sampled subgraph (intrinsic reasoning), while context-free queries rely on memorized structures in the underlying graph (extrinsic reasoning). We show that reasoning hallucinations arise from two fundamental mechanisms: path reuse, where memorized knowledge overrides contextual constraints during early training, and path compression, where frequently traversed multi-step paths collapse into shortcut edges in later training. Together, these mechanisms provide a unified explanation for reasoning hallucinations in LLMs and connected to well-known behaviors observed in downstream applications.

---

## 论文详细总结（自动生成）

# 论文总结：幻觉何时产生？路径复用与路径压缩演化的图视角

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLMs）在推理时经常产生流畅但缺乏支撑、违反上下文或事实知识的“推理幻觉”，然而解码器仅Transformer产生此类幻觉的内在机制尚不明确。
- **整体含义与动机**：当前研究对LLM幻觉的观察多停留在现象层面，缺乏对其生成机制的深入理论理解。本文旨在打破这一认知黑盒，从图结构的全新视角揭示幻觉产生的根本原因，为理解和缓解大模型推理幻觉提供理论依据。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：将LLM的“下一标记预测”过程建模为在底层图上的图搜索过程。其中，实体对应图中的节点，模型学习到的转移关系构成边。
- **关键技术细节**：
  - **内在推理**：带有上下文约束的推理，被建模为在采样子图上的受限搜索。
  - **外在推理**：无上下文查询的推理，依赖于底层图中记忆的结构。
  - **幻觉产生的两大机制**：
    1. **路径复用**：在训练早期，记忆中的知识路径覆盖了上下文约束，导致模型无视当前上下文而输出记忆中的错误结论。
    2. **路径压缩**：在训练后期，频繁遍历的多步路径坍缩为捷径边，导致推理步骤被跳过，产生缺乏中间逻辑支撑的幻觉结论。

## 3. 实验设计：数据集/场景、benchmark、对比方法
- **说明**：基于提供的论文元数据与摘要，本文未提及具体使用的数据集、测试场景、基准或对比方法。据推测，该论文侧重于理论机制的分析与揭示，可能通过合成数据或特定的探针实验来验证图演化机制，但具体细节需参考原文全文。

## 4. 资源与算力
- **说明**：提供的文本中未明确说明所使用的算力资源（如GPU型号、数量、训练时长等）。

## 5. 实验数量与充分性
- **说明**：由于缺乏具体的实验细节，无法评估实验的组数、覆盖范围及客观公平性。但从摘要强调“提供了统一解释并连接了下游应用中的已知行为”来看，理论推演的逻辑自洽性可能是本文的重点，实验可能更多是为了佐证理论而非单纯的性能比拼。

## 6. 论文的主要结论与发现
- LLM的推理幻觉并非随机错误，而是源于图搜索演化过程中的两种系统性机制：训练早期的“路径复用”和训练后期的“路径压缩”。
- 这两种机制为解码器仅Transformer在不同推理模式（内在/外在）和不同训练阶段产生的幻觉提供了统一的解释，并与LLM在下游应用中已被广泛观察到的行为相吻合。

## 7. 优点：方法或实验设计上的亮点
- **视角新颖**：创新性地将下一标记预测建模为图搜索过程，将语言生成的动态过程与图论的静态/演化结构结合，为分析LLM行为提供了可解释的几何与拓扑视角。
- **机制统一**：不仅区分了内在推理与外在推理，还从训练的动态演化（早期vs后期）角度，提出了“路径复用”与“路径压缩”的统一理论框架，解释力强。
- **理论指导意义**：将幻觉归因于具体的图结构演化机制，为未来从图结构角度（如干预路径权重、抑制压缩等）缓解大模型幻觉指明了方向。

## 8. 不足与局限
- **实证验证的缺失风险**（基于现有信息）：高度理论化的建模需要严密的实证支撑。若缺乏在主流LLM和真实任务上的大规模验证，图模型与实际Transformer内部状态的映射关系可能被质疑为过度简化。
- **语义复杂性的简化**：将自然语言的标记预测简单映射为实体（节点）和转移（边）的图搜索，可能难以完全捕捉自然语言中复杂的模糊性、多义性和高维语义特征。
- **应用限制**：虽然揭示了机制，但“路径复用”和“路径压缩”在庞大参数量的LLM中如何精确定位和量化，以及如何在不损害模型泛化能力的前提下进行干预，仍面临巨大的工程挑战。

（完）
