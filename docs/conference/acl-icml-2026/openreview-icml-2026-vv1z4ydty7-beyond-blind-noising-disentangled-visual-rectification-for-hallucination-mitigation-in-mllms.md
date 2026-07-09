---
title: "Beyond Blind Noising: Disentangled Visual Rectification for Hallucination Mitigation in MLLMs"
title_zh: 超越盲目加噪：用于缓解多模态大语言模型幻觉的解耦视觉矫正
authors: "Yujia Chen, Rui Sun, Bingzhou Wang, Huayu Mai, Wangkai Li, Zhaoyang Li, Aibing Li, Wenzhang SUN"
date: 2026-04-30
pdf: "https://openreview.net/pdf/64de9e6b766953fea31d573a16adb90430200dac.pdf"
tags: ["query:llm-halluc"]
score: 8.0
evidence: 通过视觉矫正缓解多模态大模型幻觉
tldr: 视觉对比解码通过惩罚噪声图像引起的输出偏移来缓解多模态大语言模型幻觉，但其假设噪声偏移捕获幻觉方向是有缺陷的。本文证明语言-图像预训练编码器中的噪声漂移耦合了结构退化与幻觉诱导，导致其惩罚机制不可避免地抑制了有效的视觉语义。为此，本文提出解耦视觉矫正方法，利用自监督学习编码器在噪声下仅产生与幻觉路径正交的结构退化特性，实现了更精准的幻觉缓解与视觉语义保留。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 视觉对比解码假设噪声偏移捕获幻觉方向，但实际耦合了结构退化与幻觉诱导。
method: 利用自监督学习编码器在噪声下仅产生与幻觉正交的结构退化，实现解耦视觉矫正。
result: 解耦视觉矫正有效避免了有效视觉语义的抑制，提升了多模态大模型幻觉缓解效果。
conclusion: 分离结构退化与幻觉诱导是改进多模态大模型对比解码幻觉缓解的关键。
---

## Abstract
Visual Contrastive Decoding (VCD) mitigates hallucinations in Multimodal Large Language Models (MLLMs) by penalizing the output shift from noise-perturbed images, assuming this shift captures the hallucination direction. We prove this assumption flawed: noise-induced drift in Language-Image Pretrained (LIP) encoders is a \emph{coupled vector} entangling (i) structural degradation from corrupted visual information with (ii) hallucination induction from linguistic prior activation. VCD's indiscriminate penalty inevitably suppresses valid visual semantics. Our key insight is that Self-Supervised Learning (SSL) encoders exhibit \emph{only} structural degradation under noise—geometrically orthogonal to hallucination paths—enabling principled disentanglement via LIP--SSL differential response. We propose \textbf{Disentangled Visual Rectification (DVR)}, a training-free dual-stream framework performing visual-layer rectification and decoding-layer contrast on purified representations. DVR achieves approximately $5\times$ theoretical error reduction over VCD and establishes SOTA performance on POPE, MME, LLaVA-Bench and CHAIR benchmarks.

---

## 论文详细总结（自动生成）

# 论文总结：超越盲目加噪：用于缓解多模态大语言模型幻觉的解耦视觉矫正

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究背景**：多模态大语言模型（MLLMs）普遍存在“幻觉”问题（生成与图像内容不符的文本）。现有的视觉对比解码方法试图通过向图像添加噪声并惩罚噪声引起的输出偏移来缓解幻觉。
- **核心问题**：VCD方法基于一个有缺陷的假设——认为噪声引起的偏移纯粹捕获了“幻觉方向”。本文指出，在语言-图像预训练（LIP）编码器中，噪声引起的漂移实际上是一个**耦合向量**，它同时纠缠了两种效应：(i) 视觉信息受损导致的“结构退化”；(ii) 语言先验激活导致的“幻觉诱导”。
- **研究动机**：由于VCD无法区分这两种效应，其不加区分的惩罚机制不可避免地会抑制掉有效的视觉语义。因此，亟需一种能够解耦结构退化与幻觉诱导的精准矫正方法。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程
- **核心思想**：利用自监督学习（SSL）编码器在噪声下仅产生与幻觉路径几何正交的“结构退化”这一特性，通过LIP与SSL对噪声的差分响应，实现结构退化与幻觉诱导的原则性解耦。
- **关键技术细节**：
  - **正交特性发现**：SSL编码器由于缺乏语言先验的联合训练，在遭受噪声干扰时仅表现为视觉结构的退化，而不会触发语言先验导致的幻觉偏移，即其退化方向与幻觉路径在几何上正交。
  - **差分响应机制**：通过对比LIP编码器（耦合退化与幻觉）和SSL编码器（仅结构退化）对同一噪声图像的响应，可以提取出纯粹的幻觉诱导分量。
