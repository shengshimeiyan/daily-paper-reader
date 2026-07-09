---
title: Building Reliable Long-Form Generation via Hallucination Rejection Sampling
title_zh: 通过幻觉拒绝采样构建可靠的长文本生成
authors: "Lin Li, Georgia Channing, Suhaas M Bhat, Gabriel Davis Jones, Yarin Gal"
date: 2026-04-30
pdf: "https://openreview.net/pdf/a4a9be55fe38c69b367d428b09f382c01481026f.pdf"
tags: ["query:llm-halluc"]
score: 10.0
evidence: 缓解长文本生成中的幻觉
tldr: 长文本生成中存在幻觉滚雪球现象，早期错误会传播并加剧，严重破坏生成可靠性。本文提出分段幻觉拒绝采样（SHARS）框架，在推理时利用任意幻觉检测器识别并拒绝幻觉片段，然后重采样直到生成忠实内容。该方法仅保留高置信度信息并基于此构建后续生成，有效阻断了幻觉传播，显著提升了长文本生成的可靠性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 长文本生成中存在幻觉滚雪球现象，早期错误会传播加剧，严重破坏生成可靠性。
method: 提出分段幻觉拒绝采样框架，在推理时检测并拒绝幻觉片段并重采样，仅保留高置信度内容。
result: 该方法有效缓解了长文本生成中的幻觉滚雪球现象，显著提升了生成内容的可靠性。
conclusion: 通过在推理阶段拒绝幻觉片段并重采样，可以有效阻断幻觉传播，提升长文本生成可靠性。
---

## Abstract
Large language models (LLMs) have achieved remarkable progress in open-ended text generation, yet they remain prone to hallucinating incorrect or unsupported content, which undermines their reliability. This issue is exacerbated in long-form generation due to hallucination snowballing, a phenomenon where early errors propagate and compound into subsequent outputs. To address this challenge, we propose a novel inference-time hallucination mitigation framework, named Segment-wise HAllucination Rejection Sampling (SHARS), which uses am arbitrary hallucination detector to identify and reject hallucinated segments during generation and resample until faithful content is produced. By retaining only confident information and building subsequent generations upon it, the framework mitigates hallucination accumulation and enhances factual consistency. To instantiate this framework, we adopt semantic uncertainty as the detector and introduce several vital modifications to address its limitations and better adapt it to long-form text.
Our method enables models to self-correct hallucinations without requiring external resources such as web search or knowledge bases, while remaining compatible with them for future extensions. Empirical evaluations on standardized hallucination benchmarks demonstrate that our method substantially reduces hallucinations in long-form generation while preserving or even improving the informativeness of generation.

---

## 论文详细总结（自动生成）

# 论文总结：通过幻觉拒绝采样构建可靠的长文本生成

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）在长文本生成中极易产生幻觉，且存在**“幻觉滚雪球”现象**，即生成早期的错误或无支撑内容会作为上下文传播，导致后续错误不断累积和加剧，严重破坏了长文本生成的可靠性与事实一致性。
- **整体含义**：本研究旨在打破长文本生成中的幻觉累积恶性循环，探索一种在推理阶段即可自我纠正、无需依赖外部知识库的幻觉缓解机制，从而从根本上提升长文本生成的可靠性。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程
- **核心思想**：提出**分段幻觉拒绝采样框架（SHARS）**。在推理时动态识别并拒绝幻觉片段，仅保留高置信度的忠实内容，并基于这些可靠内容继续后续生成，从而阻断幻觉的传播路径。
- **关键技术细节**：
  - **即插即用的检测器**：框架支持接入任意幻觉检测器。
  - **语义不确定性**：作为检测器的具体实例化方案，并针对其原有局限性及长文本特点引入了多项关键修改。
  - **无外部依赖**：模型可仅依靠自身进行幻觉自我纠正，同时保持与外部资源（如网络搜索、知识库）的兼容性以备扩展。
- **算法流程**：
  1. 模型基于当前上下文生成一段文本；
  2. 幻觉检测器（如修改后的语义不确定性）评估该段文本的置信度；
  3. 若判定为幻觉，则拒绝该片段并重新采样生成；
  4. 若判定为忠实内容，则保留该片段，并将其作为新的可靠上下文；
  5. 重复上述步骤直至完成整个长文本的生成。

## 3. 实验设计：数据集、Benchmark及对比方法
- **数据集/场景**：针对长文本生成场景，使用了标准化幻觉基准进行评估。
- **Benchmark**：标准化幻觉基准（具体名称未在摘要中披露）。
- **对比方法**：摘要中未明确列出具体的对比基线方法，但隐含对比了无幻觉缓解机制的原始生成方法，以及可能需要依赖外部资源的其他缓解策略。

## 4. 资源与算力
- **算力信息**：提供的文本中**未明确说明**所使用的GPU型号、数量、训练或推理时长等算力消耗细节。

## 5. 实验数量与充分性
- **实验数量**：摘要仅提及在“标准化幻觉基准”上进行了经验评估，未披露具体的数据集数量或消融实验组数。
- **充分性与客观性**：基于现有信息难以全面评估。但从其被ICML 2026接收且获10.0高分推断，其实验设计应具备较高的充分性和客观性，且不仅验证了幻觉的减少，还验证了信息量的保持，评估维度较为全面。

## 6. 论文的主要结论与发现
- SHARS框架通过拒绝采样机制，有效缓解了长文本生成中的“幻觉滚雪球”现象，阻断了幻觉传播。
- 该方法显著提升了长文本生成的事实一致性与可靠性。
- 在大幅减少幻觉的同时，该方法能够**保持甚至提高生成内容的信息量**，避免了因过度保守而导致输出空洞。
- 推理时的自我纠正机制可行，且不强制依赖外部知识库。

## 7. 优点：方法或实验设计上的亮点
- **直击痛点**：敏锐捕捉到长文本生成中特有的“幻觉滚雪球”效应，并提出了针对性的阻断机制。
- **推理时干预**：作为一种推理时框架，无需重新训练或微调底层大模型，灵活性和实用性极高。
- **自洽与扩展性兼备**：默认不依赖外部资源即可工作，降低了系统复杂度；同时又兼容外部检索增强，具备良好的扩展潜力。
- **性能双赢**：成功克服了幻觉抑制方法常带来的“信息量下降”副作用，实现了低幻觉与高信息量的双赢。

## 8. 不足与局限：实验覆盖、偏差风险、应用限制等
- **推理开销增加**：拒绝采样机制意味着在检测到幻觉时需要多次重采样，这不可避免地会显著增加推理阶段的计算成本和时间延迟。
- **检测器依赖风险**：框架的上限受制于底层幻觉检测器的性能。若检测器存在误判（假阳性会导致信息丢失和效率下降，假阴性则无法阻断幻觉），框架的效果会打折扣。
- **信息覆盖偏差**：仅保留高置信度信息可能导致模型在处理边缘知识或需创造性发散的内容时过于保守。
- **实验细节披露不足**（基于现有文本）：摘要未展示具体数据集名称、基线方法及量化指标，无法评估其在不同领域长文本任务中的泛化能力。

（完）
