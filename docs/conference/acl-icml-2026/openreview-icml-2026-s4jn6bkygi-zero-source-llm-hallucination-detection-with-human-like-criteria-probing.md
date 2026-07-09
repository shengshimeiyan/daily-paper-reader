---
title: Zero-source LLM Hallucination Detection with Human-like Criteria Probing
title_zh: 基于类人标准探测的零源LLM幻觉检测
authors: "Jiahao Yang, Shuhai Zhang, Hailong Kang, Feng Liu, Qi Chen, Mingkui Tan"
date: 2026-04-30
pdf: "https://openreview.net/pdf/6ce0582d785f2bf8d69d03028a142cd995687601.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 零源LLM幻觉检测
tldr: 在无模型内部信号或外部参考的零源约束下，仅依靠文本问答对进行大语言模型的幻觉检测极具挑战。本文提出HCPD范式，模拟人类评估者的多面推理过程。其核心机制使LLM智能体自适应地将判断分解为加权可解释标准，并聚合成最终真实性评分，有效解决了零源幻觉检测难题，为无参考场景提供了可靠、可解释且高效的检测方案，提升了模型安全性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 在缺乏模型内部信号和外部参考的零源约束下，大语言模型的幻觉检测非常困难。
method: 提出HCPD范式，模拟人类评估者推理，自适应将判断分解为加权可解释标准并聚合评分。
result: HCPD在零源约束下有效检测了LLM幻觉，性能优于现有方法，提升了模型安全性。
conclusion: 类人标准探测机制为零源约束下的LLM幻觉检测提供了有效且可解释的新途径。
---

## Abstract
Large language models (LLMs) often hallucinate by generating factually incorrect or unfaithful content, posing significant risks to their safe use. Detecting such hallucinations is particularly challenging under the zero-source constraint, where no model internals or external references are available, and detection must rely solely on the textual query–answer pair. In this paper,  we propose Human-like Criteria Probing for Hallucination Detection (HCPD), a paradigm that emulates the multi-faceted reasoning of human evaluators. Its core is a Human-like Criteria Probing (HCP) mechanism, in which a LLM agent adaptively decomposes its judgment into a weighted set of interpretable criteria and aggregates criterion-specific scores into a final truthfulness measure. To achieve this adaptive capability, we introduce a reward-based alignment scheme using only weak supervision from semantic consistency. At inference, we employ a multi-sampling aggregation strategy to ensure robust decisions while preserving full interpretability. We further provide theoretical analysis supporting the reliability of our approach. Extensive experiments show that HCPD consistently outperforms state-of-the-art baselines, offering an effective and explainable solution for zero-source hallucination detection.

---

## 论文详细总结（自动生成）

### 1. 核心问题与动机
*   **核心问题**：大语言模型（LLM）经常产生幻觉，生成不正确或无根据的内容，严重威胁其安全使用。在“零源约束”（即无法获取模型内部信号，也没有外部参考源）下，仅依靠“问答对”文本进行幻觉检测极具挑战性。
*   **研究动机**：现有的幻觉检测方法往往依赖模型内部状态或外部检索，而在无参考、无内部信号的纯黑盒场景下，缺乏有效且可解释的检测手段。因此，亟需一种能够模拟人类判断逻辑、在零源约束下依然可靠的检测方案。

### 2. 提出的方法论
*   **方法名称**：HCPD (Human-like Criteria Probing for Hallucination Detection，基于类人标准探测的幻觉检测)。
*   **核心思想**：模拟人类评估者的多面推理过程，将复杂的真实性判断自适应地分解为多个可解释的具体标准，并聚合这些标准的评分得出最终结论。
*   **关键技术细节**：
    *   **HCP机制**：自适应地将判断分解为一组加权的、可解释的特定标准，并将这些特定标准的分数聚合为最终的真实性评分。
    *   **基于奖励的对齐方案**：为了实现自适应能力，引入该方案，仅使用语义一致性的弱监督信号进行训练，摆脱了对强标注的依赖。
    *   **多采样策略**：在推理阶段使用，以确保决策的鲁棒性，同时保持系统的完全可解释性。
    *   **理论支撑**：论文提供了理论分析，证明了该方法在可靠性上的理论保证。

### 3. 实验设计
*   **数据集/Benchmark**：由于正文内容受限（受网页验证码阻挡），摘要中仅提及进行了“广泛的实验”，未具体列出使用的数据集名称或公开Benchmark（如TruthfulQA等常见幻觉评测集的具体信息缺失）。
*   **对比方法**：摘要提及与“state-of-the-art baselines（最先进的基线方法）”进行了对比，但未指明具体算法名称。

### 4. 算力消耗
*   **算力信息**：提供的文本中未明确说明训练或推理所使用的GPU型号、数量及训练时长等算力消耗细节。

### 5. 实验充分性
*   **充分性评估**：根据摘要描述，实验包含了与SOTA方法的对比以及理论分析，声称“一致地优于基线”。但受限于可见文本，无法评估消融实验的具体组数、不同零源场景下的细分测试，以及实验对比的客观公平性（如是否控制了模型参数量等变量）。

### 6. 主要结论与发现
*   HCPD在零源约束下能够有效检测LLM幻觉，性能优于现有的基线方法。
*   类人标准探测机制为零源约束下的LLM幻觉检测提供了一种有效、可解释且可靠的新途径。
*   通过弱监督和自适应标准分解，解决了无参考场景下幻觉检测难和可解释性差的问题，提升了模型应用的安全性。

### 7. 优点与不足
*   **优点**：
    *   **场景切中痛点**：聚焦极具挑战性的“零源约束”场景，实用价值高（纯黑盒、无外部知识库依赖）。
    *   **可解释性强**：通过将判断分解为具体的、可解释的标准，打破了传统黑盒检测的不可知性，提供了清晰的决策路径。
    *   **弱监督依赖**：仅需语义一致性弱监督，降低了对昂贵人工标注的依赖。
    *   **兼顾鲁棒与解释**：多采样策略在提升鲁棒性的同时，未牺牲模型的可解释性。
*   **不足/局限**：
    *   **计算开销风险**：多采样策略和LLM智能体的自适应分解可能会显著增加推理阶段的计算延迟和Token消耗。
    *   **评估偏差**：使用LLM作为评估代理（智能体）来分解标准，可能会继承评估模型自身的认知偏差或幻觉。
    *   **信息不透明**：受限于可获取的文本，缺乏对算力消耗、具体数据集表现和细粒度消融实验的验证，难以评估其在极端复杂或特定领域问答中的泛化能力。

（完）
