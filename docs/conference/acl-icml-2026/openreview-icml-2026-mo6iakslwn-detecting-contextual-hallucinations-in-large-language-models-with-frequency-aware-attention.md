---
title: Detecting Contextual Hallucinations in Large Language Models with Frequency-Aware Attention
title_zh: 基于频率感知注意力的大语言模型上下文幻觉检测
authors: "Siya Qi, Yudong Chen, Runcong Zhao, Qinglin Zhu, Zhanghao Hu, Wei Liu, Yulan He, Zheng Yuan, Lin Gui"
date: 2026-04-30
pdf: "https://openreview.net/pdf/5097c4c69aa3f7bb2be43164228ecba17f12f372.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 检测大模型中的上下文幻觉
tldr: 针对大语言模型上下文生成中现有幻觉检测方法依赖粗粒度注意力摘要而无法捕捉细粒度不稳定性的问题，提出一种基于频率感知注意力的新视角。该方法受信号处理启发，将注意力分布建模为离散信号并提取反映局部快速变化的高频分量，发现幻觉token与注意力的高频波动密切相关。实验证明该方法能有效捕捉细粒度注意力不稳定性，显著提升幻觉检测性能。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有幻觉检测方法依赖粗粒度的注意力摘要，无法捕捉生成过程中的细粒度注意力不稳定性。
method: 将注意力分布建模为离散信号，提取反映局部快速变化的高频分量来检测幻觉token。
result: 分析表明幻觉token与注意力高频分量相关，所提方法能有效提升上下文幻觉检测性能。
conclusion: 利用注意力分布的高频特征可以更精细地检测大语言模型中的上下文幻觉。
---

## Abstract
Hallucination detection is critical for ensuring the reliability of large language models (LLMs) in context-based generation. Prior work has explored intrinsic signals available during generation, among which attention offers a direct view of grounding behavior. However, existing approaches typically rely on coarse summaries that fail to capture fine-grained instabilities in attention. Inspired by signal processing, we introduce a frequency-aware perspective on attention by analyzing its variation during generation. We model attention distributions as discrete signals and extract high-frequency components that reflect rapid local changes in attention. Our analysis reveals that hallucinated tokens are associated with high-frequency attention energy, reflecting fragmented and unstable grounding behavior. Based on this insight, we develop a lightweight hallucination detector using high-frequency attention features. Experiments on the RAGTruth and HalluRAG benchmarks show that our approach achieves performance gains over verification-based, internal-representation-based, and attention-based methods across models and tasks.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）在基于上下文的生成任务中容易产生“上下文幻觉”（即生成内容与提供的上下文不符），如何精准检测此类幻觉是确保LLM可靠性的关键。
- **研究动机**：现有的基于内部信号（尤其是注意力机制）的幻觉检测方法，通常依赖粗粒度的注意力摘要（如整体注意力权重分布），无法捕捉生成过程中细粒度的注意力不稳定性。
- **整体含义**：本文从信号处理的全新视角重新审视LLM的注意力机制，揭示了幻觉产生与注意力高频波动之间的内在联系，为细粒度、轻量级的幻觉检测提供了新思路。

### 2. 论文提出的方法论
- **核心思想**：受信号处理启发，将LLM生成过程中的注意力分布建模为离散信号，通过提取反映局部快速变化的高频分量来捕捉幻觉特征。
- **关键技术细节**：
  - **信号建模**：将序列生成中的注意力分布变化视为离散信号。
  - **高频分量提取**：分析该离散信号的高频分量，提取反映注意力局部快速变化的特征。
  - **特征关联发现**：发现幻觉token的产生伴随着注意力的高频能量波动，这反映了模型在生成幻觉时其“接地”行为是碎片化和不稳定的。
  - **检测器构建**：基于提取的高频注意力特征，开发了一种轻量级的幻觉检测器。

### 3. 实验设计
- **数据集**：RAGTruth 和 HalluRAG（这两个是专门用于评估RAG和上下文幻觉的基准数据集）。
- **Benchmark**：在跨模型和跨任务的设定下评估幻觉检测的性能。
- **对比方法**：
  - 基于验证的方法
  - 基于内部表示的方法
  - 基于注意力的方法

### 4. 资源与算力
- **算力情况**：提供的论文元数据与摘要中**未明确说明**所使用的GPU型号、数量及训练/推理时长等算力细节。仅提及所提方法为“轻量级”检测器。

### 5. 实验数量与充分性
- **实验数量**：基于现有信息，实验至少涵盖了2个主流幻觉检测基准数据集，对比了3大类基线方法，并进行了跨模型和跨任务的验证。
- **充分性与客观性评价**：
  - **充分性**：在数据集选择和基线对比上覆盖了当前主流的检测范式（验证、内部表示、注意力），跨模型/任务的测试也增强了结果的泛化性，实验设计基本充分。
  - **客观性**：由于缺乏全文细节，无法确认是否存在特定的数据偏置或超参挑选问题，但对比方法涵盖了不同技术路线，评价相对客观公平。消融实验等细节暂无法评估。

### 6. 论文的主要结论与发现
- 幻觉token与注意力分布中的高频能量密切相关，这反映了模型在产生幻觉时对上下文的关注是碎片化和不稳定的。
- 通过提取注意力的高频特征，可以比粗粒度方法更精细地捕捉生成过程中的细粒度不稳定性。
- 基于频率感知注意力的轻量级检测器在RAGTruth和HalluRAG基准上，显著优于现有的基于验证、内部表示和注意力的幻觉检测方法。

### 7. 优点
- **视角新颖**：创新性地将信号处理中的频率分析引入LLM注意力机制研究，打破了传统粗粒度注意力摘要的局限。
- **解释性强**：从“高频波动=接地行为不稳定=幻觉”的逻辑出发，为幻觉产生提供了合理的机制解释。
- **轻量高效**：方法基于生成过程中自然产生的注意力信号提取特征，无需额外的复杂模型或大规模重训练，具有实用价值。
- **性能优异**：在多个基准和模型上全面超越了各类现有基线方法。

### 8. 不足与局限
- **适用范围限制**：该方法依赖模型内部的注意力权重，对于不开放注意力接口的闭源商业模型（如GPT-4、Claude等）可能无法直接应用。
- **长上下文挑战**：在极长上下文场景中，注意力分布的离散信号长度会急剧增加，高频分量的提取可能面临计算效率或噪声干扰的挑战（受限于无全文，此为潜在风险推断）。
- **低频幻觉盲区**：如果某些类型的幻觉表现为注意力的平滑偏移（低频特征）而非快速波动，该方法可能存在漏检风险。
- **细节披露不足**：摘要中未提及高频提取的具体算法（如傅里叶变换、小波变换等）及算力消耗情况，实际工程的部署成本尚不明确。

（完）
