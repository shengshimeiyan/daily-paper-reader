---
title: "PROBE: PROcess-Based BEnchmark for Hallucination Detection"
title_zh: PROBE：用于幻觉检测的基于过程的基准
authors: "Yu Zhang, Peter Belcak, Shizhe Diao, Yonggan Fu, Shaona Ghosh, Morteza Mardani, Eileen Margaret Peters Long, Bei Yu, Pavlo Molchanov"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.2099.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 大模型幻觉检测基准
tldr: 现有大语言模型智能体应用依赖单步提示让模型自评输出的事实性，但这种方法缺乏透明度与细粒度，难以诊断检测失败的具体原因。本文提出PROBE基准，将幻觉检测系统性地分解为声明分解、证据查找、证据评估和幻觉定位四个关键步骤，并对每个步骤进行独立评估。实验表明，该基准能够提供更精细的评估与诊断，揭示了现有检测方法的不足，为未来开发更可靠的幻觉检测系统指明了方向。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2099/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 793, \"height\": 647, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2099/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1493, \"height\": 392, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2099/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 270, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2099/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1661, \"height\": 344, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2099/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1643, \"height\": 997, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.2099/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 63, \"height\": 46, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2099/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1653, \"height\": 310, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2099/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1652, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2099/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1662, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.2099/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1634, \"height\": 1575, \"label\": \"Table\"}]"
motivation: 现有LLM幻觉检测的单步评估方法缺乏透明度与细粒度，难以诊断检测失败的原因。
method: 提出PROBE基准，将幻觉检测分解为声明分解、证据查找、评估和定位四个关键步骤。
result: PROBE基准能够提供更透明和细粒度的幻觉检测评估，揭示现有方法的不足。
conclusion: 过程化基准为幻觉检测提供了更精细的诊断工具，有助于改进检测方法。
---

## Abstract
Hallucination detection remains a significant challenge for large language models. Existing agentic applications rely on LLMs to self-assess the factuality of their outputs using single-step “LLM-as-a-judge” prompts. However, even when equipped with ground truth information, current LLMs still fall short in detecting hallucinations, and this one-shot evaluation offers neither the transparency nor the granularity needed to diagnose where and why the detection fails. To address this gap, we introduce PROBE (Process-based Benchmark for Hallucination Detection), a comprehensive benchmark that breaks down hallucination detection into four critical steps: claim decomposition, evidence finding, evidence evaluation, and hallucination localization, and evaluates each step individually. PROBE consists of 12,000 test cases across three task types—summarization, question answering, and style transfer. Critically, we demonstrate that when hallucination detection is treated as a multi-step process, all models achieve considerably better performance. Through extensive evaluation, we show that current LLMs struggle chiefly with evidence finding, and that finetuning on our released training data substantially improves performance on this step. PROBE represents a significant step toward more transparent, diagnosable, and robust hallucination detection systems.

---

## 论文详细总结（自动生成）

# 论文总结：PROBE: PROcess-Based BEnchmark for Hallucination Detection

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）的幻觉检测仍是一项重大挑战。现有的智能体应用通常依赖单步的“LLM-as-a-judge”提示让模型自我评估输出的事实性，但这种方法缺乏透明度和细粒度，无法诊断检测失败的具体位置和原因。
- **整体含义**：幻觉检测不应被视为一个单一的、黑盒式的分类任务，而应是一个多步骤的认知推理过程。将检测过程拆解，不仅能提供更精细的诊断，还能显著提升检测的准确性和可解释性，为构建更可靠、透明的LLM系统指明方向。

## 2. 论文提出的方法论：核心思想、关键技术细节与流程
- **核心思想**：提出 PROBE 基准，将幻觉检测系统性地分解为四个关键步骤，并对每个步骤进行独立评估。
- **四步流程**：
  1. **声明分解**：将长文本输出拆解为可独立验证的原子声明。
  2. **证据查找**：针对每个声明，从源文档中检索支持该声明的相关证据片段。
  3. **证据评估**：判断检索到的证据是否真正支持该声明（二元判断：支持/不支持）。
  4. **幻觉定位**：将没有支持证据的声明定位并标记为幻觉内容。
