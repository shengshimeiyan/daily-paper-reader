---
title: "Demystifying Uncertainty in LLMs: Active Calibration between Concepts and Human Evaluations"
title_zh: 揭秘大语言模型中的不确定性：概念与人类评估间的主动校准
authors: "Pengqi Li, Lizhong Ding, Zhehao Zhou, Chunhui Zhang, Jiarun Fu, Hao Li, Ye Yuan, Guoren Wang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.259.pdf"
tags: ["query:llm-halluc"]
score: 8.0
evidence: 通过不确定性校准缓解幻觉
tldr: 针对大语言模型因猜测而非承认潜在不确定性导致幻觉，且现有静态缓解策略未显式建模与外部环境交互信息增益的问题，提出一种交互式设置下的不确定性建模方法。该方法揭示了模型概念与人类评估之间的主动校准机制，通过引导用户提供信息丰富的澄清来主动缓解幻觉。实验证明该机制能有效提升模型在输入欠定情况下的可靠性和有效容量。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.259/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1644, \"height\": 784, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.259/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1497, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.259/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1555, \"height\": 870, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.259/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1643, \"height\": 810, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.259/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 761, \"height\": 572, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.259/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1647, \"height\": 425, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.259/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1115, \"height\": 950, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.259/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1675, \"height\": 589, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.259/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1682, \"height\": 702, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.259/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1683, \"height\": 650, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.259/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1677, \"height\": 757, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.259/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1678, \"height\": 616, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.259/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1679, \"height\": 1106, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.259/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1681, \"height\": 1048, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.259/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1559, \"height\": 960, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.259/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1688, \"height\": 701, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.259/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1673, \"height\": 1843, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.259/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1693, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.259/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1693, \"height\": 198, \"label\": \"Table\"}]"
motivation: 大语言模型常因猜测而非承认不确定性产生幻觉，现有静态缓解策略未显式建模与外部环境交互的信息增益。
method: 在交互式设置中建模LLM的不确定性，揭示模型概念与人类评估间的主动校准机制，引导用户进行信息澄清。
result: 主动校准机制能有效减少模型猜测，提升模型在欠定输入下的可靠性和有效容量。
conclusion: 通过交互式不确定性建模和主动校准，可有效缓解大语言模型的幻觉问题。
---

## Abstract
Hallucinations arise when large language models (LLMs) guess rather than acknowledge their underlying uncertainty. Existing static strategies for mitigating hallucinations have been only partially successful, largely because they do not explicitly model the information gain from interacting with the external environment. Researchers need a general method to proactively steer users toward informative clarifications, thereby unlocking the model’s effective capacity under underspecified inputs. We model the uncertainty of LLMs in interactive settings and uncover the mechanism of active calibration between model concepts and human evaluations, improving reliability. We show that calibration error in LLMs density estimation admits a non-vanishing lower bound under non-interactive learning, while interaction empirically reduces it. We further characterize that calibration error identifies informative queries and that calibration can be accelerated by shifting query distributions from imbalanced to balanced regimes. Guided by these insights, we propose a calibration-driven Interactive Learning Strategy (ILS) that selects clarification queries by optimizing calibration error, providing both theoretical guarantees and empirical gains for reliability. Code and data are available at https://github.com/zhouyeah215/Demystifying_Uncertainty.

---

## 论文详细总结（自动生成）

# 论文总结：揭秘大语言模型中的不确定性：概念与人类评估间的主动校准

## 1. 核心问题与整体含义（研究动机和背景）
*   **核心问题**：大语言模型（LLMs）常因“猜测”而非承认其潜在的不确定性而产生幻觉。现有的静态缓解策略仅取得部分成功，因为它们没有显式建模与外部环境交互所带来的信息增益。
*   **整体含义**：为了提升模型在输入欠定情况下的可靠性和有效容量，需要一种通用的方法，使模型能够主动引导用户提供信息丰富的澄清，从而在交互中校准模型的不确定性，而非仅仅被动输出单一置信度数值。

## 2. 论文提出的方法论
*   **核心思想**：提出一种“主动校准”框架，将LLM的不确定性建模为交互式设置下的概念与人类评估之间的对齐过程。通过最大化校准误差来选择最具信息量的澄清问题，并通过课程学习调度查询分布以加速校准。
*   **关键技术细节**：
    *   **不确定性分解**：将不确定性分为偶然不确定性（Aleatoric, Ale，数据内在随机性）和认知不确定性（Epistemic, Epi，模型能力限制）。
    *   **校准误差**：定义为模型预测分布 $\pi_\theta$ 与目标分布 $p$ 之间的距离（如JS散度或总变差距离），衡量模型密度估计的不匹配程度。
    *   **单事实率**：训练数据中仅出现一次的事实比例。定理1证明，在非交互式学习中，校准误差存在由MFR控制的非消失下界，即不交互就无法消除校准误差。
    *   **查询分布转移**：定理2证明，为了最小化MFR，早期应从不平衡的自然分布采样，后期应转向平衡分布。
