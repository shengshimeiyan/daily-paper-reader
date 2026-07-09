---
title: "CoDA: Restoring Contextual Dominance via Copy-Encouraged Attention Intervention for Mitigating RAG Hallucinations"
title_zh: CoDA：通过复制鼓励的注意力干预恢复上下文主导以缓解RAG幻觉
authors: "JinWei Shi, Qizhuo Xie, Qianzi Hou, Zhipeng Wang, Wanting Su, Jianhua Zhao, Tao Zheng, Tieke He"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.576.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 通过注意力干预缓解RAG幻觉
tldr: 针对检索增强生成中即使检索上下文准确充分仍因内部参数知识压倒外部上下文而产生幻觉的问题，提出CoDA方法。该方法通过注意力中心分析发现幻觉源于中后Transformer层上下文选择路由减弱，进而通过复制鼓励的注意力干预恢复上下文主导地位。实验证明CoDA能有效纠正参数知识的主导影响，缓解RAG幻觉，提升生成事实一致性。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.576/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 807, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.576/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1710, \"height\": 981, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.576/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.576/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1419, \"height\": 702, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.576/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1657, \"height\": 822, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.576/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 769, \"height\": 736, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.576/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 767, \"height\": 454, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.576/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 811, \"height\": 413, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.576/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 835, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.576/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 562, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.576/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 772, \"height\": 283, \"label\": \"Table\"}]"
motivation: 在RAG中，即使检索上下文准确，内部参数知识仍可能压倒外部上下文导致幻觉。
method: 提出CoDA方法，通过复制鼓励的注意力干预增强中后层的上下文选择路由，恢复外部上下文的主导地位。
result: CoDA有效纠正了参数知识对上下文的压倒性影响，显著缓解了RAG系统中的幻觉现象。
conclusion: 恢复上下文选择路由的主导地位是缓解检索增强生成中幻觉的有效途径。
---

## Abstract
Retrieval-augmented generation reduces hallucination by grounding model outputs in external evidence, yet hallucinations can still occur even when the retrieved context is accurate and sufficient. From the perspective of information routing in the residual stream, this reflects an imbalance where internal parametric knowledge overwhelms external context during generation. We present an attention-centric analysis of RAG hallucination under valid evidence, showing that hallucinated and factual tokens diverge in mid-to-late Transformer layers as context-selective attention routing weakens, allowing parametric influence to dominate the residual stream. Motivated by prior studies showing that some attention heads—often referred to as copying heads—exhibit stronger information transport capacity, we aim to extend similar evidence-carrying behavior to a broader set of attention heads. To this end, we introduce CoDA, a lightweight inference-time attention intervention that amplifies evidence-aligned value states, enabling more attention heads to transport reliable external evidence in a copy-encouraged manner. Experiments demonstrate that CoDA improves contextual faithfulness, reduces hallucination, and remains robust under long and noisy contexts with modest and stable inference overhead.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：在检索增强生成（RAG）中，即使检索到的外部上下文准确且充分，大模型仍可能产生与上下文矛盾的幻觉（即RAG幻觉）。
- **整体含义**：从残差流的信息路由视角看，这种幻觉并非源于检索失败，而是由于模型内部的参数知识在生成过程中压倒了外部上下文，导致上下文选择性注意力路由失效。这揭示了Transformer架构在融合内外部知识时的内在缺陷。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：受“复制头”（copying heads，即能高保真传输上下文信息的注意力头）启发，CoDA旨在将这种复制行为扩展到更广泛的非复制头中，通过在推理时对注意力机制进行轻量级干预，放大与证据对齐的Value状态，从而恢复外部上下文在残差流中的主导地位。
- **关键技术细节与流程**：
  1. **知识贡献量化**：
     - **外部上下文分数（ES）**：计算生成Token的最终隐藏状态与其注意力权重最高的Top-k上下文Token隐藏状态之间的余弦相似度，衡量上下文路由的有效性。
     - **参数知识分数（PS）**：计算FFN前后隐藏状态映射到词汇分布的Jensen-Shannon散度（JSD），衡量FFN注入的参数影响。
     - **累积比率（CR）**：归一化PS与(PS+ES)之和的比值，追踪参数主导地位随层数的累积情况。
  2. **幻觉易发层定位**：
     - 结合激活强度（$A_l$，即CR的平均绝对值）和发散强度（$\Delta_l$，即幻觉Token与事实Token的CR差异），计算幻觉敏感度（$H_l = A_l \times \Delta_l$）。
     - 选取$H_l$最高的Top-k层作为干预目标集合$R$。
  3. **复制鼓励的注意力调制**：
     - 在目标层$l \in R$中，选取平均注意力最高的Top-K上下文Token的Value向量作为“上下文锚点”。
     - 计算每个Token的Value向量与锚点的语义一致性得分$S$，并进行Min-Max归一化。
     - 通过中心化Sigmoid变换计算自适应剂量因子$w$，公式逻辑为：当语义一致性高时$w$增大（放大），低时$w$减小（抑制），同时设定最小权重$\alpha$保证不归零。
     - 将原始注意力权重乘以$w$，实现对外部证据对齐状态的放大，鼓励非复制头执行复制行为。

