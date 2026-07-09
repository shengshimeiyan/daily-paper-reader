---
title: Anchor-Final Self-Supervision Drives Hallucination-Aware Optimization in Large Vision-Language Models
title_zh: 锚点-最终自监督驱动大型视觉语言模型中的幻觉感知优化
authors: "Jiaxi Liu, Yifeng Yang, Xinbing Wang, Qinying Gu, Nanyang Ye"
date: 2026-04-30
pdf: "https://openreview.net/pdf/80988e42c7b0bd5d4b08e8eaa4b56acc1c9a23e5.pdf"
tags: ["query:llm-halluc"]
score: 8.0
evidence: 大型视觉语言模型中的幻觉感知优化
tldr: 大型视觉语言模型常生成与视觉证据不符的幻觉标记，传统方法依赖显式监督或事后干预，效果受限。本文提出锚点-最终自监督（AFS）框架，利用中间层与最终层预测之间的差异，对视觉描述性标记进行选择性自监督，并结合幻觉感知标记分类与层间分布一致性约束。不同于传统方法，AFS通过群组相对策略优化直接对模型进行幻觉感知优化，有效减少了幻觉现象并显著提升了生成内容与视觉证据的对齐度。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大型视觉语言模型常生成与视觉证据不对齐的幻觉标记，传统方法依赖显式监督。
method: 提出AFS框架，利用中间与最终层预测差异进行选择性自监督和幻觉感知优化。
result: AFS有效减少了大型视觉语言模型中的幻觉现象，提升生成内容与视觉证据的对齐度。
conclusion: 基于层间差异的自监督优化为大型视觉语言模型幻觉缓解提供了新范式。
---

## Abstract
Hallucinations in large vision-language models (LVLMs) remain a critical challenge, where models often generate tokens that fail to align with visual evidence. To address this issue, we propose AFS: Anchor-Final Self-Supervision, a novel framework for hallucination-aware optimization in LVLMs. By leveraging discrepancies between intermediate and final layer predictions, AFS selectively applies self-supervision to visually descriptive tokens, incorporates hallucination-aware token classification, and encourages consistency between intermediate and final layer distributions. Unlike traditional methods that rely on explicit supervision or post-hoc interventions, AFS optimizes the model via Group Relative Policy Optimization (GRPO), using token-specific rewards derived from internal model signals. Experiments demonstrate that AFS significantly reduces hallucinations without compromising recall in caption generation. Beyond captioning, AFS excels in discriminative tasks, improving the reliability of object existence predictions and multimodal reasoning. Furthermore, AFS demonstrates strong cross-dataset generalization, transferring effectively across diverse visual domains. Code is available at \url{https://github.com/guavayew/AFS}.

---

## 论文详细总结（自动生成）

# 论文总结：锚点-最终自监督驱动大型视觉语言模型中的幻觉感知优化

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大型视觉语言模型（LVLMs）在生成过程中经常产生“幻觉”，即生成与输入视觉证据不一致或缺乏视觉支撑的标记。
- **整体含义与动机**：传统的缓解幻觉方法主要依赖显式的外部监督（如人工标注的反幻觉数据）或事后干预（如调整解码策略），这些方法不仅成本高昂，且效果存在上限。本文旨在探索一种利用模型内部信号的自监督机制，从模型训练优化的根本上感知并抑制幻觉，从而摆脱对外部显式监督的依赖。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出锚点-最终自监督（AFS）框架，利用模型中间层（锚点）与最终层预测之间的差异作为幻觉产生的内部信号，以此驱动选择性自监督和幻觉感知优化。
- **关键技术细节**：
  - **层间差异利用**：提取并计算中间层与最终层预测分布的差异，差异较大往往暗示模型对该标记的生成存在不确定性或幻觉倾向。
  - **选择性自监督**：并非对所有标记一视同仁，而是专门针对“视觉描述性标记”应用自监督，聚焦于与视觉证据紧密相关的生成内容。
  - **幻觉感知标记分类**：对标记进行分类识别，判断其是否容易产生幻觉，以便进行差异化处理。
  - **层间分布一致性约束**：在训练中显式鼓励中间层与最终层的预测分布保持一致，减少模型内部推理的振荡与不确定性。
  - **群组相对策略优化（GRPO）**：摒弃传统的交叉熵等显式监督损失，采用GRPO强化学习算法，利用源自模型内部层间差异信号的特定标记奖励，直接对模型进行幻觉感知优化。

## 3. 实验设计：数据集 / 场景、Benchmark 及对比方法
- **数据集与场景**：涵盖了图像描述生成、对象存在预测、多模态推理等多种场景，并涉及跨越不同视觉领域的数据集以测试泛化能力。
- **Benchmark**：
  - 生成任务：评估描述生成的幻觉率与召回率。
  - 判别任务：评估对象存在预测的可靠性及多模态推理的准确率。
  - 泛化任务：跨数据集的迁移效果评估。
- **对比方法**：摘要中未列出具体的基线模型名称，但明确指出对比了“依赖显式监督或事后干预的传统方法”。

## 4. 资源与算力
- **算力情况**：提供的论文元数据与摘要中**未明确说明**所使用的GPU型号、数量及训练时长等算力细节。

## 5. 实验数量与充分性
- **实验数量**：从摘要推断，实验至少包含了三大组：生成任务实验、判别任务实验、跨数据集泛化实验。
- **充分性与客观性**：实验设计覆盖了LVLM的核心应用场景（生成与判别），且在评估幻觉减少的同时关注了召回率是否受损，评估维度较为全面客观。但由于缺乏消融实验的具体说明（如各组件的贡献度），无法完全评估其内部机制的不可或缺性，整体上实验方向充分，但深度细节有待全文验证。

## 6. 论文的主要结论与发现
- AFS框架能够显著减少LVLMs中的幻觉现象，且不会牺牲生成任务的召回率，实现了幻觉抑制与信息保留的平衡。
- AFS不仅适用于生成式任务，在判别式任务（如对象存在预测和多模态推理）上也显著提升了模型的可靠性。
- AFS展现出强大的跨数据集泛化能力，能够有效迁移到不同的视觉领域。
- 基于模型层间差异的自监督优化为缓解LVLM幻觉提供了一种不依赖外部监督的新范式。

## 7. 优点：方法或实验设计上的亮点
- **内部信号挖掘**：创新性地利用模型中间层与最终层的预测差异作为幻觉感知信号，无需额外的人工标注数据，降低了监督成本。
- **精准优化**：通过幻觉感知标记分类和选择性自监督，将优化力量集中在易产生幻觉的视觉描述性标记上，提高了优化效率。
- **强化学习结合**：将内部信号转化为标记级别的奖励，结合GRPO算法进行端到端优化，方法链路自洽且直接作用于模型策略。
- **任务通用性**：打破了幻觉缓解方法仅限于生成任务的局限，在判别和推理任务上同样表现优异。

## 8. 不足与局限：实验覆盖、偏差风险、应用限制等
- **计算开销风险**：提取中间层预测并计算层间一致性可能增加训练过程中的显存占用和计算耗时，摘要未讨论此开销的代价。
- **锚点层选择依赖**：方法依赖于“中间层（锚点）”的选取，不同架构的LVLM最优锚点层可能不同，这增加了方法在不同模型间迁移的调参成本。
- **偏差固化风险**：依赖模型自身内部信号进行自监督，如果模型初始状态存在系统性偏差，自监督机制可能会强化而非纠正这些偏差。
- **实验细节缺失**：摘要未展示具体的基线对比和消融实验结果，无法判断其相对于当前最先进（SOTA）方法的绝对优势及各组件的边际贡献。

（完）
