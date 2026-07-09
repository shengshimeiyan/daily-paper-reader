---
title: "TPA: Next Token Probability Attribution for Detecting Hallucinations in RAG"
title_zh: TPA：用于检测检索增强生成中幻觉的下一词元概率归因
authors: "Pengqian Lu, Jie Lu, Anjin Liu, Guangquan Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1159.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 检测检索增强生成中的幻觉
tldr: 现有检索增强生成中的幻觉检测方法通常将幻觉简单归因于模型内部知识与检索上下文之间的二元冲突，忽略了LLM其他组件对生成结果的影响。本文提出TPA方法，将每个词元的生成概率数学地归因于查询、RAG上下文、过去词元、自身词元、FFN等七个不同来源，量化各来源对幻觉的具体贡献，从而更全面地捕捉和检测幻觉，提升了检测效果。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1159/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 791, \"height\": 577, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1159/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 806, \"height\": 296, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1159/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1646, \"height\": 1294, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1159/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1159/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1648, \"height\": 632, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1159/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1646, \"height\": 631, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1159/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 773, \"height\": 199, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1159/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 806, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1159/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1675, \"height\": 1239, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1159/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1159/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 747, \"height\": 417, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1159/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 753, \"height\": 450, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1159/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1626, \"height\": 1983, \"label\": \"Table\"}]"
motivation: 现有RAG幻觉检测方法仅关注内部知识与检索上下文的二元冲突，忽略了LLM其他组件的影响。
method: 提出TPA方法，将每个词元的概率数学地归因于查询、上下文、过去词元等七个不同来源以量化其对幻觉的贡献。
result: 实验证明TPA能有效量化各来源对幻觉的贡献，提升了RAG场景下的幻觉检测性能。
conclusion: TPA通过全面归因词元概率来源，为RAG中的幻觉检测提供了更完整的视角和有效工具。
---

## Abstract
Detecting hallucinations in Retrieval-Augmented Generation remains a challenge. Prior approaches attribute hallucinations to a binary conflict between internal knowledge stored in FFNs and the retrieved context. However, this perspective is incomplete, failing to account for the impact of other components of the LLM, such as the user query, previously generated tokens, the self token, and the final LayerNorm adjustment. To comprehensively capture the impact of these components on hallucination detection, we propose TPA which mathematically attributes each token’s probability to seven distinct sources: Query, RAG Context, Past Token, Self Token, FFN, Final LayerNorm, and Initial Embedding. This attribution quantifies how each source contributes to the generation of the next token. Specifically, we aggregate these attribution scores by Part-of-Speech (POS) tags to quantify the contribution of each model component to the generation of specific linguistic categories within a response. By leveraging these patterns, such as detecting anomalies where Nouns rely heavily on LayerNorm, TPA effectively identifies hallucinated responses. Extensive experiments show that TPA achieves state-of-the-art performance.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：在检索增强生成（RAG）系统中，大语言模型（LLM）仍会产生幻觉（即生成与检索上下文不一致的内容）。现有的幻觉检测方法通常将幻觉简单归因于模型内部参数知识（存储在FFN中）与检索外部上下文（RAG）之间的二元冲突，这种视角是不完整的。
- **研究动机**：除了FFN和RAG，LLM的其他组件（如用户查询Query、已生成的过去词元Past Token、自身词元Self Token、最终层归一化Final LayerNorm等）同样对生成结果有重要影响，但被现有研究忽视。例如，模型对虚词和命名实体依赖不同来源的机制不同，不加区分的检测会导致误判。
- **整体含义**：本文主张必须从LLM完整的内部生成机制出发，全面分解各个组件对最终词元概率的贡献，并结合语法先验（如词性）来精准识别幻觉模式，从而提升高 stakes 应用（如临床、法律）中的可靠性。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出 TPA（Next Token Probability Attribution）框架，将每个生成词元的最终概率数学地精确归因于七个不同的来源，并结合词性（POS）标签进行聚合，以此作为特征来检测幻觉。
- **关键技术细节与流程**：
  1. **粗粒度分解**：
     - 定义探针函数 $\Phi(h, y)$，利用反嵌入矩阵直接从中间残差流状态读取目标词元 $y$ 的概率。
     - 将最终概率分解为：初始嵌入贡献 $\Delta P_{initial}$、最终LayerNorm贡献 $\Delta P_{LN}$，以及各层注意力 $\Delta P_{att}^{(l)}$ 和FFN贡献 $\Delta P_{ffn}^{(l)}$。
     - **定理1**证明了这些贡献的加和严格等于模型的最终输出概率 $P_{final}(y)$。
  2. **细粒度归因**：
     - **挑战**：Softmax的非线性导致无法直接对注意力头进行概率加和分解。
     - **Logit分配**：转向Logit空间，计算每个注意力头对目标词元Logit的贡献 $\Delta z_{h,y}$，然后按 $\exp(\Delta z_{h,y})$ 的比例将 $\Delta P_{att}^{(l)}$ 分配给各个头（公式11），保证守恒且数值稳定。
     - **来源映射**：利用注意力权重，将每个头的贡献进一步映射到四个输入来源：Query、RAG、Past、Self。至此，形成7个归因来源（加上Initial、FFN、LN）。
  3. **语法感知特征工程**：
     - **标签传播**：解决子词切分与整词不匹配的问题，子词继承其所属整词的词性标签。
     - **聚合**：对每个词性类别（如NOUN, VERB等18种），计算其包含词元的7维归因向量的平均值，拼接形成 $7 \times 18 = 126$ 维的最终特征向量，用于下游分类器。

