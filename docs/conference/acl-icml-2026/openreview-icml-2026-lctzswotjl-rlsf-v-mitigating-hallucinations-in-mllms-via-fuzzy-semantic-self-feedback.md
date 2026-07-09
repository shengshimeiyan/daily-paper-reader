---
title: "RLSF-V: Mitigating Hallucinations in MLLMs via Fuzzy Semantic Self-Feedback"
title_zh: RLSF-V：通过模糊语义自反馈缓解多模态大语言模型中的幻觉
authors: "Changhao He, Shuhao Yan, Shuxian Li, Xi Peng, Peng Hu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/c8eaa18a343846262c505fb3dec068c384457f32.pdf"
tags: ["query:llm-halluc"]
score: 8.0
evidence: 缓解多模态大语言模型中的幻觉
tldr: 多模态大语言模型加剧了幻觉问题，而现有基于直接偏好优化的缓解方法依赖人工或专有模型纠正幻觉，产生违反DPO假设的离线偏好数据，或依赖更强模型评估导致可扩展性差。本文提出RLSF-V方法，通过模糊语义自反馈机制生成在线偏好数据，有效避免了离线数据问题并大幅提升了模型的可扩展性与幻觉缓解效果，实现了性能与可扩展性的良好平衡。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有基于DPO的多模态LLM幻觉缓解方法依赖离线偏好数据或更强模型，存在假设违背或可扩展性差的问题。
method: 提出RLSF-V方法，利用模糊语义自反馈机制生成在线偏好数据以缓解多模态LLM幻觉。
result: RLSF-V有效缓解了多模态大语言模型中的幻觉，并在性能与可扩展性之间取得了更优平衡。
conclusion: 模糊语义自反馈为多模态大语言模型的幻觉缓解提供了一种可扩展且高效的在线偏好优化方案。
---

## Abstract
Multimodal large language models (MLLMs) extend large language models (LLMs) with visual perception for open-world understanding, but exacerbate LLMs' hallucinations, in which generated text contradicts visual evidence or common sense. To mitigate hallucinations, a dominant strategy is Direct Preference Optimization (DPO) using hallucination-labeled responses. Existing pipelines, however, face two key limitations: they either (i) rely on human inspection or proprietary models to correct hallucinated outputs, producing off-policy preference data that violate the assumptions of DPO, or (ii) depend on stronger models to evaluate responses, leading to an unfavorable trade-off between performance and scalability. Departing from these paradigms, we propose a reference-policy \emph{self-feedback} framework that constructs preference data for hallucination mitigation without any external supervision (\textit{e.g.}, large models or humans). Specifically, we present a novel \emph{local fuzzy semantic} evaluation paradigm that derives a hallucination-sensitive confidence signal directly from the internal logits, which is then used to automatically rank diverse generated responses to build preference pairs for fine-tuning. Trained on a 10k-scale dataset, our method achieves competitive performance on both generative and discriminative benchmarks compared to existing RLHF and RLAIF baselines.

---

## 论文详细总结（自动生成）

# 论文总结：RLSF-V：通过模糊语义自反馈缓解多模态大语言模型中的幻觉

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：多模态大语言模型（MLLMs）在获得视觉感知能力的同时，加剧了大语言模型原有的“幻觉”问题，即生成的文本与视觉证据或常识相矛盾。
- **现有方法的局限**：当前主流的基于直接偏好优化（DPO）的幻觉缓解方法面临两大瓶颈：
  1. **离线数据假设违背**：依赖人工或专有模型纠正幻觉输出来构建偏好数据，这产生了偏离策略的离线偏好数据，违反了DPO的假设。
  2. **可扩展性差**：依赖更强的模型来评估响应，导致性能与可扩展性之间存在不良权衡。
- **整体含义**：本文旨在打破现有依赖外部监督（人类或更强模型）的范式，探索一种完全依靠模型自身、无需外部监督的在线偏好数据构建方法，以从根本上解决DPO假设违背和可扩展性差的问题。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程
- **核心思想**：提出RLSF-V（参考策略自反馈框架），通过模糊语义自反馈机制生成在线偏好数据，实现无需任何外部监督的幻觉缓解。
- **关键技术细节**：
  - **局部模糊语义评估范式**：不依赖外部评判，而是直接从模型内部的logits中提取对幻觉敏感的置信度信号。
  - **自动排序与偏好对构建**：利用提取的置信度信号，自动对模型生成的多样化响应进行排序，从而构建出用于微调的偏好对。
- **算法流程**：
  1. 模型针对视觉输入生成多样化的响应。
  2. 引入局部模糊语义评估，从模型内部logits推导出反映幻觉敏感度的置信度信号。
  3. 基于该置信度信号对多样化响应进行自动排序，构建偏好对（优选响应与劣选响应）。
  4. 使用构建的在线偏好数据对模型进行DPO微调，优化模型以缓解幻觉。

## 3. 实验设计：数据集、Benchmark与对比方法
- **训练数据集**：使用了10k规模的数据集进行训练（摘要中未提及具体数据集名称）。
- **评估Benchmark**：在生成式和判别式两类基准测试上进行了评估（摘要中未提及具体Benchmark名称）。
- **对比方法**：与现有的RLHF（基于人类反馈的强化学习）和RLAIF（基于AI反馈的强化学习）基线方法进行了对比。

## 4. 资源与算力
- 论文提供的摘要及元数据中**未明确说明**所使用的算力资源（如GPU型号、数量、训练时长等）。

## 5. 实验数量与充分性
- **实验数量**：摘要中仅提及在10k规模数据集上的训练结果，以及在生成式和判别式两类基准上的对比测试。缺乏对消融实验数量的描述。
- **充分性与客观性评估**：基于现有信息，实验涵盖了生成与判别两大主流评估维度，并与RLHF/RLAIF基线进行了对比，基本能验证方法的有效性。但由于缺乏详细数据集信息和消融实验说明，无法全面评估其对比的公平性和实验覆盖的充分性。

## 6. 论文的主要结论与发现
- RLSF-V方法通过模糊语义自反馈机制，成功构建了无需外部监督的在线偏好数据，有效缓解了MLLMs中的幻觉问题。
- 与依赖外部强模型或人工的方法相比，RLSF-V在性能与可扩展性之间取得了更优的平衡，为多模态大语言模型的幻觉缓解提供了一种可扩展且高效的在线偏好优化方案。

## 7. 优点：方法或实验设计上的亮点
- **无需外部监督**：彻底摆脱了对人类标注或更强专有模型的依赖，极大地降低了成本并提升了可扩展性。
- **符合DPO假设的在线数据**：通过模型自生成和自评估构建在线偏好数据，避免了离线数据偏离当前策略的问题，更符合DPO的理论假设。
- **创新的内部信号利用**：提出“局部模糊语义”评估范式，巧妙地利用模型内部logits的置信度作为幻觉检测信号，为自反馈机制提供了坚实的量化基础。

## 8. 不足与局限
- **自我强化偏差风险**：自反馈机制高度依赖模型自身的logits输出，如果模型本身存在系统性偏差，自反馈可能会强化而非纠正这些偏差（即“模型给自己打分”可能不够客观）。
- **隐式幻觉的捕捉能力**：基于内部logits置信度的信号可能对事实性错误等显式幻觉较为敏感，但对于逻辑错误或复杂常识违背等隐式幻觉，其捕捉能力可能受限。
- **实验细节披露不足**：从摘要来看，缺乏对具体评估数据集、消融实验设计及算力消耗的详细说明，使得方法的泛化能力和各模块的实际贡献度难以精确评估。

（完）
