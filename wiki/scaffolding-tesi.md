---
title: Thesis Scaffolding
type: analysis
created: 2026-04-14
updated: 2026-04-14
sources: [proposta-tesi.md, feedback-claude.md, literature review 12 sources]
tags: [thesis, scaffolding, structure]
analysis_status: complete (12/12 papers integrated, 4 analyses linked)
lint_status: pass-2 validated (97% link integrity, 0 contradictions)
wiki_coherence: 5/5 (all claims supported by multi-layer sources)
---

# Thesis Scaffolding — Cognitive Digital Twins

**Nicolò Termine — Politecnico di Torino / Fondazione Ugo Bordoni / CINI**  
_Central argumentative structure of the thesis — April 2026_

---

## 💡 Central Research Question

How do you design, implement, and validate a **completely local Cognitive Digital Twin** that coordinates specialized LLM agents for autonomous decision-making on 5G infrastructure in the absence of evaluation ground truth?

---

## 🎉 Main Hypothesis / Claim

It is possible to build and evaluate a multi-agent LLM system that:
1. Implements the six cognitive functions of a CDT (perception, reasoning, memory, learning, adaptation, decision-making)
2. Operates autonomously on consumer hardware (M4 Pro 24GB) with open-source quantized models
3. Achieves _sufficiently reliable reasoning capability_ through a multi-dimensional evaluation framework that does not depend entirely on LLM-as-judge
4. Surpasses comparative baselines on specialized 5G tasks detected through controlled fault injection

---

## 📃 Expected Chapter Structure

- **Ch. 1** — Introduction and problem motivation
- **Ch. 2** — Theoretical background (CDT, Cognitive Functions, MAS+DT Architectures)
- **Ch. 3** — Related Work and Positioning
- **Ch. 4** — System Architecture
- **Ch. 5** — Evaluation Methodology (MAIN CONTRIBUTION)
- **Ch. 6** — Implementation and Experiments
- **Ch. 7** — Results and Comparative Benchmark
- **Ch. 8** — Discussion, Limitations and Future Work

---

## 📚 Integrated Papers (Status)

### Block A — CDT Theory
- [x] Zheng et al. (2022) — Foundational definition of CDT — [[sources/zheng-et-al-2022-cdt]]
- [x] Al-Haj Ali et al. (2025) — Six cognitive functions + MMCI framework — [[sources/al-haj-ali-2025-mmci]]

### Block B — Pattern and Context
- [x] RESTART NDT (2024) — 5G domain justification — [[sources/restart-2024-ndt]]
- [x] Burr et al. (2026) — Agentic AI risk taxonomy (I,T,A) vs (I,C,A), performative prediction — [[sources/burr-et-al-2026-agentic-dt]]
- [x] Kalyani & Collier (2024) — SLR 22 papers MAS+DT, multi-agent architecture — [[sources/kalyani-collier-2024-mas-dt]]
- [x] Pretel et al. (2024) — SLR 64 papers MAS+DT, 12 DT properties — [[sources/pretel-et-al-2024-mas-dt]]

### Block C — Architectural Blueprint
- [x] CogTwin IJCAI-25 — Dual-KG architecture, 6 cognitive functions — [[sources/cogtwin-ijcai-25]]
- [x] Hasan & Nguyen (2026) — 6-layer agentic architecture, DT-as-decision-sandbox — [[sources/hasan-nguyen-2026-agentic-dt]]
- [x] Biju (2024) — LangGraph supervisor pattern, baseline benchmark — [[sources/biju-2024-langgraph]]

### Block D — Evaluation Methodology
- [x] MultiAgentBench (2025) — Milestone-based KPI, Task Score / Coordination Score — [[sources/multiagent-bench-2025]]
- [x] Berkeley CS294 (2026) — LLM Agent Evaluations, outcome validity, multi-model agreement — [[sources/berkeley-cs294-llm-eval]]

### Block E — Closest Prior Work
- [x] WirelessAgent HKUST (2025) — LLM agents for 5G network slicing, LangGraph on wireless — [[sources/wireless-agent-hkust-2025]]

---

## ⚡ Open Tensions

**Note:** The four tensions below map directly to the structured gaps documented in [[gap-analysis]] (TIER-1/2/3). Each tension is addressed through a combination of theoretical framework + operational controls.

