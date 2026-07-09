---
title: "FaithLens: Detecting and Explaining Faithfulness Hallucination"
title_zh: FaithLens：检测与解释忠实性幻觉
authors: "Shuzheng Si, Qingyi Wang, Haozhe Zhao, Yuzhuo Bai, Guanqiao Chen, Kangyang Luo, Gang Chen, Fanchao Qi, Minjia Zhang, Baobao Chang (常宝宝), Maosong Sun (孙茂松)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.689.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 检测忠实性幻觉
tldr: 识别大语言模型输出中的忠实性幻觉对检索增强生成和摘要等实际应用至关重要，但现有方法缺乏可解释性。本文提出FaithLens模型，能够联合提供二元预测及相应解释以提升结果可信度。该方法首先通过先进LLM合成带解释的训练数据并应用严格过滤策略，随后微调模型并结合基于规则的强化学习进一步优化，实现了高效且可解释的忠实性幻觉检测。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.689/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 818, \"height\": 497, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.689/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1652, \"height\": 851, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.689/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 774, \"height\": 463, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.689/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1623, \"height\": 955, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.689/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1651, \"height\": 634, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.689/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 759, \"height\": 448, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.689/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 758, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.689/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 701, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.689/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 805, \"height\": 421, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.689/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 803, \"height\": 406, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.689/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 693, \"height\": 408, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.689/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 631, \"height\": 384, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.689/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1654, \"height\": 1395, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.689/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 756, \"height\": 1024, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.689/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 804, \"height\": 646, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.689/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1654, \"height\": 849, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.689/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1652, \"height\": 475, \"label\": \"Table\"}]"
motivation: 识别大语言模型输出中的忠实性幻觉对RAG和摘要等应用至关重要，但现有方法缺乏可解释性。
method: 提出FaithLens模型，通过合成带解释的数据进行微调，并使用基于规则的强化学习优化，联合预测与解释幻觉。
result: FaithLens能够高效准确地检测忠实性幻觉并提供高质量解释，提升了模型的可信度。
conclusion: 联合预测与解释的FaithLens为忠实性幻觉检测提供了高效且可解释的解决方案。
---

## Abstract
Recognizing whether outputs from large language models (LLMs) contain faithfulness hallucination is crucial for real-world applications, e.g., retrieval-augmented generation and summarization. In this paper, we introduce FaithLens, a cost-efficient and effective faithfulness hallucination detection model that can jointly provide binary predictions and corresponding explanations to improve trustworthiness. To achieve this, we first synthesize training data with explanations via advanced LLMs and apply a well-defined data filtering strategy to ensure label correctness, explanation quality, and data diversity. Subsequently, we fine-tune the model on these well-curated training data as a cold start and further optimize it with rule-based reinforcement learning, using rewards for both prediction correctness and explanation quality. Results on 12 diverse tasks show that the 8B-parameter FaithLens outperforms advanced models such as GPT-5.2 and o3. Also, FaithLens can produce high-quality explanations, delivering a distinctive balance of trustworthiness, efficiency, and effectiveness.

---

## 论文详细总结（自动生成）

# 论文总结：FaithLens: Detecting and Explaining Faithfulness Hallucination

## 1. 核心问题与整体含义
- **研究背景**：大语言模型（LLMs）在检索增强生成（RAG）和摘要等场景中，极易生成与给定上下文不一致或无关的“忠实性幻觉”内容，这对实际应用构成了严重风险。
- **现有痛点**：
  1. **缺乏可解释性**：现有检测方法多为黑盒二元分类，无法提供判断依据，降低了结果的可信度。
  2. **跨任务泛化不一致**：不同任务（如摘要与RAG）的幻觉模式不同，现有通用模型表现参差不齐。
  3. **缺乏高质量数据**：人工标注成本高且一致性低，现有合成数据缺乏严格的质量控制（如多样性不足、简单样本过多）。
- **整体含义**：本文旨在构建一个兼具高效性、高准确率与强可解释性的忠实性幻觉检测模型，使用户不仅能知道“是否幻觉”，还能理解“为什么是幻觉”。

