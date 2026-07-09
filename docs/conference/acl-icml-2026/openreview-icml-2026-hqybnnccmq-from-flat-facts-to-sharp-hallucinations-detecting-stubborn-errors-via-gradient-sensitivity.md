---
title: "From Flat Facts to Sharp Hallucinations: Detecting Stubborn Errors via Gradient Sensitivity"
title_zh: 从平坦事实到尖锐幻觉：通过梯度敏感性检测顽固错误
authors: "Liew Yee Zhing, Andrew Huey Ping Tan, Anwar P.P. Abdul Majeed"
date: 2026-04-30
pdf: "https://openreview.net/pdf/c74520e6afdd6d81b9cb9b2a11855281c8dd6c42.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 检测顽固幻觉
tldr: 传统幻觉检测方法难以识别大模型自信出错的顽固幻觉，缺乏有效的检测信号。本文提出嵌入扰动梯度敏感性（EPGS）方法，假设顽固幻觉位于尖锐极小值，通过高斯噪声扰动输入嵌入并测量梯度幅值峰值来检测。实验表明，该方法显著优于基于熵和表示的基线方法，为检测顽固幻觉提供了稳健的几何信号。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 传统幻觉检测方法难以识别大模型自信出错的顽固幻觉，缺乏有效的检测信号。
method: 提出嵌入扰动梯度敏感性方法，通过高斯噪声扰动输入嵌入并测量梯度幅值峰值来检测幻觉。
result: 该方法显著优于基于熵和表示的基线方法，为检测顽固幻觉提供了稳健信号。
conclusion: 顽固幻觉位于尖锐极小值，基于梯度敏感性的几何方法是检测此类幻觉的有效手段。
---

## Abstract
Traditional hallucination detection fails on "Stubborn Hallucinations" — errors where LLMs are confidently wrong. We propose a geometric solution: Embedding-Perturbed Gradient Sensitivity (EPGS). We hypothesize that while robust facts reside in flat minima, stubborn hallucinations sit in sharp minima, supported by brittle memorization. EPGS detects this sharpness by perturbing input embeddings with Gaussian noise and measuring the resulting spike in gradient magnitude. This acts as an efficient proxy for the Hessian spectrum, differentiating stable knowledge from unstable memorization. Our experiments show that EPGS significantly outperforms entropy-based and representation-based baselines, providing a robust signal for detecting high-confidence factual errors.

---

## 论文详细总结（自动生成）

# 论文总结：从平坦事实到尖锐幻觉：通过梯度敏感性检测顽固错误

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）存在“顽固幻觉”现象，即模型在生成错误事实时表现出极高的置信度。传统的幻觉检测方法（如基于概率或熵的方法）难以识别此类高置信度错误，缺乏有效的检测信号。
- **整体含义**：本研究从损失景观的几何视角重新审视幻觉问题，揭示了稳健知识与顽固幻觉在几何特性上的本质差异，为解决大模型“自信犯错”的难题提供了全新的理论切入点和实践路径。

## 2. 论文提出的方法论
- **核心思想**：提出嵌入扰动梯度敏感性方法。基于几何假设：稳健的事实知识位于损失景观的平坦极小值，而顽固幻觉位于尖锐极小值（由脆弱的记忆支撑）。
- **关键技术细节**：EPGS 方法作为计算昂贵的 Hessian 谱的有效代理。通过向输入嵌入层注入高斯噪声进行扰动，然后测量模型梯度的幅值变化。
- **算法流程**：
  1. 获取输入文本的嵌入表示；
  2. 对输入嵌入施加高斯噪声扰动；
  3. 计算扰动后模型的梯度幅值；
  4. 根据梯度幅值的尖峰程度判断是否为顽固幻觉（尖锐极小值对扰动更敏感，导致梯度幅值产生剧烈尖峰）。

## 3. 实验设计
- **场景与目标**：针对大模型高置信度事实错误的检测场景。
- **对比方法**：将 EPGS 与基于熵的方法和基于表示的方法两类基线进行了对比。
- **Benchmark/数据集**：受限于提供的信息，摘要与元数据中未明确提及具体使用的数据集名称。

## 4. 资源与算力
- **算力情况**：文中未明确说明所使用的GPU型号、数量及训练/推理时长等算力细节。

## 5. 实验数量与充分性
- **实验数量**：根据摘要和元数据，实验至少包含了与两类主要基线（基于熵、基于表示）的对比实验。但缺乏消融实验及多数据集验证的具体数量信息。
- **充分性与客观性**：从结果描述“显著优于基线方法”来看，核心对比实验支撑了核心假设；但受限于信息不足，无法全面评估其在不同规模模型、不同领域数据上的充分性与公平性。不过，该论文已被 ICML 2026 接收且评分高达 9.0，表明其实验设计已达到顶会认可的客观与充分标准。

## 6. 论文的主要结论与发现
- 顽固幻觉在模型的损失景观中位于尖锐极小值，而稳健事实位于平坦极小值。
- 嵌入扰动引起的梯度幅值尖峰是检测尖锐极小值的有效指标，可作为 Hessian 谱的高效近似。
- EPGS 方法在检测高置信度事实错误方面显著优于传统基线，为顽固幻觉的检测提供了一种稳健的几何信号。

## 7. 优点
- **视角新颖**：跳出传统的输出概率/熵框架，从损失景观的几何平坦/尖锐特性出发解释幻觉，理论深刻。
- **方法巧妙**：用高斯噪声扰动结合梯度幅值测量来替代计算代价极高的 Hessian 谱，兼顾了理论严谨性与工程可行性。
- **针对性强**：直击大模型“自信出错”这一传统方法难以处理的痛点，具有极高的实用价值。

## 8. 不足与局限
- **计算开销**：尽管比直接计算 Hessian 谱高效，但 EPGS 仍需在推理时进行噪声注入和梯度计算，对于超大规模模型可能带来不可忽视的推理延迟和显存开销。
- **超参数敏感性**：高斯噪声的强度（方差）选择可能对梯度幅值的尖峰测量有较大影响，不同模型或不同层可能需要针对性调参。
- **信息缺失限制**：由于原文内容受限，无法评估该方法在非事实性幻觉（如逻辑谬误）上的表现，以及是否存在将正常罕见但正确的长尾知识误判为幻觉的偏差风险。

（完）