### 3. 实验设计：数据集、Benchmark与对比方法
- **数据集**：
  - **幻觉基准**：RAGTruth、Dolly (AC)。
  - **上下文忠实度基准**：CoFaithfulQA的6个子集（HotpotQA, NewsQA, NQ, SearchQA, SQuAD, TriviaQA）。
- **评估指标**：
  - Context Recall (ConR，越高越好)、Memory Recall (MemR，越低越好)、Misalignment Rate (MR，越低越好)。
  - GPT-4o成对比较胜率。
- **对比方法**：
  - 提示工程：AttrPrompt, OIPrompt。
  - 解码策略：COIECD。
  - 微调与对齐：SFT, KAFT, C-DPO, DDR。
  - 机制干预：ParamMute, ReDeEP。

### 4. 资源与算力
- **算力说明**：论文**未明确说明**所使用的GPU型号、数量或训练时长。由于CoDA是纯推理时的干预方法，无需训练，因此无训练算力消耗；论文仅报告了端到端的推理延迟时间（秒）和开销比例。

### 5. 实验数量与充分性
- **实验数量**：
  - 在8个数据集/子集上进行了忠实度与幻觉缓解评估。
  - 进行了层级行为轨迹分析（幻觉与事实Token的CR轨迹对比）。
  - 进行了长上下文和噪声鲁棒性测试（不同长度与噪声比例下的ConR下降对比）。
  - 进行了推理延迟效率测试。
- **充分性与客观性**：实验设计非常充分且客观。不仅涵盖了多种领域和长度的QA数据集，对比了不同范式（提示、解码、微调、干预）的基线方法，还针对RAG实际场景中的噪声和长度干扰进行了专门测试，并严格区分了上下文依赖（ConR）和参数记忆依赖（MemR），评估维度全面公平。

### 6. 论文的主要结论与发现
- **幻觉形成机制**：RAG幻觉在Transformer的中后期层形成，此时上下文选择性注意力路由减弱，参数影响主导了残差流。
- **CoDA的有效性**：通过在幻觉易发层放大与证据对齐的Value状态，CoDA能有效恢复上下文主导，显著提升ConR并降低幻觉，在GPT-4o评判中胜率显著优于ReDeEP。
- **鲁棒性与效率**：CoDA在长文本和噪声环境下表现稳健（ConR下降最小），且推理开销稳定在15%-17%左右，不随上下文长度增加而剧增。

### 7. 优点
- **机制解释性强**：从残差流和注意力路由的微观视角重新定义了RAG幻觉，而非仅停留在输入输出层面。
- **即插即用且轻量**：无需修改模型参数或重新训练，仅在推理时对特定层进行干预，工程落地成本低。
- **干预策略合理**：不同于全局抑制FFN（如ParamMute），CoDA通过增强上下文锚点来“疏导”而非“堵截”参数知识，保留了模型的表示灵活性。

### 8. 不足与局限
- **模型架构覆盖有限**：实验仅在Llama系列模型上进行验证，未扩展到其他架构（如GPT、Mistral等）。
- **推理开销存在**：虽然开销稳定在15%-17%，但对于延迟极度敏感的严格在线应用仍可能构成瓶颈。
- **超参数设置简单**：锚点选择和剂量强度的设定采用了简单的默认值，在复杂检索条件下的自适应性有待提升。
- **无法纠正错误上下文**：CoDA仅增强对上下文的忠实度，若检索到的上下文本身具有误导性或不完整，模型仍会生成错误内容（甚至更坚信错误上下文）。

（完）
