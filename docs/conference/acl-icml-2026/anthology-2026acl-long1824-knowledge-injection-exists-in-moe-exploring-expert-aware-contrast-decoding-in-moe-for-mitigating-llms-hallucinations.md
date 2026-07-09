---
title: Knowledge Injection Exists in MoE? Exploring Expert-Aware Contrast Decoding in MoE for Mitigating LLMs’ Hallucinations
title_zh: MoE中存在知识注入？探索专家感知对比解码以缓解大模型幻觉
authors: "Xinyue Fang, Zhiliang Tian, Zhen Huang, Ziyi Pan, Zhihua Wen, Xi Wang, Quntian Fang, Dongsheng Li"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1824.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 通过专家感知对比解码缓解大模型幻觉
tldr: 现有缓解大模型幻觉的对比解码方法仅探索了基于Transformer的模型，忽略了混合专家等有效框架。本文通过实证研究探究了MoE中是否存在类似的层间差异，发现共享专家中不存在该差异，但不同MoE的高层专家表现出显著差异。基于此，提出专家感知对比解码方法，利用高层专家的显著差异来缓解幻觉，为MoE架构的幻觉缓解提供了有效方案。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 912, \"height\": 693}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 912, \"height\": 693}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-003.webp\", \"caption\": \"\", \"page\": 3, \"index\": 3, \"width\": 912, \"height\": 693}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-004.webp\", \"caption\": \"\", \"page\": 3, \"index\": 4, \"width\": 912, \"height\": 693}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-005.webp\", \"caption\": \"\", \"page\": 12, \"index\": 5, \"width\": 1375, \"height\": 704}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-006.webp\", \"caption\": \"\", \"page\": 12, \"index\": 6, \"width\": 980, \"height\": 821}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-007.webp\", \"caption\": \"\", \"page\": 12, \"index\": 7, \"width\": 980, \"height\": 821}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-008.webp\", \"caption\": \"\", \"page\": 12, \"index\": 8, \"width\": 980, \"height\": 821}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-009.webp\", \"caption\": \"\", \"page\": 12, \"index\": 9, \"width\": 980, \"height\": 821}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-010.webp\", \"caption\": \"\", \"page\": 12, \"index\": 10, \"width\": 1367, \"height\": 700}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-011.webp\", \"caption\": \"\", \"page\": 12, \"index\": 11, \"width\": 1367, \"height\": 693}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-012.webp\", \"caption\": \"\", \"page\": 13, \"index\": 12, \"width\": 1375, \"height\": 704}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-013.webp\", \"caption\": \"\", \"page\": 17, \"index\": 13, \"width\": 621, \"height\": 616}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.1824/fig-014.webp\", \"caption\": \"\", \"page\": 17, \"index\": 14, \"width\": 621, \"height\": 616}]"
motivation: 现有缓解幻觉的对比解码方法仅关注Transformer，未探索混合专家模型中的层间差异。
method: 探究MoE中的层间差异，提出专家感知对比解码方法以缓解大模型幻觉。
result: 发现MoE高层专家存在显著差异，利用该特性的方法有效缓解了大模型幻觉。
conclusion: 专家感知对比解码方法为MoE架构的大模型幻觉缓解提供了有效方案。
---

## Abstract
Existing LLM hallucination mitigation methods, including prompt engineering and model optimization, either hardly alter models’ internal knowledge or have poor cross-domain generalization. Contrastive decoding mitigates hallucinations by using layer-wise differences in LLMs. However, prior studies only explore transformer-based models (e.g., GPT), ignoring other effective frameworks like mixture-of-experts (MoE) models. Since MoE alters the traditional transformer architecture, we conduct empirical studies to investigate whether similar layer-wise differences exist in MoEs. Our results show that they do not exist in MoE with shared experts; nevertheless, across different MoEs, higher layers exhibit distinct expert activation patterns between factual and non-factual outputs. Building on these, we propose EAACD, an expert-aware adaptive contrast decoding that uses expert differences in MoE’s higher layers to mitigate hallucinations on QA tasks. EAACD splits high-layer experts into a higher-reliability group and several lower-reliability groups based on their confidence and consistency. It contrasts the higher-reliability group’s prediction with each lower-reliability group’s prediction to calibrate the model’s original predictions. To strengthen this contrast, EAACD amplifies hallucinations from lower-reliability experts via attention and masking to provide stronger negative references. EAACD outperforms all baselines on four datasets

---

## 论文详细总结（自动生成）

# 论文总结：MoE中存在知识注入？探索专家感知对比解码以缓解大模型幻觉

## 1. 核心问题与整体含义
*   **研究动机**：现有的基于对比解码的大模型（LLM）幻觉缓解方法（如DoLa）主要依赖于传统Transformer架构中的“知识注入”现象（即高层比低层包含更多事实知识，层间存在显著差异）。然而，混合专家模型作为当前主流的LLM架构，其结构与传统Transformer不同，直接套用现有方法面临挑战。
*   **核心问题**：MoE模型中是否也存在类似的层间“知识注入”现象？如果不存在，如何利用MoE特有的内部差异来进行对比解码以缓解幻觉？
*   **整体含义**：本文首次深入探究了MoE架构内部的知识分布与激活差异，揭示了“知识注入”现象与MoE架构类型的相关性，并基于MoE高层专家在事实/非事实输出下的激活差异，提出了一种无需外部资源的专家感知对比解码方法，为MoE模型的幻觉缓解提供了新范式。

