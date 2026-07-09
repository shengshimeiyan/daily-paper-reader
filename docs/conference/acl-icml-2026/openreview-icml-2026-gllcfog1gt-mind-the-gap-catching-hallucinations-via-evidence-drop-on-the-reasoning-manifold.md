---
title: "Mind the Gap: Catching Hallucinations via Evidence Drop on the Reasoning Manifold"
title_zh: 注意差距：通过推理流形上的证据下降捕捉幻觉
authors: "Qunjie Chen, Yufei Chen, Xiaodong Yue, Linye Li"
date: 2026-04-30
pdf: "https://openreview.net/pdf/8844975f09dcb4dfc7c576a88908f2199718640c.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 通过证据下降检测大模型幻觉
tldr: 现有基于不确定性的幻觉检测器通常依赖序列级平均，忽略了推理的逐步动态，容易误分类困难但正确或容易但错误的样本。本文提出一种动态视角，将推理建模为证据流形上的轨迹，将幻觉特征化为局部证据支持突然下降的证据下降现象，并基于此设计了一种免训练且与模型无关的检测方法。实验表明该方法能有效捕捉推理过程中的拓扑偏离，提升幻觉检测准确性，为动态检测提供了新范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有基于序列平均的幻觉检测器忽略了推理的逐步动态，容易误分类样本。
method: 提出将推理建模为证据流形上的轨迹，将幻觉定义为证据下降，并设计免训练的检测方法。
result: 该方法能有效捕捉推理过程中的局部证据支持突然下降，提升幻觉检测准确性。
conclusion: 通过动态视角建模推理轨迹和证据下降，为幻觉检测提供了新范式和有效工具。
---

## Abstract
Large Language Models (LLMs) show strong reasoning abilities, yet their reliability is hindered by hallucinations, where fluent reasoning becomes factually or logically incorrect.
Most existing uncertainty-based detectors rely on sequence-level averaging, which ignores the step-wise dynamics of reasoning and often misclassifies hard-but-correct or easy-but-wrong samples.
We propose a dynamic perspective that models reasoning as a trajectory on a latent Evidence Manifold, where each step is supported by local evidence.
Hallucinations are characterized as Evidence Drops, i.e., sudden declines in local evidence support that indicate topological deviations from this manifold.
Based on this insight, we design a training-free and model-agnostic detector that identifies hallucinations via the worst-case Evidence Drop and enables step-level error localization.
Experiments on GSM8K, MATH, and ProcessBench show consistent improvements over sequence-level uncertainty baselines in selective accuracy and risk–coverage trade-offs.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）在推理过程中容易产生“幻觉”，即生成流畅但事实或逻辑错误的推理步骤，这严重影响了模型的可靠性。
- **研究动机**：现有的基于不确定性的幻觉检测器通常依赖“序列级平均”来评估置信度，这种方式忽略了推理过程的逐步动态特征。因此，它们容易误分类“困难但正确”的样本（不确定性高但实际正确）和“容易但错误”的样本（不确定性低但实际产生幻觉）。
- **整体含义**：幻觉检测需要从静态的整体评估转向动态的局部评估，关注推理过程中每一步的证据支持变化，从而更精准地捕捉逻辑崩塌的瞬间。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出一种动态视角，将推理过程建模为潜在“证据流形”上的轨迹，将幻觉特征化为“证据下降”，即局部证据支持的突然下降，这代表了推理轨迹偏离了流形的拓扑结构。
- **关键技术细节**：
  - **证据流形**：假设正确的推理步骤在流形上具有连续的局部证据支持。
  - **证据下降**：当推理步骤缺乏局部证据支持时，发生拓扑偏离，表现为证据支持的突然下降。
  - **最坏情况检测**：基于最坏情况的证据下降来识别整体序列的幻觉，避免了序列级平均带来的平滑效应。
  - **步骤级定位**：通过定位证据下降最剧烈的步骤，实现步骤级的错误定位。
- **方法特性**：免训练且模型无关，可直接应用于现有黑盒或白盒LLM的推理过程。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法
- **数据集/场景**：在数学推理场景下进行验证，使用了 GSM8K、MATH 和 ProcessBench 三个数据集。
- **评估基准**：使用选择性准确率和风险-覆盖权衡作为评估指标。
- **对比方法**：主要对比了现有的序列级不确定性基线方法。

### 4. 资源与算力
- **算力情况**：由于提供的文本信息受限，文中未明确说明所使用的GPU型号、数量、训练时长或推理开销等算力细节。鉴于该方法为“免训练”方法，主要算力消耗应集中在模型推理与证据下降指标的计算上。

### 5. 实验数量与充分性
- **实验数量**：在3个主流且具有挑战性的数学推理数据集上进行了实验，并与基线方法进行了对比。
- **充分性与客观性**：实验设计针对性强，直接切中“序列级 vs 步骤级”的对比核心，且使用了风险-覆盖权衡等严谨的评估指标，具有一定的客观性。但仅局限于数学推理领域，场景覆盖稍显单一，缺乏在开放域问答、代码生成等更易产生事实幻觉场景下的验证。

### 6. 论文的主要结论与发现
- 将推理建模为证据流形上的轨迹，并通过捕捉局部“证据下降”来检测幻觉是高度有效的。
- 基于最坏情况证据下降的检测器在选择性准确率和风险-覆盖权衡上，持续且显著地优于传统的序列级不确定性基线。
- 该方法不仅能判断整体推理是否产生幻觉，还能精准定位产生幻觉的具体推理步骤，为动态幻觉检测提供了新范式。

### 7. 优点：方法或实验设计上有哪些亮点
- **视角创新**：从静态的序列级平均转向动态的流形轨迹视角，深刻揭示了幻觉产生的局部拓扑偏离本质。
- **理论优雅**：将幻觉定义为“证据下降”，具有清晰的几何与拓扑直观性。
- **实用性强**：免训练且模型无关，极大降低了部署成本和门槛；同时支持步骤级错误定位，可解释性和实用价值高。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **实验覆盖局限**：目前仅在数学推理数据集上验证，未涉及事实性幻觉（如常识问答、摘要生成）等其他高频幻觉场景，泛化性有待证明。
- **偏差风险**：证据下降的计算依赖于模型自身的输出概率分布，对于本身概率校准较差的模型，证据下降的阈值设定可能存在偏差。
- **应用限制**：虽然免训练，但计算每一步的局部证据支持及流形轨迹可能带来额外的推理延迟，原文未讨论其实时计算效率。

（完）
