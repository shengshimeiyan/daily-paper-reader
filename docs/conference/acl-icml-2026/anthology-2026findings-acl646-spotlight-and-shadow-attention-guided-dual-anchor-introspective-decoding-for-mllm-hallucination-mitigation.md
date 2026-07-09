---
title: "Spotlight and Shadow: Attention-Guided Dual-Anchor Introspective Decoding for MLLM Hallucination Mitigation"
title_zh: 聚光灯与阴影：面向多模态大模型幻觉缓解的注意力引导双锚点内省解码
authors: "Yebo Wu, Han Jin, Zhijiang Guo, Li Li"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.646.pdf"
tags: ["query:llm-halluc"]
score: 6.0
evidence: 通过内省解码缓解多模态大模型幻觉
tldr: 针对多模态大语言模型生成文本与视觉内容矛盾的幻觉问题，提出双锚点内省解码框架DaID。该对比解码框架通过挖掘模型内部感知差异，动态识别聚光灯层以放大视觉事实信号和阴影层以抑制文本惯性。通过利用视觉注意力分布指导双锚点选择，该方法确保了精确的token级自适应。实验表明，DaID在多个基准测试中显著缓解了多模态幻觉，提升了生成质量。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.646/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 776, \"height\": 740, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.646/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1649, \"height\": 423, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.646/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1651, \"height\": 515, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.646/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1534, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.646/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 735, \"height\": 325, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.646/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 737, \"height\": 324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.646/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1449, \"height\": 457, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.646/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1646, \"height\": 588, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.646/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1338, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.646/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1651, \"height\": 535, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.646/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1639, \"height\": 551, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.646/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1665, \"height\": 943, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.646/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 789, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.646/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 788, \"height\": 248, \"label\": \"Table\"}]"
motivation: 多模态大语言模型常生成与视觉内容矛盾的幻觉文本，需有效方法抑制文本惯性并增强视觉信号。
method: 提出双锚点内省解码框架DaID，利用视觉注意力分布动态选择聚光灯层和阴影层，对比解码校准token生成。
result: DaID在多个基准测试中显著缓解了多模态大模型的幻觉问题，提升了视觉事实一致性。
conclusion: 通过双锚点内省解码动态调节视觉与文本信号，可有效缓解多模态大语言模型的幻觉。
---

## Abstract
Multimodal Large Language Models (MLLMs) have demonstrated remarkable reasoning capabilities yet continue to suffer from hallucination, where generated text contradicts visual content. In this paper, we introduce Dual-Anchor Introspective Decoding (DaID), a novel contrastive decoding framework that dynamically calibrates each token generation by mining the model’s internal perceptual discrepancies. Specifically, DaID identifies a Spotlight layer to amplify visual factual signals and a Shadow layer to suppress textual inertia. By leveraging visual attention distributions to guide this dual-anchor selection process, our method ensures precise, token-specific adaptation. Experimental results across multiple benchmarks and MLLMs demonstrate that DaID significantly mitigates hallucination while enhancing general reasoning capabilities.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：多模态大语言模型（MLLMs）在生成文本时存在严重的“幻觉”问题，即生成的内容与输入的视觉信息相矛盾。
- **现有方法的局限**：现有的无训练对比解码方法（如VCD、ICD）存在两大缺陷：一是需要为负样本额外进行一次前向传播，导致计算开销大、推理延迟高；二是依赖启发式的外部扰动（如视觉遮蔽）来构建负分布，容易引入随机噪声，导致语义错误偏移。
- **整体含义**：本文提出从“外部干预”转向“内部自省”，通过挖掘模型内部不同层级的感知差异来构建对比信号，从而在单次前向传播中高效、无噪声地缓解幻觉问题。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出双锚点内省解码框架（DaID）。基于MLLMs浅层幻觉严重（视觉失认）、中间层视觉感知最强（先看见后遗忘）的观察，动态选择一个“聚光灯层”（正锚点）放大视觉事实信号，一个“阴影层”（负锚点）抑制文本惯性。
- **关键技术细节与流程**：
  1. **视觉注意力得分（VAS）**：作为模型视觉依赖程度的代理指标。计算每一层中所有注意力头对视觉token的累积注意力质量，得分越高表示该层越依赖视觉信息。
  2. **动态锚点选择**：
     - **聚光灯层（Spotlight Anchor）**：选择VAS得分最高的层，用于提取最真实的视觉感知信号。
     - **阴影层（Shadow Anchor）**：在聚光灯层之前的浅层中，选择VAS得分最低的层，用于捕捉纯粹的文本惯性噪声（约束阴影层必须在聚光灯层之前，确保其处于视觉失认状态）。
  3. **双锚点对比解码公式**：最终校准的logits由三部分组成：最终层的原始logits，加上α乘以聚光灯层logits（强化视觉），再乘以(1+β)后减去β乘以阴影层logits（抑制语言先验）。α和β为调节强度的超参数。
  4. **自适应合理性约束**：为防止中间层注入的logits破坏语法连贯性，仅对最终层概率大于阈值（γ乘以最大概率）的候选token集合进行对比调整，其余token概率置零。

