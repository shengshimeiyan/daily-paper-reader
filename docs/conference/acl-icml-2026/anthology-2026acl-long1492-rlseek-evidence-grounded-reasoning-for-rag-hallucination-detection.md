---
title: "RLSeek: Evidence-Grounded Reasoning for RAG Hallucination Detection"
title_zh: RLSeek：面向RAG幻觉检测的证据接地推理
authors: "Zhaoheng Huang, Dacheng Wen, Yutao Zhu (朱余韬), Xiaoying Lian, Yushi Liang, Kai Hao, Nan Li, Liangjie Zhang, Qi Zhang, Ji-Rong Wen, Zhicheng Dou (窦志成), Fangzhao Wu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1492.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 基于证据接地推理的RAG幻觉检测
tldr: 针对检索增强生成系统中基于推理的幻觉检测器常因思维链过程缺乏源证据显式接地而导致预测错误的问题，提出RLSeek框架。该框架利用强化学习训练跨度级幻觉检测器，促使思维链验证步骤明确引用和验证检索文档中的声明，从而对齐人类验证实践。实验表明，显式证据接地的推理过程显著减少了错误预测，提升了RAG幻觉检测的准确性和整体可靠性。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 807, \"height\": 770, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1647, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1571, \"height\": 438, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 762, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 390, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1642, \"height\": 967, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 799, \"height\": 1095, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 799, \"height\": 1156, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 802, \"height\": 1124, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 784, \"height\": 1173, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 787, \"height\": 394, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 787, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 798, \"height\": 402, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1492/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 795, \"height\": 404, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1492/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 736, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1492/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 782, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1492/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1572, \"height\": 917, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1492/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 813, \"height\": 432, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1492/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1240, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1492/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 658, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1492/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 697, \"height\": 176, \"label\": \"Table\"}]"
motivation: 现有基于推理的RAG幻觉检测器常因思维链未显式引用源证据而导致预测错误。
method: 提出RLSeek框架，利用强化学习训练检测器，使其在思维链验证步骤中显式引用和验证检索文档。
result: 显式证据接地的推理过程显著减少了错误预测，提升了RAG幻觉检测的性能。
conclusion: 强制思维链显式接地于源证据是提升检索增强生成系统幻觉检测有效性的关键。
---

## Abstract
Large language models (LLMs) in retrieval-augmented generation systems can still produce hallucinations, generating content that is unsupported or contradicted by the source texts and undermines reliability. Recent work addressed this problem by training span-level hallucination detectors using reinforcement learning (RL) and chain-of-thought (CoT) reasoning. In this work, we show through error analysis that incorrect predictions by existing reasoning-based detectors are strongly associated with CoT processes that lack explicit grounding in source evidence, particularly when verification steps do not quote or verify claims against the retrieved documents. This behaviour contrasts with human verification practices in benchmarks such as RAGTruth, where evidence quotation is a prerequisite for determining hallucinated spans. Motivated by this observation, we propose an evidence-grounded RL framework, namely RLSeek, to explicitly enforce active evidence seeking during CoT reasoning by requiring quotation of relevant source segments at each verification step. Experiments on the RAGTruth and NewsSum dataset demonstrate consistent improvements in hallucination span detection performance, with limited additional reasoning overhead and improved robustness in out-of-domain settings.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：检索增强生成（RAG）系统中的大语言模型仍会产生幻觉（生成不支持或 contradicted 源文本的内容）。现有的基于强化学习（RL）和思维链推理的细粒度幻觉跨度检测器存在预测错误的问题。
- **研究动机**：通过对现有推理检测器的错误分析发现，**预测错误与思维链过程中缺乏源证据的显式接地高度相关**。模型在验证步骤中往往不引用源文档就得出结论，这与人类标注实践（如RAGTruth基准要求必须引用证据才能判定幻觉）形成鲜明对比。
- **整体含义**：为了提升RAG幻觉检测的准确性和可靠性，必须从过程层面干预模型的推理行为，强制模型在推理的每一步都主动寻找并引用源文本证据，使推理过程对齐人类的验证标准。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出 **RLSeek** 框架，一种证据接地的强化学习框架。在CoT推理的每个验证步骤中，强制要求模型主动寻找并引用源文本中最相关的片段，并基于引用内容判定幻觉跨度。
- **关键技术细节**：
  - **证据寻找推理**：修改CoT指令，要求模型在验证某部分是否幻觉时，必须先从源文档中定位并原封不动地引用最相关、最精确的证据，放入 `<quote>...</quote>` 标签中，然后再解释该证据如何支持评估。
  - **引用忠实度测量**：评估模型是否忠实地引用了原文，而非改写或概括。
    - **无效引用集**：若某步骤未引用证据或引用为空，则视为无效。
    - **有效引用集**：格式合规但需测量词汇对齐度。使用**最长公共子串（LCS）**计算引用片段与源文本的归一化重叠度 $LCS(Q_i, D)/|Q_i|$。LCS轻量级且无需模型，能直接衡量词汇重叠。
  - **证据接地的策略优化**：将引用忠实度转化为RL的惩罚项，构建复合奖励函数：
    - $r_{final} = r_{span} - r_{penalty}$
    - 其中 $r_{span}$ 是标准的跨度级F1结果奖励；$r_{penalty}$ 是过程级惩罚：
      - 若存在无效引用集，给予固定惩罚（0.5）。
      - 若为有效引用集，惩罚值为所有引用片段中未匹配内容比例的平均值 $\frac{1}{|Q|}\sum [1 - LCS(Q_i, D)/|Q_i|]$。
    - 使用GRPO（Group Relative Policy Optimization）算法基于 $r_{final}$ 计算优势函数进行策略优化。

