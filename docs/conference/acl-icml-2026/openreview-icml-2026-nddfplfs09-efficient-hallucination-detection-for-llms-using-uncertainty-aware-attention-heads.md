---
title: Efficient Hallucination Detection for LLMs Using Uncertainty-Aware Attention Heads
title_zh: 使用不确定性感知注意力头进行大语言模型的高效幻觉检测
authors: "Artem Vazhentsev, Lyudmila Rvanova, Gleb Kuzmin, Ekaterina Fadeeva, Ivan Lazichny, Alexander Panchenko, Maxim Panov, Mrinmaya Sachan, Preslav Nakov, Timothy Baldwin, Artem Shelmanov"
date: 2026-04-30
pdf: "https://openreview.net/pdf/1446c8010a1341939cdc122010c930ca4b3fd8b3.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 使用不确定性感知注意力头进行高效幻觉检测
tldr: 针对现有幻觉检测方法计算量大或需监督的问题，提出了一种无监督且高效的幻觉检测框架RAUQ。该方法利用Transformer注意力行为的特点，即生成错误信息时某些不确定性感知注意力头会减少对前序词元的关注，自动检测这些头并结合其激活值，实现了高效的幻觉识别。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有大语言模型幻觉检测方法通常计算量大或需要监督数据，难以高效应用。
method: 提出无监督框架RAUQ，利用生成错误信息时不确定性感知注意力头减少关注前序词元的行为进行检测。
result: RAUQ框架实现了无监督且高效的幻觉检测，降低了计算和标注成本。
conclusion: 不确定性感知注意力头为大语言模型幻觉检测提供了一种高效且无监督的新途径。
---

## Abstract
While large language models (LLMs) have become highly capable, they remain prone to factual inaccuracies, commonly referred to as "hallucinations." Uncertainty quantification (UQ) offers a promising way to mitigate this issue, but most existing methods are computationally intensive and/or require supervision. In this work, we propose Recurrent Attention-based Uncertainty Quantification (RAUQ), an unsupervised and efficient framework for identifying hallucinations. The method leverages an observation about transformer attention behavior: when incorrect information is generated, certain "uncertainty-aware" attention heads tend to reduce their focus on preceding tokens. RAUQ automatically detects these attention heads and combines their activation patterns with token-level confidence measures in a recurrent scheme, producing a sequence-level uncertainty estimate in just a single forward pass. Through experiments on twelve datasets spanning question answering, summarization, and translation across nine different LLMs, we show that RAUQ consistently outperforms state-of-the-art UQ baselines. Importantly, it incurs minimal overhead, requiring less than 1% additional computation.
Since it requires neither labeled data nor extensive parameter tuning, RAUQ serves as a lightweight, plug-and-play solution for real-time hallucination detection in white-box LLMs.

---

## 论文详细总结（自动生成）

# 论文总结：使用不确定性感知注意力头进行大语言模型的高效幻觉检测

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）极易生成事实不准确的“幻觉”内容，而现有的不确定性量化（UQ）幻觉检测方法通常面临计算量大或依赖监督数据的困境，难以在实际中高效应用。
- **整体含义**：本研究旨在探索一种无需标注数据且计算开销极低的幻觉检测途径，以实现白盒LLM的实时幻觉识别，提升LLM在实际应用中的可靠性和安全性。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程
- **核心思想**：利用Transformer内部注意力机制的行为特征——当LLM生成错误信息（幻觉）时，模型中某些特定的“不确定性感知”注意力头会表现出减少对前序词元关注的倾向。
- **方法名称**：RAUQ（Recurrent Attention-based Uncertainty Quantification，基于循环注意力不确定性量化）。
- **关键技术细节与流程**：
  1. **自动检测**：自动识别出模型中对不确定性敏感的特定注意力头。
  2. **特征提取与结合**：提取这些注意力头的激活模式，并将其与词元级别的置信度度量相结合。
  3. **循环聚合**：采用循环方案处理结合后的特征。
  4. **单次推断**：仅需一次前向传播即可生成序列级别的不确定性估计，无需多次采样或额外模型训练。

## 3. 实验设计：数据集、场景与对比方法
- **数据集与场景**：在12个数据集上进行了评估，任务场景涵盖问答（QA）、摘要生成和机器翻译。
- **验证模型**：跨越9种不同的大语言模型进行测试。
- **对比方法**：与当前最先进的不确定性量化（SOTA UQ）基线方法进行了对比。

## 4. 资源与算力
- **算力情况**：提供的论文摘要与元数据中**未明确说明**所使用的GPU型号、数量及训练/推理时长等具体算力细节。
- **计算开销评估**：文中强调该方法额外增加的计算开销极小，低于总计算量的1%。

## 5. 实验数量与充分性
- **实验数量**：在9个不同LLM和12个涵盖多种任务的数据集上进行了广泛实验。
- **充分性与客观性评估**：实验设计**非常充分且客观**。跨模型（9个LLM）和跨任务（3大类生成任务）的广泛验证，有力地证明了该方法的泛化能力；与SOTA基线的对比也确保了评估的公平性。

## 6. 论文的主要结论与发现
- RAUQ框架实现了无监督且高效的幻觉检测，无需标注数据和大量参数调整。
- 在多种任务和模型上，RAUQ的检测性能持续优于现有的SOTA UQ基线方法。
- 该方法计算开销极低（<1%），可作为白盒LLM实时幻觉检测的轻量级、即插即用解决方案。

## 7. 优点：方法或实验设计上的亮点
- **极高的推理效率**：仅需单次前向传播，额外计算开销不到1%，具备实时检测的工程落地价值。
- **零监督成本**：完全无监督，不依赖任何标注数据，避免了高昂的数据标注成本。
- **深刻的机理洞察**：基于对Transformer注意力头行为的细致观察（不确定性感知注意力头的关注转移），具有较强的可解释性，而非纯粹的黑盒统计方法。
- **极强的泛化性**：在9个模型和12个数据集上的一致性优异表现，证明了方法的鲁棒性。

## 8. 不足与局限
- **应用场景受限**：该方法依赖于访问模型内部的注意力头激活值，因此仅适用于白盒LLM，无法应用于只能获取输入输出接口的黑盒API模型。
- **机理假设的普适性风险**：方法建立在“不确定性感知注意力头减少对前序词元关注”这一行为假设上，若某些特殊架构的模型或特定任务（如代码生成、复杂数学推理）不符合此注意力行为模式，方法效能可能会受损。
- **任务覆盖的局限**：尽管实验涵盖了QA、摘要和翻译，但未涉及代码生成或长上下文逻辑推理等幻觉同样严重的场景，在这些场景下的有效性有待进一步验证。

（完）