- **算法流程（DVR框架）**：
  - 提出了**解耦视觉矫正**，一种免训练的双流框架。
  - **视觉层矫正**：分别通过LIP和SSL编码器处理噪声图像，利用两者差分提取净化后的视觉表示。
  - **解码层对比**：在解码阶段，基于净化后的表示进行对比解码，精准惩罚幻觉分量，同时保留有效的视觉语义。

## 3. 实验设计：数据集、Benchmark与对比方法
- **使用的数据集/Benchmark**：
  - POPE（对象存在性幻觉评估）
  - MME（多维多模态评估）
  - LLaVA-Bench（开放式生成能力评估）
  - CHAIR（幻觉覆盖率评估）
- **对比方法**：主要对比了基线方法及视觉对比解码（VCD）等现有幻觉缓解方法（基于摘要推断）。

## 4. 资源与算力
- **说明**：提供的论文元数据与摘要中**未明确说明**所使用的算力资源（如GPU型号、数量、训练/推理时长等）。但值得注意的是，本文提出的DVR是一种**免训练**框架，因此不涉及额外的训练算力消耗，主要额外开销在于推理时的双流编码过程。

## 5. 实验数量与充分性
- **实验数量**：在4个主流且具代表性的多模态幻觉Benchmark上进行了实验，并提供了理论误差分析（相比VCD约5倍误差降低）。
- **充分性与客观性**：实验覆盖了判别式任务（POPE, MME）和生成式任务（LLaVA-Bench, CHAIR），评估维度较为全面，能够客观反映模型在缓解幻觉及保留视觉语义上的综合能力。但由于缺乏完整正文，无法确认消融实验的细粒度及不同模型架构上的泛化性测试数量。

## 6. 论文的主要结论与发现
- VCD等“盲目加噪”方法的根本缺陷在于其惩罚了不应被惩罚的有效视觉结构信息。
- SSL编码器的结构退化与幻觉路径正交是解耦两者的关键特性。
- 基于LIP-SSL差分响应的DVR方法，能够实现约5倍于VCD的理论误差降低，并在多个基准上达到SOTA，有效避免了有效视觉语义的抑制。

## 7. 优点：方法或实验设计上的亮点
- **洞察深刻**：精准定位了现有VCD方法的理论缺陷，打破了“噪声偏移即幻觉方向”的错误假设，从几何正交的角度提出了解耦思路。
- **即插即用且高效**：DVR为免训练框架，无需额外参数更新，降低了实际应用门槛。
- **理论与实证结合**：不仅有严密的几何与理论推导（5倍误差降低），还在多个权威基准上验证了SOTA效果，说服力强。

## 8. 不足与局限
- **推理开销增加**：双流框架意味着推理时需要同时运行LIP和SSL两个编码器，这会增加显存占用和推理延迟，摘要中未讨论此开销的影响。
- **依赖SSL编码器特性**：方法的有效性高度依赖SSL编码器在噪声下“绝对不产生幻觉诱导”的假设，若面对极端噪声或特定领域的SSL编码器，该正交假设是否依然严格成立存在风险。
- **实验覆盖度未知**：受限于提供的信息，无法确认该方法在不同规模MLLMs（如7B与13B对比）或闭源模型上的泛化表现，以及是否对图像分辨率和噪声类型敏感。

（完）
