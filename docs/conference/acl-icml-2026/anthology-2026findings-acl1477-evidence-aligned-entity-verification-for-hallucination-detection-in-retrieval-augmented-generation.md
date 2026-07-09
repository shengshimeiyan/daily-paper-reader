---
title: Evidence-Aligned Entity Verification for Hallucination Detection in Retrieval-Augmented Generation
title_zh: 检索增强生成中幻觉检测的证据对齐实体验证
authors: "Runsong Jia, Zhen Fang, Mengjia Wu, Jie Lu, Yi Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1477.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 检索增强生成中的幻觉检测
tldr: 现有幻觉检测方法依赖模型内部信号和预训练知识，存在知识过时和覆盖受限的问题，难以应对专业或最新信息。针对检索增强生成场景，本文提出一种证据对齐的实体验证方法，通过在推理时检索相关外部证据，将生成内容严格建立在超出模型参数知识的范围之上，有效克服了预训练知识的局限性，显著提升了幻觉检测的准确性与可靠性，具有极高的实用价值。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1477/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1636, \"height\": 621, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1477/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1641, \"height\": 802, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1477/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 797, \"height\": 431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1477/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 809, \"height\": 439, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1477/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1654, \"height\": 975, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1477/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1654, \"height\": 987, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1477/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1647, \"height\": 1657, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1477/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1644, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1477/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 838, \"height\": 311, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1477/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1643, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1477/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 752, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1477/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1149, \"height\": 264, \"label\": \"Table\"}]"
motivation: 现有幻觉检测方法依赖可能过时或覆盖受限的预训练知识，难以应对专业或最新信息。
method: 提出证据对齐的实体验证方法，利用检索增强生成中的外部证据对齐并验证生成内容。
result: 该方法有效克服了预训练知识的局限性，显著提升了RAG场景下的幻觉检测性能。
conclusion: 证据对齐的实体验证为RAG中的幻觉检测提供了一种有效且可靠的解决方案。
---

## Abstract
Hallucination detection is crucial for large language models (LLMs), as hallucinated content creates significant barriers in applications requiring factual accuracy. Current detection methods mainly depend on internal signals like uncertainty and self-consistency checks, using the model’s pre-trained knowledge to identify unreliable outputs. However, pre-trained knowledge may become outdated and has coverage limitations, especially for specialized or recent information. To address these limitations, retrieval-augmented generation (RAG) has emerged as a promising solution by retrieving relevant evidence at inference time, grounding outputs beyond the model’s parametric knowledge. In this paper, we target a critical and practical learning problem RAG-based hallucination detection (RHD), where RAG is employed to enhance hallucination detection by addressing information updating challenges. To address RHD, we propose a novel method Evidence-Aligned Entity Verification (EAEV), which detects entity-level hallucinations by leveraging RAG to align generated entities with retrieved evidence contexts. Specifically, EAEV evaluates entity-evidence alignment through three complementary dimensions and introduces counterfactual stability analysis to ensure robust alignments under evidence perturbations. Experiments across multiple RAG benchmarks demonstrate that EAEV achieves consistent improvements over existing methods with strong generalization capabilities.

---

## 论文详细总结（自动生成）

# 论文总结：检索增强生成中幻觉检测的证据对齐实体验证

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）在生成内容时容易产生幻觉。现有的幻觉检测方法主要依赖模型内部信号（如不确定性估计、自一致性检查），受限于模型预训练知识的覆盖范围和时效性，难以应对专业领域或最新信息的幻觉检测。
- **RAG场景的挑战**：虽然检索增强生成（RAG）通过引入外部证据缓解了知识滞后问题，但模型仍可能在检索到正确证据的情况下“捏造”实体。现有的RAG幻觉检测通常在句子或段落级别进行粗粒度判断，容易遗漏细粒度的实体错误，且容易受到表面关键词重叠造成的虚假关联欺骗。
- **整体含义**：本文针对RAG场景下的幻觉检测（RHD）问题，提出将检测粒度下沉至实体级别，通过生成实体与检索证据的严格对齐来实现细粒度、可追溯且抗干扰的幻觉检测。

