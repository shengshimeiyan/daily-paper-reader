---
title: Hallucination Detection in LLMs with Topological Divergence on Attention Graphs
title_zh: 基于注意力图拓扑散度的大语言模型幻觉检测
authors: "Alexandra Bazarova, Andrei Volodichev, Aleksandr Yugay, Andrey Shulga, Alina Ermilova, Konstantin Polev, Julia Belikova, Rauf Parchiev, Dmitry Simakov, Maxim Savchenko, Andrey Savchenko, Serguei Barannikov, Alexey Zaytsev"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.704.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 基于注意力图拓扑散度的幻觉检测
tldr: 针对检索增强生成中大语言模型易产生与提供上下文不符的无支持输出的问题，提出基于拓扑的幻觉检测器TOHA。该检测器利用拓扑散度指标量化注意力矩阵诱导图的结构特性，发现提示与响应子图间的高拓扑散度与不忠实输出高度相关，且该模式独立于数据集。大量实验证明该方法在问答和摘要任务中具有优异且稳定的幻觉检测性能。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.704/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1665, \"height\": 484, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.704/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 793, \"height\": 1043, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.704/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1709, \"height\": 470, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.704/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1652, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.704/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 814, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.704/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 788, \"height\": 315, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.704/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 789, \"height\": 304, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.704/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 795, \"height\": 516, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.704/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 792, \"height\": 441, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.704/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1615, \"height\": 1024, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.704/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1638, \"height\": 710, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1661, \"height\": 1469, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 811, \"height\": 689, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 811, \"height\": 411, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 815, \"height\": 354, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1476, \"height\": 581, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1504, \"height\": 721, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 813, \"height\": 378, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 697, \"height\": 163, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 700, \"height\": 757, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 727, \"height\": 419, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1484, \"height\": 598, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 838, \"height\": 1499, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 741, \"height\": 466, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 625, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1650, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1650, \"height\": 199, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 553, \"height\": 326, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1653, \"height\": 275, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.704/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 805, \"height\": 250, \"label\": \"Table\"}]"
motivation: 在检索增强生成场景中，大语言模型仍易产生与上下文不符的幻觉输出。
method: 提出TOHA检测器，利用拓扑散度指标量化注意力矩阵诱导图的结构特性，比较提示与响应子图的拓扑差异。
result: 特定注意力头中较高的拓扑散度与不忠实输出显著相关，TOHA在多项任务中表现出色。
conclusion: 注意力图结构的拓扑散度为大语言模型幻觉检测提供了有效且一致的新信号。
---

## Abstract
Hallucinations remain a critical challenge for large language models (LLMs), particularly in Retrieval-Augmented Generation (RAG) settings where models may generate outputs unsupported by the provided context. To address this, we introduce TOHA, a TOpology-based HAllucination detector, which leverages a topological divergence metric to quantify the structural properties of graphs induced by attention matrices. Examining the topological divergence between prompt and response subgraphs in RAG settings reveals consistent patterns: higher divergence values in specific attention heads correlate with unfaithful outputs, independent of the dataset. Extensive experiments — including evaluations on question answering and summarization tasks — show that our approach achieves state-of-the-art or competitive results on several benchmarks while requiring minimal annotated data and computational resources. Our findings indicate that the topological structure of attention matrices provides an efficient and robust metric for assessing the correctness of LLM’s responses.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）在检索增强生成（RAG）场景中极易产生“幻觉”，即生成与提供上下文不符或无支持的内容。
- **研究动机**：现有的幻觉检测方法存在明显局限：基于监督学习的方法需要大量标注数据；基于一致性的方法（多次采样）计算成本极高；基于不确定性的方法忽略了模型丰富的内部状态；而现有的基于注意力的方法往往忽略注意力图的几何结构，或对所有注意力头一视同仁。
- **整体含义**：本文提出从拓扑数据分析（TDA）的视角，利用注意力图的拓扑结构特性来检测幻觉，为高效、低资源消耗且具有强泛化能力的幻觉检测提供了新范式。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出 TOHA（TOpology-based HAllucination detector），通过计算注意力图中提示词子图与响应子图之间的拓扑散度来量化幻觉程度。核心假设是：响应相对于提示的拓扑结构越“新颖”（散度越大），产生幻觉的概率越高。
- **关键技术细节**：
  - **注意力图构建**：将注意力矩阵视为全连接无向加权图，边权设为 $1 - w_{ij}$（表示伪距离），节点分为提示集 $P$ 和响应集 $R$。
  - **拓扑散度指标 $MTop-Div_G(R, P)$**：改编自流形拓扑散度。在计算前，先将 $P$ 节点间的边权置零（消除提示内部连接的噪声），然后计算 Vietoris-Rips 复形的 0 阶同调条形码，散度值为条形码区间长度之和：$MTop-Div_G(R, P) = \sum_{[b_i, d_i] \in B_0} |d_i - b_i|$。
  - **几何与信息论解释**：该散度在几何上等价于将响应节点 $R$ 连接到提示节点 $P$ 的最小生成森林（MSF）的长度；在信息论上，它衡量了响应相对于提示的结构新颖度（与MST长度的熵估计相关）。
