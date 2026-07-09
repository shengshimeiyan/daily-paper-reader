---
title: Principled Detection of Hallucinations in Large Language Models via Multiple Testing
title_zh: 基于多重检验的大语言模型幻觉原则性检测
authors: "Jiawei Li, Akshayaa Magesh, Venugopal Veeravalli"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1705.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 将幻觉检测形式化为假设检验问题
tldr: 针对现有大语言模型幻觉检测经验评分规则性能不一且难以依赖的问题，将幻觉检测形式化为假设检验问题，并与分布外检测建立联系。提出了一种基于多重检验的幻觉检测方法，为不同模型和数据集提供了更可靠、更有原则的幻觉检测方案。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1705/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 746, \"height\": 1183, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1705/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 737, \"height\": 531, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 778, \"height\": 590, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1500, \"height\": 737, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 805, \"height\": 309, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 811, \"height\": 572, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 809, \"height\": 603, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 812, \"height\": 603, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 811, \"height\": 421, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 809, \"height\": 422, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 809, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 809, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 814, \"height\": 527, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 810, \"height\": 509, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 809, \"height\": 523, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1705/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 806, \"height\": 255, \"label\": \"Table\"}]"
motivation: 现有幻觉检测经验评分规则性能不一，缺乏可靠且有原则的检测方法。
method: 将幻觉检测形式化为假设检验问题，借鉴分布外检测思路，提出多重检验方法。
result: 提供了更可靠、有原则的幻觉检测方案，克服了经验规则的局限性。
conclusion: 基于多重检验的原则性检测方法能有效提升大语言模型幻觉检测的可靠性。
---

## Abstract
While Large Language Models (LLMs) have emerged as powerful foundational models to solve a variety of tasks, they have also been shown to be prone to hallucinations, i.e., generating responses that sound confident but are actually incorrect or even nonsensical. Existing hallucination detectors propose a wide range of empirical scoring rules, but their performance varies across models and datasets, and it is hard to determine which ones to rely on in practice or to treat as a reliable detector. In this work, we formulate the problem of detecting hallucinations as a hypothesis testing problem and draw parallels with the problem of out-of-distribution detection in machine learning models. We then propose a multiple-testing-inspired method that systematically aggregates multiple evaluation scores via conformal p-values, enabling calibrated detection with controlled false alarm rate. Extensive experiments across diverse models and datasets validate the robustness of our approach against state-of-the-art methods.

---

## 论文详细总结（自动生成）

# 基于多重检验的大语言模型幻觉原则性检测

## 1. 核心问题与整体含义
- **核心问题**：大语言模型（LLM）容易产生“幻觉”（即生成听起来自信但实际错误或无意义的回答）。现有的幻觉检测方法多基于经验性评分规则，但这些规则在不同模型和数据集上的表现差异巨大，难以在实践中确定哪种方法可靠。
- **整体含义**：本文旨在为LLM幻觉检测提供一个具有统计学原则性、可靠且鲁棒的通用框架。通过将幻觉检测建模为假设检验问题，并借鉴分布外（OOD）检测的思路，系统性地整合多种现有评估指标，从而在控制误报率的前提下实现校准检测。

## 2. 方法论
- **核心思想**：将幻觉检测重构为多重假设检验问题。零假设 $H_0$ 为“提示不太可能产生幻觉”，备择假设 $H_1$ 为“提示可能产生幻觉”。通过整合多个基线检测器的分数，只要其中任何一个零假设被拒绝，就判定为幻觉。
- **关键技术细节**：
  - **共形p值**：由于零假设下的分数分布未知，利用一个仅包含非幻觉提示的校准集 $C$ 来计算经验p值。
  - **多重检验流程**：基于允许分数依赖的Benjamini-Hochberg (BH) 程序。计算测试样本的共形p值后，将其与排序后的阈值进行比较，以决定是否拒绝全局零假设。
  - **校准集构建**：使用Rouge-L相似度对生成结果与参考答案进行比较，若大部分生成结果被视为非幻觉，则将该提示加入校准集。
