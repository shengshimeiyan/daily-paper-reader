---
title: Attention Sinks as Internal Signals for Hallucination Detection in Large Language Models
title_zh: 注意力汇聚作为大模型幻觉检测的内部信号
authors: "Jakub Binkowski, Kamil Adamczewski, Tomasz Jan Kajdanowicz"
date: 2026-04-30
pdf: "https://openreview.net/pdf/3bca1d3a220105d57fb57c0f3262756fb3561e03.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 利用注意力汇聚检测幻觉
tldr: 大模型经常产生幻觉，而现有基于注意力图的幻觉检测方法对其利用的底层机制理解不足。本文发现幻觉与注意力汇聚现象深度纠缠，表明生成过程从分布式输入接地注意力转向压缩的先验主导计算。基于此洞察，提出SinkProbe幻觉检测方法，仅利用注意力图计算的汇聚分数即可有效识别幻觉输出，为幻觉检测提供了简单有效的内部信号。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有基于注意力图的幻觉检测方法对其利用的底层机制理解仍然不足。
method: 提出SinkProbe方法，利用注意力汇聚分数作为内部信号来检测大模型幻觉。
result: 注意力汇聚分数能有效指示幻觉发生，SinkProbe实现了高效的幻觉检测。
conclusion: 揭示了注意力汇聚与幻觉的内在联系，为幻觉检测提供了简单有效的信号。
---

## Abstract
Large language models frequently exhibit hallucinations: fluent and confident outputs that are factually incorrect or unsupported by the input context. While recent hallucination detection methods have explored various features derived from attention maps, the underlying mechanisms they exploit remain poorly understood. In this work, we propose SinkProbe, a hallucination detection method grounded in the observation that hallucinations are deeply entangled with attention sinks - tokens that accumulate disproportionate attention mass during generation - indicating a transition from distributed, input-grounded attention to compressed, prior-dominated computation. Importantly, although sink scores are computed solely from attention maps, we find that the classifier preferentially relies on sinks whose associated value vectors have large norms. Moreover, we show that previous methods implicitly depend on attention sinks by establishing their mathematical relationship to sink scores. Our findings yield a novel hallucination detection method grounded in theory that produces state-of-the-art results across popular datasets and LLMs.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）经常产生“幻觉”，即生成流畅且自信但事实上不正确或缺乏输入上下文支撑的内容。
- **研究动机**：尽管近期已有研究尝试利用注意力图来检测幻觉，但对这些方法背后的底层机制理解仍然不足。现有方法多停留在表象特征的应用，缺乏对注意力机制与幻觉产生之间内在联系的深入剖析。
- **整体含义**：本文揭示了幻觉产生与“注意力汇聚”现象的深度纠缠，指出幻觉的发生本质上是模型从“基于输入的分布式注意力”向“基于先验的压缩计算”的转变。这不仅为理解LLM幻觉提供了新的理论视角，也为幻觉检测提供了简单且高效的内部信号。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出 SinkProbe 方法，利用注意力汇聚分数作为内部信号来检测大模型的幻觉输出。
- **关键技术细节**：
  - **注意力汇聚**：指在生成过程中，某些特定词元积累了不成比例的注意力质量。这种现象标志着模型生成机制的转变。
  - **汇聚分数计算**：SinkProbe 仅依赖注意力图来计算汇聚分数。
  - **值向量范数偏好**：研究发现，虽然汇聚分数仅由注意力图计算得出，但分类器在实际检测中会优先依赖那些其关联的“值向量”具有较大范数的汇聚点。
  - **理论统一**：通过数学推导，证明了以往的幻觉检测方法实际上隐式地依赖于注意力汇聚，并建立了先前方法与汇聚分数之间的数学关系。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法
- **数据集与场景**：在多个主流的幻觉检测数据集上进行实验（摘要中未列举具体名称，统称为 popular datasets）。
- **Benchmark**：在多种流行的大语言模型（LLMs）上评估检测性能。
- **对比方法**：与现有的基于注意力图的幻觉检测方法进行对比，并通过数学关系揭示了这些基线方法与 SinkProbe 的内在联系。

### 4. 资源与算力
- **说明**：提供的论文元数据与摘要中未明确提及所使用的算力资源（如 GPU 型号、数量、训练/推理时长等）。

### 5. 实验数量与充分性
- **实验数量**：涵盖了多个主流数据集和多种 LLM 的验证，并进行了理论层面的数学关系推导。
- **充分性与客观性**：实验设计较为充分。不仅有跨数据集、跨模型的实证结果支撑，还通过数学证明将现有方法统一在本文的理论框架下，增强了结论的客观性和理论深度。但受限于摘要信息，无法判断消融实验的具体组数和细粒度。

### 6. 论文的主要结论与发现
- 幻觉与注意力汇聚现象深度纠缠，幻觉的产生伴随着模型计算模式从“输入接地”到“先验主导”的过渡。
- 仅利用注意力图计算的汇聚分数即可有效识别幻觉输出。
- 分类器在检测时偏好具有大范数值向量的汇聚点。
- 现有的基于注意力的幻觉检测方法在数学上隐式地依赖于注意力汇聚。
- SinkProbe 作为一种基于理论的方法，在主流数据集和 LLM 上达到了 SOTA 的幻觉检测效果。

### 7. 优点：方法或实验设计上有哪些亮点
- **理论洞察深刻**：不局限于经验性的特征工程，而是深入揭示了幻觉与注意力汇聚的底层机制，解释了“为何注意力图能检测幻觉”。
- **方法简单高效**：SinkProbe 仅需注意力图即可计算，无需复杂的模型结构修改或额外的大规模训练数据。
- **理论统一性强**：通过数学推导将先前方法统一为隐式依赖注意力汇聚，不仅验证了自身理论的普适性，也为后续研究提供了统一视角。
- **性能优异**：在简单机制的基础上取得了 SOTA 效果，兼具理论创新与实用价值。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **应用限制（白盒依赖）**：方法依赖于模型内部的注意力图和值向量，这要求对模型具有白盒访问权限，难以直接应用于仅提供 API 输出的闭源黑盒大模型。
- **偏差风险**：注意力汇聚现象可能不仅由幻觉引起，某些特殊的语法结构或常见固定搭配也可能引发汇聚，可能导致检测的误报（摘要中未详细讨论此偏差）。
- **信息缺失**：由于仅基于摘要分析，缺乏对算力消耗、推理延迟、以及不同解码策略下鲁棒性等实际部署关键指标的评估信息。

（完）
