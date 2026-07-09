---
title: "PretrainRL: Alleviating Factuality Hallucination of Large Language Models at the Beginning"
title_zh: PretrainRL：从源头缓解大语言模型的事实幻觉
authors: "Langming Liu, Kangtao Lv, Haibin Chen, Weidong Zhang, Yejing Wang, Shilei Liu, Xin Tong, Yujin Yuan, Yongwei Wang, Wenbo Su, Bo Zheng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.910.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 缓解大语言模型的事实幻觉
tldr: 大语言模型的事实幻觉源于预训练语料库的数据分布不平衡，导致低概率真相和高概率谬误。本文提出PretrainRL框架，将强化学习融入预训练阶段，通过先去偏再学习的原则巩固事实知识并重塑数据分布。实验表明，PretrainRL从根源上缓解了事实幻觉，避免了后处理方法的灾难性遗忘问题，为幻觉缓解提供了新路径。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.910/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 771, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.910/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 645, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.910/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1650, \"height\": 812, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.910/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 804, \"height\": 368, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.910/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.910/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 254, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.910/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 804, \"height\": 759, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.910/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 798, \"height\": 201, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.910/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 789, \"height\": 726, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.910/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 788, \"height\": 494, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.910/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 796, \"height\": 1045, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.910/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 800, \"height\": 279, \"label\": \"Table\"}]"
motivation: 大语言模型的事实幻觉源于预训练语料库的数据分布不平衡，导致低概率真相和高概率谬误。
method: 提出PretrainRL框架，将强化学习融入预训练阶段，通过先去偏再学习重塑数据分布。
result: PretrainRL从根源上缓解了事实幻觉，避免了后处理方法的灾难性遗忘问题。
conclusion: 在预训练阶段引入强化学习重塑数据分布，是从根源上缓解大模型事实幻觉的有效方法。
---

## Abstract
Large language models (LLMs), despite their powerful capabilities, suffer from factual hallucinations where they generate verifiable falsehoods. We identify a root of this issue: the imbalanced data distribution in the pretraining corpus, which leads to a state of "low-probability truth" and "high-probability falsehood". Recent approaches, such as teaching models to say "I don’t know" or post-hoc knowledge editing, either evade the problem or face catastrophic forgetting. To address this issue from its root, we propose PretrainRL, a novel framework that integrates reinforcement learning into the pretraining phase to consolidate factual knowledge. The core principle of PretrainRL is "debiasing then learning." It actively reshapes the model’s probability distribution by down-weighting high-probability falsehoods, thereby making "room" for low-probability truths to be learned effectively. To enable this, we design an efficient negative sampling strategy to discover these high-probability falsehoods and introduce novel metrics to evaluate the model’s probabilistic state concerning factual knowledge. Extensive experiments on three public benchmarks demonstrate that PretrainRL significantly alleviates factual hallucinations and outperforms state-of-the-art methods.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLMs）在生成内容时存在严重的事实幻觉，即产生可验证的错误事实。
- **深层原因**：论文指出事实幻觉的根源在于预训练语料库中**数据分布的不平衡**。高频的“头部知识”在下一词预测（NTP）目标中占据主导，导致模型走捷径，将条件概率$P(o|s, p; \theta)$退化为边缘概率$P(o|p; \theta)$。这造成了“低概率真相”与“高概率谬误”并存的概率错位现象。
- **现有方法的局限**：现有的应对策略（如教导模型回答“我不知道”或事后知识编辑）要么只是掩盖问题（导致模型过度拒绝回答），要么面临严重的灾难性遗忘和可扩展性差的问题。
- **整体含义**：必须从预训练阶段这一根源入手，通过重塑模型的概率分布来缓解事实幻觉，而非依赖后处理手段。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：“先去偏再学习”。即在预训练阶段引入强化学习，先降低高概率谬误的权重以“腾出空间”，再有效学习低概率真相。
- **负采样策略**：
  - 为了获取DPO所需的被拒绝样本（即高概率谬误），论文提出使用束搜索解码。
  - 给定知识三元组$(s, p, o)$，将$s, p$输入基础模型，通过束搜索获取多个候选答案及其累积概率，过滤掉真实答案$o$后，按概率排序选取Top-K作为负样本。
  - 该方法直接反映了模型内在的头部知识偏好，且无需访问原始语料库计算词频。
- **优化时机与方法**：
  - **时机**：选择在持续预训练阶段执行，因为此阶段模型具有更好的可塑性，而后训练阶段的模型知识已“僵化”，强行注入知识易导致崩溃。
  - **方法**：采用直接偏好优化（DPO）进行概率重塑。
