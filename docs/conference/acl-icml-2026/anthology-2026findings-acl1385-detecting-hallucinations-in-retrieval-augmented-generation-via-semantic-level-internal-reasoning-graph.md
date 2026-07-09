---
title: Detecting Hallucinations in Retrieval-Augmented Generation via Semantic-level Internal Reasoning Graph
title_zh: 基于语义级内部推理图的检索增强生成幻觉检测
authors: "Jianpeng Hu, Yanzeng Li, Jialun Zhong, Lei Zou, Wenfa Qi"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1385.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 检索增强生成中的忠实性幻觉检测
tldr: 针对检索增强生成系统中存在的忠实性幻觉问题，提出了一种基于语义级内部推理图的检测方法。该方法将逐层相关性传播算法从词元级扩展到语义级，构建基于归因向量的内部推理图，从而更精细地捕捉模型内部推理过程，提升幻觉检测效果。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1385/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 836, \"height\": 403, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1385/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1635, \"height\": 897, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1385/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 806, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1385/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1385/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1385/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 797, \"height\": 473, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1385/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 1035, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1385/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 795, \"height\": 847, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1385/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 797, \"height\": 185, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1385/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 794, \"height\": 166, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1385/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 795, \"height\": 149, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1385/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 798, \"height\": 157, \"label\": \"Table\"}]"
motivation: 现有RAG系统忠实性幻觉检测方法难以有效捕捉模型内部推理过程，导致判别器学习困难。
method: 提出语义级内部推理图方法，将逐层相关性传播算法扩展至语义级，构建基于归因向量的推理图。
result: 有效捕捉了模型内部推理过程，提升了RAG系统中忠实性幻觉的检测性能。
conclusion: 语义级内部推理图能够更精细地表征模型推理，为忠实性幻觉检测提供了新思路。
---

## Abstract
The Retrieval-augmented generation (RAG) system based on Large language model (LLM) has made significant progress. It can effectively reduce factuality hallucinations, but faithfulness hallucinations still exist. Previous methods for detecting faithfulness hallucinations either neglect to capture the models’ internal reasoning processes or handle those features coarsely, making it difficult for discriminators to learn. This paper proposes a semantic-level internal reasoning graph-based method for detecting faithfulness hallucination. Specifically, we first extend the layer-wise relevance propagation algorithm from the token level to the semantic level, constructing an internal reasoning graph based on attribution vectors. This provides a more faithful semantic-level representation of dependency. Furthermore, we design a general framework based on a small pre-trained language model to utilize the dependencies in LLM’s reasoning for training and hallucination detection, which can dynamically adjust the pass rate of correct samples through a threshold. Experimental results demonstrate that our method achieves better overall performance compared to state-of-the-art baselines on RAGTruth and Dolly-15k. Implementation available here: https://anonymous.4open.science/r/SIRG-1022.

---

## 论文详细总结（自动生成）

# 论文总结：基于语义级内部推理图的检索增强生成幻觉检测

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：基于大语言模型（LLM）的检索增强生成（RAG）系统虽然能缓解事实性幻觉，但依然存在“忠实性幻觉”，即生成内容与用户提供的上下文不一致。
- **研究动机**：现有的忠实性幻觉检测方法要么忽略了模型的内部推理过程，要么对内部特征的处理过于粗糙（例如直接在词元级别累加归因向量会引入大量连接词噪声），导致判别器难以有效学习。
- **整体含义**：本文旨在从语义层面忠实建模LLM的内部推理依赖关系，通过区分“连接词元”与“实质词元”，精准捕捉模型生成幻觉时的内部归因偏差，从而提升忠实性幻觉的检测效果。

## 2. 方法论：核心思想、关键技术细节与流程
- **核心思想**：提出一种基于语义级内部推理图（SIRG）的幻觉检测方法。将逐层相关性传播（LRP）算法从词元级扩展到语义级，构建归因向量驱动的内部推理图，并利用轻量级预训练模型进行幻觉判别。
- **关键技术细节与流程**：
  1. **词元分类与实体提取**：将生成词元分为“连接词元”（用于语法连接）和“实质词元”（反映语义内容）。幻觉本质上是模型将实质词元误当作连接词元处理（依赖前序生成而非上下文）。使用Spacy和Stanza提取名词、动词、命名实体等作为实质内容，过滤连接词噪声。
  2. **归因分数计算**：基于LRP算法计算每个生成词元对上下文词元的相关性向量。在聚合到语义片段级别时，对目标片段内的实体向量取平均，对源片段内的实体向量取最大值，以避免长片段中高贡献信息被稀释。
  3. **内部推理图构建**：
     - **节点**：上下文语义片段与模型响应语义片段的并集。
     - **边与权重**：片段间的归因分数。提出两种建边策略：**Top-k方法**（选择归因分数最高的k个源片段连边）和**自适应方法**（基于离散梯度的最大点区分重要与不重要源片段）。
  4. **幻觉判别**：
     - 将推理图中每个响应片段及其入边源片段线性化拼接为提示，输入轻量级PLM（AlignScore基于RoBERTa）进行二分类微调。
     - **阈值判定**：设定阈值 $\alpha$，若响应中幻觉片段的比例超过 $\alpha$，则判定整个响应为幻觉（公式：$l_a = I[\frac{\sum I[l_{a,j}=0]}{n_a} \le \alpha]$）。$\alpha$ 可根据场景对正确样本通过率的需求动态调整。