- **算法流程（TOHA）**：
  1. **探针集评估**：使用少量标注数据（幻觉样本 $S_h$ 和真实样本 $S_g$），计算每个注意力头的分离能力 $\Delta_{ij}$（幻觉样本与真实样本散度均值之差）。
  2. **头选择**：按 $\Delta_{ij}$ 降序排列，选择排名前 $N_{opt}$（最大设为10）的“幻觉感知”注意力头。
  3. **预测**：对测试样本，计算所选头的 $MTop-Div_G(R, P)$ 均值作为最终幻觉得分。

### 3. 实验设计：数据集、场景、Benchmark及对比方法
- **数据集与场景**：涵盖问答（QA）和摘要生成任务。包括 RAGTruth 的长格式QA（MS MARCO）和摘要（CNN/DM）、对话QA（CoQA）、阅读理解（SQuAD）、极端摘要（XSum），以及多跳QA（HotpotQA）。
- **Benchmark**：ROC AUC（受试者工作特征曲线下面积）。
- **对比方法**（8种基线）：
  - **基于不确定性**：Perplexity, Max entropy。
  - **基于内部状态**：ReDeEP, HaloScope, LLM-Check。
  - **基于一致性**：Semantic entropy, EigenScore, SelfCheckGPT。

### 4. 资源与算力
- **算力资源**：论文在实现细节中提及所有实验均在 **NVIDIA L40** GPU 上进行。
- **算力消耗说明**：未明确说明使用的GPU数量和具体训练/推理时长，但提供了相对时间对比：在16个样本上，TOHA耗时约10.5秒，比单次生成的SelfCheckGPT快约7倍，比标准多次生成的SelfCheckGPT快70倍以上，接近轻量级熵基线的速度。

### 5. 实验数量与充分性
- **实验数量**：实验规模庞大且覆盖全面。
  - **主实验**：5个主流开源模型（7B-13B）在5个数据集上的对比。
  - **多跳验证**：在HotpotQA上的额外验证。
  - **消融实验**：探针集大小敏感性、注意力头数量影响、置零提示节点距离的必要性、与其他注意力特征（如Wasserstein距离、谱范数等）的对比。
  - **零样本变体**：完全无标注数据下的测试（TOHA Copy Heads）。
  - **统计检验**：使用 Wilcoxon-Holm 事后分析验证统计显著性。
- **充分性与客观性**：实验设计非常充分且公平。不仅对比了单次生成和多次生成设定下的基线，还进行了跨数据集的迁移实验和严格的统计显著性检验，客观证明了方法的有效性和鲁棒性。

### 6. 论文的主要结论与发现
- **性能优越**：TOHA在多项基准上达到SOTA或极具竞争力的结果，在部分数据集上大幅超越基线（如Mistral-7B上提升11.7%，LLama-2-7B上提升21.6%）。
- **存在“幻觉感知”注意力头**：发现少量特定的注意力头在不同数据集上始终对幻觉样本产生更高的拓扑散度，仅需平均这10个头的散度即可实现鲁棒检测。
- **与复制行为的关联**：这些“幻觉感知”头在机制上与“复制/归纳头”高度重合。当模型无法在上下文中找到可复制的模式时，会默认关注首个token，这种模式在拓扑散度上表现为高发散。
- **高效与强泛化**：仅需50个标注样本即可稳定检测，且跨数据集迁移能力强，计算速度比同质量方法快一个数量级。

### 7. 优点：方法或实验设计上的亮点
- **视角新颖**：首次将拓扑数据分析（TDA）中的流形拓扑散度引入注意力图的幻觉检测，赋予了注意力图明确的几何与信息论解释。
- **极致高效**：无需训练，极少标注数据，单次前向传播级别的时间消耗，解决了实际部署中计算资源受限的痛点。
- **机制可解释性**：不仅提出了检测指标，还深入挖掘了其背后的机制（与复制头的关联），增强了方法的理论深度。
- **零样本能力**：通过利用模型固有的复制头排名，TOHA可退化为完全无标注的零样本方法，且依然保持强劲性能。

### 8. 不足与局限
- **模型覆盖局限**：实验仅限于开源中小规模模型（7B-13B），对于闭源商业模型或超大规模模型（如GPT-4, Claude）的有效性尚未验证，且“幻觉感知头”可能因架构而异。
- **模态局限**：当前框架仅适用于文本模态，尚未扩展到多模态（如视觉语言模型），跨模态注意力图的拓扑定义需重新设计。
- **对抗攻击风险**：论文在风险声明中承认，对抗性提示可能会人为篡改注意力模式，从而逃避TOHA的检测。
- **极短响应退化**：当模型响应极短（如单个词）时，响应图退化为单点，TOHA的性能会出现下降（尽管仍优于随机猜测）。

（完）
