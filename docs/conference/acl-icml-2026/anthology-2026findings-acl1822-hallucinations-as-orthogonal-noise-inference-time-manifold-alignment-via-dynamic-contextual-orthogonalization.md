---
title: "Hallucinations as Orthogonal Noise: Inference-Time Manifold Alignment via Dynamic Contextual Orthogonalization"
title_zh: 幻觉作为正交噪声：通过动态上下文正交化进行推理时流形对齐
authors: "Mingkuan Zhao, Wentao Hu, Tianchen Huang, Yuheng Min, Suquan Chen, Yide Gao, Yanbo Zhai, Shuangyong Song (宋双永), Xuelong Li"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1822.pdf"
tags: ["query:llm-halluc"]
score: 9.0
evidence: 通过流形对齐缓解幻觉
tldr: 大模型中与上下文事实不一致的幻觉严重影响了部署可靠性。本文基于线性表示假设提出一种几何框架，认为幻觉表现为相对于残差流语义流形的正交噪声，即特定注意力头引入了与上下文子空间正交的分量。基于此，提出一种基于动态上下文正交化的推理时流形对齐方法，通过抑制这些正交分量来缓解幻觉，为推理时幻觉缓解提供了有效途径。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1822/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 800, \"height\": 792, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1822/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1323, \"height\": 729, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1822/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 752, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1822/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1645, \"height\": 852, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1822/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 755, \"height\": 348, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.1822/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 683, \"height\": 911, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1822/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1583, \"height\": 644, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1822/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1187, \"height\": 651, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.1822/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1253, \"height\": 681, \"label\": \"Table\"}]"
motivation: 大模型生成的幻觉内容与上下文事实不一致，严重影响了其部署可靠性。
method: 提出将幻觉视为语义流形上的正交噪声，并通过动态上下文正交化抑制该噪声。
result: 该方法在推理时有效对齐了语义流形，显著缓解了大模型的幻觉现象。
conclusion: 基于几何框架的动态正交化方法为推理时缓解大模型幻觉提供了有效途径。
---

## Abstract
Hallucination in Large Language Models (LLMs)—characterized by the generation of content inconsistent with contextual facts or logical constraints—remains a persistent challenge for reliable deployment. In this work, we address this issue through a geometric framework rooted in the linear representation hypothesis. We propose that hallucinations manifest as orthogonal noise relative to the semantic manifold of the residual stream. Specifically, we hypothesize that while attention heads ideally propagate information congruent with the context subspace, hallucinations arise when specific heads introduce components orthogonal to this subspace, disrupting the coherence of the latent representation. Based on this formulation, we introduce Dynamic Contextual Orthogonalization (DCO), an inference-time intervention method. DCO utilizes the input residual stream as a dynamic context anchor to perform orthogonal decomposition on attention head outputs. To distinguish between context-aligned semantic updates and divergent noise, DCO employs a layer-wise Z-score suppression mechanism that selectively attenuates outlier orthogonal components based on statistical distributions. Evaluations on Llama-3-8B and 70B across benchmarks such as XSum, NQ-Swap, and IFEval demonstrate that DCO achieves superior contextual faithfulness compared to state-of-the-art intervention baselines. Furthermore, DCO maintains high performance on knowledge-intensive tasks like TriviaQA and TruthfulQA, effectively mitigating the trade-off between hallucination suppression and parametric knowledge retention often observed in existing methods. Our findings validate the geometric interpretation of hallucinations and establish DCO as a computationally efficient approach for enforcing manifold alignment.Our code is available at https://anonymous.4open.science/r/DCO-4AB0

---

## 论文详细总结（自动生成）

# 论文总结：幻觉作为正交噪声：通过动态上下文正交化进行推理时流形对齐

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）在生成内容时经常出现与上下文事实或逻辑约束不一致的“幻觉”，这严重阻碍了模型在高可靠性要求场景下的部署。
- **整体含义与动机**：现有的幻觉缓解策略（如RAG或对比解码）多在输出概率层面操作，缺乏对模型内部表征动态变化的机制性理解。本文从几何视角出发，基于“线性表示假设”，提出幻觉并非仅仅是表层的统计异常，而是模型潜空间中的几何失准。具体而言，当模型处理冲突或模糊上下文时，特定注意力头会引入偏离上下文语义流形的“正交噪声”，导致生成轨迹偏离事实。

