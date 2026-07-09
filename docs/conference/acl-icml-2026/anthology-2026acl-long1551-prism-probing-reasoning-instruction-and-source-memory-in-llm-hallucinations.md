---
title: "PRISM: Probing Reasoning, Instruction, and Source Memory in LLM Hallucinations"
title_zh: PRISM：探究LLM幻觉中的推理、指令与来源记忆
authors: "Yuhe Wu, Guangyu Wang, Yuran Chen, Jiatong Zhang, Yutong Zhang, Yujie Chen, Jiaming Shang, Guang Zhang, Zhuang Liu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1551.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 探究LLM幻觉
tldr: 现有幻觉评估基准多依赖混合查询和输出级评分，仅量化幻觉严重程度，难以洞察幻觉在生成管道中产生的具体原因和位置。本文将幻觉评估重构为诊断问题，提出PRISM基准，将幻觉解耦为知识缺失、知识错误、推理错误和指令遵循错误四个维度，并基于记忆、指令和推理三个生成阶段进行细粒度评估，为深入理解幻觉产生机制提供了有力分析工具，推动了精准缓解策略的发展。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1551/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1653, \"height\": 847, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1551/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1573, \"height\": 505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1551/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 767, \"height\": 839, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1551/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 670, \"height\": 520, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1551/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 788, \"height\": 777, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1551/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1633, \"height\": 962, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1654, \"height\": 584, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 360, \"height\": 400, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 834, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1647, \"height\": 1115, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 800, \"height\": 483, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1452, \"height\": 1544, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1690, \"height\": 2215, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1645, \"height\": 322, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1651, \"height\": 797, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1652, \"height\": 546, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1654, \"height\": 746, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1647, \"height\": 1139, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1652, \"height\": 666, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 803, \"height\": 591, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1647, \"height\": 275, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1645, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.1551/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1304, \"height\": 384, \"label\": \"Table\"}]"
motivation: 现有幻觉评估基准仅量化严重程度，难以洞察幻觉在生成管道中产生的原因和位置。
method: 提出PRISM基准，将幻觉解耦为四个维度，并基于记忆、指令和推理三个生成阶段进行诊断评估。
result: PRISM能够有效诊断LLM幻觉的来源，为理解幻觉产生机制提供了细粒度分析工具。
conclusion: 将幻觉评估重构为诊断问题有助于深入理解LLM幻觉的根本原因，推动更精准的缓解策略发展。
---

## Abstract
As large language models (LLMs) evolve from conversational assistants into agents capable of handling complex tasks, they are increasingly deployed in high-risk domains. However, existing benchmarks largely rely on mixed queries and posterior evaluation, output-level scoring, which quantifies hallucination severity but offers limited insight into where and why hallucinations arise in the generation pipeline. We therefore reformulate hallucination evaluation as a diagnostic problem and propose PRISM, a controlled benchmark that disentangles hallucinations into four dimensions: knowledge missing, knowledge errors, reasoning errors, and instruction-following errors, grounded in three stages of generation (memory, instruction, and reasoning). PRISM contains 9,448 instances across 65 tasks and supports fine-grained, stage-aware diagnostic evaluation. Evaluating 24 mainstream open-source and proprietary LLMs, we uncover consistent trade-offs across instruction following, memory retrieval, and logical reasoning, showing that mitigation strategies often improve specific dimensions at the expense of others.We hope PRISM provides a framework for understanding the specific mechanisms behind LLMs hallucinations, ultimately accelerating the development of trustworthy large language models.

---

## 论文详细总结（自动生成）

# 论文总结：PRISM: Probing Reasoning, Instruction, and Source Memory in LLM Hallucinations

## 1. 论文的核心问题与整体含义
- **研究动机**：随着大语言模型（LLM）在高风险领域的广泛应用，幻觉问题成为制约其可信度的核心挑战。然而，现有的幻觉评估基准（如TruthfulQA, HaluEval）通常采用混合查询和后验的输出级评分，只能量化幻觉的严重程度，无法回答“模型为什么失败”以及“幻觉在生成管道中的哪个阶段产生”的根本问题。
- **整体含义**：本文将幻觉评估从一个“量化问题”重构为一个“诊断问题”，旨在通过解耦不同的认知阶段，精准定位幻觉产生的根源（记忆、推理还是指令遵循），从而为模型优化提供方向，避免盲目优化带来的能力权衡。

## 2. 论文提出的方法论
- **核心思想**：提出 PRISM 基准，基于 LLM 的交互式生成管道，将幻觉严格解耦为四个独立的失败维度，并遵循正交性原则构建数据，确保每个子集独立测试单一的失败模式。
- **四维幻觉解耦**：
  - **知识错误**：模型参数化知识存储了错误或过时信息。
  - **知识缺失**：模型参数化知识缺乏回答问题所需的正确信息。
  - **推理错误**：模型拥有事实，但未能通过逻辑或推理将其结合。
  - **指令遵循错误**：模型知识和推理正确，但输出违反了用户的显式约束。