## 2. 方法论
*   **核心思想**：利用MoE模型高层中不同专家在生成事实与非事实输出时的激活模式差异，将专家划分为高可靠性与低可靠性组，通过放大低可靠性专家的幻觉作为负参考，与高可靠性专家的预测进行对比，从而校准模型输出。
*   **关键技术细节与流程**：
    1.  **专家划分**：
        *   **聚类**：在最后层收集所有专家的logits，计算相似度矩阵并使用层次聚类将专家分为多个组。
        *   **可靠性评估**：结合**置信度**（由预测熵和logits的L2范数自适应加权计算）和**一致性**（组内专家数量占比）计算每个组的可靠性得分。得分最高的为高可靠性组，其余为低可靠性组。
        *   **预测融合**：使用路由器的门控值对高可靠性组内的专家logits进行加权求和，得到高可靠性预测 $p_r$。
    2.  **注意力引导的幻觉放大**：
        *   利用注意力机制识别对预测影响最大的上下文token（计算最后一层所有头的平均注意力权重作为重要性得分）。
        *   掩码掉重要性得分超过阈值 $\beta$ 的token，重新输入给低可靠性专家。
        *   缺失关键上下文会迫使低可靠性专家产生更多幻觉，从而提供更强的负参考 $\tilde{l}_w$。
    3.  **自适应专家组对比解码**：
        *   **自适应惩罚系数**：计算高可靠性组质心与每个低可靠性组质心之间的KL散度 $G_j$，并将其归一化作为惩罚系数 $\alpha_j$。差异越大，惩罚越重。
        *   **对比与校准**：融合低可靠性组logits得到 $p_l$，对比结果为 $p' = p_r - p_l$。最后，利用模型原始预测的熵作为不确定性权重 $\lambda$，动态调整校准强度，最终预测为 $p_f = \text{softmax}((1-\lambda) p_o + \lambda p')$。

## 3. 实验设计
*   **数据集**：使用了4个主流QA数据集，包括 FACTOR (Expert-FACTOR, News-FACTOR, Wiki-FACTOR), HellaSwag, StrategyQA 和 MathQA。
*   **Benchmark**：主要评估指标为准确率。
*   **对比方法**：
    *   解码方法：Greedy, Contrastive Decoding (CD), DoLa, SCMoE, END。
    *   非解码方法：Self-Endorsement。
*   **实验模型**：LLaMA-MoE（无共享专家）和 Qwen-MoE（有共享专家）。

## 4. 资源与算力
*   论文主要提出一种推理阶段的解码策略，无需训练。
*   **算力说明**：文中仅在附录F中提及使用 **GPU A100** 进行延迟和显存开销的测试，但**未明确说明**进行完整评估所需的具体GPU数量、集群规模或总推理时长。

## 5. 实验数量与充分性
*   **实验数量**：
    *   主实验：2种MoE架构 × 6个数据集子集 × 7种方法。
    *   消融实验：移除一致性、置信度、评估模块、注意力放大模块共4组。
    *   分析实验：专家可靠性分析、显著性检验、延迟/显存开销对比、案例研究、阈值 $\beta$ 分析等。
*   **充分性与客观性**：实验设计非常充分。覆盖了不同类型的MoE架构（有/无共享专家）和多种QA场景（常识、数学、事实核查）；消融实验详尽验证了各模块贡献；显著性检验确保了结果的统计可靠性；与专门针对MoE的SCMoE方法进行开销对比体现了公平性。

## 6. 主要结论与发现
*   **“知识注入”的架构依赖性**：MoE中的“知识注入”现象取决于架构。它仅存在于**无共享专家**的MoE中（如LLaMA-MoE, Mixtral），而在**有共享专家**的MoE中（如Qwen-MoE, DeepSeek-MoE）不存在。这导致传统基于层间差异的对比解码（如DoLa）在共享专家MoE上表现极差。
*   **专家激活差异的普遍性**：在所有MoE架构中，高层专家在生成事实与非事实输出时表现出显著不同的激活模式。
*   **方法有效性**：EAACD在所有数据集上均超越了现有基线，特别是在Qwen-MoE上的HellaSwag数据集上，比最强基线提升了近13%。
*   **模块贡献**：置信度比一致性对专家可靠性评估更关键；注意力引导的幻觉放大机制能有效提升对比解码的效果。

## 7. 优点
*   **洞察深刻**：首次揭示并验证了“知识注入”现象在MoE中的架构依赖性，解释了为何现有方法在部分MoE上失效。
*   **针对性强**：巧妙利用了MoE特有的“专家激活差异”替代传统的“层间差异”，设计了完全适配MoE的对比解码方案。
*   **机制创新**：提出“幻觉放大”机制，通过掩码关键注意力token主动诱导低可靠性专家犯错，解决了对比解码中负参考可能正确的问题。
*   **即插即用**：无需额外训练或外部资源，可直接应用于推理阶段。

## 8. 不足与局限
*   **架构泛化风险**：方法高度依赖MoE架构中的专家路由与激活机制。论文自身也承认，如果未来MoE不再是主流架构，该方法的直接适用性将受限。
*   **推理开销**：虽然与SCMoE相比开销增加可控（延迟增加10%-26%，显存增加9%-14%），但相比最简单的贪心解码，仍存在额外的计算负担。
*   **安全风险**：幻觉放大模块在生成更强负参考的同时，可能在某些极端情况下引入不可控的生成风险（作者建议在实际部署中结合知识库进行事后验证或限制在沙盒环境中使用）。

（完）