- **数据构建流程**：
  1. **基础内容生成**：使用 GPT-OSS-120B 基于 Clean Wikipedia 生成摘要、问答和风格转换三种任务的基础回答。
  2. **幻觉注入**：合成注入看似合理但源文档中不存在的“中毒语义”，构建三个复杂度级别（包含1个、2个、3个幻觉声明）的样本。
  3. **声明-证据对生成**：使用 Llama-3.1-70B 进行声明分解；使用4个前沿模型（Llama-3.1-70B, GPT-4o-mini, Mixtral-8x22B, Claude-Sonnet-4.5）进行证据查找与评估，采用多数投票（≥0.75共识）机制确保证据标注的鲁棒性。

## 3. 实验设计：数据集、Benchmark 与对比方法
- **数据集**：PROBE 基准，包含 12,000 个测试用例（涵盖摘要、问答、风格转换），共计 118,628 个带详细标注的声明。
- **Benchmark 评估指标**：
  - 声明分解与幻觉定位：字符级别的 Precision、Recall、F1。
  - 证据查找：部分匹配（检索到至少一个正确证据）和完全匹配（检索到所有必需证据）。
  - 证据评估：准确率。
- **对比方法**：
  - **直接提示**：单步“LLM-as-a-judge”直接判断是否包含幻觉。
  - **过程评估**：本文提出的多步拆分评估法。
  - **参与评测的模型**：Llama-3.1-70B, GPT-4o-mini, Mixtral-8x22B, Claude-Sonnet-4.5。
  - **微调模型**：使用 PROBE 训练集微调的 Llama-3.1-8B。

## 4. 资源与算力
- **算力使用**：微调 Llama-3.1-8B 模型时使用了 **8 张 NVIDIA A100 (80GB) GPU**，采用全分片数据并行（FSDP）技术。
- **未明确说明的信息**：论文未提及具体的训练时长（小时/天数）及推理阶段的算力消耗。

## 5. 实验数量与充分性
- **实验数量**：
  - 对 4 个前沿模型在 3 个任务、4 个评估步骤上进行了全面评测。
  - 对比了直接提示与过程评估在 3 个任务上的表现。
  - 进行了 1 组微调实验（Llama-3.1-8B）以验证过程监督数据的有效性。
- **充分性与客观性**：实验设计较为充分，涵盖了不同规模和家族的模型，且从多维度（细粒度步骤、不同任务类型、不同幻觉复杂度）进行了剖析；评估指标采用了严格的字符级匹配和完全匹配，客观公平地揭示了模型在“证据查找”等步骤的短板。

## 6. 论文的主要结论与发现
- **过程评估优于单步评估**：将幻觉检测视为多步过程时，所有模型的召回率显著提升（从直接提示的低于 40% 提升至 80%-90% 以上）。
- **声明分解较容易**：当前 LLM 在声明分解步骤表现优异（Recall 持续 >95%），为后续步骤奠定了良好基础。
- **证据查找是主要瓶颈**：前沿模型在部分证据匹配上表现尚可（约80%），但在完全匹配（找回所有必需证据）上表现大幅下降，严重制约了后续的评估与定位。
- **证据评估存在不足**：即使提供了候选证据，模型仍难以可靠判断证据的充分性与相关性（如 Claude-Sonnet-4.5 在 QA 任务上准确率仅 69.8%）。
- **过程监督数据可大幅提升性能**：在 PROBE 训练集上微调较小的 Llama-3.1-8B 模型，其在证据查找和评估步骤上的表现超越了参数量更大的前沿模型。

## 7. 优点：方法或实验设计上的亮点
- **细粒度诊断**：首次将幻觉检测拆解为四步过程，打破了传统黑盒评估，能够精准定位模型检测失败的环节（如诊断出证据查找是核心瓶颈）。
- **高质量数据构建**：采用受控的幻觉注入机制（3个复杂度级别）和多模型共识投票机制，确保了数据集标注的准确性、多样性和挑战性。
- **实用价值高**：证明了过程监督微调的有效性，为社区提供了高质量的训练数据，有助于开发专门化的幻觉检测小模型。

## 8. 不足与局限
- **算力限制导致微调规模有限**：由于计算资源限制，仅微调了 8B 规模的模型，未验证在更大模型（如 70B）上的微调效果。
- **推理延迟增加**：多步过程评估需要多次调用 LLM，相比单步直接提示延迟更高。
- **领域与语言局限**：当前基准仅限于英语和非专家领域（维基百科），未覆盖医疗、金融等高风险专业领域及多语言场景。

（完）
