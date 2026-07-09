---
title: "Dynamic PMI-Guided Contrastive Decoding Reduces Hallucination in Large Language Models: A Unified Framework of Fine-Grained Input Transformations"
title_zh: 动态PMI引导的对比解码减少大语言模型幻觉：细粒度输入变换的统一框架
authors: "Dongsheng Chen, Yingqi Zhu, Xingyue Zhang, Wenqing Zhou, Lei Li"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1212.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 通过对比解码减少大模型幻觉
tldr: 大语言模型具有强大的生成能力，但其易拟合预训练数据中的虚假依赖而非潜在因果逻辑，导致严重的幻觉问题。本文从信息论视角提出基于动态点互信息的统一对比解码框架，设计了针对上下文、语法和语义的三种细粒度输入变换策略，以构建动态背景分布。这些策略能够系统性地解耦虚假依赖，从而在解码阶段有效减少幻觉的产生。实验证明该框架显著提升了生成内容的可靠性，为缓解大模型幻觉提供了统一的解决方案。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1212/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1496, \"height\": 567, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1212/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 805, \"height\": 351, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1212/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1491, \"height\": 396, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1212/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1662, \"height\": 1110, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1212/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1662, \"height\": 788, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1212/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 805, \"height\": 217, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1212/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 815, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1212/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 813, \"height\": 426, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1212/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 805, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1212/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 807, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1212/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1638, \"height\": 712, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1212/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1663, \"height\": 862, \"label\": \"Table\"}]"
motivation: 大语言模型易拟合预训练数据中的虚假依赖而非潜在因果逻辑，导致严重的幻觉。
method: 提出基于动态点互信息的统一对比解码框架，通过细粒度输入变换构建动态背景分布。
result: 该框架有效减少了大语言模型中的幻觉现象，提升了生成内容的可靠性。
conclusion: 动态PMI引导的对比解码为缓解大语言模型幻觉提供了统一且有效的信息论解决方案。
---

## Abstract
Despite the remarkable generation capabilities demonstrated by large language models (LLMs), the issue of hallucination remains a critical challenge. This is largely attributed to the models’ tendency to fit spurious dependencies in pre-training data rather than underlying causal logic. To address this, from an information-theoretic perspective, this paper proposes a unified contrastive decoding framework based on dynamic pointwise mutual information (Dynamic PMI). Under this framework, we design three fine-grained input transformation strategies targeting context, syntax, and semantics to construct dynamic background distributions. These strategies systematically disentangle and suppress spurious dependencies induced by context priors, lexical co-occurrences, and syntactic structures, thereby guiding the model to prioritize underlying causal logic. Experiments on extensive discriminative and generative benchmarks demonstrate that our method significantly improves the model’s factuality and reasoning robustness. Notably, despite employing a single-model architecture, our framework surpasses state-of-the-art dual-model strategies while maintaining high computational efficiency. Furthermore, the framework exhibits strong cross-model generalizability and effectively alleviates the over-refusal tendency in open-ended generation.

---

## 论文详细总结（自动生成）

# 论文总结：动态PMI引导的对比解码减少大语言模型幻觉

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）在生成内容时存在严重的“幻觉”问题，即生成与客观事实或上下文不符的内容。
- **根本原因**：模型倾向于拟合预训练数据中的“虚假依赖”（如上下文先验、词汇共现、句法结构惯性），而非潜在的因果逻辑。在长文本生成中，这种倾向易通过“雪球效应”被放大。
- **现有方法的局限**：现有的对比解码（CD）方法中，双模型架构（如专家-业余模型）计算开销大；单模型方法（如利用模型内部层间差异）则忽略了输入空间中细粒度特征对虚假依赖的影响。
- **整体含义**：亟需一种既能保持单模型高效率，又能从输入特征层面系统性解耦并抑制虚假依赖的统一解码范式。

## 2. 方法论：核心思想、关键技术细节与算法流程
- **核心思想**：从信息论视角出发，提出基于动态点互信息的统一对比解码框架。通过细粒度的输入变换构建“动态背景分布”，以隔离和量化特定输入特征带来的虚假依赖，并在解码时将其从原始分布中减去，从而引导模型依赖真实的因果逻辑。
- **统一打分公式**：
  - $S(y_t | x, y_{<t}) = \log P_\theta(y_t | x, y_{<t}) - \beta \log P_\theta(y_t | T(x), y_{<t})$
  - 其中，第一项为基于完整输入的预测概率（包含真实逻辑与虚假依赖），第二项为基于变换后输入的预测概率（主要捕获特定特征引入的虚假依赖），$\beta$ 为惩罚强度系数。通过对比相减，抑制虚假依赖的token概率，放大基于真实逻辑的token概率。
