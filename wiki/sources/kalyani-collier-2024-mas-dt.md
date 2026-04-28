---
title: "The Role of Multi-Agents in Digital Twin Implementation: A Short Survey"
type: source
created: 2026-04-14
updated: 2026-04-28
authors: [Yogeswaranathan Kalyani, Rem Collier]
year: 2024
publication: "ACM Computing Surveys, Vol. 57, No. 3"
sources: [kalyani-collier-2024, valore-tesi-riassunto]
tags: [MAS, DT, survey, systematic-review, multi-agent-patterns]
thesis-contribution: 1-architecture
---

# Kalyani & Collier (2024) — The Role of Multi-Agents in Digital Twin Implementation

**Authors:** Yogeswaranathan Kalyani, Rem Collier — University College Dublin  
**Published:** ACM Computing Surveys, Vol. 57, No. 3 — November 2024  
**DOI:** https://doi.org/10.1145/3697350  
**Thesis relevance:** **MEDIUM-HIGH** — Validates MAS+DT architecture patterns and highlights an evaluation gap

---

## 🎯 Core Idea

A **Systematic Literature Review (SLR)** mapping how **Multi-Agent Systems (MAS)** are integrated with **Digital Twins (DT)** to build autonomous and adaptive systems. Starting from ~16,100 Google Scholar results (2020–2024), the authors select and analyze **22 relevant papers** across four research questions.

**Paper thesis:** MAS and DT are complementary: DTs provide simulation and physical grounding; MAS provide coordination, autonomy, and adaptability. Their synergy enables intelligent systems.

---

## 📋 The 4 Research Questions

| RQ | Question | Short Answer |
|---|---|---|
| **RQ1** | Which domains use agents in DTs? | Manufacturing dominates (10/22); edge computing, agriculture, healthcare are emerging |
| **RQ2** | Which agent capabilities are leveraged? | Autonomous decision-making, scheduling, task allocation, real-time processing, simulation & optimization |
| **RQ3** | Which technologies are commonly paired with agents? | DRL, ABS, ontologies/KG, JADE, JaCaMo, SPADE, WLDT, 3D simulators |
| **RQ4** | Which gaps remain? | Scalability, interoperability, advanced AI/ML, privacy/security, reliability evaluation |

---

## 📊 Key Results

### Covered Domains

| Domain | # Papers | Maturity | Notes |
|---|---|---|---|
| **Manufacturing** | 10 | Mature | Factory DT, supply chain, quality control |
| **Edge Computing / CPS** | 5 | Niche | Vehicular DT, air mobility, resource allocation |
| **Smart Agriculture** | 3 | Emerging | Irrigation, crop monitoring, farm optimization |
| **Smart Cities** | 2 | Emerging | Traffic, energy grids |
| **Healthcare** | 2 | Emerging | Patient monitoring, hospital operations |

**Thesis insight:** 5G/telecom is absent → a domain gap that the thesis targets by positioning itself in edge computing / network management.

### Most Used Agent Capabilities

1. **Autonomous Decision-Making** — agents decide without human intervention
2. **Dynamic Scheduling** — real-time resource reallocation
3. **Cooperative Task Allocation** — a coordinator agent distributes tasks
4. **Real-Time Data Processing** — tight feedback loops (milliseconds)
5. **Simulation & Optimization** — agents test scenarios before execution

**Thesis relevance:** the 4 LangGraph agents (Perception, Reasoning, Planning, Communication) collectively implement these capabilities.

### Recurring Technology Stack

**Agent Frameworks:** JADE, JaCaMo, SPADE, custom frameworks  
**DT Platforms:** WLDT, Unity3D, Microsoft AirSim, custom simulators  
**Learning:** Deep Reinforcement Learning (DRL) dominante; alcuni rule-based e ontology-based  
**Knowledge:** Ontologie Semantic Web (RDF/OWL), Knowledge Graphs, domain-specific rule sets

**Difference vs thesis:** The 22 papers primarily use **classical DRL** or **rule-based agents**. **None use LLMs** as a cognitive layer. This supports the novelty claim.

---

## 🏗️ Proposed Architecture (Smart Agriculture Showcase)

The authors propose a **Web of Digital Twins** for open-environment arable farming with the following structure:

```
User Interface (input: farm_id, field_id, sowing_date)
    ↓
Microservices Layer
    ├── Weather Forecasting Service
    ├── Soil Analysis Service
    ├── Crop Growth Model (ML)
    └── Irrigation Scheduling Service
    ↓
Agent Layer
    ├── Manager Agent          — Orchestrazione
    ├── Farm Agent             — DT della farm
    ├── Field Agent            — Monitoraggio + sensori
    └── Recommendation Agent   — Output verso utente
    ↓
Knowledge Layer
    └── Semantic Web + Domain Ontologies (AGROVOC)
```

**Mapping to the thesis:**
- Manager Agent ← Planning Agent (overall orchestration)
- Farm Agent ← Perception Agent (DT state)
- Field Agent ← Perception Agent (sensor data)
- Recommendation Agent ← Planning + Communication (actionable decisions)
- Knowledge Layer ← Neo4j KG (domain knowledge, constraints)

---

## 🔴 Identified Gaps (Future Work)

