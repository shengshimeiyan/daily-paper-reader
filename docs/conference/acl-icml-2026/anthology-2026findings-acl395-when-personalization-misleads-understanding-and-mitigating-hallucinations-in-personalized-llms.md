---
title: "When Personalization Misleads: Understanding and Mitigating Hallucinations in Personalized LLMs"
title_zh: 当个性化产生误导：理解与缓解个性化大语言模型中的幻觉
authors: "ZhongXiang Sun, Yi Zhan, Chenglei Shen, Weijie Yu, Xiao Zhang, Ming He, Jun Xu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.395.pdf"
tags: ["query:llm-halluc"]
score: 8.0
evidence: 缓解个性化大模型中的幻觉
tldr: 个性化大语言模型通过适应用户偏好提升满意度，但个性化可能扭曲事实推理，导致模型生成符合用户历史而非客观真相的答案，形成个性化诱导的幻觉。本文发现该现象源于个性化与事实表示的纠缠，并提出事实性保留个性化引导（FPPS）方法。作为一种轻量级推理时方法，FPPS在保持个性化优势的同时有效缓解了个性化诱导的幻觉，提升了事实可靠性，避免了错误信念的传播，为个性化与事实性的平衡提供了新思路。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.395/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 774, \"height\": 1144, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.395/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 761, \"height\": 371, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.395/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 789, \"height\": 875, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.395/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1650, \"height\": 319, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.395/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 799, \"height\": 715, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.395/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1589, \"height\": 526, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.395/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1653, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.395/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1652, \"height\": 1385, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.395/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1644, \"height\": 1065, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.395/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1632, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.395/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1622, \"height\": 966, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.395/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1632, \"height\": 825, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.395/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 793, \"height\": 486, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.395/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 794, \"height\": 147, \"label\": \"Table\"}]"
motivation: 个性化大语言模型在处理事实查询时，易因个性化与事实表示的纠缠生成幻觉。
method: 提出事实性保留个性化引导（FPPS），一种轻量级推理时方法，缓解个性化诱导的幻觉。
result: FPPS有效缓解了个性化导致的幻觉问题，在保持个性化的同时提升了事实可靠性。
conclusion: 解耦个性化与事实表示是缓解个性化大语言模型幻觉、提升事实可靠性的有效途径。
---

## Abstract
Personalized large language models (LLMs) adapt model behavior to individual users to enhance user satisfaction, yet personalization can inadvertently distort factual reasoning. We show that when personalized LLMs face factual queries, there exists a phenomenon where the model generates answers aligned with a user’s prior history rather than the objective truth, resulting in **personalization-induced hallucinations** that degrade factual reliability and may propagate incorrect beliefs, due to representational entanglement between personalization and factual representations. To address this issue, we propose **Factuality-Preserving Personalized Steering (FPPS)**, a lightweight inference-time approach that mitigates personalization-induced factual distortions while preserving personalized behavior. We further introduce **PFQABench**, the first benchmark designed to jointly evaluate factual and personalized question answering under personalization. Experiments across multiple LLM backbones and personalization methods show that FPPS substantially improves factual accuracy while maintaining personalized performance.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：个性化大语言模型在适应用户偏好时，会无意中扭曲事实推理。当面对事实性查询时，模型倾向于生成符合用户历史记录而非客观事实的答案，这种现象被称为**个性化诱导的幻觉**。
- **整体含义与动机**：随着个性化LLM成为商业产品的核心范式，其带来的“信息茧房”和事实可靠性下降的风险被忽视。研究发现，这种幻觉并非源于表面解码噪声，而是由于模型隐空间中**个性化表示与事实表示发生了纠缠**，导致激活状态向个性化对齐但事实错误的区域偏移。这不仅降低了模型的事实可靠性，还可能向下游用户传播错误信念。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出**事实性保留个性化引导（FPPS）**，一种轻量级的推理时框架。通过检测并解耦个性化与事实表示的纠缠，在必要时自适应地将隐状态引导回事实子空间，同时保留对个性化查询有益的行为。
- **算法流程（三阶段）**：
  1. **层选择（离线阶段）**：通过计算有无用户历史下的相对困惑度偏差，识别个性化对事实预测干扰最大的模型层 $L$。
  2. **探测检测器（离线阶段）**：在选定的层 $L$ 上训练逻辑回归分类器。输入为该层的隐状态，输出 $\hat{p} \in [0,1]$ 表示当前表示中个性化干扰事实推理的程度（纠缠概率）。正例为事实退化样本，负例为个性化有益样本。
  3. **自适应引导（推理阶段）**：根据探测器的输出 $\hat{p}$，对隐状态 $h'_L$ 进行调整，提供三种变体：
     - **硬引导（FPPS-H）**：当 $\hat{p} \ge \tau$ 时，直接从隐状态中减去个性化偏移向量 $v_u$（即 $h'_L - v_u$），完全移除个性化影响；否则保持不变。
     - **软引导（FPPS-S）**：构建引导向量 $s_f = m_{fact} - m_{pers}$（事实正确均值隐状态减去个性化正确均值隐状态），根据 $\hat{p}$ 连续调整：$\tilde{h}_L^S = h'_L + \gamma(\hat{p} - 0.5) s_f$。系数为正时抑制个性化，为负时增强个性化。
     - **混合引导（FPPS-M）**：结合两者，低风险（$\hat{p} < \tau$）时使用软引导微调，高风险（$\hat{p} \ge \tau$）时使用硬引导彻底移除个性化偏移。

