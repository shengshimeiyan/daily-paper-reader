---
title: "Context-Fidelity Boosting: Enhancing Faithful Generation through Watermark-Inspired Decoding"
title_zh: 上下文忠实度提升：通过受水印启发的解码增强忠实生成
authors: "Weixu Zhang, Fanghua Ye, Qiang Gao, Jian Li, Haolun Wu, Yuxing Tian, Sijing Duan, Nan Du, Xiaolong Li"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.2121.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 通过解码时框架减少忠实性幻觉
tldr: 针对大语言模型生成内容与输入上下文矛盾或忽略的忠实性幻觉问题，提出了一种轻量级的解码时框架Context-Fidelity Boosting。该框架受水印技术中的logit调整原理启发，通过提升与上下文相关词元的生成概率来减少幻觉，包含静态、上下文感知和词元感知三种递进策略。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2121/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 811, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2121/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1502, \"height\": 786, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2121/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1606, \"height\": 601, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2121/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1624, \"height\": 784, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2121/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1649, \"height\": 910, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2121/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1653, \"height\": 798, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2121/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 195, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2121/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2121/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1603, \"height\": 133, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2121/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1650, \"height\": 596, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2121/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 813, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2121/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 819, \"height\": 252, \"label\": \"Table\"}]"
motivation: 大语言模型常生成与输入上下文矛盾或忽略信息的忠实性幻觉内容，影响生成可靠性。
method: 提出Context-Fidelity Boosting框架，利用受水印启发的logit调整，提升上下文相关词元的生成概率。
result: 通过静态、上下文感知和词元感知三种策略，有效减少了模型生成中的忠实性幻觉。
conclusion: 解码时的logit调整策略能够有效提升生成内容的上下文忠实度，缓解幻觉问题。
---

## Abstract
Large language models (LLMs) often produce content that contradicts or overlooks information provided in the input context, a phenomenon known as faithfulness hallucination. In this paper, we propose Context-Fidelity Boosting (CFB), a lightweight and general decoding-time framework that effectively reduces such hallucinations by boosting the generation probability of context-relevant tokens. Motivated by logit-shaping principles in watermarking techniques, CFB leverages token-level logit adjustments based on their presence or salience in the input context. Specifically, we develop three boosting strategies, static, context-aware, and token-aware that progressively incorporate distributional divergence, attention scores, and semantic similarity. Notably, CFB requires no retraining or architectural changes, making it compatible with a wide range of LLMs. Experiments on summarization and question answering tasks across multiple open-source LLMs show that CFB consistently improves faithfulness metrics, with minimal generation overhead. Our implementation is fully open-sourced.

---

## 论文详细总结（自动生成）

# 论文总结：Context-Fidelity Boosting: Enhancing Faithful Generation through Watermark-Inspired Decoding

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）在生成过程中常出现“忠实性幻觉”，即生成内容与输入上下文矛盾或忽略上下文信息。这与事实性幻觉（违背客观事实）不同，忠实性幻觉特指模型在上下文给定的情况下，仍依赖其内部参数记忆生成冲突内容。
- **研究动机**：在RAG、摘要、问答等场景中，模型必须严格遵循外部证据。当外部证据与模型参数知识冲突时，模型往往倾向于生成流畅但偏离上下文的内容。现有的缓解方法（如微调、提示工程、对比解码）存在计算成本高、跨任务不一致或在忠实度与流畅度之间难以平衡的问题。
- **整体含义**：本文提出一种轻量级、无需重训练的解码时干预框架，旨在通过调整词元生成概率，在不损害生成流畅度的前提下，强制模型“忠实”于输入上下文。

## 2. 方法论：核心思想、关键技术细节与算法流程
- **核心思想**：受文本水印技术中“Logit塑形”机制的启发，CFB在解码时对受上下文支持的词元添加正向偏置，提升其生成概率，从而引导模型输出与上下文对齐。
- **关键技术细节与公式**：CFB设计了由粗到细的三级提升策略：
  1. **静态提升**：对所有在上下文源跨度中出现的词元 $w \in V_S$ 添加固定偏置 $\Delta_t(w) = \delta$。该方法简单但缺乏自适应性。
  2. **上下文感知提升**：根据上下文对模型预测分布的影响程度动态调整偏置。计算有上下文和无上下文时预测分布的JS散度 $D = JSD(P_w \| P_{wo})$，偏置公式为 $\Delta_t(w) = \delta_{min} + (\delta_{max} - \delta_{min}) \cdot D$。散度越大，说明上下文影响越强，提升力度越大。
  3. **词元感知提升**：在样本级自适应偏置的基础上，进一步在词元级别重新分配偏置。结合源位置注意力得分 $\alpha_t(w)$ 和源范围语义相似度 $s(w)$ 计算词元相关性 $r_t(w) = \lambda_1 \alpha_t(w) + \lambda_2 s(w)$。归一化后 $\hat{r}_t(w)$，最终偏置为 $\Delta_t(w) = \delta(D) \cdot \hat{r}_t(w)$。
