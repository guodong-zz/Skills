# 1. Skill Name

Biomedical Paper Card

# 2. Purpose

将用户提供的生物医学论文系统解析为标准化、可长期积累的 Paper Card，用于 Obsidian 知识库管理、后续文献横向比较、专题综述、研究假说生成和课题设计。

核心目标不是简单总结论文，而是回答：

1. 作者真正想解决什么科学问题？
2. 该问题为什么重要？
3. 作者采用了什么实验和分析策略？
4. 每个关键实验如何支持核心结论？
5. Figures 之间形成了怎样的故事线？
6. 哪些结论是数据直接支持的，哪些属于作者推断？
7. 研究存在哪些技术或逻辑局限？
8. 这篇论文对用户自己的研究有什么可迁移的启发？

---

# 3. Input

优先基于用户提供的论文全文 PDF 进行分析。

如果只有摘要、Figure、图注或部分正文，必须明确说明分析范围，禁止将缺失内容推测为论文事实。

当同时提供多篇论文时，默认每篇论文分别生成独立 Paper Card，除非用户明确要求进行综合分析。

---

# 4. Core Principles

## 4.1 Evidence-based

所有关于论文内容的判断必须尽可能对应具体实验、Figure、Extended Data、Supplementary Figure 或正文结果。

不得仅根据摘要推断全文结论。

## 4.2 Separate Evidence from Interpretation

明确区分：

- Direct evidence：实验数据直接支持的事实
- Authors' interpretation：作者基于数据提出的解释
- Further inference：基于论文结果可以合理延伸出的推断

避免将相关性描述为因果关系。

## 4.3 Mechanism-oriented

对于机制性研究，重点梳理：

Phenomenon → Association → Mechanism → Perturbation → Functional consequence → In vivo validation

判断论文是否真正形成完整的因果证据链。

## 4.4 Figure-driven

优先按照 Figure 的推进顺序理解论文，而不是简单按照 Introduction–Methods–Results–Discussion 复述。

重点回答每张主 Figure 在整个 story 中承担什么任务。

## 4.5 Research-value-oriented

从 PI 和课题设计视角评价论文：

- 科学问题的重要性
- 创新点
- 方法学优势
- 关键证据是否充分
- 潜在漏洞
- 可重复性
- 后续可研究方向
- 对用户现有研究体系的启发

---

# 5. Output Format

---

# 6. One-sentence Take-home Message

用 1–3 句话概括论文最核心的科学贡献。

要求回答：

**这篇论文真正发现了什么？**

避免简单复制摘要。

---

# 7. Scientific Background

简要说明该研究所在领域的背景。

包括：

- 已知事实
- 当前领域共识
- 关键未解决问题
- 为什么这个问题值得研究

重点解释论文出现之前的 knowledge gap。

---

# 8. Core Scientific Question

明确提出论文试图回答的核心问题。

格式：

> The central question of this study is:

随后用中文解释。

如果论文包含多个层级的问题，区分：

- Primary question
- Secondary questions

---

# 9. Central Hypothesis

总结作者隐含或明确提出的核心假说。

格式：

> 作者假设：A → B → C

尽可能构建清晰的机制链。

如果论文属于描述性 atlas/resource study，没有明确机制假说，则说明：

> 本研究主要属于 discovery-driven / atlas-building study，而非 hypothesis-driven mechanistic study。

---

# 10. Study Design

从宏观层面描述整个研究设计。

包括：

- Cohort / samples
- Experimental models
- Omics datasets
- Animal models
- In vitro models
- Key perturbations
- Validation strategies

重点解释作者如何从问题走向结论。

可使用：

Question\
↓\
Experiment 1\
↓\
Observation\
↓\
Experiment 2\
↓\
Mechanistic validation\
↓\
Functional validation

---

# 11. Figure-by-Figure Storyline

这是 Paper Card 的核心部分。

对每张主 Figure 分别解析。

## Figure 1 — [核心目的]

### Question

这一 Figure 想回答什么问题？

### Experimental design

使用了什么实验、样本或分析方法？

### Key results

最关键的数据是什么？

### Interpretation

这些结果说明什么？

### Role in the story

这一 Figure 在整篇论文逻辑中承担什么作用？

例如：

- Establishing the phenomenon
- Defining cellular states
- Identifying candidate mechanism
- Demonstrating spatial association
- Establishing causality
- Functional validation
- Clinical validation

依次分析 Figure 1、Figure 2、Figure 3……

如 Supplementary Figure 对核心结论至关重要，也应纳入。

---

# 12. Overall Storyline

将所有 Figures 串联为一条完整科学故事线。

推荐格式：

Observation\
↓\
Cellular / molecular characterization\
↓\
Spatial or temporal association\
↓\
Candidate mechanism\
↓\
Experimental perturbation\
↓\
Functional consequence\
↓\
In vivo / clinical validation

最终回答：

**作者是如何一步一步说服读者接受核心结论的？**

---

# 13. Key Findings

总结 3–7 个最重要的研究发现。

每一个 Finding 应包含：

### Finding X

结论

**Evidence：**\
对应实验或 Figure。

