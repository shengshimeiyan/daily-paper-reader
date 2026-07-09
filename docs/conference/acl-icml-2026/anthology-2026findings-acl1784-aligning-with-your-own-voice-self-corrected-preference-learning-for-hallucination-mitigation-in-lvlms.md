---
title: "Aligning with Your Own Voice: Self-Corrected Preference Learning for Hallucination Mitigation in LVLMs"
title_zh: 与自己的声音对齐：用于LVLM幻觉缓解的自纠正偏好学习
authors: "Byeonggeuk Lim, JungMin Yun, Junehyoung Kwon, Kyeonghyun Kim, Youngbin Kim"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1784.pdf"
tags: ["query:llm-halluc"]
score: 8.0
evidence: 用于缓解幻觉的自纠正偏好学习
tldr: 针对现有偏好学习方法依赖专有模型导致分布不匹配从而阻碍对齐的问题，提出了AVES-DPO框架。该框架利用模型内在知识生成的分布内数据对齐大视觉语言模型，采用基于共识的验证机制诊断多种幻觉并引导模型自纠正，生成与内部兼容的偏好对，有效缓解了多模态场景下的幻觉问题。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1784/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 280, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1784/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 482, \"height\": 109, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1784/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 784, \"height\": 499, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1784/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 793, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1784/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1652, \"height\": 719, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1784/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 720, \"height\": 434, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1784/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 805, \"height\": 663, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1784/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 775, \"height\": 304, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1784/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 805, \"height\": 482, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1654, \"height\": 698, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1331, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1654, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 415, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 805, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1656, \"height\": 916, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1425, \"height\": 464, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1421, \"height\": 379, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 799, \"height\": 610, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1653, \"height\": 555, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1330, \"height\": 547, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 808, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 809, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 690, \"height\": 507, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1784/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 806, \"height\": 167, \"label\": \"Table\"}]"
motivation: 现有基于偏好学习的LVLM幻觉缓解方法依赖专有模型，存在分布不匹配问题。
method: 提出AVES-DPO框架，利用模型内在知识生成分布内数据，通过共识验证引导自纠正。
result: 生成了与模型内部兼容的偏好对，有效缓解了大视觉语言模型中的多种幻觉。
conclusion: 基于自纠正的分布内偏好学习能有效解决分布不匹配问题，提升多模态幻觉缓解效果。
---

## Abstract
Large Vision-Language Models (LVLMs) frequently suffer from hallucinations. Existing preference learning-based approaches largely rely on proprietary models to construct preference datasets. We identify that this reliance introduces a distributional mismatch between the proprietary and target models that hinders efficient alignment. To address this, we propose Alignment via VErified Self-correction DPO (AVES-DPO), a framework that aligns LVLMs using in-distribution data derived from the model’s intrinsic knowledge. Our approach employs a consensus-based verification mechanism to diagnose diverse hallucinations and guides the model to self-correct, thereby generating preference pairs strictly compatible with its internal distribution. Extensive experiments demonstrate that AVES-DPO surpasses existing baselines in hallucination mitigation while requiring only 5.2k samples.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大型视觉语言模型（LVLMs）在生成内容时经常出现“幻觉”（生成与图像不符的内容）。现有的基于偏好学习（如DPO）的缓解方法主要依赖专有模型（如GPT-4V）来构建偏好数据集。
- **研究动机**：
  - **分布不匹配**：依赖专有模型生成的数据会引入分布不匹配问题，即外部模型的生成模式与目标模型的内在分布存在差异，这阻碍了高效的偏好对齐。
  - **幻觉类型单一**：现有数据集和训练目标过度偏向于“对象幻觉”（判断对象是否存在），而忽略了属性和关系等更细粒度的幻觉。
- **整体含义**：本文提出应利用模型自身的内在知识生成“分布内”的偏好数据，通过自我纠正来对齐模型，从而更高效、全面地缓解多模态幻觉。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出 AVES-DPO（Alignment via VErified Self-correction DPO）框架，通过基于共识的验证机制诊断多种幻觉，并引导模型自我纠正，生成与其内部分布严格兼容的偏好对。
- **关键技术细节与流程**：
  - **阶段一：幻觉验证**
    - **场景图提取**：将模型生成的初始响应解析为结构化场景图，包含对象、属性和关系。
    - **O/A/R 验证**：采用基于共识的验证策略，使用两个独立的验证模型，仅当两者一致时才确定标签，否则标记为“模糊”。
      - *对象验证*：主验证器使用 YOLO 和 Grounding DINO；对于模糊对象，次验证器使用 Qwen3-VL 系列模型进行二次共识验证。
      - *属性与关系验证*：仅对确认为真实的对象进行，使用 Qwen3-VL 系列模型验证。若发现幻觉，则从预构建的词汇表（基于GQA数据集）中检索同语义子类的正确候选词进行替换。
  - **阶段二：自我纠正**
    - **事实纠正**：根据验证结果，删除或替换幻觉元素，生成简洁且无幻觉的响应。
    - **细节丰富**：为避免仅删除错误导致的描述过于简单，引导模型补充缺失的视觉细节。为防止引入新幻觉，采用**循环迭代过滤管道**：丰富后的文本再次进入验证模块，若仍有幻觉则重新生成。7B模型最多循环3次，13B模型最多5次，未通过则丢弃样本。
  - **偏好学习**：将初始的幻觉响应作为不偏好数据 $y^-$，将自我纠正并丰富后的响应作为偏好数据 $y^+$，构成偏好对 $(x, y^+, y^-)$。使用 DPO 损失函数进行优化，公式核心为最大化生成 $y^+$ 的对数概率与生成 $y^-$ 的对数概率之差（通过 sigmoid 函数 $\sigma$ 和参考模型 $\pi_{ref}$ 进行约束）。

