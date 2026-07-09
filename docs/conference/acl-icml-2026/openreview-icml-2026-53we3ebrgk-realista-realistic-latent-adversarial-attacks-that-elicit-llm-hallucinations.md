---
title: "REALISTA: Realistic Latent Adversarial Attacks that Elicit LLM Hallucinations"
title_zh: REALISTA：引发大模型幻觉的现实潜在对抗攻击
authors: "Buyun Liang, Jinqi Luo, Liangzu Peng, Kwan Ho Ryan Chan, Darshan Thaker, Kaleab A Kinfu, Fengrui Tian, Hamed Hassani, Rene Vidal"
date: 2026-04-30
pdf: "https://openreview.net/pdf/b2b8da31b97232523c0b4a54ef899933268c1189.pdf"
tags: ["query:llm-halluc"]
score: 8.0
evidence: 通过对抗攻击引发大模型幻觉
tldr: 系统评估大模型在现实对抗输入下的可靠性需要引发幻觉，但现有离散提示攻击搜索空间有限，连续潜在空间攻击则常破坏语义等价性。本文将幻觉引发建模为约束优化问题，提出REALISTA方法，在连续潜在空间中寻找与良性提示语义等价的连贯对抗提示。实验表明，REALISTA成功生成了语义等价的对抗提示，有效引发了大模型幻觉，为评估模型可靠性提供了工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有对抗攻击方法在保持语义等价性和搜索空间丰富度之间存在局限，难以现实地引发幻觉。
method: 提出REALISTA方法，将幻觉引发建模为约束优化问题，在潜在空间寻找语义连贯的对抗提示。
result: REALISTA成功生成了语义等价的对抗提示，有效引发了大模型幻觉。
conclusion: 该方法为评估大模型在现实对抗场景下的幻觉脆弱性提供了有效工具。
---

## Abstract
Large language models (LLMs) achieve strong performance across many tasks but remain vulnerable to hallucinations, making it important to systematically evaluate their reliability under realistic adversarial inputs. We formulate hallucination elicitation as a constrained optimization problem, where the goal is to find semantically coherent adversarial prompts that are equivalent to benign user prompts. Existing attack methods remain limited: discrete prompt-based attacks preserve semantic equivalence and coherence but search only over a limited set of prompt variations, while continuous latent-space attacks explore a richer space but often decode into prompts that are no longer valid rephrasings. To address these limitations, we propose REALISTA, a realistic latent-space attack framework. REALISTA constructs an input-dependent dictionary of valid editing directions, each corresponding to a semantically equivalent and coherent rephrasing, and optimizes continuous combinations of these directions in latent space. This design combines the optimization flexibility of continuous attacks with the semantic realism of discrete rephrasing-based attacks. Experiments demonstrate that REALISTA achieves superior or comparable performance to state-of-the-art realistic attacks on open-source LLMs and, crucially, succeeds in attacking large reasoning models under free-form response settings, where prior realistic attacks fail.

---

## 论文详细总结（自动生成）

# 论文总结：REALISTA: Realistic Latent Adversarial Attacks that Elicit LLM Hallucinations

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）极易产生幻觉，系统评估其在现实对抗输入下的可靠性至关重要，但现有的对抗攻击方法难以在“保持语义等价性”和“搜索空间丰富度”之间取得平衡。
- **研究动机**：
  - **离散提示攻击**：虽然能保持语义等价和连贯性，但搜索空间仅限于有限的提示变体，难以发现深层漏洞。
  - **连续潜在空间攻击**：虽然探索了更丰富的搜索空间，但解码出的提示往往不再是原提示的有效复述，破坏了语义等价性，导致攻击不具现实意义。
- **整体含义**：亟需一种能够在连续潜在空间中进行灵活优化，同时又能保证生成的对抗提示在语义上与现实良性提示等价的新方法，以真实评估LLM的幻觉脆弱性。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：将引发大模型幻觉建模为一个**约束优化问题**，目标是寻找与良性用户提示语义等价且连贯的对抗提示。提出 REALISTA 框架，将连续攻击的优化灵活性与离散复述攻击的语义真实性相结合。
- **关键技术细节**：
  - **构建输入依赖的有效编辑字典**：针对每个输入，构建一个包含多个有效编辑方向的字典，其中每个方向都对应一种语义等价且连贯的复述方式。
  - **潜在空间连续组合优化**：在连续潜在空间中，对这些有效的编辑方向进行连续组合的优化，而不是单一离散的选择。
  - **算法流程简述**：1) 获取良性提示的潜在表示；2) 提取并构建该提示特定的语义等价编辑方向字典；3) 在潜在空间中优化这些方向的连续组合系数；4) 解码优化后的潜在表示，生成语义连贯且等价的对抗提示，以诱发模型幻觉。

## 3. 实验设计：数据集/场景、Benchmark 及对比方法
- **数据集/场景**：文中未在摘要中明确具体数据集名称，但指出了两个关键评估场景：开源大语言模型场景，以及**自由形式响应设置下的大型推理模型**场景。
- **Benchmark**：以现实对抗攻击下诱发LLM幻觉的成功率及语义等价性为核心评估基准。
- **对比方法**：与当前最先进的现实攻击方法（SOTA realistic attacks，包括前文提及的离散提示攻击和连续潜在空间攻击）进行对比。

## 4. 资源与算力
- **说明**：基于提供的论文元数据和摘要，**文中未明确说明所使用的算力资源（如GPU型号、数量、训练/优化时长等）**。

## 5. 实验数量与充分性
- **实验设置**：至少涵盖了开源LLM和大型推理模型两大类场景的评估，且特别针对“自由形式响应”这一更具挑战性的设定进行了验证。
- **充分性与客观性评价**：实验设计具有较强的针对性和充分性。特别是针对大型推理模型的攻击成功，弥补了先前现实攻击方法失效的空白，验证了方法的先进性；对比了SOTA方法，保证了评估的相对客观与公平。但受限于摘要信息，无法判断数据集规模及消融实验的细粒度。

## 6. 论文的主要结论与发现
- REALISTA 成功生成了语义等价且连贯的对抗提示，有效引发了大语言模型的幻觉。
- 在开源LLM上，REALISTA 取得了优于或媲美当前最先进现实攻击方法的性能。
- **关键发现**：在自由形式响应设置下的大型推理模型上，先前的现实攻击方法均告失败，而 REALISTA 成功实现了攻击，证明了其在复杂推理场景下暴露模型脆弱性的能力。

## 7. 优点：方法或实验设计上的亮点
- **巧妙融合优势**：创新性地通过“有效编辑方向字典+连续组合优化”的设计，完美融合了离散攻击的语义真实性和连续攻击的优化灵活性。
- **约束建模严谨**：将幻觉诱发建模为约束优化问题，从理论上保障了生成提示的现实可用性。
- **突破现有瓶颈**：在先前方法无法攻破的“大型推理模型自由形式响应”场景下取得成功，具有显著的实践价值和前沿性。

## 8. 不足与局限
- **信息局限**：由于原文PDF受验证码限制无法获取全文，无法评估其计算开销（构建输入依赖字典和连续优化的时间成本可能较高）、具体数据集的覆盖广度以及详细的消融实验结果。
- **语义等价性评估偏差风险**：尽管方法旨在保证语义等价，但“语义等价和连贯”的判定标准可能存在主观性或依赖特定指标，若未进行严格的人类评估，可能存在偏差。
- **应用限制**：该方法依赖于构建输入依赖的编辑方向字典，对于极度缺乏同义复述空间的特定领域提示，其攻击效果和字典构建质量可能会受到限制。

（完）
