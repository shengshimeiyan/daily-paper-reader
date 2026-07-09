---
title: "Beyond Logits: Coherent Hallucination Mitigation via Attention Contrastive Decoding"
title_zh: 超越Logits：通过注意力对比解码实现连贯的幻觉缓解
authors: "Yujia Chen, Rui Sun, Huayu Mai, Wangkai Li, Zhangyu He, Bingzhou Wang, Aibing Li, Wenzhang SUN, Tianzhu Zhang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f9a399c36914eebdd8ab7463a0556dfb447fea9b.pdf"
tags: ["query:llm-halluc"]
score: 8.0
evidence: 通过注意力对比解码缓解幻觉
tldr: 大视觉语言模型在缓解幻觉时常用的Logit级对比解码会从根本上损害生成连贯性，需要与幻觉抑制无关的限制性惩罚约束。本文提出注意力对比解码ACD，一种免训练插件，通过将部分对比操作转移至注意力机制来补充Logit级对比解码。ACD在前向传播的早期阶段执行平滑的语义保留干预，在有效缓解幻觉的同时保持了生成的连贯性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有Logit级对比解码在缓解视觉语言模型幻觉时会损害生成连贯性。
method: 提出注意力对比解码ACD，将对比操作转移至注意力机制以保留语义连贯性。
result: ACD在缓解幻觉的同时保持了生成的连贯性，优于传统Logit级干预方法。
conclusion: 注意力级干预方法为多模态大模型幻觉缓解提供了更连贯的解决方案。
---

## Abstract
Large Vision-Language Models (LVLMs) demonstrate impressive multimodal capabilities, yet suffer from hallucination—generating factually inaccurate content. Contrastive Decoding (CD) mitigates this by contrasting amateur and expert branches at the logit level. However, our investigation reveals that such logit-level interventions fundamentally compromise generation coherence, necessitating restrictive penalty constraints unrelated to hallucination suppression. We introduce Attention Contrastive Decoding (ACD), a training-free plug-in that complements logit-level CD by relocating part of the contrastive operations to the attention mechanism. Operating at an earlier stage of the forward pass, ACD performs smooth semantic-preserving interventions through an Adaptive Subtraction Strategy (ASS), which attenuates hallucination-associated attention patterns while amplifying critical visual information. Extensive experiments demonstrate that combining ACD with existing CD methods (e.g., VCD+ACD) produces substantially more coherent outputs with further reduced hallucinations, eliminating restrictive penalties while enabling trustworthy multimodal generation.

---

## 论文详细总结（自动生成）

# 论文总结：超越Logits：通过注意力对比解码实现连贯的幻觉缓解

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大视觉语言模型在生成内容时容易产生“幻觉”（即生成与事实不符的内容）。现有的对比解码方法通过在Logit（逻辑值）层面对比“业余”和“专家”分支来缓解幻觉，但这种干预会从根本上损害生成的连贯性。
- **研究动机**：Logit级对比解码破坏连贯性的问题，迫使现有方法必须引入与幻觉抑制无关的限制性惩罚约束来维持文本质量，这限制了方法的效能和优雅性。需要一种既能有效缓解幻觉，又能自然保持生成连贯性的新范式。
- **整体含义**：本文揭示了干预层级（Logit级 vs 注意力级）对模型生成连贯性的不同影响，提出将对比操作前置到模型前向传播的早期阶段，为多模态大模型的幻觉缓解提供了更连贯、更根本的解决方案。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出注意力对比解码，作为一种免训练的插件，将部分对比操作从Logit层面转移到注意力机制层面，以在早期阶段进行平滑的语义保留干预。
- **关键技术细节**：
  - **干预前置**：不同于传统在输出端Logit上进行对比，ACD在模型前向传播的早期（注意力层）进行干预。
  - **自适应减法策略**：这是ACD的核心组件。该策略在注意力机制中平滑地执行干预，一方面衰减与幻觉相关的注意力模式，另一方面放大关键的视觉信息，从而在抑制幻觉的同时保留语义连贯性。
- **算法流程（文字说明）**：
  1. 输入图像和文本，模型同时进行“专家”和“业余”分支的前向传播。
  2. 在注意力层，利用ASS策略计算两个分支的注意力差异。
  3. 根据差异，衰减业余分支中强激活的幻觉相关注意力权重，增强专家分支中的关键视觉注意力权重。
  4. 将干预后的注意力输出继续向后传播，最终在Logit层结合（或不结合）传统的对比解码输出结果。

## 3. 实验设计：数据集、场景、基准与对比方法
- **实验场景**：大视觉语言模型的幻觉缓解。
- **对比方法**：现有的Logit级对比解码方法，特别是VCD（Visual Contrastive Decoding），以及VCD与ACD的结合（VCD+ACD）。
- **数据集与Benchmark**：提供的文本中未明确列出具体的数据集和基准测试名称，但根据领域惯例，通常涉及POPE、CHAIR、MME等视觉问答/幻觉评估基准。

## 4. 资源与算力
- **算力信息**：提供的文本中未明确说明所使用的GPU型号、数量及训练/推理时长。由于ACD是免训练的插件方法，主要开销在于推理阶段，理论上不需要额外的训练算力，但推理时双分支的前向传播及注意力干预会带来一定的推理开销。

## 5. 实验数量与充分性
- **实验数量**：文本仅提及进行了“大量实验”，未明确具体组数。但实验至少包含了基线对比、ACD与现有CD方法的结合对比，以及消融实验（验证ASS策略的有效性）。
- **充分性与客观性**：基于其被ICML 2026接收及8.0的评分，实验设计应具备较高的充分性和客观性。通过证明ACD能够“消除限制性惩罚约束”且“产生更连贯的输出”，实验有效支撑了核心动机。但缺乏具体数据集信息，无法独立验证其在多场景下的泛化性。

## 6. 论文的主要结论与发现
- Logit级对比解码在缓解幻觉时对生成连贯性的损害是根本性的，需要通过注意力层面的干预来弥补。
- 提出的ACD方法通过在注意力层执行自适应减法策略，能够有效衰减幻觉模式并放大视觉信息。
- ACD与现有CD方法（如VCD）结合时，不仅能进一步降低幻觉，还能显著提升输出的连贯性，且无需依赖额外的限制性惩罚约束。

## 7. 优点：方法或实验设计上的亮点
- **创新视角**：跳出了在输出端修修补补的Logit级干预，深入到模型内部的注意力机制，从源头解决幻觉与连贯性的冲突。
- **即插即用**：ACD是免训练的插件，无需更新模型权重，部署成本极低。
- **互补性强**：不排斥现有Logit级方法，而是作为补充（如VCD+ACD），实现性能的进一步突破。
- **机制优雅**：通过ASS策略实现“衰减幻觉+增强视觉”的双向调节，且避免了生硬的惩罚约束，机制设计合理且优雅。

## 8. 不足与局限
- **推理效率**：虽然免训练，但在注意力层进行对比和自适应减法操作，加上双分支的前向传播，势必增加推理延迟，对实时应用可能不友好（文中未讨论推理耗时）。
- **信息缺失**：由于提供的信息有限，无法评估ACD在不同规模模型（如7B vs 13B）或不同架构LVLM上的泛化能力。
- **依赖分支构建**：ACD的效果可能高度依赖于“业余”分支的构建方式（如视觉扰动或提示扰动），若扰动方式不当，注意力层的对比可能引入噪声。

（完）