- **三种细粒度输入变换策略（构建动态背景分布）**：
  - **CPMI（Context-only PMI）**：针对**上下文维度**，抑制上下文先验依赖。变换方式为保留上下文 $C$，移除查询 $Q$（即 $T(x) = [C, \emptyset]$），迫使模型关注查询带来的增量信息。
  - **SPMI（Syntax-shuffled PMI）**：针对**语法维度**，抑制词汇共现依赖。变换方式为保留查询词汇但随机打乱词序（即 $T(x) = [C, \text{Shuffle}(Q)]$），破坏句法结构，惩罚仅靠词汇共现做出的浅层预测。
  - **DCPMI（Dropped-content PMI）**：针对**语义维度**，抑制句法结构惯性依赖。变换方式为剥离查询中的内容词，仅保留功能词和标点（即 $T(x) = [C, \text{DropContent}(Q)]$），暴露模型对句法骨架的“填空”倾向并予以惩罚。

## 3. 实验设计：数据集、Benchmark与对比方法
- **数据集与Benchmark**：
  - **判别式任务（6个）**：TruthfulQA（事实性核心指标）、MMLU、ARC-Challenge、CommonsenseQA、HellaSwag、GPQA。
  - **生成式任务（5个）**：GSM8K、SVAMP、MultiArith（数学推理）；StrategyQA（多跳推理）；BigBench的4个子任务（符号推理）。
- **对比方法**：
  - **基础基线**：Greedy Decoding。
  - **双模型方法**：CD、UCD。
  - **单模型方法**：DoLa、SH2、ITI、ActLCD。
- **评测指标**：TruthfulQA使用MC1/MC2/MC3及自动/人工评判；其他判别式任务使用准确率；生成式任务使用GPT-4o自动评判。

## 4. 资源与算力
- **算力说明**：论文**未明确说明**所使用的GPU型号、数量及训练时长。但文中强调该方法为纯单模型推理时干预策略，且实验测得其解码延迟仅为贪心解码的1.12倍，吞吐量约为0.90，计算效率远超双模型方法。

## 5. 实验数量与充分性
- **实验数量**：实验覆盖极广，包括11个主流基准测试、3种不同架构的模型（Llama 3.1系列、Mistral、Qwen）、参数敏感性分析（$\beta$取值）、策略互补性分析（集成实验）、推理效率分析、人工评估、定性案例分析，以及专门构建的3组诊断数据集分析。
- **充分性与客观性**：实验设计**非常充分且客观**。不仅涵盖了判别与生成、常识与数学推理等多场景，还专门构建了诊断数据集来验证CPMI/SPMI/DCPMI是否各自精准抑制了对应的虚假依赖（验证了假设的因果性），排除了偶然性。同时引入人工评估验证自动评估的可靠性，增强了结论的可信度。

## 6. 主要结论与发现
- **显著降低幻觉**：Dynamic PMI框架在TruthfulQA等事实性基准上大幅超越贪心解码，且单模型架构下超越了SOTA双模型方法（如UCD）。
- **提升推理鲁棒性**：在数学、多跳和符号推理任务上均取得显著提升，证明抑制虚假依赖不会损害反而增强了逻辑推理能力。
- **缓解过度拒绝**：在开放域生成中，该方法在提升真实性的同时，将模型的拒绝回答率从11.02%降至4%-6%，说明其并非通过“让模型闭嘴”来规避错误，而是实质性地提升了事实辨别力。
- **策略互补与泛化性**：三种策略针对不同维度的虚假依赖具有特异性与互补性，集成后效果更佳；框架在Llama、Mistral、Qwen等不同架构和参数规模上均表现出强泛化性。

## 7. 优点
- **理论统一**：从信息论（动态PMI）视角统一了对比解码范式，为输入变换抑制幻觉提供了坚实的理论解释。
- **细粒度与可解释性**：三种输入变换策略设计精巧，分别精准对齐上下文、词汇、句法三大虚假依赖源，机制清晰可解释。
- **高效实用**：无需额外模型，仅通过输入变换和并行计算即可实现，推理开销极小，具有极高的工业落地价值。
- **评估严谨**：构建诊断数据集验证方法假设，比单纯刷榜更具学术价值。

## 8. 不足与局限
- **语言局限**：当前评估主要局限于英文数据集，对多语言或低资源场景中特定语言细微差别的适用性尚不明确。
- **启发式规则依赖**：输入变换策略依赖启发式规则（如随机打乱词序、基于NLTK停用词表剥离内容词），这些规则可能并非所有情况下的最优解，存在破坏真实语义的风险。
- **未来改进空间**：作者也指出，未来可探索基于学习的方法，自动发现针对特定样本的最优变换策略，以取代人工设计的启发式规则。

（完）
