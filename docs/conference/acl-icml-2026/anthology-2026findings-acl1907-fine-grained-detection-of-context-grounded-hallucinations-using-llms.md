---
title: Fine-Grained Detection of Context-Grounded Hallucinations Using LLMs
title_zh: 使用大语言模型进行上下文相关幻觉的细粒度检测
authors: "Yehonatan Peisakhovsky, Zorik Gekhman, Yosi Mass, Liat Ein-Dor, Roi Reichart"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1907.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 使用大语言模型定位上下文相关的幻觉
tldr: 针对现有复杂评估流水线难以实用的问题，研究了利用大语言模型进行上下文相关幻觉的细粒度定位。构建了针对大语言模型的元评估基准和评估协议，并提出了一种基于自由文本描述的新幻觉表示方法，能够捕捉更广泛的错误类型，提升了幻觉检测的实用性和细粒度。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1907/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 733, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1907/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 788, \"height\": 146, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1907/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 812, \"height\": 155, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1907/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 831, \"height\": 277, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1907/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 798, \"height\": 195, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1907/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 789, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1907/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 799, \"height\": 235, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1907/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 766, \"height\": 413, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1907/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 751, \"height\": 629, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1907/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1640, \"height\": 656, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1907/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1646, \"height\": 772, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1907/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 806, \"height\": 166, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1907/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1650, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1907/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1650, \"height\": 390, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1907/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 812, \"height\": 390, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1907/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1648, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1907/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 811, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1907/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 806, \"height\": 390, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1907/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1645, \"height\": 473, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1907/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1645, \"height\": 796, \"label\": \"Table\"}]"
motivation: 现有上下文相关幻觉检测流水线复杂且不实用，缺乏细粒度定位基准和表示方法。
method: 构建了幻觉定位元评估基准，提出基于自由文本描述的幻觉表示方法及LLM评估协议。
result: 新表示方法能捕捉更广泛的错误类型，LLM评估协议在人工评估中验证了其有效性。
conclusion: 基于自由文本描述的幻觉表示和LLM评估协议提升了细粒度幻觉检测的实用性和准确性。
---

## Abstract
Context-grounded hallucinations are cases where model outputs contain information not verifiable against the source text. We study the applicability of LLMs for localizing such hallucinations, as a more practical alternative to existing complex evaluation pipelines. In the absence of established benchmarks for meta-evaluation of hallucinations localization, we construct one tailored to LLMs, involving a challenging human annotation of over 1,000 examples. We complement the benchmark with an LLM-based evaluation protocol, verifying its quality in a human evaluation. Since existing representations of hallucinations limit the types of errors that can be expressed, we propose a new representation based on free-form textual descriptions, capturing the full range of possible errors. We conduct a comprehensive study, evaluating four large-scale LLMs, which highlights the benchmark’s difficulty, as the best model achieves an F1 score of only 0.67. Through careful analysis, we offer insights into optimal prompting strategies for the task and identify the main factors that make it challenging for LLMs: (1) a tendency to incorrectly flag missing details as inconsistent, despite being instructed to check only facts in the output; and (2) difficulty with outputs containing factually correct information absent from the source - and thus not verifiable - due to alignment with the model’s parametric knowledge.

---

## 论文详细总结（自动生成）

# 论文总结：使用大语言模型进行上下文相关幻觉的细粒度检测

## 1. 核心问题与整体含义（研究动机和背景）
* **核心问题**：在上下文相关的生成任务中，模型输出可能包含无法由源文本验证的信息（即幻觉）。现有的幻觉检测方法多为粗粒度的二分类（一致/不一致），无法定位具体错误；而现有的细粒度方法（如基于实体、片段、QA对、原子事实）在错误表示能力上存在局限（无法覆盖动词、形容词等复杂错误，且标注主观模糊），且通常依赖复杂、难以维护的多阶段流水线。
* **整体含义**：本研究旨在探索利用大语言模型（LLM）端到端地定位上下文相关幻觉，以替代复杂的传统评估流水线。为此，论文提出了一种基于自由文本的幻觉表示法，并构建了专门针对LLM的细粒度幻觉定位元评估基准，以推动更实用、更精准的幻觉检测技术的发展。

## 2. 提出的方法论
* **核心思想**：使用自由文本描述来表示幻觉错误，并利用LLM进行端到端的错误定位，同时设计基于LLM的匹配评估协议来衡量定位结果。
* **关键技术细节**：
  * **自由文本描述表示法**：摒弃传统的实体高亮或片段截取，要求模型用自然语言句子明确描述摘要中的哪一点与源文本不一致（例如：“摘要称两人均为39岁，但原文称阿姆斯特朗为38岁”）。此方法能表达任意类型的错误，且消除了片段边界的主观性。
  * **FINAL基准构建**：
    * **阶段1**：基于DeFacto数据集，通过人工将原有的粗粒度解释转化为独立的自由文本描述（涉及提取、分解、修正模糊解释等操作）。
    * **阶段2**：人机协作的错误丰富化。使用LLM以高召回率提示挖掘潜在错误，再由人工过滤误报，使标注的错误数量增加了31%。
  * **LLM评估协议**：
    * 将评估转化为“匹配任务”。使用GPT-4o作为裁判，将模型预测的错误描述列表与金标描述列表进行对齐匹配，匹配上的计为真正例。
    * 为防止模型重复预测同一错误刷高分数，评估时统计的是被匹配上的金标错误数量，而非预测匹配数量。