- **算法流程**：
  1. 从输入提示中解析出源跨度，提取受支持的词元集合；
  2. 预计算词元的语义相似度得分；
  3. 在每步解码时，计算上下文感知的自适应偏置基数 $\delta(D)$；
  4. 获取当前步对源位置的注意力得分，结合语义相似度计算词元级权重；
  5. 对原始logits加上对应的偏置值，通过Softmax采样生成下一个词元。

## 3. 实验设计：数据集、Benchmark与对比方法
- **数据集与场景**：
  - **摘要生成**：CNN/DM 和 XSum，评估模型在生成摘要时对源文档的忠实度。
  - **问答（QA）**：NQ-Synth（上下文与参数知识互补）和 NQ-SWAP（上下文与参数知识冲突），评估模型在知识冲突/互补场景下的表现。
- **评估指标**：
  - 摘要：ROUGE-L（质量）、FactKB（事实一致性）、BERT-P（语义保留）。
  - 问答：上述指标 + 准确率。
  - 辅助评估：人工评估（忠实度、流畅度、信息量）及 GPT-4o 评估（一致性、幻觉数、矛盾率）。
- **对比方法**：
  - **CAD** (Context-Aware Decoding)：固定超参调整输出概率。
  - **AdaCAD**：基于JSD动态推断调整力度。
  - **COIECD**：基于上下文信息熵约束的解码。
- **基座模型**：Mistral-7B-Instruct, Llama2-13B-chat-hf, Llama3-8B-Instruct。

## 4. 资源与算力
- **算力说明**：论文**未明确说明**所使用的GPU型号和数量（由于是解码时方法，无需训练，因此无训练时长）。
- **效率测算**：文中通过FLOPS和单样本运行时间评估了计算开销。在单GPU、Batch Size为1的设定下，静态和上下文感知CFB的额外FLOPS不到基座模型的0.003%，单样本耗时约1.3-2.0秒；词元感知CFB因需逐步计算注意力，耗时约9-10秒/样本，但仍轻于COIECD。

## 5. 实验数量与充分性
- **实验数量**：
  - 主实验：3个模型 × 4个数据集 × 3种CFB变体及3个基线方法。
  - 消融实验：针对词元感知CFB的三个核心组件（注意力、语义、JSD）进行逐一移除测试。
  - 参数敏感性分析：对偏置值 $\delta$ 和权重 $\lambda_1, \lambda_2$ 进行了扫描。
  - 人工与LLM评估：抽取200个样本进行多维评价。
  - 补充实验：在HotpotQA和TriviaQA上测试推理任务边界。
- **充分性与客观性**：实验设计非常充分且客观。不仅涵盖了不同规模和架构的模型，还特别区分了“知识冲突”与“知识互补”两种截然不同的场景，揭示了方法的适用边界；消融实验清晰验证了各组件的贡献；同时引入人工和GPT-4o评估弥补了自动指标的不足。

## 6. 论文的主要结论与发现
- CFB框架能有效提升生成内容的上下文忠实度，尤其在摘要任务和知识互补型QA（NQ-Synth）中表现优异，词元感知变体在准确率上达到最佳。
- 在知识强冲突场景（NQ-SWAP）下，CFB表现不如强对比抑制方法（如AdaCAD），说明CFB更擅长“增强”上下文信号，而非在强冲突下“抑制”参数记忆。
- 消融实验发现，语义相似度组件对词元感知CFB至关重要，移除后性能急剧下降；注意力机制贡献有限；JSD的自适应缩放不可或缺。
- 适中的偏置值 $\delta$ 效果最好，过大反而损害性能。

## 7. 优点
- **即插即用与轻量级**：无需重训练或修改模型架构，兼容各类开源LLM，推理开销极小（尤其是静态和上下文感知变体）。
- **新颖的跨域启发**：巧妙地将水印技术中的Logit塑形思想迁移至忠实性幻觉缓解问题，提供了新的解题视角。
- **精细的层次化设计**：提供静态、上下文感知、词元感知三级策略，允许用户在计算效率与控制粒度之间灵活权衡。
- **评估严谨**：结合了自动指标、人工标注与LLM评判，且对冲突/互补场景进行了细致的拆解分析。

## 8. 不足与局限
- **白盒依赖**：方法需要访问模型的logits、注意力权重和词元嵌入，无法应用于黑盒API场景。
- **高冲突场景局限**：在上下文与参数知识直接冲突时，CFB的“加法”提升策略不如对比解码的“减法”抑制策略有效。
- **词元感知变体的开销**：虽然整体轻量，但词元感知变体因逐步计算注意力，耗时显著增加（约5-7倍），限制了其在极低延迟场景的应用。
- **依赖局部相关性估计质量**：词元感知变体的表现高度依赖于注意力得分和语义相似度计算的准确性，若这些信号噪声较大，可能影响效果。

（完）