## 2. 方法论
- **核心思想**：提出 **FaithLens** 模型，将传统的二元分类任务扩展为“预测+解释”的联合生成任务。方法分为两个阶段：冷启动监督微调（SFT）和基于规则的强化学习（RL）。
- **关键技术细节**：
  - **数据合成与过滤（SFT阶段）**：
    1. **数据合成**：利用先进的大推理模型（DeepSeek-V3.2-Think）为开源数据集生成思维链、解释和预测标签。
    2. **三维数据过滤策略**：
       - **标签正确性**：剔除合成标签与真实标签不一致的样本，防止模型学习错误模式。
       - **解释质量**：计算加入解释前后模型对真实标签的困惑度（PPL），仅保留能降低PPL（即增强模型对正确答案信心）的解释。
       - **数据多样性**：使用K-Medoids聚类选取代表性样本作为探针集，保留能帮助探针集样本降低PPL的候选样本，确保数据分布广泛。
  - **基于规则的强化学习（RL阶段）**：
    - 采用GRPO算法优化模型，设计了复合奖励函数：$R_{final} = R_{pred} + R_{exp} + R_{format}$。
    - **预测正确性奖励 ($R_{pred}$)**：预测标签与真实标签一致则为1，否则为0。
    - **解释质量奖励 ($R_{exp}$)**：将生成的解释提供给一个“新手模型”（未微调的Llama-3.1-8B-Instruct），如果新手模型能基于该解释预测出正确标签，则奖励为1。这确保了解释的连贯性和信息量。
    - **格式奖励 ($R_{format}$)**：输出符合规定的XML标签格式则为1。

## 3. 实验设计
- **数据集**：使用了 **LLM-AggreFact**（包含11个不同任务，如摘要、RAG、对话等）和 **HoVer**（多跳推理任务）的清洗后版本，共12个评估任务。
- **评估基准**：
  - **有效性**：Macro-F1 分数。
  - **可解释性**：使用 GPT-4.1 从可读性、帮助性和信息量三个维度打分，并进行人工评估。
  - **效率**：推理成本（美元）。
- **对比方法**：
  - **先进LLMs**：GPT-4o, o1, GPT-4.1, o3-mini, o3, GPT-5.2, DeepSeek-V3.2, Claude-3.7-Sonnet, Llama-3.1-405B-Inst。
  - **专用检测模型**：AlignScore, MiniCheck, FactCG, ClearCheck。

## 4. 资源与算力
- **硬件**：使用了 NVIDIA A800 SXM4 80G GPU。
- **算力细节**：文中明确提到RL训练阶段使用了7张GPU（mini-batch size为16，总计112跨7个GPU），但**未明确说明具体的训练时长或总GPU小时数**。推理成本方面，FaithLens在1.2K样本上的推理成本仅为 $0.1，远低于GPT-4o的 $7.3 和 o1的 $140.6。

## 5. 实验数量与充分性
- **实验数量**：
  - 主实验：12个数据集上的全面对比。
  - 消融实验：7组（移除SFT、移除各类过滤、移除RL、移除解释质量奖励）。
  - 分析实验：声明去语境化/分解研究、人工评估（120样本）、跨基座模型泛化测试（Llama和Qwen系列）、参数研究（聚类数K、嵌入模型、新手模型选择）、变体方法测试。
- **充分性与客观性**：实验非常充分且设计公平。使用了清洗后的基准以避免标签噪声；与FactCG使用相同的初始数据和基座模型确保对比公平；不仅评估了准确性，还深入评估了可解释性和效率；通过人工评估验证了LLM-as-a-judge的可靠性。

## 6. 主要结论与发现
- **性能卓越**：8B参数的FaithLens在12个任务上的整体平均性能超越了GPT-5.2、o3等顶级大模型，且跨任务标准差最低（泛化最稳定）。
- **可解释性强**：FaithLens生成的解释在可读性、帮助性和信息量上优于或媲美顶级大模型，且远超现有的专用检测模型。
- **高效低成本**：在实现SOTA性能的同时，推理成本极低。
- **关键组件有效性**：数据过滤策略和RL阶段（特别是解释质量奖励）对提升检测性能和解释质量至关重要。此外，FaithLens无需额外的声明去语境化或分解步骤即可有效捕捉上下文依赖关系。

## 7. 优点
- **创新的任务建模**：将黑盒的二元分类扩展为可解释的联合预测，极大提升了检测结果的信任度。
- **巧妙的奖励设计**：利用“新手模型”能否看懂解释来作为解释质量的奖励，巧妙解决了自由文本解释难以用规则评估的难题。
- **严谨的数据质量控制**：提出基于PPL和聚类的三维数据过滤框架，有效提升了合成数据的可用性和多样性。
- **极高的实用价值**：以8B的小参数量击败顶级大模型，兼顾了效果、解释性与推理成本。

## 8. 不足与局限
- **模态局限**：仅针对文本模态，未扩展到多模态场景（多模态需要不同的接地信号和解释格式）。
- **推理开销**：由于采用先生成CoT、再生成解释、最后生成标签的串行生成范式，相比仅输出二元标签的同类小模型，存在额外的推理延迟。
- **分类粒度**：仅输出二元标签（忠实/幻觉），缺乏更细粒度的幻觉类别划分（受限于现有数据集缺乏统一分类法）。
- **评估偏差风险**：解释质量的自动评估主要依赖GPT-4.1，尽管有人工评估补充，但LLM作为评判者仍可能存在对自身输出评分偏高的偏差（文中也观察到了GPT-4.1对自身可读性评分虚高的现象）。

（完）