### 3. 实验设计：数据集、Benchmark及对比方法
- **数据集/Benchmark**：提出了**PFQABench**，这是首个联合评估个性化与事实问答的基准。它结合了LongMemEval（提供真实用户长期交互历史）和FactQA（基于HotpotQA和2WikiMultiHopQA构建的多跳事实QA），共1000个样本（500个性化问题+500事实问题），确保事实查询与用户历史主题相关但答案独立。
- **对比方法**：覆盖了两种主流基于提示的个性化范式（检索增强和画像增强），包括：**PAG**（画像增强提示）、**DPL**（差异感知个性化）、**RAG**（检索增强生成）、**LLM-TRSR**（大模型时序摘要）。
- **基座模型**：LLaMA-3.1-8B-IT, Qwen2.5-7B-IT, Qwen2.5-14B-IT。

### 4. 资源与算力
- 文中仅提及**使用 NVIDIA A6000 GPU** 进行实验，但**未明确说明**具体的GPU数量、训练时长或推理耗时等详细算力消耗数据。

### 5. 实验数量与充分性
- **实验数量**：进行了大量实验，包括3个基座模型 × 4种个性化基线 × 3种FPPS变体的主实验；探测器和引导向量的消融实验；用户历史长度影响分析；受控模拟实验（LLM作为师生评估知识获取）；以及阈值 $\tau$、引导强度 $\gamma$、干预层 $L$ 的敏感性分析。
- **充分性与客观性**：实验设计非常充分且客观。不仅报告了事实准确率（F-Score），还严格报告了个性化准确率（P-Score）和综合得分，清晰展示了硬引导虽能大幅提升事实性但会损害个性化，而混合引导能取得最佳平衡，没有回避方法带来的权衡代价。

### 6. 论文的主要结论与发现
- 个性化LLM存在系统性的“个性化诱导幻觉”，其根源在于隐空间中个性化与事实表示的纠缠。
- 受控模拟表明，使用个性化LLM学习的用户，其事实知识获取准确率显著低于使用标准LLM（平均下降10.5%），即个性化会传播错误信念。
- 提出的FPPS-M方法在所有基座和个性化方法上，均能在保持个性化性能的同时大幅恢复事实准确性（Overall分数平均提升50%以上），并有效缓解个性化对下游知识获取的负面影响。
- 用户历史越长，个性化诱导的幻觉越严重，而FPPS能在各种历史长度下保持事实性能稳定。

### 7. 优点：方法或实验设计上的亮点
- **问题切入新颖**：首次系统定义并研究了“个性化诱导的幻觉”，揭示了个性化与事实性的内在冲突。
- **机理分析深入**：从表示纠缠的机制层面解释了幻觉成因，而非仅停留在输入输出层面。
- **方法轻量高效**：FPPS是推理时方法，无需修改或重训练模型参数，且混合引导（FPPS-M）设计精巧，实现了风险感知的动态干预。
- **评估体系完善**：构建了PFQABench填补了该领域缺乏联合评估基准的空白；设计了LLM模拟师生的受控实验，有力证明了个性化幻觉对人类知识获取的实际危害。

### 8. 不足与局限
- **模型适用范围受限**：FPPS依赖模型中间层的隐状态，因此无法直接应用于闭源的API模型（如GPT-4等），限制了其在主流商业黑盒模型上的直接部署。
- **模型规模与多样性有限**：实验仅在8B至14B参数的开源模型上进行，未验证其在更大规模（如70B+）或更多样化模型架构上的表现。
- **基准测试的局限**：PFQABench虽然有效，但尚未包含社会偏见或长期纵向视角的分析，对现实世界复杂影响的刻画仍有提升空间。
- **非万能的安全保障**：FPPS仅针对个性化诱导的幻觉，不能解决LLM的其他类型幻觉或误用问题。

（完）
