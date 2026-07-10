---
title: "Structured Schemas for Provenance-Rich, LLM-Assisted QSP Model Calibration"
title_zh: 用于溯源丰富、LLM辅助的QSP模型校准的结构化模式
authors: "Eliason, J., Popel, A. S."
date: 2026-07-08
pdf: "https://www.biorxiv.org/content/10.64898/2026.03.05.709623v2.full.pdf"
tags: ["query:llm-halluc"]
score: 6.0
evidence: 验证器捕获LLM幻觉值
tldr: QSP模型校准依赖文献，但人工整理记录不一且LLM提取易生幻觉与伪造引用。提出MAPLE框架，利用结构化验证模式作为LLM与建模者的协作接口，分离数据提取与建模决策。在胰腺癌QSP模型中，验证器自动重试纠错，所有数值均含直接引语与验证引用，近六成参数获多源支持。该框架完整记录建模推理过程，支持重跑与独立核查，有效防止团队更迭导致的知识流失。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-05-709623-v2/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1664, \"height\": 1080, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-03-05-709623-v2/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1211, \"height\": 1067, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-03-05-709623-v2/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 597, \"height\": 483, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-03-05-709623-v2/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1018, \"height\": 529, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-03-05-709623-v2/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1140, \"height\": 335, \"label\": \"Table\"}]"
motivation: QSP模型校准数据的人工整理缺乏一致性，而LLM提取易产生数值幻觉和伪造引用，亟需可靠的协作框架。
method: 提出MAPLE框架，采用双尺度结构化模式分离数据提取与建模决策，并通过定向验证器匹配源片段、解析DOI及执行代码以捕获LLM错误。
result: "在胰腺癌QSP模型中，验证器触发50次自动重试，所有数值均含直接引语与验证引用，11/19参数获多源支持，建模者修正了65%的正向模型选择。"
conclusion: MAPLE将建模者的推理过程以可重跑和独立核查的形式记录，有效避免了建模团队变更时的知识流失问题。
---

## 摘要
定量系统药理学（QSP）模型需要来自文献的校准数据，然而人工整理的文档记录往往不一致，而大语言模型（LLM）在提取时可能会产生数值幻觉并捏造引用。我们提出了MAPLE（基于文献证据的模型感知参数化），该方法使用结构化验证模式作为LLM与建模者之间的协作接口。两种模式跨越两个尺度：用于约束单个参数的独立实验的子模型目标（SubmodelTarget）模式，以及用于约束完整模型的临床和体内终点的校准目标（CalibrationTarget）模式。两者均将数据提取与建模决策分离，并记录每个数值的完整溯源信息。定向验证器通过将数值与来源片段匹配、解析DOI以及执行代码，来捕获LLM的典型错误。针对胰腺导管腺癌QSP模型，我们使用MAPLE提取并整理了37个子模型目标和45个校准目标。在任何人工审查之前，验证器触发了50次自动重试；每个数值都带有来自其来源的直接引语和经过验证的引用；且19个参数中有11个得到了不止一个独立来源的支持。LLM根据上下文起草了可用的正向模型和代码，而建模者则提供了LLM无法推断的上下文和科学判断，在65%的子模型目标中修改了正向模型选择，在46%中修改了先验，并在所有文件中修改了来源相关性。本次评估仅涵盖单一团队在单一疾病领域的一个模型，因此它是对该框架特性的描述，而非确立其泛化广度。MAPLE以可重新运行和独立检查的形式记录建模者的推理过程，因此当建模团队发生变更时，这些推理不会丢失。

## Abstract
Quantitative systems pharmacology (QSP) models require calibration data from literature, yet manual curation is inconsistently documented and large language model (LLM) extraction can hallucinate values and fabricate citations. We present MAPLE (Model-Aware Parameterization from Literature Evidence), which uses structured validation schemas as a collaboration interface between LLMs and modelers. Two schemas span two scales: the SubmodelTarget schema for isolated experiments constraining individual parameters, and the CalibrationTarget schema for clinical and in vivo endpoints constraining the full model. Both separate data extraction from modeling decisions, recording every value with full provenance. Targeted validators catch characteristic LLM errors by matching values to source snippets, resolving DOIs, and executing code. For a pancreatic ductal adenocarcinoma QSP model, we used MAPLE to extract and curate 37 SubmodelTargets and 45 CalibrationTargets. Before any human review, the validators triggered 50 automated retries; every value carries a direct quote from its source and a verified citation; and 11 of 19 parameters are supported by more than one independent source.The LLM drafted usable forward models and code from context, while the modeler supplied the context and scientific judgment it cannot infer, revising forward-model choices in 65% of SubmodelTargets, priors in 46%, and source relevance in all files. This evaluation covers one model in one disease area, by a single group, so it characterizes the framework rather than establishing how broadly it generalizes. MAPLE records the modelers reasoning in a form that can be re-run and independently checked, so it is not lost when the modeling team changes.