**Strength of evidence：**\
Strong / Moderate / Suggestive

避免把所有 Results 简单罗列。

---

# 14. Mechanistic Model

如果论文提出机制，构建完整机制模型。

格式：

A\
↓\
B activation / inhibition\
↓\
C cellular state change\
↓\
D functional phenotype\
↓\
Disease progression

需要区分：

- 已被实验直接验证的环节
- 只有相关性证据的环节
- 作者提出但尚未验证的环节

---

# 15. Cell States / Cellular Ecosystem

如果涉及 single-cell、spatial transcriptomics 或 tumor ecosystem，仅总结：

### Cell populations

主要细胞类型或 malignant cell states。

### Marker genes

各主要细胞类型或状态对应的 marker genes。

---

# 16. Key Technologies

总结主要技术平台。

例如：

- scRNA-seq
- snRNA-seq
- scATAC-seq
- Spatial Transcriptomics
- Visium
- MERFISH
- CODEX
- Xenium
- Patch clamp
- Rabies tracing
- CRISPR screening
- Organoid
- PDX

对于每项关键技术说明：

**Purpose：**\
为什么使用？

**Strength：**\
解决了什么问题？

**Limitation：**\
该技术不能证明什么？

---

# 17. Strongest Evidence

指出整篇论文最有说服力的 1–3 个实验。

解释：

为什么这些实验是决定性的？

是否真正建立：

- causality
- mechanism
- functional relevance

---

# 18. Weakest Link

指出论文证据链中最薄弱的环节。

例如：

- 样本量不足
- 缺乏独立队列
- 缺少 functional validation
- 只有 transcriptomic inference
- 缺乏 lineage tracing
- 缺少 in vivo perturbation
- 空间共定位被过度解释
- 小鼠模型与人类疾病存在差异

---

# 19. Overinterpretation Check

主动检查作者是否存在结论过度延伸。

按照以下格式：

### Claim

作者声称什么？

### Evidence

实际数据证明了什么？

### Assessment

Fully supported / Partially supported / Overinterpreted

尤其检查：

Correlation → Causation

Gene expression → Functional activity

Ligand–receptor prediction → Real interaction

Spatial proximity → Direct communication

Cell-state association → Lineage transition

---

# 20. Major Limitations

从以下维度系统评价：

### Biological limitations

### Technical limitations

### Statistical limitations

### Model limitations

### Clinical translation limitations

不要简单重复 Discussion 中作者自己列出的 limitations，需要独立判断。

---

# 21. Novelty

回答：

**这篇论文相比此前研究真正新增了什么？**

区分：

- Conceptual novelty
- Biological novelty
- Technical novelty
- Resource novelty

同时判断创新属于：

Incremental

Moderate

Substantial

Field-changing

并给出理由。

---

# 22. Implications for the Field

分析该研究可能如何改变领域认知。

包括：

- 是否提出新的 disease model
- 是否重新定义 cell state
- 是否发现新的 microenvironment niche
- 是否建立新的 neuron–tumor interaction
- 是否提出新的 therapeutic vulnerability

---

# 23. Implications for My Research

默认从以下研究方向思考：

- Glioblastoma
- Malignant cell states
- OPC-like cells
- Cellular plasticity
- Tumor ecosystem
- Tumor microenvironment
- Neuron–tumor interaction
- Cancer neuroscience
- Single-cell omics
- Spatial transcriptomics
- Spatial multiomics

回答：

### 可直接借鉴的方法

### 可验证的新假说

### 可以进行的二次数据分析

### 可以设计的关键实验

### 可能形成的新 Figure

重点思考论文中的方法或发现如何转化为新的研究问题，而不是简单说“值得进一步研究”。

---

# 24. Reusable Data / Resources

判断论文是否公开：

- scRNA-seq
- spatial transcriptomics
- bulk RNA-seq
- proteomics
- imaging
- code
- cell atlas

记录：

Dataset accession:

Repository:

Potential reuse:

重点判断这些数据是否适合用于二次分析。

---

# 25. Knowledge Base Tags

最后生成适合 Obsidian 的标签。

例如：

\#GBM\
\#CancerNeuroscience\
\#OPC-like\
\#NeuronTumorInteraction\
\#SingleCell\
\#SpatialTranscriptomics\
\#TumorEcosystem\
\#CellularPlasticity

---

# 26. Execution Rules

1. 不得虚构论文未报告的实验。
2. 找不到的信息写“Not reported”或“论文中未明确说明”。
3. 结论必须与证据对应。
4. 涉及具体 Figure 时尽可能标注 Figure 编号。
5. 用户追问某个细节时，优先回到原始论文证据，而不是仅依赖 Paper Card 摘要。
6. 对多篇论文进行比较时，以各自 Paper Card 为基础建立 comparison matrix。
7. Paper Card 应保持信息密度高，避免大段泛泛复述。
8. 专业术语保留英文，解释使用中文。
9. 对用户研究方向特别相关的信息可以适当展开，但不能改变作者原始结论。
10. 最终目标是建立一个可检索、可比较、可用于生成新科研假说的长期文献知识库。