## 2. 方法论：核心思想、关键技术细节与算法流程
- **核心思想**：提出动态上下文正交化，一种推理时干预方法。将幻觉视为相对于残差流语义流形的正交噪声，通过动态构建上下文锚点，对注意力头输出进行正交分解，并利用基于统计分布的Z-score机制自适应抑制异常的正交分量。
- **关键技术细节与算法流程**：
  1. **上下文锚点构建**：取第 $L$ 层的输入残差流 $x_{in}^L$，对其进行RMSNorm归一化得到单位参考向量 $c$，作为当前语义一致性的方向锚点（公式1）。
  2. **子空间正交分解**：对于第 $h$ 个注意力头的输出 $o_h$，将其分解为与锚点对齐的共振分量 $o_{h\parallel}$（通过投影计算，公式2）和与锚点正交的噪声分量 $o_{h\perp}$（通过向量排斥计算，公式3）。定义正交性指标 $\rho_h$ 为正交分量模长与总模长的比值（公式4），$\rho_h$ 趋近1表示该头引入了高度独立的偏离信息。
  3. **基于Z-score的动态抑制**：计算当前层所有头的 $\rho_h$ 均值 $\mu_\rho$ 和标准差 $\sigma_\rho$（公式5），并计算每个头的Z-score $z_h$（公式6）。假设幻觉头是统计分布中的长尾离群点，使用Sigmoid门控函数计算抑制系数 $\lambda_h$（公式7），其中 $\tau$ 为容忍阈值，$\beta$ 为温度系数。
  4. **输出重构**：最终注意力模块的输出为所有头干预后向量的总和，即保留对齐分量，并对正交分量乘以抑制系数：$\sum (o_{h\parallel} + \lambda_h \cdot o_{h\perp})$（公式8）。
- **实施策略**：仅作用于模型的中后期层（早期层用于局部句法解析，需保留高正交性），计算复杂度为 $O(L \cdot H \cdot d_{model})$，远低于注意力机制的二次复杂度，且仅需单次前向传播。

## 3. 实验设计：数据集、Benchmark与对比方法
- **基础模型**：Llama-3-8B-Instruct 和 Llama-3-70B-Instruct。
- **评估Benchmark与数据集**：
  - **上下文忠实度与指令遵循**：IFEval, XSum, NQ-Swap, NQ-Open (Open-Book)。
  - **事实性与参数知识保留**：TruthfulQA, TriviaQA, NQ-Open (Closed-Book)。
  - **复杂推理稳定性**：MuSiQue (多跳推理)。
- **对比方法**：Greedy Decoding (基线), ITI (推理时干预), CAD (上下文感知解码), DoLa (对比层解码), AD (自对比解码), DeCoRe (静态检索头对比), CD (对比解码)。

## 4. 资源与算力
- **算力说明**：论文**未明确说明**所使用的GPU型号、数量或具体的推理时长。但文中强调，DCO方法的计算开销极小，仅引入线性复杂度的投影和归一化操作，且与需要多次前向传播的对比解码方法（如CAD, DoLa）相比，DCO在单次推理中完成，具有显著的延迟和吞吐量优势。

## 5. 实验数量与充分性
- **实验数量**：共设置了3个主表，涵盖7个以上不同维度的数据集/设定，在2种不同参数规模（8B, 70B）的模型上进行验证，对比了7种主流基线方法，并包含1个定性分析案例。
- **充分性与客观性**：实验设计**非常充分且客观**。不仅评估了幻觉缓解的效果（忠实度），还重点考察了方法对模型原有参数知识的破坏程度（知识保留），验证了Pareto前沿的优化。同时，针对不同任务特性（如反事实任务收紧约束，多跳推理放松约束）进行了超参数校准说明，反映了客观的实验态度。

## 6. 主要结论与发现
- DCO在上下文忠实度任务（如IFEval, XSum）上显著优于现有干预基线，Llama-3-70B上的IFEval指令级准确率提升至90.29%。
- DCO有效缓解了“幻觉抑制与参数知识保留”之间的权衡问题，在TriviaQA和NQ-Open闭卷测试中保持甚至提升了性能，而静态方法（如ITI）则导致知识检索能力大幅下降。
- 在多跳推理中，DCO通过抑制残差流中的累积偏差，缓解了语义漂移，取得了最优的闭卷推理表现。
- 验证了幻觉的几何解释：幻觉在潜空间中表现为正交噪声，动态正交化是实现流形对齐的有效途径。

## 7. 优点
- **视角新颖**：将幻觉问题从概率层面的现象提升到几何层面的流形对齐与正交噪声分解，具有强机制可解释性。
- **动态自适应**：摒弃了静态转向向量，利用输入残差流作为动态锚点，结合Z-score统计分布进行软性门控抑制，既过滤了噪声又保留了必要的语义多样性。
- **高效低损**：单次前向传播、线性计算复杂度，且不损害模型固有的参数知识检索能力，实用性极高。

## 8. 不足与局限
- **上下文依赖**：DCO的几何语义流形定义高度依赖于输入残差流作为上下文锚点。在完全没有上下文的纯闭卷生成场景中，正交性的定义变得不够明确（尽管实验表明其仍具鲁棒性）。
- **线性假设的简化**：方法基于“线性表示假设”，而Transformer底层包含非线性激活函数，用线性近似来操控高层语义特征是一种简化，可能遗漏某些非线性交互的幻觉机制。
- **超参数敏感性**：容忍阈值 $\tau$ 和温度 $\beta$ 需要根据下游任务的语义密度和推理深度进行针对性校准（如反事实任务需紧约束，多跳推理需松约束），目前缺乏全自动的元学习校准机制，限制了其开箱即用的零样本泛化能力。
- **模型架构覆盖**：实验仅在Llama-3系列的Decoder-only模型上验证，未探讨其在Encoder-Decoder或MoE等其他主流架构上的表现。

（完）