## 3. 实验设计
- **数据集**：
  - **RAGTruth**：包含Llama-7B和Llama-13B生成的RAG样本，具有人工标注的幻觉标签。
  - **Dolly-15k**：涵盖多场景的问答数据集，筛选出面向RAG的封闭问答场景，使用GPT-4进行标注。
- **评估指标**：Precision（精确率）、Recall（召回率）、F1-score。
- **对比方法**：
  - 基于提示的方法：Prompt (Llama-7b, GPT-3.5-turbo)
  - 基于自校验的方法：SelfCheckGPT
  - 基于微调的方法：Fine-tune (Llama-7b, Qwen2-7b)
  - 基于嵌入空间的方法：EigenScore, SEP
  - 基于归因的方法：LRP4RAG

## 4. 资源与算力
- **算力说明**：论文在计算延迟测试中提到了使用 **A100 GPU**，判别模型使用了124M参数的AlignScore。
- **未明确说明**：论文**未明确说明**模型训练所需的具体GPU数量、集群规模及总训练时长。

## 5. 实验数量与充分性
- **实验数量**：
  - 主实验：2个数据集 × 4个生成模型设置 × 9个基线方法。
  - 消融与分析实验：LRP忠实性扰动测试、阈值 $\alpha$ 影响分析、Top-k与自适应建边策略对比、5种实体提取配置对比、3种语义分割策略对比、4种框架计算延迟对比。
- **充分性与客观性**：实验设计非常充分，涵盖了定量对比、消融实验、超参敏感性分析、效率对比和定性可视化分析。对比方法涵盖多种主流范式，评估指标全面，实验设置客观公平。

## 6. 论文的主要结论与发现
- SIRG在RAGTruth和Dolly-15k数据集上的F1得分全面超越了现有SOTA方法（如LRP4RAG），在Llama-13B上F1提升达5.78%。
- 基于提示和自校验的方法（如SelfCheckGPT）极不稳定且容易盲目判定；基于嵌入的方法缺乏直接语义信息；而词元级归因方法（LRP4RAG）因引入过多连接词噪声导致性能次优。
- 扰动测试证明，基于LRP构建的语义级推理图能忠实反映模型内部推理过程，高归因片段对模型输出确实起决定性作用。
- 幻觉片段在推理图上表现为对模型前序生成的依赖远强于对用户上下文的依赖。

## 7. 优点
- **创新性归因升维**：首次将LRP从词元级扩展到语义级，提出“连接词元/实质词元”的区分机制，有效解决了粗粒度归因的噪声问题。
- **强可解释性**：构建的内部推理图直观揭示了幻觉的根源（模型将实质内容作连接词处理，依赖自身生成而非上下文），而非仅依赖黑盒特征。
- **轻量高效**：仅需微调小参数模型（124M）即可达到超越大模型微调的检测效果，且计算延迟低于需多次采样的SelfCheckGPT和需调用LLM的LRP4RAG。

## 8. 不足与局限
- **计算瓶颈**：LRP计算需要对每个词元生成过程计算内部梯度，时间复杂度高（单样本约25.49秒），且难以直接利用VLLM等推理加速框架。
- **图利用方式朴素**：线性化推理图的判别方式忽略了图中多跳依赖和细微的错误传播信息，限制了图结构潜力的充分发挥。
- **实体提取的误差与信息丢失**：依赖Spacy/Stanza进行实体提取可能存在误差；自适应建边策略倾向于只选1-2个源片段，可能导致判别器信息不足。
- **泛化性验证局限**：主要在特定参数量级的Llama和Qwen模型上验证，缺乏对超大规模模型或非Transformer架构的测试。

（完）