### 3. 实验设计：数据集、Benchmark及对比方法
- **评估模型**：LLaVA-1.5, LLaVA-NeXT, Qwen2-VL, MiniGPT-4, InstructBLIP（主实验为7B规模，部分扩展至13B及2B）。
- **数据集/Benchmark**：
  - **视觉幻觉任务**：POPE（二元对象幻觉）、CHAIR（图像描述对象幻觉）、MME（感知与认知能力，关注对象和属性子集）。
  - **通用视觉语言任务**：GQA, VQA v2, MMB, Seed I, VizWiz。
- **对比方法**：Greedy Decoding, Beam Search, DoLa, VCD, OPERA, SID, EAZY。

### 4. 资源与算力
- **算力资源**：文中明确提到使用 **NVIDIA RTX 5070 Ti GPU** 进行评估。
- **训练时长/数量**：由于DaID是一种无需训练的解码策略，文中未提及训练时长和GPU数量，主要关注推理延迟指标（如ms/token）。

### 5. 实验数量与充分性
- **实验数量**：实验涵盖了5个主流MLLM架构、8个不同维度的Benchmark；进行了超参数分析（α和β）、消融实验（正负锚点贡献）、泛化性分析、定性分析，以及附录中的计算效率对比、约束条件分析、动态锚点可视化等。
- **充分性与客观性**：实验设计非常充分且客观。不仅验证了幻觉缓解效果，还验证了通用推理能力的保持/提升；消融实验清晰拆解了双锚点的各自贡献；效率对比客观展示了相比VCD的延迟优势；泛化实验证明了方法不局限于特定模型架构。

### 6. 论文的主要结论与发现
- DaID在多个幻觉基准上显著优于现有方法（如LLaVA-1.5上POPE F1提升3.72%，CHAIR S大幅下降）。
- DaID不仅缓解了幻觉，还通过净化表征提升了模型在通用视觉语言任务上的推理能力。
- 浅层（阴影层）是语言惯性的主要来源，中间层（聚光灯层）是视觉保真度的巅峰，利用视觉注意力（VAS）可以免训练地精准定位这两类层级。
- 相比外部扰动方法，内部自省解码在单次前向传播中即可完成校准，推理延迟显著降低（比VCD快约37.6%）。

### 7. 优点：方法或实验设计上的亮点
- **计算高效**：摒弃了额外的前向传播，通过复用单次推理的中间状态（注意力分布和隐藏层）实现对比解码，大幅降低了推理延迟。
- **避免外部噪声**：不依赖图像扰动或指令扰动，完全从模型内部挖掘对比信号，避免了因扰动不当导致的语义偏移（如图1中VCD将黄色误判为红色的案例）。
- **动态细粒度适配**：基于VAS的动态锚点选择是token级别的，能够根据每个生成步骤的实际视觉依赖情况自适应调整正负锚点，而非使用固定层。
- **机制互补**：正负双锚点设计同时兼顾了“增强视觉信号”和“抑制语言先验”，消融实验证实了两者缺一不可。

### 8. 不足与局限
- **模型规模限制**：受限于计算硬件，实验主要在7B/13B规模的模型上进行，在超大规模（如70B+）MLLM上的层间动态变化规律及方法有效性尚未验证。
- **模态局限**：当前研究仅聚焦于图像-文本模态，未探索视频、音频等时序多模态任务。视频理解中的时序动态会导致更复杂的注意力偏移，DaID的直接适用性存疑。
- **超参数敏感性**：自适应合理性约束的阈值γ需要根据任务类型调整（判别式任务设为0.9，生成式任务设为0.1），在实际应用中可能需要根据场景人工选取。

（完）
