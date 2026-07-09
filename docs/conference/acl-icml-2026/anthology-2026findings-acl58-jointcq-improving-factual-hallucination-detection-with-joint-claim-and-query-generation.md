---
title: "JointCQ: Improving Factual Hallucination Detection with Joint Claim and Query Generation"
title_zh: JointCQ：通过联合声明和查询生成改进事实幻觉检测
authors: "Fan Xu (徐凡), Huixuan Zhang, Zhenliang Zhang, Jiahao Wang, Xiaojun Wan"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.58.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 事实幻觉检测
tldr: 现有幻觉检测流水线在声明提取时易丢失上下文，且查询生成特异性低，导致检测性能下降。本文提出联合声明与查询生成框架JointCQ，通过构建高效的联合声明-查询生成器，优化了检测流水线的前两个阶段。实验表明，JointCQ框架显著提升了事实幻觉检测的性能，优于现有基线方法，为提升检测效率提供了新范式。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.58/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1641, \"height\": 751, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.58/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 808, \"height\": 362, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 726, \"height\": 322, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 805, \"height\": 488, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1641, \"height\": 508, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 731, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 774, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 810, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 807, \"height\": 428, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 727, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1651, \"height\": 1179, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1576, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1658, \"height\": 1035, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1617, \"height\": 452, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1631, \"height\": 852, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1648, \"height\": 889, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1634, \"height\": 900, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1634, \"height\": 816, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1635, \"height\": 797, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1640, \"height\": 768, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1643, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.58/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1645, \"height\": 393, \"label\": \"Table\"}]"
motivation: 现有幻觉检测流水线在声明提取时易丢失上下文，且查询生成特异性低，导致检测性能下降。
method: 提出联合声明与查询生成框架JointCQ，构建高效的声明-查询生成器以优化检测流水线。
result: JointCQ框架显著提升了事实幻觉检测的性能，优于现有基线方法。
conclusion: 联合优化声明提取和查询生成是提升大模型事实幻觉检测性能的有效途径。
---

## Abstract
Current large language models (LLMs) often suffer from hallucination issues, i,e, generating content that appears factual but is actually unreliable. A typical hallucination detection pipeline involves response decomposition (i.e., claim extraction), query generation, evidence collection (i.e., search or retrieval), and claim verification. However, existing methods exhibit limitations in the first two stages, such as context loss during claim extraction and low specificity in query generation, resulting in degraded performance across the hallucination detection pipeline. In this work, we introduce JointCQ, a joint claim-and-query generation framework designed to construct an effective and efficient claim-query generator. Our framework leverages elaborately designed evaluation criteria to filter synthesized training data, and finetunes a language model for joint claim extraction and query generation, providing reliable and informative inputs for downstream search and verification. Experimental results demonstrate that our method outperforms previous methods on multiple open-domain QA hallucination detection benchmarks, advancing the goal of more trustworthy and transparent language model systems.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：大语言模型（LLM）在生成内容时经常出现事实幻觉，即生成看似合理但实际上不可靠的信息。基于检索的幻觉检测方法通常包含四个步骤：响应分解（声明提取）、查询生成、证据检索和声明验证。
- **核心问题**：现有的检测流水线在前两个阶段存在明显缺陷：一是在声明提取时容易丢失上下文，二是生成的查询特异性低，导致下游检索和验证的性能严重下降。
- **整体含义**：本文旨在通过联合优化声明提取和查询生成这两个初始阶段，解决幻觉检测流水线的上游瓶颈，从而提升整体的事实幻觉检测准确率和效率。

### 2. 论文提出的方法论
- **核心思想**：提出 JointCQ 框架，将声明提取和查询生成统一为单次推理步骤，构建一个高效的联合声明-查询生成器。
- **关键技术细节与流程**：
  1. **数据合成**：
     - 使用 ANAH-v2 数据集的问题，利用 4 个不同的开源 LLM 生成多样化答案。
     - 使用 Qwen3-32B 通过 3-shot 提示从 QA 对中提取候选声明，并为每个声明生成对应的搜索查询。
  2. **标准引导的数据过滤**：
     - **声明评估标准**：蕴含性（声明被原文支持）、覆盖性（涵盖所有可验证事实）、去上下文化（声明可独立理解）。
     - **查询评估标准**：相关性（与声明紧密相关）、简洁性（聚焦核心信息）、可用性（适合搜索引擎检索）。
     - 利用 Qwen3-32B 对合成数据进行双阶段过滤，确保训练数据的高质量和对齐。
  3. **模型训练**：
     - 使用过滤后的高质量数据微调 Qwen2.5-14B-Instruct 模型，使其能够在单次推理中联合输出声明和查询。