- **算法流程（Algorithm 1）**：
  1. 对于每个基线评分函数 $j$，计算测试提示的分数 $t_{test}^j$；
  2. 利用校准集计算共形p值 $q_{con}^j = \frac{1 + |\{i: t_{test}^j \le s_i^j\}|}{1 + |C|}$；
  3. 将p值升序排列；
  4. 若存在某个 $j$ 满足 $\hat{q}_{con}^j \le \frac{\alpha}{(1+\epsilon)\sum_{i=1}^K \frac{1}{i}} \cdot \frac{j}{K}$，则判定为“幻觉”，否则为“无幻觉”。
- **理论保证**：当校准集足够大时，算法的误报率在概率 $1-\delta$ 下被限制在 $\alpha$ 以内。

## 3. 实验设计
- **数据集**：HaluEval, CoQA, TriviaQA, GSM8K。
- **模型**：LLaMA-2-13B, Mistral-7B, Llama-3.1-8B, DeepSeek-v2-Lite, Qwen3-4B, Llama-3.2-3B-Instruct, Qwen2.5-Math-1.5B-Instruct。
- **Benchmark/评估指标**：
  - AUROC（受试者工作特征曲线下面积）；
  - 检测力（Detection Power，在10%误报率下的检测概率）。
- **对比方法**：
  - 基线评分：语义熵（SE）、Alpha语义熵（αSE）、核语义熵（KSE）、聚类SE、Alpha聚类SE、谱特征值、词汇相似度（LS）。
  - 聚合策略：多数投票、平均。

## 4. 资源与算力
- **GPU型号与数量**：主要使用单张 L40S GPU，LLaMA-2-13B 使用了两张 L40S GPU。
- **训练/推理时长**：采样生成和计算分数大约需要3天时间（可通过并行计算加速）；提取token概率需要数小时，计算各版本语义熵/谱特征值/词汇相似度各需1小时内；而本文提出的多重检验框架本身运行时间不到0.1秒。

## 5. 实验数量与充分性
- **实验数量**：
  - 主实验：4个数据集 × 4个主模型 × 7个基线 + 2个聚合策略。
  - 扩展实验：在GSM8K上测试了2个数学模型，在CoQA上测试了Qwen3-4B推理模型。
  - 消融/分析实验：不同标注协议（Rouge-L vs. LLM-as-a-judge）、不同校准集大小（1000, 2000, 3000）、混合校准集、不同相似度阈值 $\tau$ 和容忍度 $\theta$ 的敏感性分析。
- **充分性与客观性**：实验非常充分。覆盖了不同规模和架构的模型、不同类型的任务（对话QA、常识QA、数学推理）。对比方法包含了当前主流的无训练/无检索检测方法，且所有方法基于相同的采样生成结果进行评估，保证了公平性。

## 6. 主要结论与发现
- 本文方法在大多数模型-数据集组合中取得了最优或次优的AUROC和检测力，宏观平均AUROC在所有评估套件中最高。
- 单一基线指标表现极不稳定（如LS在Llama标注下大幅下降，SE变体在GSM8K上表现极差），而本文的框架能够有效整合异构信号，即使部分基线退化，也能保持鲁棒。
- 简单的聚合策略（如平均、多数投票）容易受表现差的分数拖累，而多重检验方法能系统性地管理依赖关系并接近最佳基线表现。
- 框架对校准集大小不敏感（1000到2000提升有限），且在混合不同分布的校准集下性能仅微小波动。

## 7. 优点
- **原则性与理论保证**：首次将幻觉检测形式化为多重假设检验问题，提供了误报率的理论上界控制，摆脱了经验性阈值的随意性。
- **通用性与轻量级**：框架与模型和数据集无关，无需额外训练或外部知识库，且聚合步骤计算开销极小（<0.1s）。
- **鲁棒性强**：能够自适应地利用最可靠的信号，克服了单一指标在不同场景下泛化能力差的问题。

## 8. 不足与局限
- **标注依赖**：校准集的构建依赖于Rouge-L或LLM-as-a-judge进行幻觉标注，标注质量直接影响检测上限，且Rouge-L对语义重述的捕捉能力有限。
- **任务覆盖**：虽然测试了数学推理，但对于更复杂的推理场景（如智能体任务、复杂数学证明）的评估仍显不足。
- **基线依赖**：该方法本质上是一种聚合策略，其性能下界受限于所使用的基线分数。如果所有基线分数都毫无意义，该框架也无法凭空创造优秀的检测能力。

（完）
