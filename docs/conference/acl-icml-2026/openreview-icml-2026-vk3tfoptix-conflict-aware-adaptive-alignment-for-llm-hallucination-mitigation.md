---
title: Conflict-Aware Adaptive Alignment for LLM Hallucination Mitigation
title_zh: 面向大模型幻觉缓解的冲突感知自适应对齐
authors: "Ruohan Zong, Yang Zhang, Dong Wang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/75002956154f9d873829254e7b26105091d0b787.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 大模型幻觉缓解
tldr: 现有偏好对齐方法在缓解大模型幻觉时，常将真实性与有用性视为全局协作或冲突，导致真实性提升往往以牺牲有用性为代价。本文提出冲突感知自适应对齐方法，根据样本动态调整真实性与有用性的优化策略。实验表明，该方法在提升模型真实性的同时，有效保持甚至提升了模型的有用性，为缓解大模型幻觉提供了更优的权衡方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有偏好对齐方法在缓解大模型幻觉时，常导致有用性下降，未能动态平衡真实性与有用性。
method: 提出冲突感知自适应对齐方法，根据样本动态调整真实性与有用性的优化策略。
result: 实验表明该方法在提升模型真实性的同时，有效保持甚至提升了模型的有用性。
conclusion: 动态平衡真实性与有用性是缓解大模型幻觉的有效途径，冲突感知对齐优于传统方法。
---

## Abstract
Despite strong performance, large language models (LLMs) still suffer from hallucinations. Most existing mitigation methods operate at inference time, without addressing the alignment limitation: LLMs are not trained to recognize their own lack of knowledge, and therefore tend to generate plausible responses even when the required knowledge is missing. Preference alignment approaches encourage uncertainty expression or refusal to improve truthfulness, but often consequently degrade helpfulness. To address this trade-off, existing preference alignment methods typically treat truthfulness and helpfulness as either universally collaborative or universally conflicting objectives across all samples. In contrast, we show that these objectives are consistent for most samples and conflict only in a small subset—where adaptive trade-off is truly needed. Based on this insight, we propose Conflict-Aware Adaptive Margin Preference Alignment (CAMP), which explicitly models when conflicts arise and adaptively regulates optimization strength. Experiments on UltraFeedback and representative hallucination benchmarks demonstrate that CAMP consistently improves truthfulness while maintaining a favorable helpfulness trade-off compared to strong hallucination mitigation and multi-objective alignment baselines.

---

## 论文详细总结（自动生成）

# 论文总结：面向大模型幻觉缓解的冲突感知自适应对齐

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）存在严重的幻觉问题。现有的偏好对齐方法为了提升模型的真实性（如鼓励表达不确定性或拒绝回答），往往会导致模型的有用性显著下降。
- **现有研究的局限**：传统方法通常将“真实性”与“有用性”视为全局协作或全局冲突的目标，忽略了不同样本之间的差异性，导致在提升真实性时不可避免地牺牲了有用性。
- **整体含义**：本文旨在打破传统全局视角的局限，探索在缓解大模型幻觉的同时，如何有效保持甚至提升模型的有用性，实现两者的更优权衡。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：研究发现，“真实性”与“有用性”在大多数样本中是一致的，仅在少部分样本中存在冲突。因此，不需要进行全局妥协，而应根据样本特性动态调整优化策略。
- **方法名称**：冲突感知自适应边际偏好对齐
- **关键技术细节**：
  - **显式冲突建模**：识别并建模真实性与有用性目标发生冲突的样本子集。
  - **自适应优化强度调节**：对于目标一致的常规样本，正常进行优化；对于目标冲突的样本，自适应地调节优化强度（如通过调整Margin），在真实性与有用性之间实现动态平衡，避免因过度追求真实性而损害有用性。

## 3. 实验设计：数据集、Benchmark与对比方法
- **训练数据集**：UltraFeedback
- **评估Benchmark**：代表性的大模型幻觉评估基准（具体基准名称在给定材料中未详述）
- **对比方法**：
  - 强效的幻觉缓解基线方法
  - 多目标对齐基线方法

## 4. 资源与算力
- **未明确说明**：提供的论文元数据与摘要中未提及所使用的GPU型号、数量及训练时长等算力细节。

## 5. 实验数量与充分性
- **实验设置**：至少包含了一组在UltraFeedback上的对齐训练实验，以及在多个代表性幻觉基准上的评估实验，并与多类基线方法进行了对比。
- **充分性与客观性评估**：基于现有信息，实验设计覆盖了方法的核心主张（真实性与有用性的权衡），并对比了相关SOTA方法，具备一定的充分性。但缺乏对消融实验、不同规模模型泛化性等细节的描述，全面性有待全文验证。

## 6. 论文的主要结论与发现
- **关键发现**：真实性与有用性并非全局冲突，而是在大部分样本中一致，仅在小部分子集中冲突，这为自适应优化提供了基础。
- **主要结论**：动态平衡真实性与有用性是缓解大模型幻觉的有效途径。所提出的CAMP方法通过冲突感知和自适应调节，在提升模型真实性的同时，有效保持甚至提升了模型的有用性，优于传统的幻觉缓解和多目标对齐方法。

## 7. 优点：方法或实验设计上的亮点
- **洞察深刻**：打破了“真实性必然牺牲有用性”的固有认知，揭示了样本级别的目标冲突差异，动机具有启发性。
- **方法精细**：从“全局一刀切”转向“样本级自适应”，CAMP方法的设计紧贴其洞察，逻辑自洽且针对性强。
- **效果双赢**：成功缓解了偏好对齐中常见的“拒绝回答导致有用性下降”的痛点，实现了真实性与有用性的双赢。

## 8. 不足与局限
- **实验覆盖度未知**：摘要未明确幻觉Benchmark的具体类型（如是否涵盖事实幻觉、忠实性幻觉等），对方法泛化能力的评估范围未知。
- **偏差风险**：冲突建模的准确性高度依赖于训练数据中的偏好标注质量，若标注本身对“冲突”的定义存在偏差，可能影响自适应调节的效果。
- **应用限制**：自适应机制（如动态Margin调节）可能增加模型训练的复杂度和超参数调优难度，在极端数据分布下的鲁棒性需进一步验证。

（完）