### 3. 实验设计：数据集、Benchmark与对比方法
- **数据集**：
  - 训练数据：使用 MS-COCO 训练集作为图像源，构建了 5.2k（7B模型）和 4.6k（13B模型）个偏好对。
  - 扩展评估：GQA 数据集（用于词汇构建和扩展规模实验）。
- **Benchmark**：
  - **Object HalBench**：评估标准对象幻觉（CHAIRs, CHAIRi）。
  - **AMBER**：综合分析生成和判别任务中的幻觉。
  - **MMHal-Bench**：基于 GPT-4 的开放式评估。
  - **MME Benchmark**：评估多模态泛化能力。
  - **POPE**：判别性幻觉评估。
- **对比方法**：VCD（解码干预）、LLaVA-RLHF（PPO强化学习）、HALVA（对比学习）、POVID、oDPO、mDPO、SENTINEL（偏好优化方法）。

### 4. 资源与算力
- **算力资源**：明确指出所有实验均在**单张 NVIDIA RTX A6000 Ada GPU** 上完成。
- **训练设置**：采用 LoRA 微调（rank=128, alpha=256），AdamW 优化器，训练 1 个 epoch。

### 5. 实验数量与充分性
- **实验数量**：
  - 主实验：在 4 个主要 Benchmark 上对比了 7 种基线方法（7B和13B两个规模）。
  - 消融与分析实验：验证策略鲁棒性分析、分布不匹配缓解效果分析、数据规模影响分析（600到10.9k）、两阶段对象验证必要性分析、偏好对质量评估（GPT-4o评判）、多模态评判评估等。
- **充分性与客观性**：实验设计非常充分且客观。不仅涵盖了生成式和判别式多种评估维度，还针对核心创新点（分布不匹配、自纠正有效性）进行了深入的边际分布可视化和对比分析；对于有官方checkpoint的基线方法进行了重新评估，确保了对比的公平性。

### 6. 论文的主要结论与发现
- **高效性与数据效率**：AVES-DPO 仅用 5.2k 样本就超越了现有基线，数据量约为 LLaVA-RLHF 的 1/25，实现了极佳的数据效率。
- **分布对齐的有效性**：实验证明，使用专有模型纠正会导致偏好边际为负（分布偏离），而自纠正使偏好边际呈显著正偏移，证明自生成数据更符合模型内在分布，对齐更有效。
- **细粒度幻觉改善显著**：特别是在“关系”类别上，现有方法往往表现不佳，而 AVES-DPO 在 7B 和 13B 模型上均取得了大幅提升。
- **模型规模的权衡**：7B模型在缓解幻觉的同时增强了多模态泛化能力；但13B模型在抑制幻觉时变得过于保守，导致在依赖外部知识的 MME 基准上性能略有下降。

### 7. 优点
- **切中痛点**：敏锐地发现了依赖专有模型构建偏好数据带来的“分布不匹配”问题，并提出自纠正的解决思路，同时摆脱了对昂贵专有API的依赖。
- **细粒度全覆盖**：突破了以往仅关注“对象有无”的局限，设计了涵盖对象、属性、关系的完整验证与纠正流程。
- **数据质量保障机制**：通过双模型共识验证和循环迭代过滤管道，有效控制了自纠正过程中可能产生的噪声和二次幻觉，保证了偏好对的高质量。

### 8. 不足与局限
- **验证范围的局限**：属性和关系的验证严格限制在单对象级别，未涉及多个对象共现的复杂场景。
- **大模型上的性能权衡**：在13B等更大规模模型上，幻觉抑制与保持广泛预训练知识之间存在更明显的冲突，导致泛化能力轻微下降。
- **自生成数据的潜在风险**：尽管有严格的过滤，但完全基于模型自身能力进行纠正和丰富，可能受限于模型本身的上限，难以纠正模型根本“看不见”的严重幻觉。

（完）