### 3. 实验设计：数据集、Benchmark与对比方法
- **数据集**：RAGTruth 和 Dolly (AC)。
- **Benchmark与评估指标**：将幻觉检测视为二分类任务，评估指标为 AUC、Recall 和 F1 Score。
- **对比方法**：涵盖了三大类代表性基线方法：
  1. **不确定性与代理指标**：EigenScore, SEP, SelfCheckGPT, Perplexity, Energy 等。
  2. **基于LLM的评估**：ChainPoll, RAGAS, Trulens, RefCheck 等。
  3. **探测内部激活**：ReDeEP, ITI, TSV, Novo 等。

### 4. 资源与算力
- **硬件配置**：单张 NVIDIA A100 (40GB) GPU，200GB 内存。
- **计算开销**：
  - 特征提取阶段：每个响应平均耗时约20秒；每个LLM在每个数据集上的总特征提取成本约为 17 GPU小时。
  - 分类器推理阶段：每个响应耗时不到1秒。
- **实现备注**：由于显存限制，实际采用顺序前缀重放（逐词元）而非完全并行的Teacher-forced pass，但数学上严格等价。

### 5. 实验数量与充分性
- **实验规模**：在5个不同架构和参数规模的LLM（Llama2-7B/13B, Llama3-8B, Mistral-7B, Qwen3-8B）和2个数据集上进行了全面评测。
- **消融实验**：验证了7个归因来源的必要性（如移除LN导致Llama3-8B上F1下降5.83%）以及POS聚合策略的有效性（对比TPA-Mean和TPA-Stat，TPA-POS在所有7项设置中胜出）。
- **充分性与公平性**：
  - 实验设计非常严谨，针对不同数据集规模采用了不同的交叉验证策略（标准划分、20折CV、嵌套留一法CV）。
  - 使用5个随机种子进行集成评估，并报告了统计显著性检验（p < 0.05）。
  - 评估客观公平，不仅对比了多种SOTA，还通过SHAP分析提供了可解释性验证。

### 6. 论文的主要结论与发现
- **性能提升**：TPA在多种架构上达到了SOTA性能，特别是在Mistral-7B上F1比最强基线高出7%。
- **超越二元冲突**：幻觉的根源不仅是FFN与RAG的冲突，Final LayerNorm和Query等组件的贡献同样是关键的幻觉信号（如LN对数字词元的高贡献暗示幻觉）。
- **模型特异性**：幻觉指纹因模型架构而异。例如，LN对NUM的高贡献在Llama2-7B中是强烈的幻觉信号，但在Llama2-13B中模式却相反（与事实性正相关），说明大模型可能以不同方式使用LayerNorm，必须采用可学习的检测器而非静态启发式规则。
- **语法感知的必要性**：不同模型对信息的依赖体现在不同的词性结构上（如Llama2依赖名词NOUN，Llama3依赖介词ADP），POS聚合能有效捕捉这些模式。

### 7. 优点
- **理论严谨**：基于残差流的加性性质，数学证明了概率分解的完备性（定理1），并巧妙利用Logit空间分配解决了Softmax非线性带来的归因难题。
- **视角全面**：打破了以往FFN-RAG二元对立的局限，将归因扩展到7个来源，揭示了LayerNorm等被忽视组件的检测价值。
- **特征工程巧妙**：引入词性（POS）聚合，将底层归因分数与高层语法功能结合，有效区分了良性的语法依赖（如虚词靠FFN）和恶性的实体幻觉（如名词靠FFN/LN）。
- **可解释性强**：结合SHAP分析，不仅给出了检测结果，还清晰展示了模型产生幻觉的内部机制和不同架构间的行为差异。

### 8. 不足与局限
- **白盒依赖**：方法需要访问模型的内部状态（隐藏层、注意力矩阵、FFN输出等），无法应用于闭源商业API模型。
- **计算开销较大**：相较于简单的标量探测或不确定性指标，TPA的特征提取过程（需逐层探针和注意力映射）计算复杂度较高，耗时较长。
- **外部工具依赖**：特征工程依赖于外部词性标注器，对于代码生成等专业领域或非英语场景，标准语法标签可能不适用，泛化能力受限。

（完）
