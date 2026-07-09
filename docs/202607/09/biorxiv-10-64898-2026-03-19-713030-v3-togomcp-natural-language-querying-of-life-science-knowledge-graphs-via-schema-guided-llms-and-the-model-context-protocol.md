---
title: "TogoMCP: Natural Language Querying of Life-Science Knowledge Graphs via Schema-Guided LLMs and the Model Context Protocol"
title_zh: TogoMCP：通过模式引导的LLM和模型上下文协议实现生命科学知识图谱的自然语言查询
authors: "Kinjo, A. R., Yamamoto, Y., Bustamante-Larriet, S., Labra-Gayo, J. E., Fujisawa, T."
date: 2026-07-06
pdf: "https://www.biorxiv.org/content/10.64898/2026.03.19.713030v3.full.pdf"
tags: ["query:llm-halluc"]
score: 6.0
evidence: 缓解大模型生成SPARQL时的谓词捏造
tldr: "查询生命科学知识图谱通常需要精通SPARQL和特定数据库模式，这对多数研究者构成障碍。本文提出TogoMCP系统，利用模型上下文协议（MCP）将大语言模型重构为协议驱动的推理引擎，通过MIE文件动态提供模式上下文，并采用两阶段工作流分离实体解析与SPARQL生成。在50个生物学问题的基准测试中，TogoMCP相比无辅助基线取得大幅提升，精确答案类型的胜率超80%。研究表明，动态提供的简洁模式上下文对平均性能的提升优于复杂编排逻辑，而过程指导则能有效缩小方差。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-19-713030-v3/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1752, \"height\": 1488, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-03-19-713030-v3/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 790, \"height\": 516, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-03-19-713030-v3/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 781, \"height\": 257, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-03-19-713030-v3/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 773, \"height\": 255, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-03-19-713030-v3/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 885, \"height\": 330, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-03-19-713030-v3/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1158, \"height\": 253, \"label\": \"Table\"}]"
motivation: 查询生命科学RDF知识图谱需SPARQL和特定模式，而现有LLM缺乏模式上下文易产生幻觉和实体解析失败。
method: 提出TogoMCP系统，基于MCP协议驱动LLM，利用MIE文件动态提供模式上下文，并采用两阶段工作流分离实体解析与SPARQL生成。
result: "在50个问题基准测试中大幅优于基线，精确问题胜率超80%，消融实验证明MIE文件对平均分提升最大。"
conclusion: 动态提供的简洁模式上下文比复杂编排逻辑对平均性能更有价值，而过程指导在缩小方差上起互补作用。
---

## 摘要
查询由DBCLS维护的RDF Portal知识图谱（该图谱聚合了约60个生命科学数据库）需要熟练掌握SPARQL和特定数据库的RDF模式，这使得大多数研究人员无法使用该资源。大语言模型（LLM）原则上可以将自然语言问题翻译为可执行的SPARQL，但在缺乏模式级上下文的情况下，它们经常捏造不存在的谓词，或者无法将实体名称解析为特定数据库的标识符。我们提出了TogoMCP，这是一个将LLM重新定义为协议驱动推理引擎的系统，它通过模型上下文协议（MCP）来协调专门的工具。其设计中有两个关键机制：(i) MIE（元数据互操作性交换）文件，这是一种简洁的YAML文档，在查询时动态为LLM提供每个目标数据库的结构和语义上下文；(ii) 两阶段工作流，将通过外部REST API进行的实体解析与模式引导的SPARQL生成分离开来。在一个包含50个生物学问题（涵盖5种类型和23个数据库）的基准测试中，TogoMCP相比无辅助基线取得了巨大提升（Cohen's d = 1.82，Wilcoxon p < 0.001），对于具有精确、可验证答案的问题类型，其胜率超过80%。消融研究表明，所有组件配置均带来了显著提升，其中MIE模式文件对每题平均得分的边际贡献最大（相对于无MIE条件，Δ = +0.50，双侧Wilcoxon p = 0.067；90% bootstrap置信区间[+0.04, +0.94]不包含零）；加载相关MIE文件的单行指令能够获得与完整程序协议相同的平均提升，而该协议还额外降低了下行风险（损失率为1.6%对4.8%，Fisher p = 0.036）。这些结果提出了一项通用设计原则：对于平均得分表现而言，简洁、动态交付的模式上下文比复杂的编排逻辑更有价值，而程序性指导在缩小方差方面起着补充作用。

数据库网址：https://togomcp.rdfportal.org/

## Abstract
Querying the RDF Portal knowledge graph maintained by DBCLS--which aggregates approximately 60 life-science databases--requires proficiency in both SPARQL and database-specific RDF schemas, placing this resource beyond the reach of most researchers. Large Language Models (LLMs) can, in principle, translate natural-language questions into executable SPARQL, but without schema-level context, they frequently fabricate non-existent predicates or fail to resolve entity names to database-specific identifiers. We present TogoMCP, a system that recasts the LLM as a protocol-driven inference engine orchestrating specialized tools via the Model Context Protocol (MCP). Two mechanisms are essential to its design: (i) the MIE (Metadata-Interoperability-Exchange) file, a concise YAML document that dynamically supplies the LLM with each target databases structural and semantic context at query time; and (ii) a two-stage workflow separating entity resolution via external REST APIs from schema-guided SPARQL generation. On a benchmark of 50 biologically grounded questions spanning five types and 23 databases, TogoMCP achieved a large improvement over an unaided baseline (Cohens d = 1.82, Wilcoxon p < 0.001), with win rates exceeding 80% for question types with precise, verifiable answers. An ablation study shows that all component configurations deliver significant improvements, with MIE schema files providing the largest marginal contribution on mean per-question score ({Delta} = +0.50 relative to a no-MIE condition, two-sided Wilcoxon p = 0.067; 90% bootstrap CI [+0.04, +0.94] excludes zero); a one-line instruction to load the relevant MIE file recovers the same mean improvement as a full procedural protocol, while the protocol additionally reduces downside risk (loss rate 1.6% vs. 4.8%, Fisher p = 0.036). These results suggest a general design principle: concise, dynamically delivered schema context is more valuable than complex orchestration logic for mean-score performance, while procedural guidance plays a complementary role in narrowing variance.

Database URL: https://togomcp.rdfportal.org/