- **数据构建流程**：
  1. **数据收集**：从权威来源收集语料并去噪。针对参数知识任务收集事实数据（维基百科等）和分布外数据（OOD，如2025年新闻、虚构实体、私有域数据）；针对推理/指令任务收集自包含推理数据（数学、代码）和复杂指令数据（对抗性合成约束）。
  2. **多智能体构建**：采用四智能体框架：① Schema规范化智能体；② 证据检索智能体；③ 类型分类智能体；④ 质量评分智能体。
  3. **人工筛选**：80名领域专家分为两组（知识组与推理指令组），从清晰度、领域相关性和连贯性三个维度进行多轮审核。
- **质量评分算法**：
  - 采用加权评估：$S(x) = 0.5 \cdot A(x) + 0.3 \cdot B(x) + 0.2 \cdot C(x)$，其中A为事实性，B为区分度，C为清晰度。
  - 阈值淘汰：各维度得分均需超过7.0（满分10），否则剔除。

## 3. 实验设计
- **数据集/Benchmark**：本文构建的 **PRISM** 基准，包含 9,448 个评估实例，覆盖 4 个失败维度和 65 个具体子任务。
- **评估指标**：
  - **Accuracy**：用于封闭式任务。
  - **LLM-Eval**：用于开放式任务，由LLM裁判给出0-5分。
  - **Hallucination Rate (H)**：$H = 100 - S$（S为统一映射到0-100的得分）。
  - **H-Score**：四个维度幻觉率的宏观平均值，作为综合评价指标。
- **对比方法与模型**：
  - 评估了 **24 款** 主流开源与闭源模型，包括 GPT-5.2/5.1/4o, Gemini-3/2.5, Claude-Opus/Sonnet/Haiku-4.5, Grok-4, DeepSeek-V3.2/R1, Qwen3, GLM-4.5, Llama-4/3.3 等。
  - 对比了不同缓解策略：上下文学习（ICL，0/1/3-shot）、指令微调、推理微调。

## 4. 资源与算力
- **未明确说明**：论文正文中**未明确提及**具体的硬件算力资源（如GPU型号、数量、训练时长等）。
- **间接消耗**：文中提到使用 Gemini 3 Pro 作为证据检索智能体，使用 GPT-4o 进行超参数网格搜索和开放式任务评估，但未披露API调用的具体规模或成本。

## 5. 实验数量与充分性
- **实验规模**：
  - 主实验：24个模型 × 4个维度 × 65个子任务。
  - 缓解策略实验：3种策略（ICL/Instruct/Reasoning）在Llama3.1-8B上的对比。
  - 机制分析实验：注意力图可视化和计算成本分析（GFLOPs, 活跃神经元数）。
  - 超参数搜索：温度和top-p的网格搜索。
- **充分性与客观性**：
  - **充分**：涵盖了当前最前沿的模型系列，且从宏观得分到微观机制（注意力、计算开销）进行了多层次分析；LLM-Eval与人工标注的一致性验证（MAD=0.07）增强了评估的客观性。
  - **公平**：通过网格搜索为不同任务类型确定最佳采样参数，确保模型能在较优状态下比较；严格的正交数据设计排除了混淆因素。

## 6. 论文的主要结论与发现
- **模型表现**：Claude-Opus-4.5、Gemini-3-Pro 和 Gemini-3-Flash 位列前三（H-Score最低）。开源模型在KM维度接近闭源，但在RE和IFE维度显著落后。
- **维度相关性**：KE与RE相关性最强，与IFE相关性最弱；说明推理错误常与知识错误伴生，而指令遵循相对独立。
- **缓解策略的权衡**：现有缓解策略本质上是针对特定阶段的归纳偏置，存在不可避免的权衡：
  - **推理微调**：显著提升RE，但严重损害KE和IFE（灾难性遗忘）。
  - **指令微调**：改善IFE和KE冲突，但损害多步推理RE。
  - **ICL**：边际效应小，主要帮助格式对齐，无法解决知识根因。
- **幻觉机制洞察**：
  - **KE**：由参数化先验主导，模型忽视输入中的正确证据。
  - **KM**：由误导性上下文主导，模型在缺乏内部知识时易被虚假输入带偏。
  - **IFE**：拒绝回答（合规）比产生幻觉（违规）需要更多的计算开销（更高的GFLOPs和更低的注意力稀疏度），因为模型需要进行更重的交叉检查。

## 7. 优点
- **诊断视角的创新**：首次将幻觉评估从“结果评分”转向“过程诊断”，解决了混合查询导致的归因模糊问题。
- **严格的正交设计**：通过变量控制，确保每个子任务只测试单一认知阶段，使得错误归因具有可靠的科学基础。
- **深度的机制分析**：不仅停留在指标打分，还深入到注意力机制和计算成本层面解释幻觉成因（如参数先验主导、拒绝的计算代价），为后续算法改进提供了理论依据。

## 8. 不足与局限
- **模态与语言局限**：目前仅覆盖文本模态，未涉及多模态幻觉；仅涵盖5种高资源语言，对低资源语言适用性未知。
- **静态与时效性局限**：依赖静态权威语料，难以捕捉现实世界知识的实时更新与遗忘；尽管OOD数据设定在2025年，但仍无法完全排除未公开训练截止日期模型的数据污染风险。
- **长尾覆盖不足**：为保证可验证性和可复现性，依赖权威静态语料，可能导致对长尾信息的覆盖不足。
- **应用限制**：PRISM定位为研究诊断工具，不宜作为医疗、法律等高风险领域模型安全评估的唯一依据。

（完）