## 2. 方法论：核心思想、关键技术细节与流程
- **核心思想**：提出**证据对齐实体验证（EAEV）**框架，将幻觉检测转化为实体与检索证据的多维度对齐任务，并引入反事实稳定性分析来剔除虚假关联，最后通过监督微调将验证信号转移给单一模型。
- **关键技术细节与流程**：
  1. **候选提及提取**：从生成的答案中提取实体提及，分为命名实体（ENT）、数值（NUM）和名词短语（NP）三类，并为每个提及检索证据窗口，选出主要证据 $e^*$。
  2. **多维度对齐评估**：从三个互补维度计算提及 $s$ 与证据 $e^*$ 的对齐度：
     - **身份对齐 ($Id$)**：基于精确子串匹配和模糊Token集合比率的字面相似度。
     - **语义对齐 ($Sem$)**：基于编码器嵌入的余弦相似度，捕捉释义和改写。
     - **一致性对齐 ($Con$)**：基于数值交集比和模式匹配的矛盾检测，评估数值一致性与事实冲突。
     - **类型自适应支持合成**：根据提及类型分配不同权重（如NUM更看重一致性，ENT更看重身份和语义），加权求和得到正向支持信号 $S_{pos}$，并结合矛盾指示器计算支持裕度 $SCM$。
  3. **反事实稳定性分析（CRS）**：为解决虚假关联问题，对证据施加四种扰动（留一法去除、标点与大小写归一化、空白压缩、仅保留字母数字）。计算扰动下的最低支持度 $CRS_{min}$ 和稳定性间隙 $CRS_\Delta$。真正的对齐在扰动下应保持稳健，而虚假匹配则会崩塌。
  4. **实体中心聚合**：将同一实体的多个提及信号聚合（正向支持取Top-K均值，负向冲突取最大值），结合一致性与稳定性计算最终的实体幻觉风险分数。
  5. **EAEV引导的监督学习**：利用上述计算的风险分数，在训练数据中对高风险实体添加 `<E>` 标签，通过令牌加权交叉熵损失微调骨干LLM，使其学会直接输出带有幻觉标记的答案。

## 3. 实验设计：数据集、Benchmark与对比方法
- **数据集**：
  - **RAGTruth**：包含QA、数据到文本、新闻摘要的通用RAG幻觉检测数据集。
  - **HotpotQA**：基于维基百科的多跳问答数据集，测试跨文档推理能力。
  - **DelucionQA**：基于汽车手册的领域特定QA数据集，测试精准技术领域检测。
- **评估指标**：AUROC、Accuracy、F1 Score（主要关注AUROC）。
- **对比方法**：对比了11种强基线，包括：
  - 传统内部信号方法：SelfCheckGPT, Semantic Entropy, LLM-Check, EarlyDetect, NoVo, Linear Probe, HaloScope。
  - RAG/证据验证方法：RAGAS, RefChecker, ReDEeP, TSV。

## 4. 资源与算力
- **硬件配置**：使用配备 **4张 NVIDIA A100 GPU** 的服务器进行实验。
- **效率对比**：与需要多次采样的SelfCheckGPT相比，EAEV速度快7.3倍，GPU显存占用更低（6578.7 MB vs 7735.4 MB），CPU内存占用也更低。

## 5. 实验数量与充分性
- **实验数量**：
  - 主实验：3个数据集 × 3个骨干模型（Qwen2.5-7B, LLaMA2-7B, LLaMA2-13B）= 9组对比。
  - 消融实验：移除身份/语义/一致性/稳定性4个变体在3个数据集上的对比。
  - 敏感性分析：5种不同窗口大小（20-40）的测试。
  - 附加实验：在新模型Qwen3-8B上的测试、实体级检测性能、资源成本对比、案例研究。
- **充分性与客观性**：实验设计非常充分且客观。涵盖了不同规模、不同架构的模型，以及通用、多跳推理和专业领域等不同特性的数据集；消融实验清晰拆解了各模块贡献；敏感性分析验证了超参的鲁棒性；且在较新的Qwen3-8B上也验证了泛化性。

## 6. 主要结论与发现
- **性能提升**：EAEV在所有设置下均取得一致提升，在LLaMA2-13B上达到87.89%的平均AUROC，比最强基线TSV高出3.34个百分点。
- **模型无关性**：实体级事实错误是RAG系统中与模型无关的挑战，EAEV在不同架构和规模的模型上均有效，且模型越大效果越好。
- **稳定性分析至关重要**：消融实验表明，反事实稳定性分析贡献最大，移除后AUROC平均下降5.52个点，证明区分真实证据支撑与虚假关联的必要性。
- **参数鲁棒性**：答案侧窗口大小在25-35 tokens内性能稳定，30 tokens为最优。

## 7. 优点
- **细粒度与可解释性**：将检测粒度从句子/段落级下沉至实体级，不仅能精确定位错误，还能提供明确的证据追溯路径。
- **抗虚假关联**：创新性地引入反事实稳定性分析，有效解决了RAG检测中因表面关键词重叠导致的误判问题。
- **高效易部署**：通过EAEV引导的监督微调，将复杂的对齐与稳定性计算转化为单次生成过程中的标签预测，避免了推理时的多模型协作或多次采样开销。

## 8. 不足与局限
- **依赖检索质量**：作为纯上下文验证框架，EAEV的性能上限受限于检索证据的质量和覆盖率，若检索缺失或错误，检测效果将大打折扣。
- **模型输出不稳定性**：LLM在复杂多步推理任务中的输出本身具有不稳定性，可能影响检测的一致性。
- **只检测不缓解**：本文仅聚焦于幻觉的“检测”，并未直接解决生成过程中的幻觉“缓解”问题，如何将实体级验证信号反馈至解码或训练阶段以抑制幻觉是未来的方向。

（完）