| Gap | Description | Thesis Relevance |
|---|---|---|
| **Scalability & adaptability** | Not solved in any of the 22 papers | 🟡 Medium — local M4 Pro prototype is micro-scale; not the main focus |
| **Interoperability & standardization** | Each paper uses a different stack; no standard | 🔴 High — the thesis’ concrete stack (LangGraph+Ditto+Neo4j) can propose a pattern |
| **Advanced AI/ML integration** | Still shallow; DRL dominates; no LLMs | 🔴 **MAXIMUM** — this is exactly the gap the thesis addresses |
| **Reliability evaluation** | How to measure that an agent is “reliable”? | 🔴 **MAXIMUM** — MMCI provides a scaffold |
| **Privacy & security** | Mentioned but not addressed | 🟡 Medium — out of scope |
| **Domains beyond manufacturing** | Edge computing / network management under-explored | 🟡 Medium-High — the thesis explores this space |

---

## ✅ What This Adds to the Thesis

### 1. Architectural Validation

The 4-agent design (Perception, Reasoning, Planning, Communication) matches the agent-per-function pattern consolidated by the survey across the 22 papers. In Related Work you can cite: _"Our agent taxonomy aligns with established MAS+DT patterns (Kalyani & Collier, 2024)"_.

### 2. Knowledge Graphs Are a Standard Component

Kalyani et al. identify **ontologies and knowledge graphs** as recurring key components across multiple papers. This provides direct support for Neo4j as a best practice rather than an arbitrary choice.

### 3. Explicit Gap on Evaluation

The paper states: _"Evaluation methodologies for trustworthiness and reliability of multi-agent systems in DT are not adequately addressed"_. The thesis directly targets this gap (MMCI + multi-agent agreement + KG validation).

### 4. LLMs as a Cognitive Layer Are Genuinely New Here

None of the 22 papers uses LLM agents; most rely on DRL or rules. This implies:
- ✅ The thesis is novel (one of the first to combine LLM + MAS + DT in this way)
- ⚠️ But you cannot rely on this survey to justify model-level choices (e.g., Llama vs Mistral; 8B vs larger)
- 🟠 You must triangulate with LLM-agent evaluation sources (Berkeley MOOC, MultiAgentBench, WirelessAgent)

---

## ❌ Limitations for the Thesis

| Limitation | Impact |
|---|---|
| **No original experiments** | It is an SLR; you cannot extract quantitative performance metrics |
| **No LLMs** | The 22 papers use classic DRL/rules; Kalyani cannot guide model selection |
| **Manufacturing-heavy domain** | ~45% of papers are manufacturing; 5G is niche, making direct comparison harder |
| **No 5G/Telecom** | Entirely absent from the SLR; you need other points of comparison |
| **Evaluation remains open** | The SLR identifies the gap but does not solve it; the thesis must |

---

## 📝 Notes for Advisor

**Q: "Have you verified that your multi-agent design is supported by the literature?"**

A: "Yes — Kalyani & Collier (2024) analyze 22 MAS+DT papers and identify a recurring agent-per-function pattern (manager, data, processing, recommendation). Our design instantiates this pattern with Perception, Reasoning, Planning, Communication agents, which map directly to the capabilities recognized by the SLR."

**Q: "Why Neo4j rather than a Semantic Web ontology?"**

A: "Both approaches (Semantic Web vs property graphs) appear as best practices in the survey. Neo4j is chosen for real-time scalability (Cypher vs SPARQL latency) and because 3GPP constraints are naturally represented as dependency graphs (node=KPI, edge=causal relation) rather than OWL axioms."

**Q: "Which gaps are you filling relative to the SLR?"**

A: "Three main gaps: (1) advanced AI/ML (especially LLM agents) is not present in the 22-paper set; (2) trustworthiness evaluation remains open — the SLR provides no methodology; (3) 5G/network domains are missing entirely. The thesis addresses all three."

---

## 🔗 Concepts Linked

- [[theoretical-concepts/knowledge-graph-in-cdt]] — KG as a best-practice component
- [[sources/pretel-et-al-2024-mas-dt]] — Complementary SLR (64 papers vs 22)

---

## 📚 Papers Inside the Survey Worth Checking

| Authors | Title | Why Read |
|---|---|---|
| **Zhang et al., 2021** | Adaptive DT + Multi-agent DRL for vehicular edge computing | Closest to the domain: edge networks, resource allocation, adaptive agents |
| **Xu et al., 2023** | DT-driven collaborative scheduling via MAS, edge computing | Very close to the use case: edge resource scheduling |
| **Latsou et al., 2023** | Automated anomaly detection + bottleneck identification with MAS | Pattern inspiration for the Reasoning Agent; rule-based baseline |
| **Galuzin et al., 2022** | Knowledge-based multi-agent adaptive management | KG + agents for real-time decision-making |

---

## Related Pages

- [[sources/restart-2024-ndt]] — 5G domain context
- [[sources/burr-et-al-2026-agentic-dt]] — Risk taxonomy and governance
- [[sources/pretel-et-al-2024-mas-dt]] — Companion SLR (64 papers, 7 DT properties analysis)
- [[theoretical-concepts/knowledge-graph-in-cdt]] — KG as standard component
- [[glossary]] — Terminology