- **目标函数**：
  - 最终损失函数为DPO损失与标准下一词预测（NTP/NLL）损失的加权和：$L_{PretrainRL} = L_{DPO} + \lambda L_{CT}$
  - $L_{DPO}$：以真实答案为获胜样本，负采样答案为失败样本，通过偏好优化降低谬误概率。
  - $L_{CT}$：作为正则化项，锚定模型分布以维持核心语言能力，并主动提升真实答案的绝对概率。
- **评估指标**：引入了三个基于束搜索的新指标来全面评估概率状态：HR@k（命中率，衡量多样性）、MRR@k（平均倒数排名，平衡概率与命中率）、Prob@k（生成正确答案的条件概率，衡量置信度）。

### 3. 实验设计：数据集、Benchmark与对比方法
- **数据集**：POPQA（13k）、Wikidata-knowledge infusion（16k）、EntityQuestions（1.75M），均具有显著的长尾分布特征。
- **评估Benchmark**：
  - 事实性评估：上述三个数据集的ACC, HR, MRR, Prob指标（束大小k=50）。
  - 通用能力评估：CEval, MMLU, MATH, GSM8K, BBH，使用OpenCompass平台。
- **对比方法**：
  - 开源基线：Chain-of-Thought (CoT)、标准DPO、Continual Training (CT)、Iterative RPO。
  - 闭源大模型：GPT-4o, Claude-sonnet4, Deepseek-v3, Deepseek-R1。

### 4. 资源与算力
- **算力资源**：所有实验均在 **8张 H800 GPU** 上进行。
- **训练时长**：论文中**未明确说明**具体的训练时长。

### 5. 实验数量与充分性
- **实验数量**：
  - 主实验：3个数据集 × 3个基础模型（Qwen3-4B/8B, Llama3-8B）。
  - 扩展性实验：模型规模扩展（Qwen3-14B）、数据规模扩展（EntityQuestions 1.75M）。
  - 消融实验：损失函数消融（w/o NTP, w/o DPO）、采样策略对比（基于流行度采样 vs 本文采样）。
  - 泛化性实验：5个通用能力Benchmark。
  - 其他分析：Base模型与Instruct模型的对比、案例研究。
- **充分性与客观性**：实验设计非常充分且客观。不仅验证了方法在多种模型架构和不同规模数据集上的有效性，还通过详尽的消融实验证明了每个模块的不可替代性。特别是引入通用能力测试，有力地反驳了“知识注入损害通用能力”的潜在质疑。对比方法使用了相同超参数，保证了公平性。

### 6. 论文的主要结论与发现
- PretrainRL从根源上显著缓解了事实幻觉，在长尾知识数据集上的表现大幅超越了现有的开源基线方法，甚至优于参数量更大、具备高级推理能力的闭源模型。
- 单纯的DPO（w/o NTP）虽能提升正确答案概率，但会降低准确率；单纯的CT（w/o DPO）能巩固知识但会抑制其他知识。PretrainRL通过两者结合完美实现了权衡。
- 基础模型比指令微调模型具有更大的“可学习空间”，更适合进行知识重塑。
- PretrainRL在大幅提升事实准确率的同时，不会导致模型通用能力的下降（未发生灾难性遗忘），而传统的SFT则会导致通用能力严重崩溃。

### 7. 优点
- **视角深刻**：直击幻觉的预训练根源（数据不平衡导致的概率退化），而非停留在后处理的修修补补。
- **机制巧妙**：“先去偏再学习”的思路结合DPO+NTP的混合损失函数，既解决了“腾空间”的问题，又避免了模式崩溃。
- **高效实用**：负采样策略利用模型自身生成偏好，避免了昂贵的语料库词频统计；且在持续预训练阶段实施，计算开销可控。
- **评估全面**：针对基础模型生成概率的特点，引入HR/MRR/Prob指标，比单一的准确率更能反映模型内部知识掌握的真实状态。

### 8. 不足与局限
- **数据集依赖**：负采样策略依赖于数据集能够提供有意义的“问题类别”划分。如果数据集缺乏这种区分度，该采样策略的效率会下降，需退回到其他方法（如RLVR）。
- **幻觉类型覆盖有限**：本文仅针对基于知识图谱三元组的“事实性幻觉”进行了解决，对于逻辑相关或指令相关的幻觉未涉及。
- **计算开销未透明化**：虽然说明了硬件配置，但未报告束搜索生成负样本以及PretrainRL训练的实际时间开销，使得对其计算成本效益的评估不够完整。

（完）
