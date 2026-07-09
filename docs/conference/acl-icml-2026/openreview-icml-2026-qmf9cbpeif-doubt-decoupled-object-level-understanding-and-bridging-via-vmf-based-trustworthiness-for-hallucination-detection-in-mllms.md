---
title: "DOUBT: Decoupled Object-level Understanding and Bridging via vMF-based Trustworthiness for Hallucination Detection in MLLMs"
title_zh: DOUBT：基于vMF信任度的解耦对象级理解与桥接用于多模态大模型幻觉检测
authors: "Kaiqi Chen, Yang Qin, Changhao He, Xi Peng, Peng Hu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/8302e27f09a0751d1342bfa9c091b0fb99569bb3.pdf"
tags: ["query:llm-halluc"]
score: 7.0
evidence: 多模态大模型幻觉检测
tldr: 现有多模态大模型幻觉检测方法因视觉模块滞后，常高估模型可信度，导致漏检。本文提出模型无关方法DOUBT，通过解耦对象级理解并基于vMF分布评估信任度来检测幻觉。实验表明，DOUBT有效降低了多模态大模型幻觉的漏检率，提升了检测准确性，其解耦检测思路对大语言模型幻觉检测亦具有重要的借鉴意义。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有多模态大模型幻觉检测方法因视觉模块滞后，常高估模型可信度，导致漏检。
method: 提出模型无关方法DOUBT，解耦对象级理解并基于vMF分布评估信任度以检测幻觉。
result: DOUBT方法有效降低了多模态大模型幻觉的漏检率，提升了检测准确性。
conclusion: 解耦视觉与语言模块的理解并独立评估信任度，是提升多模态幻觉检测的有效途径。
---

## Abstract
Multimodal Large Language Models (MLLMs) frequently produce hallucinations (i.e., assertions that contradict the image or facts), undermining reliability in high-risk applications. Existing detection approaches typically feed images and texts jointly and estimate hallucination scores by measuring the consistency of model outputs. However, because the visual module often lags behind the language module in understanding and reasoning, MLLMs can repeatedly produce similar yet incorrect answers, yielding overestimated trustworthiness and missed detections. To address this, we propose a simple yet effective model-agnostic method, dubbed Decoupled Object-level Understanding and Bridging via vMF-based Trustworthiness (DOUBT). DOUBT first employs Object-level Understanding and Bridging (OUB), a two-step prompting scheme that decouples object recognition from relational reasoning by prompting the model to identify objects and then reason based on them. It further introduces a von Mises-Fisher (vMF)-based trustworthiness metric, which is more stable than semantic entropy metrics in small-sample settings. Extensive experiments and ablation studies on multiple benchmarks show that DOUBT consistently outperforms state-of-the-art baselines, demonstrating its robustness and generalizability for hallucination detection in MLLMs. The code is available at https://github.com/XLearning-SCU/2026-ICML-DOUBT.

---

## 论文详细总结（自动生成）

# 论文总结：DOUBT：基于vMF信任度的解耦对象级理解与桥接用于多模态大模型幻觉检测

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：多模态大语言模型（MLLMs）在生成过程中常产生“幻觉”（即生成与图像或事实相矛盾的内容），这严重影响了模型在高风险应用中的可靠性。现有的幻觉检测方法通常将图像和文本联合输入，通过测量模型输出的一致性来估计幻觉分数。
- **研究动机**：在MLLMs中，视觉模块在理解和推理能力上往往滞后于语言模块。这导致模型在面对视觉信息时，容易重复产生相似但错误的答案。现有方法基于输出一致性的评估会因此高估模型的可信度，最终导致幻觉的漏检。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出一种简单且有效的模型无关方法 DOUBT（Decoupled Object-level Understanding and Bridging via vMF-based Trustworthiness），通过解耦对象识别与关系推理，并引入更稳定的信任度评估指标来检测幻觉。
- **关键技术1：对象级理解与桥接（OUB）**：这是一种两步提示方案，旨在解耦视觉对象识别与语言关系推理。
  - 第一步：提示模型识别图像中的对象（解耦对象识别）。
  - 第二步：基于第一步识别出的对象，提示模型进行关系推理。
- **关键技术2：基于vMF的信任度度量**：引入基于 von Mises-Fisher (vMF) 分布的信任度指标来评估模型输出的可信度。相比于传统的语义熵指标，vMF指标在小样本设置下更加稳定，能更准确地反映模型是否产生幻觉。

## 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法
- **数据集/Benchmark**：论文提及在“多个基准”上进行了广泛的实验和消融研究，但受限于提供的信息，未列出具体的基准数据集名称。
- **对比方法**：与当前最先进的幻觉检测基线方法进行了对比。
- **实验场景**：多模态大模型的幻觉检测场景，重点评估在不同基准下检测幻觉的准确性和漏检率。

## 4. 资源与算力
- **算力情况**：提供的论文摘要与元数据中**未明确说明**所使用的算力资源（如GPU型号、数量、训练/推理时长等）。

## 5. 实验数量与充分性
- **实验数量**：进行了广泛的对比实验和消融研究。
- **充分性评估**：实验设计涵盖了多基准验证和消融研究，基本满足证明方法鲁棒性和泛化性的要求。但由于缺乏具体的数据集规模和实验组数细节，难以评估其在极端多样化场景下的覆盖充分性。总体而言，实验设置符合该领域的标准客观评估流程。

## 6. 论文的主要结论与发现
- 解耦视觉与语言模块的理解（即分离对象识别与关系推理）并独立评估信任度，是提升多模态大模型幻觉检测的有效途径。
- DOUBT方法有效克服了视觉模块滞后导致的可信度高估问题，显著降低了多模态大模型幻觉的漏检率，提升了检测准确性。
- 基于vMF的信任度指标在小样本场景下比语义熵更稳定，更适合用于幻觉评估。

## 7. 优点：方法或实验设计上有哪些亮点
- **洞察深刻**：精准指出了现有方法因“视觉模块滞后于语言模块”而导致模型重复生成错误答案、进而高估可信度的根本缺陷。
- **方法巧妙且通用**：提出的OUB两步解耦提示方案简单有效，且方法是模型无关的，无需修改模型内部结构即可直接应用。
- **指标优化**：针对小样本下语义熵不稳定的问题，引入vMF分布评估信任度，提升了评估的鲁棒性。
- **借鉴意义**：解耦检测的思路不仅适用于多模态模型，对大语言模型（LLM）的幻觉检测也具有重要的启发价值。

## 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **实验细节缺失**：摘要中未明确提及具体使用的数据集名称，无法判断其在特定领域（如医学图像、复杂图表等细粒度场景）的检测效果。
- **误差累积风险**：OUB方案将检测分为两步，第一步对象识别的错误可能会直接传递并放大到第二步的关系推理中，论文未提及如何缓解这种潜在的级联误差。
- **提示词敏感性**：作为基于提示方案的方法，其性能可能对提示词的表述较为敏感，不同模型对相同提示词的响应差异可能影响检测效果的稳定性。

（完）