### 3. 实验设计：数据集、Benchmark与对比方法
- **数据集/场景**：
  - **RAGTruth**：涵盖三个代表性任务（摘要生成、问答QA、数据到文本生成Data-to-Text）。
  - **NewsSum**：一个专有的新闻摘要数据集（包含多篇源新闻和带幻觉跨度标注的摘要）。
- **评估指标**：
  - 跨度级检测：数据集级别的 Span-F1（主要指标）。
  - 样本级检测：二分类的 Precision, Recall, F1。
- **对比方法**：
  - **微调模型**：SFT-7B, SFT-14B, MVA-7B（基于注意力特征）。
  - **推理模型**：Qwen3-14B, GPT-5-mini, GPT-5, o3，测试了标准CoT和CoT+Seek（仅提示引用）。
  - **基于RL的模型**：RL4HS-GRPO, RL4HS-CAPO（最相关的SOTA基线）。

### 4. 资源与算力
- **算力资源**：实验在 **8张 NVIDIA A100 GPU** 上进行。
- **训练配置**：Batch size为64，训练3个epoch。7B模型学习率为 $1 \times 10^{-6}$，14B模型为 $5 \times 10^{-7}$。

### 5. 实验数量与充分性
- **实验数量**：
  - 主实验：4个数据集/任务场景 × 多种基线对比（表1, 2, 3）。
  - 消融实验：移除惩罚项、结合CAPO、移除RL、移除Seek等5组对比（表4）。
  - 分析实验：引用行为分析（CoT长度与引用数量）、OOD泛化测试（留一法）、错误率分析（FNR/FPR）、惩罚项影响分析、引用多样性与相关性分析、案例研究。
- **充分性与客观性**：实验设计非常充分且客观。不仅涵盖了多种任务场景和主流大模型，还从结果指标、推理过程行为、OOD泛化等多个维度进行了深入分析；消融实验清晰剥离了RL优化和引用惩罚各自的贡献；使用LCS和LLM-as-a-judge客观评估了推理过程的质量，避免了仅看结果指标的片面性。

### 6. 论文的主要结论与发现
- **显式引用提升性能**：在CoT中强制引用证据能持续提升跨度级检测性能，但仅靠提示词不够，必须结合RL优化。
- **更好的精确率-召回率权衡**：相比CAPO通过抑制非幻觉样本优势来平衡，RLSeek通过强制证据引用，在训练中实现了精确率和召回率的同步稳定提升。
- **惩罚项至关重要**：没有惩罚项，模型倾向于改写而非逐字引用（词汇重叠度降至约55%），导致性能增益有限；加入惩罚后有效引用率和重叠度接近100%。
- **推理开销有限且防作弊**：训练初期CoT变长，但随训练推进，引用变得简洁结构化，总CoT长度与基线相当。模型没有通过重复引用长文本来作弊，而是分布在不同片段且保持高相关性。
- **OOD鲁棒性增强**：在跨域设置下，RLSeek优于CAPO，表明证据接地使模型依赖寻证策略而非特定域的模式。

### 7. 优点
- **洞察深刻**：精准定位了现有RL+CoT检测器失败的原因——推理过程缺乏证据接地，将模型行为与人类标注标准对齐。
- **奖励设计巧妙**：基于LCS的引用忠实度惩罚项轻量、无需额外模型，且有效解决了RL优化中模型“敷衍了事”（改写、不引用）的reward hacking问题。
- **分析全面深入**：不仅报告了F1分数，还深入剖析了CoT长度演变、引用多样性、相关性，有力证明了模型确实学到了“寻证”能力而非过拟合。

### 8. 不足与局限
- **依赖高质量标注**：训练跨度级检测器依赖昂贵的细粒度跨度标注，限制了数据规模。作者也指出未来需探索用强模型合成轨迹。
- **静态检索假设**：假设源文档是固定提供的，未考虑检索器质量对检测的影响，也未涉及动态调用工具的Agent场景。
- **词汇重叠的局限性**：LCS衡量引用忠实度虽然高效，但可能对合理的语法调整或同义词替换施加了不必要的惩罚，无法捕捉深层语义的完全等价。

（完）