- **检测流水线**：问题+答案 -> Claim-Query Generator（联合生成声明和查询） -> Searcher（Google Search检索证据） -> Verifier（Qwen3-14B验证事实性）。

### 3. 实验设计
- **数据集 / 场景**：
  - **ANAH**：双语（中英文）数据集，包含句子级幻觉标注，每语言采样 500 个 QA 对。
  - **HalluQA**：中文幻觉检测基准，包含 206 个事实相关样本，用于响应级评估。
- **评估指标**：准确率和 F1 分数，涵盖响应级和句子级评估。
- **对比方法**：
  - **先进通用 LLMs**：Gemini-2.5-Pro, GPT-5, GPT-4.1, Deepseek-V3.1, DeepSeek R1。
  - **专用幻觉检测方法**：SelfCheckGPT（基于一致性的黑盒方法）、FacTool（工具增强框架）、HaluAgent（基于智能体的框架）。

### 4. 资源与算力
- **训练算力**：使用 4 张 NVIDIA H100 GPU（80GB 显存），采用 DeepSpeed Zero-3 分布式训练。
- **训练超参**：Batch size 为 128，学习率 1e-5（10% 线性预热），训练 1 个 epoch，使用 bfloat16 混合精度和梯度检查点。
- **推理效率**：在 4 张 H100 上使用 vllm 引擎处理 200 个 QA 样本耗时 599 秒，其中搜索阶段占 303 秒，模型推理高效。

### 5. 实验数量与充分性
- **实验数量**：
  - 主实验：在 2 个数据集（ANAH-en, ANAH-zh, HalluQA）上进行了响应级和句子级共多组对比。
  - 消融实验：进行了 6 组消融研究（无过滤、仅过滤声明、仅过滤查询、无查询、替换生成器、非联合生成）。
  - 辅助分析：验证器可靠性分析、效率分析、案例研究。
- **充分性与客观性**：实验设计非常充分。消融实验精准隔离了“数据过滤”、“查询生成”和“联合生成”三个核心组件的贡献；对比基线涵盖了最先进的闭源模型和开源专用工具；且支持中英双语，证明了方法的泛化性。评估方式客观公平。

### 6. 论文的主要结论与发现
- JointCQ 在多个开放域 QA 幻觉检测基准上取得了最优或次优性能，特别是在句子级检测上显著优于 FacTool（准确率提升 5~8%，F1 提升 3~4 个点）。
- 专门的查询生成步骤是必要的，直接用声明作为查询会导致 F1 显著下降（整体下降 4.82 个点）。
- 标准引导的数据过滤策略对提升训练数据质量和最终检测性能至关重要。
- 联合生成模型在效果和效率上均优于分离式的声明提取和查询生成模型。
- 幻觉检测流水线的瓶颈在于前端的声明/查询生成，而非后端的验证（验证器与人类一致性达 91.4%）。

### 7. 优点
- **流水线优化**：创新性地将原本分离的声明提取和查询生成合并为单次推理，既减少了误差累积，又提升了效率。
- **数据质量控制**：设计了严密的双阶段、多维度过滤标准，有效解决了合成数据噪声大的问题。
- **完全开源与低成本**：整个框架基于开源模型构建，不依赖闭源 API，且推理效率高（每次判断仅需 1 次搜索调用），可部署性强。

### 8. 不足与局限
- **任务局限性**：框架主要针对开放域 QA 任务设计，能否直接迁移到摘要生成、代码生成等其他易产生幻觉的 NLP 任务尚需验证。
- **外部依赖**：证据检索依赖 Google Search，不可避免地继承了搜索引擎的固有局限（如信息滞后、索引偏差等）。
- **过滤模型偏差**：人工验证表明，自动过滤模型在“覆盖性”这一指标上不够严格（假阳性率达 27%），可能遗漏部分信息缺失问题。

（完）