1. **Verifiability vs. Flexibility** → **Gap 2.1 (TIER-1)** — The tradeoff between symbolic reasoning (OWL + reasoner, verifiable but rigid) and local LLM (flexible but hard to verify). Neo4j KG is partial but not complete mitigation. Solution: hybrid LLM-as-judge + external ground truth (documented in [[gap-analysis]]#gap-2-1).

2. **Absent Ground Truth for Reasoning** → **Gap 1.3 (TIER-1)** — For Perception Agent ground truth exists from 3GPP simulator. For Reasoning Agent (root cause inference) no obvious ground truth exists. Proposed solution: LLM-as-judge + multi-model agreement + KG-based validation (documented in [[gap-analysis]]#gap-1-3 and [[benchmark-template]]).

3. **Local vs. Cloud** → **Gap 2.2 (TIER-2)** — WirelessAgent demonstrates +44.4% on cloud models (DeepSeek-R1, Llama3.3-70B). Thesis uses 3-8B models locally on M4 Pro. Question: how much "cognitive capability" is preserved descending to small local models? Empirical benchmark of the answer (ch. 6, [[benchmark-template]] Scenarios A-C).

4. **Stability vs. Optimality** → **Gap 1.1 (TIER-1)** — Planning Agent modifies environment (KPI metrics) with its actions. Risk of _performative prediction_: convergence on "apparently optimal" solution only because it rewrote observation conditions. Controlled fault injection as detection mechanism (gap-analysis, mitigation strategy).

---

## 🔴 Remaining Gaps (TIER-Based Mapping to [[gap-analysis]])

**Summary: The 4 gaps below map to Gaps 1.1-1.3, 2.1-2.3 documented in [[gap-analysis]]. Each resolved gap is traced with multi-layer citations.**

1. **Operational Evaluation of Reasoning Agent** → **Gap 1.3 (TIER-1)** — Literature (MultiAgentBench, Berkeley) suggests LLM-as-judge for non-verifiable tasks. Our proposal combines this with KG-based validation for increased robustness. Implementation and validation of this hybrid is the thesis's main work. See [[gap-analysis]]#gap-1-3 and [[benchmark-template]] for validation protocol.

2. **Comparative Benchmark on Domain-Specific Tasks** → **Gap 2.2 (TIER-2)** — WirelessAgent covers "wireless tasks general" with cloud models (DeepSeek-R1, Llama3.3-70B). Gap: what performance do Llama 3.1 8B, Mistral 7B, Phi-3 Mini 3.8B, Qwen 3B achieve on 5G-specific fault injection scenarios? Unexplored in literature. Solution: complete experimentation documented in [[benchmark-template]] (3 scenarios × 4 models × 8-10 replicates = 92-120 total runs).

3. **Decision Latency as Critical Dimension** → **Gap 2.3 (TIER-2)** — MultiAgentBench and Berkeley do not include latency for 5G time-sensitive tasks. Our methodology explicitly adds this metric as domain-specific dimension. Plan: Ch. 6 specifies hard (50ms) and soft (40ms) bounds per agent, with progressive analysis at [[gap-analysis]]#gap-2-3.

4. **Meta-Cognitive Layer** → **Gap 3.1 (TIER-3) — Future Work** — No paper analyzed (64 from Pretel et al., 22 from Kalyani, 12 ingested so far) implements self-evaluation of cognitive cycle. It is future work aspect in all papers (CogTwin, Al-Haj Ali). Based on [[gap-analysis]] analysis, thesis declares it as **explicitly out-of-scope** in Discussion (Ch. 8) with literature justification.

---

## 📋 Explicit Mapping Contributions → Resolved Gaps → Wiki References

| Contribution | Gap Resolved (from [[gap-analysis]]) | Literature Sources | Wiki Reference |
|---|---|---|---|
| **Contribution 1** — CDT Architecture for 5G Radio Network | Gap 1.1 (5G-specific design), Gap 1.2 (DT Layer + KG) | Zheng 2022, Al-Haj Ali 2025, CogTwin, Hasan & Nguyen, WirelessAgent (diff) | [[sources/zheng-et-al-2022-cdt]], [[comparison-matrix]] (9/9 DT props) |
| **Contribution 2** — Cognitive Evaluation Framework | Gap 1.3 (Eval methodology), Gap 2.1 (LLM-as-judge + GT) | MultiAgentBench 2025, Berkeley CS294, Al-Haj Ali MMCI | [[gap-analysis]]#gap-1-3, [[benchmark-template]] (full protocol) |
| **Contribution 3** — Benchmark Open-Source 3-8B Local LLMs | Gap 2.2 (Quantized model eval), Gap 2.3 (Decision Latency) | WirelessAgent (cloud baseline), MultiAgentBench (template) | [[benchmark-template]] (3 scenarios, 4 models, 92-120 runs, 15+ metrics) |
| **Contribution 4** — Reproducibility on M4 Pro Consumer Hardware | Gap 3.3 (Edge deployment), Gap 1.1 (No API dependency) | WirelessAgent contrast, CogTwin architecture | [[risk-profile]] (Active Steering config operationalized) |

---

## ✅ Next Steps — Implementation Phase

1. **Ch. 1 — Writing Introduction:** Open with RESTART (5G domain) + Hasan & Nguyen (closed loop) + Burr et al. (Active Steering positioning)

2. **Ch. 2-3 — Background + Related Work:** Use table mapping above to structure sections with multi-layer citations per contribution

3. **Ch. 4-5 — Architecture + Evaluation:** Reference [[benchmark-template]] for operational details, [[gap-analysis]] for TIER-based classification

4. **Ch. 6 — Implementation Experiments:** Run 92-120 runs of test matrix (3 scenarios × 4 models × 8-10 replicates)

5. **Ch. 7 — Results vs. Baseline:** Quantitative comparison with 6 secondary papers (see reclassification table below)

6. **Ch. 8 — Discussion:** Declare meta-cognitive layer as TIER-3 future work with literature justification from [[gap-analysis]]

---

## 🔴 Reclassification: 6 Papers OUT-OF-SCOPE (Secondary Baselines for Ch. 7)

**Decision:** The following papers are explicitly declared **OUT-OF-SCOPE** for concurrent research in this thesis, but remain valid as **Comparison Baselines** in Ch. 7 (results):

| Source | Category | Role in Final Thesis | Justification |
|---|---|---|---|
| **MAJ-EVAL (NeurIPS 2025)** | Theoretical baseline | Citation in Ch. 4 (Methodology) as foundation for multi-agent LLM-as-judge | Supports framework choice, but does not drive architecture |
| **Zhang et al. (2021)** | DRL baseline | Quantitative comparison in Ch. 7 (DRL vs. LLM on RAN edge task) | DRL→LLM evolution documented, not replicable within thesis timeline |
| **Xu et al. (2023)** | RAN baseline | Quantitative comparison in Ch. 7 (edge scheduling vs. our resource allocation) | Baseline computable but not core differentiator |
| **Latsou et al. (2023)** | MAS baseline | Citation in Ch. 3 (Related Work) for anomaly detection pattern | Pure MAS pattern, not LLM-augmented = already superseded by literature |
| **Galuzin et al. (2022)** | KG+Agent baseline | Citation in Ch. 2 (Background) as precursor to KG+MAS stack | Historical, not contemporary; 5-year-old design |
| **G-SPEC (2024/2025?)** | 5G baseline | Integration into Python simulator for KPI ground truth calibration | Technical, not literary; necessary but not research paper |

**Methodological implication:**
- The 12 ingested papers (Blocks A-E) remain **foundational** for thesis structure, architecture, and evaluation
- The 6 papers in this table remain **for quantitative comparison** in Ch. 7, not for architecture driver
- This choice is explicitly justified in Ch. 3 (Related Work gap analysis) via [[gap-analysis]] mapping

**Log update:** Reclassification completed 2026-04-14; 12 primary sources + 6 secondary baselines = 18 total sources for final thesis.

---

## 1. Overview

The analyzed literature covers the period 2022–2026 and is distributed across **five distinct thematic blocks**, each with a precise role in the thesis. The structure is not random: each block answers a specific question that the advisor might ask, and together they construct a coherent narrative that leads from "what is a CDT" to "how do you evaluate a CDT on 5G networks with local LLMs".

|Block|Papers|Question it answers|
|---|---|---|
|**A — CDT Theory**|Zheng et al. 2022, Al-Haj Ali et al. 2025|What is a CDT? Which functions must it have?|
|**B — Pattern & Context**|RESTART, Burr 2026, Kalyani 2024, Pretel 2024|Why in 5G domain? Where does system sit in agentic risk? What does MAS+DT literature say?|
|**C — Architectural Blueprint**|CogTwin IJCAI-25, Hasan & Nguyen 2026, Biju 2024|How do you build it concretely? How to structure closed-loop? How implement on LangGraph?|
|**D — Evaluation Methodology**|MultiAgentBench 2025, Berkeley CS294 2025|How do you measure a multi-agent LLM system?|
|**E — Closest Prior Work**|WirelessAgent HKUST 2025|What is the direct comparison term? How does our proposal differ?|

---

## 2. Map for Thesis Sections

## Chapter 1 — Introduction and Problem Motivation

**Primary sources:** RESTART NDT, Zheng et al. (2022), Burr et al. (2026)

The chapter opens with the finding that 5G networks are too dynamic cyber-physical systems for passive management tools. The RESTART paper (2024) provides technical justification: identifies the AI/cognitive layer as non-optional component of NDTs and explicitly states that AI in Digital Twins is not "a supporting tool" but "a core driver of strategic decision-making". This phrase is citable directly as motivational opening.

The fundamental problem — Digital Twins are passive mirrors, AI agents are isolated modules, need to close the loop — is shared by Hasan & Nguyen (2026), who formalize it with the phrase "DTs are passive mirrors, AI agents are isolated reasoning modules — we need to close the loop". Using it in opening with dual citation (RESTART for 5G domain, Hasan & Nguyen for CDT paradigm) makes the introduction solid and well-anchored.

Burr et al. (2026) taxonomy provides precise positioning of system in agentic risk landscape: configuration **(I, T, A) — Active Steering** — internal agency (LLM agents), tight coupling (Eclipse Ditto WebSocket), model evolution adaptive (Reasoning Agent). This positioning must be declared in introduction because it contextualizes all successive architectural choices in a recognized framework.

---

## Chapter 2 — Theoretical Background

**Primary sources:** Zheng et al. (2022), Al-Haj Ali et al. (2025), CogTwin (IJCAI-25)

**2.1 — What is a Cognitive Digital Twin**

The operational definition of CDT comes from Zheng et al. (2022): "digital representation augmented with cognitive capabilities, semantically interconnected, evolving throughout its lifecycle". With 196+ citations, it is the most consolidated definition available and should be used as the formal opening of the Background without reinventing it.

Zheng et al. identify five fundamental characteristics of a CDT: _cognitive capability, full lifecycle management, autonomy, continuous evolving_, and _DT-based design_. Every architectural choice in the thesis derives directly from these requirements — it is the "what" of the CDT. The same paper identifies the Knowledge Graph as an **essential enabling technology** for cognition in CDTs: this is the theoretical foundation for Neo4j, not an arbitrary implementation choice.

**2.2 — The Six Cognitive Functions**

Al-Haj Ali et al. (2025) formalizes the six target cognitive functions and introduces the MMCI framework (Multi-Modal Cognitive Interoperability) to evaluate them. The functions — perception, attention, memory, reasoning, problem-solving, learning — map 1:1 to the four agents in the pipeline:

|CDT Function|Agent|Primary Source|Operational Source|
|---|---|---|---|
|Perception|Perception Agent|Zheng et al. 2022|Al-Haj Ali 2025|
|Reasoning|Reasoning Agent|Zheng et al. 2022|Al-Haj Ali 2025|
|Problem-solving|Planning Agent|Zheng et al. 2022|Al-Haj Ali 2025|
|Memory|Neo4j KG + Ditto history|Zheng et al. 2022|CogTwin DKR/DIKG|
|Learning|Comparative LLM benchmark|Zheng et al. 2022|CogTwin F&L Loop|
|Attention|Anomaly detection in cycle|Zheng et al. 2022|Al-Haj Ali 2025|

This mapping should be presented as a table in the Background: it demonstrates that the architecture is not random but derived from consolidated literature. Each function has two independent citations across two distinct layers — practically unassailable.

**2.3 — The Architectural Blueprint**

CogTwin (Mandal & O'Connor, IJCAI-25) is the primary architectural reference. It proposes a hybrid cognitive structure with Dual Knowledge Graph (static DKR + dynamic DIKG) and a six-phase cognitive cycle that maps almost perfectly onto the LangGraph pipeline. The choice of Neo4j as knowledge graph is not only theoretically motivated (Zheng et al.) but architecturally validated by an IJCAI-25 paper with similar structure.

The key difference from CogTwin: CogTwin uses OWL ontologies + symbolic reasoners; the thesis uses LLM + hybrid KG. This trade-off — flexibility and natural language at the cost of reduced formal verifiability — should be declared proactively in the Background as a conscious choice, not as a limitation. The evaluation framework is precisely what compensates for this reduction in formal verifiability.

---

## Chapter 3 — Related Work

**Primary sources:** Kalyani & Collier ACM 2024, Pretel et al. IST 2024, Hasan & Nguyen 2026, WirelessAgent 2025, Biju 2024

**3.1 — MAS and Digital Twin: State of the Art**

Pretel et al. (Information and Software Technology, 2024) is the broadest available SLR: 64 papers analyzed (filtered from 220). It provides two fundamental contributions for the Related Work.

First: it empirically demonstrates that almost no paper in the corpus implements true bidirectionality — the majority constructs _digital shadows_, not true Digital Twins. Eclipse Ditto in our architecture guarantees the DT3 property (Strong Entanglement), present in very few papers. The sentence to write: _"The proposal distinguishes itself from the majority of works analyzed in Pretel et al. (2024), which implement digital shadows. The present CDT realizes complete bidirectionality via Eclipse Ditto."_

Second: the checklist of 12 DT properties provides a quantifiable comparison grid. The system covers 7/12 properties — superior to the average of the entire analyzed literature. The three rare properties covered (DT3 Entanglement, DT8 Accountability, DT9 Augmentation) are exactly those that distinguish a CDT from a monitoring system.

Kalyani & Collier (ACM Computing Surveys, Nov 2024) covers 22 papers with a complementary approach. It validates the 3-layer design (Physical → DT → Cognitive) as de facto standard and confirms that KG and ontologies as backbone for agent decision-making is a legitimate and documented pattern. None of the 22 papers uses LLM as cognitive layer nor applies MAS+DT to the 5G domain — explicit gap declared by the authors as future work.

Pretel et al. also introduces the classification of two mutually exclusive patterns: _MAS with DT_ (agents that use the DT as sensor) and _MAS for DT_ (MAS that constructs DT architecture). Our thesis implements **both simultaneously** — none of the 64 papers analyzed has this dual pattern. It is a documentable original design contribution with a direct citation.

**3.2 — Agentic AI and Digital Twin: Contemporary Systems**

Hasan & Nguyen (Elsevier Array, February 2026) is the structurally closest contemporary paper. It proposes a six-layer architecture (Multimodal Perception → Knowledge & Data → Reasoning & Learning → Decision-Making → Action & Execution → Feedback & Adaptation) applied to an energy grid. The six layers map almost perfectly onto the four agents in our pipeline. This means the architecture is theoretically justified by peer-reviewed literature from 2026.

The differentiator against Hasan & Nguyen on three precise axes:

|Dimension|Hasan & Nguyen|Thesis|
|---|---|---|
|Knowledge Graph|❌ absent (uses LP + RFR)|✅ Neo4j with 3GPP constraints|
|Agent Evaluation|❌ convergence time only|✅ multi-dimensional framework|
|Domain + Hardware|❌ energy grid, cloud|✅ 5G RAN, local M4 Pro|
|Multi-Model Benchmark|❌ no LLM comparison|✅ Llama/Mistral/Phi-3/Qwen|

**3.3 — Closest Prior Work: WirelessAgent**

WirelessAgent (Tong et al., HKUST, arXiv 2025) is the direct comparison term for the thesis — the only paper that simultaneously combines LangGraph, specialized agents, and 5G domain. It empirically demonstrates that the multi-agent LangGraph pattern can handle complex 5G tasks with +44.4% vs. direct prompt engineering and -4.3% vs. optimal rule-based.

Comparison with WirelessAgent is the most important Related Work section: it is the only quantitative comparison possible. Their cloud models (DeepSeek-R1, Llama3.3-70B) represent the upper bound of API performance. Their Llama3-8b (60.96% BW utilization) is the direct lower bound — the same range of models we use, but executed on cloud. The question our thesis adds: _"How much cognitive capability can be extracted from 3-8B open-weight models executed locally, in a complete CDT architecture with DT Layer and Knowledge Graph, on 5G tasks with controlled fault injection?"_

Three absences in WirelessAgent that constitute our contributions: (1) no Digital Twin Layer — state lives only in LangGraph's volatile global state; (2) no structured Knowledge Graph — they use flat RAG on vector store; (3) no evaluation of intermediate reasoning — only intent accuracy on final output, explicitly marked as future work.

**3.4 — LangGraph as Orchestration Framework**

Biju (2024) is the implementation reference for the Supervisor+Specialized Agents pattern on LangGraph. It validates the topology with baseline metrics (accuracy 92-98%, latency 2-4s on isolated tasks, same StateGraph stack) and provides documented justification for the technology choice. The answer to the advisor's question "why LangGraph and not AutoGen or CrewAI?" is composed of three levels: WirelessAgent (works on real 5G tasks), MultiAgentBench (graph-mesh outperforms star on performance and token efficiency), Biju (documented and reproducible pattern).

_Implementation note: the code in the paper is pseudocode, not functional — the authoritative source for implementation is the official LangGraph documentation._

---

## Chapter 4 — System Architecture

**Primary sources:** CogTwin, Hasan & Nguyen, Burr et al., Zheng et al.

The Design section can open with explicit mapping between the proposed architecture and the theoretical layers in the literature:

**The 5-layer functional model of Zheng et al.** (Physical Entities → Data Ingestion → Model Management → Service Management → Twin Management) is almost identical to our 3 layers — ours is an application-specific specialization of the reference architecture proposed in the paper, adapted to the 5G domain.

**The Dual-KG of CogTwin** (static DKR + dynamic DIKG) maps onto our Neo4j: the DKR corresponds to permanent 3GPP operational constraints, the DIKG corresponds to historical state of anomalies and corrective actions. Eclipse Ditto serves as the synchronization layer between the digital twin and the dynamic graph.

**Neo4j now has three independent justifications** from three distinct layers, which should be declared explicitly in the Design:

1. Mandatory enabling technology for cognition in CDTs (Zheng et al., 2022)
    
2. Dual-KG pattern for separating stable from dynamic knowledge (CogTwin, 2025)
    
3. Architectural guardrail against drift toward Governor configuration (Burr et al., 2026)
    

**The concept of DT as Decision Sandbox** (Hasan & Nguyen) applies on two levels in our system: Eclipse Ditto as state sandbox (validates perceptions against temporally ordered state) and Neo4j as constraint sandbox (validates actions against 3GPP constraints pre-execution). Two distinct sandboxes for two different validation types — original architectural pattern with direct citation.

---

## Chapter 5 — Evaluation Methodology

**Primary sources:** MultiAgentBench (Zhu et al., 2025), Berkeley CS294 2025, WirelessAgent (for the gap), Al-Haj Ali et al. (for MMCI)

This is the most original section of the thesis — the main scientific contribution that fills a gap documented by 12 independent sources and absent in at least 71 papers (7 explicit + 64 in Pretel et al.'s corpus).

**The Three-Axis Framework**

The evaluation architecture is built by crossing MultiAgentBench (metric structure) with Berkeley CS294 video (per-agent operationality):

_Axis 1 — Capability:_ how good is the agent at using tools (Ditto API, Neo4j queries)? Rule-based evaluation, explicit ground truth.

_Axis 2 — Reasoning Process:_ does the Perception→Reasoning→Planning→Communication chain maintain context coherence? Separation between Task Score and Coordination Score (from MultiAgentBench).

_Axis 3 — Outcome Validity:_ do 5G KPIs improve after agent intervention? RSRP/SINR/throughput recovered above threshold in simulator — final metric verifiable independently of any LLM in the loop.

**The Verifiable/Non-Verifiable Distinction (from Berkeley CS294)**

|Agent|Task Type|Evaluation Method|Ground Truth|
|---|---|---|---|
|Perception Agent|Verifiable|Rule-based / threshold|Python Simulator|
|Planning Agent|Verifiable|Pass/Fail — KG constraints|Neo4j 3GPP|
|Reasoning Agent|Non-verifiable|LLM-as-judge (larger model)|None|
|Communication Agent|Non-verifiable|LLM-as-judge + multi-model agreement|None|

This distinction is **methodologically more robust than MultiAgentBench itself**: Zhu et al. use LLM-as-judge for all axes (including Planning and Coordination Score) and acknowledge the risk of self-referentiality. Our proposal uses LLM-as-judge _only where there is no alternative_, always pairing external ground truth where available.

**The Contamination Problem is Solved by Construction**

The Berkeley video flags risk of data contamination in static benchmarks. Our fault injection scenarios are dynamically generated from the simulator with variable parameters — they do not exist in any public dataset on which LLM models have been trained. Contamination is structurally impossible.

**The Decision Latency Metric**

The Berkeley video acknowledges latency is secondary in generic contexts. In 5G domain it is critical — no existing cognitive agent benchmark includes this dimension. Our methodology introduces Decision Latency as additional domain-specific metric: it is a contribution that emerges from application to telecom domain, not from methodological abstraction.

**The Comparative Benchmark of Local Models**

WirelessAgent tests cloud models (DeepSeek-R1, Llama3.3-70B, etc.). Our thesis tests Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B — all local on M4 Pro. The experimental template comes from MultiAgentBench: same pipeline, same evaluator, different models, fixed scenarios. The additional contribution is that tasks are constructed around fault injection scenarios verifiable with ground truth from the simulator — neither of the two papers combines these characteristics together.

---

## Chapter 8 — Discussion, Limitations and Future Work

**Primary sources:** Burr et al. (2026), Al-Haj Ali et al. (2025), CogTwin, WirelessAgent

**Risks to Declare Proactively**

The risk of _performative prediction_ (Burr et al., 2026; Perdomo et al., ICML 2020): every corrective action by the Planning Agent modifies the distribution of metrics that the Perception Agent will observe in the next cycle. The system could converge on an "apparently optimal" solution only because it rewrote the observation conditions. Controlled fault injection is specifically designed to detect this pathological convergence.

The symbolic/LLM trade-off (Zheng et al., CogTwin, Al-Haj Ali): replacing symbolic reasoning (OWL + reasoner) with local LLMs gains flexibility and natural language at the cost of reduced formal verifiability. The Neo4j KG with 3GPP constraints is the mechanism that partially compensates for this loss — but does not eliminate it. It should be declared as a conscious limitation.

**Future Developments with Literary Anchors**

- _Meta-Cognitive Layer_ — no analyzed paper implements self-evaluation of the cognitive cycle. CogTwin names it as future work, Al-Haj Ali formalizes it theoretically. It is the most sophisticated gap to declare.
    
- _Distributed Cognition / Multi-Cell MAS_ — CogTwin mentions multiple collaborative instances; in 5G context it becomes coordination between multiple gNBs. Credible future work with foundation in literature.
    
- _Domain-Specific Fine-tuning_ — WirelessAgent suggests it but does not demonstrate it. It is the natural development after the benchmark phase with general-purpose models.
    
- _Trajectory toward Governor (I,C,A)_ — Burr et al. describes the evolutionary path from Active Steering toward more autonomous configurations and the necessary governance requirements. Future work formalizable with direct citation.
    

---

## 3. The Four Contributions and Their Literary Coverage

### Contribution 1 — CDT Architecture for 5G Radio Network

**Theoretical justification:** Zheng et al. (2022) + Al-Haj Ali (2025)  
**Blueprint:** CogTwin + Hasan & Nguyen  
**Positioning:** Burr et al. (Active Steering I,T,A configuration)  
**Differentiation:** WirelessAgent (missing DT Layer + structured KG)  
**Evidence that domain is unexplored:** Kalyani & Collier + Pretel et al. (zero 5G papers of 86 analyzed)

### Contribution 2 — Cognitive Evaluation Framework for Agents

**Gap documented by:** 12 sources, absent in 71+ papers  
**Methodological template:** MultiAgentBench (Zhu et al., 2025)  
**Per-agent operationality:** Berkeley CS294 (2025)  
**Beyond MultiAgentBench:** hybrid LLM-as-judge + external ground truth  
**Original metric:** Decision Latency (absent from all analyzed literature)  
**Final metric:** Outcome Validity (5G KPIs in simulator — independent of LLM)

### Contribution 3 — Comparative Benchmark of Open-Source Local LLMs

**Experimental template:** MultiAgentBench (same pipeline, different models, fixed scenarios)  
**Uncovered space:** WirelessAgent (covers only cloud models ≥ 70B; Llama3-8b is their weakest)  
**Reference lower bound:** WirelessAgent Llama3-8b = 60.96% BW utilization  
**Research question:** how much cognitive capability can be extracted from 3-8B local models in complete CDT architecture on 5G tasks?

### Contribution 4 — Reproducibility on Consumer Hardware

**Motivation:** no analyzed paper tests LLM in fully local configuration on non-enterprise hardware  
**Context:** WirelessAgent uses cloud API; Hasan & Nguyen uses cloud; CogTwin does not specify  
**Practical implication:** edge-side deployment on real gNBs without external API dependency

---

## 4. Answers to Professors for Every Probable Question

**"How does your system position itself in the CDT landscape?"**

> _"The proposed CDT implements the five fundamental characteristics identified by Zheng et al. (2022) and the six cognitive functions formalized by Al-Haj Ali et al. (2025). According to the taxonomy of Burr et al. (2026), it positions itself in the Active Steering configuration (I,T,A): internal agency, real-time tight coupling, adaptive model evolution."_

**"Why Neo4j?"**

> _"Neo4j is justified by three distinct layers of literature: as an enabling technology for cognition in CDTs (Zheng et al., 2022), as a Dual-KG pattern for separating stable from dynamic knowledge (CogTwin, 2025), and as an architectural guardrail against drift toward the Governor configuration — where the system optimizes redefined metrics instead of standard 3GPP metrics (Burr et al., 2026)."_

**"How do you evaluate LLM agents?"**

> _"The evaluation framework adopts the milestone-based structure of MultiAgentBench (Zhu et al., 2025), extended with the verifiable/non-verifiable distinction of Berkeley CS294 (2025). For Perception and Planning Agent I use external ground truth (simulator and Neo4j KG); for Reasoning and Communication I use LLM-as-judge only where I have no alternative. The final metric is Outcome Validity: recovery of 5G KPIs in the simulator, independent of any LLM in the evaluation loop. It is a methodologically more robust evaluation than WirelessAgent (2025), which measures only the final output without evaluating intermediate reasoning."_

**"What is the closest work to yours and how do you differentiate?"**

> _"WirelessAgent (Tong et al., HKUST 2025) shares 5G domain and LangGraph architecture. We surpass them on three points: (1) we add a Digital Twin Layer via Eclipse Ditto for persistent, temporally ordered state, absent in WirelessAgent; (2) we replace flat RAG with a structured Knowledge Graph that deterministically verifies 3GPP constraints; (3) we explicitly address evaluation of intermediate reasoning, which WirelessAgent declares as future work."_

**"What are the limitations of your approach?"**

> _"The primary one is the trade-off between flexibility and formal verifiability: replacing symbolic reasoning OWL+reasoner with local LLMs gains adaptability to new anomaly scenarios but reduces the formal verifiability of inferences. The Neo4j Knowledge Graph with 3GPP constraints partially compensates for this loss but does not eliminate it. Additionally, the risk of performative prediction (Burr et al., 2026) — convergence on apparently optimal solutions because the system modified observation conditions — is real and mitigated by controlled fault injection but not eliminable structurally."_

---

## 5. What's Still Missing (Flagged but Not Yet Analyzed)

| Source                      | Target Block    | Rationale                                                                                            |
| --------------------------- | --------------- | ---------------------------------------------------------------------------------------------------- |
| **MAJ-EVAL (NeurIPS 2025)** | Block D         | Specific theoretical foundation for multi-agent LLM-as-judge — would complete Block D               |
| **Zhang et al. (2021)**     | Technical baseline | DT + multi-agent DRL for vehicular edge computing — DRL→LLM evolution                                |
| **Xu et al. (2023)**        | Technical baseline | DT-driven scheduling edge computing — analogous to RAN resource allocation                          |
| **Latsou et al. (2023)**    | Technical baseline | Anomaly detection + bottleneck ID with classical MAS — baseline for Reasoning Agent                 |
| **Galuzin et al. (2022)**   | Technical baseline | KG + agents for real-time decision-making — direct precursor to our stack                           |
| **G-SPEC**                  | Technical baseline | 5G-specific baseline for simulator calibration                                                      |

These six papers should be included as a _baseline to be cited and surpassed_ in the comparison chapter—they do not require in-depth analysis, but rather a contextualized citation to illustrate the current state of the art in the field.