## 3. 实验设计
* **数据集/场景**：FINAL基准，包含1,405个文本-摘要对，共2,131个细粒度幻觉标注（其中约45%的摘要包含多个错误）。
* **对比方法**：
  * **E2E（端到端）**：直接提示LLM输出错误描述，包括Zero-shot、Few-shot和CoT（思维链）三种提示策略。
  * **Pipeline（流水线）**：改进的FactScore方法，先分解为原子事实，再逐一验证并生成描述，最后去重。
  * **2-Step（两阶段）**：先进行二分类判断是否一致，若不一致再进行细粒度定位。分类器包括Self（LLM自身CoT分类）、TrueTeacher和Oracle（真实标签上限）。
* **评估模型**：GPT-4o, Claude-3.5-sonnet, Gemini-1.5-pro, Llama-3.1-405B。

## 4. 资源与算力
* **算力说明**：文中**未明确说明**所使用的GPU型号、数量或训练时长。由于主要评估的是闭源API模型（GPT-4o, Claude, Gemini）和开源大模型（Llama-3.1-405B）的推理能力，核心算力消耗在于API调用及大模型推理，且人工标注成本较高，但具体的计算资源开销未在文中披露。

## 5. 实验数量与充分性
* **实验数量**：
  * 测试了4种主流大模型在3种E2E提示、1种Pipeline和4种2-Step设定下的表现。
  * 进行了详尽的错误分析：对每个模型抽样150个假阴性样本和100个假阳性样本进行人工归类。
  * 进行了评估协议的验证：在140个开发集样本上对比了LLM裁判与人工裁判的匹配精度。
* **充分性与客观性**：实验设计非常充分且客观。不仅横向对比了不同架构的模型，还纵向对比了E2E、流水线和两阶段等不同范式；错误分析深入到了LLM参数化知识干扰的层面；LLM裁判的可靠性也通过了人工交叉验证。不过，Pipeline基线为了适配自由文本输出做了较大修改，可能存在轻微的对比不公平。

## 6. 论文的主要结论与发现
* **任务极具挑战**：即使是最好的模型（Claude-3.5-sonnet配合CoT），F1分数也仅为0.67，且精确度普遍高于召回率，表明模型倾向于只检测有把握的错误。
* **提示策略**：CoT（思维链）显著优于Zero-shot和Few-shot，也优于受控的Pipeline推理，表明让模型自由推理比强制分步更有效。
* **两阶段方法的反直觉表现**：2-Step方法表现不如端到端，因为LLM在二分类阶段过于保守（高精确度低召回），导致许多有错误的摘要被误判为一致，从而跳过了定位阶段。
* **LLM的两大核心弱点**：
  1. **参数化知识干扰**：对于摘要中存在、源文本不存在但事实正确的信息，LLM极易漏报，因为这与模型内部知识相符。
  2. **指令遵循缺陷**：LLM常将“摘要中遗漏的信息”误判为“不一致”，尽管提示词明确要求只检查摘要中存在的事实。

## 7. 优点
* **表示方法创新**：自由文本描述法突破了传统实体/片段表示的局限性，能够精准表达复杂、非连续的语义错误，且天然契合LLM的生成特性。
* **评估协议设计巧妙**：将主观的文本相似度评估转化为客观的“匹配对齐”任务，有效缓解了LLM作为裁判时的自我偏好和长度偏见，且经人工验证具有高可靠性（精确率0.95，召回率0.92）。
* **洞察深刻**：通过严密的假阴性/假阳性分析，实证了“参数化知识覆盖上下文”是幻觉定位失败的核心驱动力，为后续改进LLM的忠实度提供了明确方向。

## 8. 不足与局限
* **适用范围受限**：基准和评估协议专为LLM设计，难以直接与传统基于片段或QA的非LLM系统进行横向比较。
* **标注覆盖度**：尽管采用了人机协作丰富标注，但细粒度幻觉标注具有固有主观性，仍可能存在未被发现的遗漏错误。
* **场景泛化性**：数据集基于DeFacto，主要涉及较短的文本和摘要生成任务，能否泛化到长文本RAG或对话场景尚未可知。
* **计算成本透明度**：未公开具体的推理算力消耗和API成本。

（完）
