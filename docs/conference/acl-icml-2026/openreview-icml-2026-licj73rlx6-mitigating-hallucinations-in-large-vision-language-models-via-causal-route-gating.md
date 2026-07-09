---
title: Mitigating Hallucinations in Large Vision-Language Models via Causal Route Gating
title_zh: 通过因果路径门控缓解大型视觉语言模型中的幻觉
authors: "Zhe Cheng, Wenyu Chen, Fode Zhang, Dehuan Shen"
date: 2026-04-30
pdf: "https://openreview.net/pdf/475104fd1f24d762412a3acea5adef3a132516ab.pdf"
tags: ["query:llm-halluc"]
score: 6.0
evidence: 缓解视觉语言模型中的幻觉
tldr: 针对大型视觉语言模型中视觉与文本路径竞争导致模型生成流畅但不受图像支持的幻觉内容问题，提出一种免训练的因果路径门控干预方法。该方法将注意力头分解为视觉和文本路径，并利用高效的一次前向和一次梯度近似估计其token级效应，从而选择性地抑制先验主导的路径。实验表明该方法能有效揭示路径冲突并缓解幻觉，提升模型在真实世界部署中的可靠性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大型视觉语言模型常生成流畅但不受图像支持的幻觉内容，其关键失败模式源于视觉与文本路径的竞争。
method: 提出免训练的决策对齐干预，将注意力头分解为视觉和文本路径，并估计其token级效应以识别并抑制先验主导路径。
result: 该方法能有效揭示注意力头内的路径冲突，并通过选择性干预缓解幻觉，提升模型可靠性。
conclusion: 通过因果路径门控干预解决视觉与文本路径竞争，可有效缓解大型视觉语言模型的幻觉问题。
---

## Abstract
Large vision-language models (LVLMs) often hallucinate content that is fluent yet unsupported by the image, limiting their reliability in real-world deployment. We show that a key failure mode arises from route competition: even when visual tokens receive attention, the final token decision can be dominated by the textual pathway, causing the decoder to follow linguistic priors over visual evidence. To mitigate this, we propose a training-free, decision-aligned intervention that decomposes each attention head into a visual route and a text route, and estimates their token-level effects using an efficient one-forward/one-gradient approximation. These estimates reveal route conflict within heads and identify prior-dominant ones, enabling selective suppression of only the text route while keeping the visual route intact. Across five benchmarks spanning discriminative and generative settings, our method consistently reduces hallucination-related errors across models with limited impact on overall multimodal performance, while incurring a modest inference-time overhead.

---

## 论文详细总结（自动生成）

# 论文总结：通过因果路径门控缓解大型视觉语言模型中的幻觉

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大型视觉语言模型经常生成流畅但不受图像支持的幻觉内容，这严重限制了其在真实世界部署中的可靠性。
- **研究动机**：作者发现导致这种幻觉的一个关键失败模式是“路径竞争”。即使视觉token获得了注意力，最终的token决策仍可能被文本路径主导，导致解码器遵循语言先验而非视觉证据。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：提出一种免训练的、决策对齐的因果路径门控干预方法，通过识别并抑制先验主导的文本路径来缓解幻觉。
- **关键技术细节**：
  - **路径分解**：将模型中的每个注意力头分解为视觉路径和文本路径。
  - **效应估计**：利用高效的一次前向和一次梯度近似，估计这两条路径在token级别上的效应。
  - **冲突识别与选择性干预**：基于上述估计结果，揭示注意力头内部的路径冲突，识别出先验主导的注意力头。在生成时，选择性地仅抑制文本路径，同时保持视觉路径完整。

## 3. 实验设计：数据集、场景与对比方法
- **数据集与场景**：跨越判别式和生成式两种场景的五个基准测试。
- **Benchmark**：具体基准名称未在给定信息中详述，但明确涵盖了判别与生成两大核心评估维度。
- **对比方法**：未在给定信息中明确列出具体的对比基线方法，但实验跨越了多个不同的LVLM模型进行验证。

## 4. 资源与算力
- **算力消耗**：给定信息中未明确说明所使用的GPU型号、数量及训练/推理时长等具体算力细节。
- **额外开销**：摘要指出该方法会带来适度的推理时间开销。

## 5. 实验数量与充分性
- **实验数量**：在5个基准测试上进行了跨模型、跨场景（判别式+生成式）的实验。
- **充分性与客观性评估**：基于现有信息，实验覆盖了多模型、多任务场景，具备一定的充分性和客观性。但由于缺乏消融实验的具体描述，难以全面评估其内部各模块（如梯度近似、选择性抑制机制）的有效性。

## 6. 论文的主要结论与发现
- 视觉与文本路径的竞争是导致LVLMs产生幻觉的关键机制。
- 通过将注意力头分解并估计其token级效应，可以有效揭示模型内部的路径冲突。
- 采用因果路径门控进行选择性干预（抑制文本先验路径、保留视觉路径），能够持续减少幻觉相关错误，且对模型整体的多模态性能影响有限。

## 7. 优点：方法或实验设计上的亮点
- **免训练设计**：方法无需额外训练，即插即用，极大降低了应用成本和门槛。
- **精准细粒度干预**：深入到注意力头内部进行视觉/文本路径分解，仅抑制先验主导的文本路径而保留视觉路径，干预更具针对性和可解释性。
- **高效近似计算**：采用一次前向和一次梯度近似来估计效应，在实现因果干预的同时将计算开销控制在适度范围内。
- **性能平衡**：在缓解幻觉的同时，较好地保持了对整体多模态性能的影响。

## 8. 不足与局限
- **推理延迟**：作为推理时干预方法，虽然开销“适度”，但仍不可避免地增加推理时间，对极低延迟要求的应用可能存在限制。
- **路径分解的简化风险**：将注意力头严格划分为视觉和文本路径可能过于简化，实际中可能存在更复杂的混合交互路径。
- **信息覆盖局限**：受限于提供的信息，无法评估其在极端长尾分布数据上的偏差风险，以及不同规模模型（如极小或极大参数模型）上的泛化稳定性。

（完）
