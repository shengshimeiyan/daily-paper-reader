---
title: "Hallucination is a Consequence of Space-Optimality: A Rate-Distortion Theorem for Membership Testing"
title_zh: 幻觉是空间最优性的后果：成员测试的率失真定理
authors: "Anxin Guo, Jingwei Li"
date: 2026-04-30
pdf: "https://openreview.net/pdf/4d3f5259d90768db47158b21896de1ccb28063b8.pdf"
tags: ["query:llm-halluc"]
score: 7.0
evidence: LLM幻觉的理论解释
tldr: 大语言模型常对缺乏推理模式的随机事实产生高置信度幻觉，亟需理论层面的根本解释。本文将事实记忆形式化为成员测试问题，统一了布隆过滤器的离散误差指标与LLM的连续对数损失，并建立了率失真定理。该理论框架严格证明了即使在最优训练、完美数据和简化封闭世界设定下，幻觉也是空间最优性的必然结果，为理解幻觉提供了深刻理论见解与指导。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大语言模型常对缺乏推理模式的随机事实产生高置信度幻觉，需要从理论层面解释其根本原因。
method: 将事实记忆形式化为成员测试问题，统一布隆过滤器的离散误差指标与LLM的连续对数损失，建立率失真定理。
result: 理论证明即使在最优训练和完美数据下，幻觉也是空间最优性的必然结果。
conclusion: 幻觉是大语言模型在有限容量下追求空间最优性的固有代价，为幻觉现象提供了深刻的理论解释。
---

## Abstract
Large language models often hallucinate with high confidence on "random facts" that lack inferable patterns. 
We formalize the memorization of such facts as a membership testing problem, unifying the discrete error metrics of Bloom filters with the continuous log-loss of LLMs. 
By analyzing this problem in the regime where facts are sparse in the universe of plausible claims, we establish a rate-distortion theorem: the optimal memory efficiency is characterized by the minimum KL divergence between score distributions on facts and non-facts. 
This theoretical framework provides a distinctive explanation for hallucination under an idealized setting: even with optimal training, perfect data, and a simplified ``closed world'' setting, the information-theoretically optimal strategy under limited capacity is not to abstain or forget, but to assign high confidence to some non-facts, resulting in hallucination. 
We validate this theory empirically on both synthetic and real-world data, showing that hallucinations persist as a natural consequence of lossy compression.
The same theorem recovers and sharpens classical space lower bounds for Bloom-type filters, pinning down an additive constant left open for two-sided filters.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）经常对缺乏推理模式的“随机事实”产生高置信度的幻觉，目前亟需从理论层面解释这一现象的根本原因。
- **整体含义**：本研究旨在探究幻觉是否是模型架构或训练过程的缺陷，还是某种更底层规律（如信息论与空间最优性）的必然结果。论文提出，幻觉并非单纯的工程失误，而是模型在有限容量下追求空间最优性的固有代价。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：将LLM对事实的记忆问题形式化为“成员测试问题”，并从率失真理论的角度，证明幻觉是有限容量下实现空间最优性的必然产物。
- **关键技术细节**：
  - **统一误差指标**：将传统布隆过滤器中的离散误差指标与LLM的连续对数损失统一起来，建立跨领域的分析桥梁。
  - **建立率失真定理**：在事实在合理声明宇宙中呈稀疏分布的机制下进行分析，得出最优内存效率由“事实”与“非事实”分数分布之间的最小KL散度来表征。
  - **理论推导**：证明在有限容量下，信息论最优策略不是拒绝回答或遗忘，而是对某些非事实赋予高置信度，这正是幻觉的体现。
  - **附加理论贡献**：该定理还恢复并锐化了Bloom型过滤器的经典空间下界，解决了两边过滤器遗留的加法常数问题。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法
- **数据集/场景**：使用了合成数据和真实世界数据。
- **Benchmark与对比方法**：摘要中未详细说明具体的benchmark和对比基线模型，但实验的核心目标是验证“幻觉作为有损压缩的自然结果而持续存在”这一理论预测。

### 4. 资源与算力
- **算力情况**：提供的论文元数据与摘要中未明确说明所使用的算力资源（如GPU型号、数量、训练时长等）。

### 5. 实验数量与充分性
- **实验数量**：摘要仅提及在合成和真实世界数据上进行了验证，未明确具体实验组数或消融实验的规模。
- **充分性与客观性**：作为一篇理论驱动（Rate-distortion theorem）的论文，其实验主要起验证理论预测的辅助作用。虽然实验细节披露有限，但理论证明本身的严密性构成了论文的核心说服力，实验设计围绕“有损压缩导致幻觉”展开，具备客观性。

### 6. 论文的主要结论与发现
- **幻觉的必然性**：即使在最优训练、完美数据和简化的“封闭世界”设定下，幻觉依然不可避免。
- **空间最优性的代价**：在有限容量下，信息论最优策略不是放弃或遗忘，而是对某些非事实赋予高置信度，从而导致幻觉。
- **幻觉的本质**：幻觉是有损压缩的自然结果。
- **经典理论的拓展**：该理论框架不仅解释了LLM，还顺带解决并锐化了经典Bloom过滤器空间下界中的加法常数问题。

### 7. 优点：方法或实验设计上有哪些亮点
- **视角新颖深刻**：跳出常规的模型结构或数据偏差视角，从信息论和空间最优性的底层逻辑解释幻觉，提供了根本性的理论见解。
- **理论统一性强**：巧妙地将传统数据结构（Bloom filter）的离散误差与LLM的连续对数损失统一在成员测试的框架下。
- **证明条件苛刻**：在“最优训练、完美数据、封闭世界”的理想假设下证明幻觉必然存在，使得结论极具说服力和普适性。
- **附加理论价值**：不仅解释了LLM现象，还反哺了经典计算机科学理论，解决了Bloom过滤器遗留的常数问题。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **理想化设定限制**：理论证明基于简化的“封闭世界”设定和“随机事实缺乏推理模式”的前提，而真实世界LLM面临的是开放世界和复杂逻辑推理，理论模型可能无法完全覆盖所有幻觉场景。
- **实验细节与覆盖度不足**：从摘要看，实验部分主要作为理论验证，缺乏对复杂真实场景下不同规模LLM的广泛实证覆盖和工程性探讨。
- **应用指导有限**：虽然指出了幻觉是空间最优性的必然代价，但未直接提供缓解或消除幻觉的工程性方案（因为理论表明完全消除是不可能的，只能寻求权衡）。

（完）