*   **算法流程（ILS, Interactive Learning Strategy）**：
    1.  给定欠定查询 $x$，LLM生成候选澄清问题集 $C_t$。
    2.  从调度分布 $q_t(x) \propto \mu(x)^{\beta(t)}$ 中采样候选集（$\beta(t)$ 随交互轮数单调递增，实现从不平衡到平衡的过渡）。
    3.  计算每个候选问题的校准误差 $D_t(x) = Cal_x(\pi_\theta, p)$。
    4.  选择校准误差最大的问题 $x_t$ 询问人类。
    5.  获取人类回答 $y_t$，通过上下文更新模型参数 $\theta_{t+1}$，进入下一轮。

## 3. 实验设计
*   **数据集/场景**：
    *   **n-gram模拟**：基于IMDb语料库构建的六元组数据，用于受控验证定理1。
    *   **交互式推理**：AR-Bench（侦探案件 DC，情境谜题 SP）。
    *   **自由形式生成QA**：AmbigQA，构建的模糊版HotpotQA。
    *   **迁移任务**：TruthfulQA（事实QA），ToolBench（工具使用）。
*   **Benchmark/评估指标**：
    *   校准误差（Cal，基于JS散度或语义聚类构建的分布距离）。
    *   认知不确定性（Epi，基于语义熵）。
    *   偶然不确定性（Ale，基于错误率）。
    *   有效解率。
*   **对比方法**：
    *   **Random**：从候选集中均匀随机采样问题。
    *   **SelfSelect**：让LLM自己从候选集中选择最佳后续问题。

## 4. 资源与算力
*   论文中**未明确说明**所使用的GPU型号、数量及训练/推理时长等算力细节。

## 5. 实验数量与充分性
*   **实验数量**：
    *   1组n-gram受控模拟实验。
    *   6个不同LLM基座（Qwen2.5-7/14/32B, LLaMA3-8B, DeepSeek-R1, GPT-4o）在2个交互推理任务上的测试。
    *   2个基座模型在2个模糊QA任务上的主实验。
    *   1个基座模型在2个迁移任务上的测试。
    *   超参数敏感性分析（候选集大小 $M$）。
*   **充分性与客观性**：实验设计较为充分，涵盖了从理论验证到多场景应用，且对比了不同规模和架构的模型；评估指标全面，不仅看最终准确率，更关注不确定性和校准误差的收敛过程；对比基线公平，使用相同的提示词和候选集生成策略。

## 6. 论文的主要结论与发现
*   **理论发现**：非交互设置下，LLM的校准误差存在由单事实率（MFR）决定的非消失下界；交互可以打破这一下界。
*   **实证发现**：多轮交互能持续降低校准误差和不确定性；收敛速度越快的模型，其渐近校准误差越低。
*   **方法有效性**：校准误差能有效定位最具信息量的查询；ILS通过最大化校准误差选择问题和调度查询分布，比随机选择或模型自选择收敛更快，且在多种任务中均表现出鲁棒的增益。

## 7. 优点
*   **理论深刻**：从计算学习理论和Good-Turing估计出发，严格证明了非交互校准误差的下界，为交互式学习的必要性提供了理论保障。
*   **视角新颖**：将不确定性量化从静态的数值评估转变为动态的“主动校准”过程，利用校准误差作为信息增益的指标来指导提问。
*   **策略实用**：ILS算法结合了校准误差最大化和课程学习式的分布调度，既有理论支撑又具有工程落地性。

## 8. 不足与局限
*   **人类模拟偏差**：实验依赖LLM（如Qwen2.5-7B）模拟人类/先知回答，可能因模型自身能力限制导致中间交互失败或偏差，无法完全反映真实人机交互的复杂性。
*   **评估范围有限**：作者在Limitations中承认，当前评估范围仍显不足，缺乏更广泛的收敛性诊断和消融研究（如不同调度策略和不确定性估计器的影响）。
*   **系统级扩展缺失**：目前仅关注独立LLM，未扩展到包含事实核查组件的多智能体系统。
*   **资源透明度低**：未报告算力消耗，难以评估该交互式策略在实际部署中的计算成本。

（完）
