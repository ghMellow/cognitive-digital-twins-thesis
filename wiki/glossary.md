---
title: Thesis Glossary
type: concept
created: 2026-04-14
updated: 2026-04-14
sources: []
tags: [terminology, reference]
---

# Glossary — Cognitive Digital Twins

Canonical nomenclature and definitions established by the thesis.

---

## Core Concepts

### Digital Twin (DT)
Synchronized digital representation of a physical entity or process, capable of storing state, history, and enabling simulations.

### Cognitive Digital Twin (CDT)
Digital Twin augmented with cognitive capabilities (perception, reasoning, memory, learning) that operates autonomously and evolves throughout the entity's lifecycle. Canonical reference: **Zheng et al. (2022)**.

### Knowledge Graph (KG)
Semantic structure (graph of nodes and labeled edges) that represents facts, relationships, and operational constraints of a domain. In thesis context: representation of 5G constraints and validation rules for the Planning Agent.

### Multi-Agent System (MAS)
Collection of specialized autonomous agents coordinated to achieve a common objective through structured communication.

### LLM (Large Language Model)
Neural model trained on text corpus, exposed as API or hosted locally (Ollama + quantization).

---

## Cognitive Functions (Six CDT Pillars)

Follow the taxonomy of **Zheng et al. (2022)** and **Al-Haj Ali et al. (2025)**.

### Perception (Perception Agent)
Acquisition, normalization, and structuring of observational data from the physical system. Output: canonical 3GPP metrics.

### Reasoning (Reasoning Agent)
Inference on anomalies, correlations, root causes. Uses natural logic + KG. Output: structured diagnosis with confidence levels.

### Planning (Planning Agent)
Translation of diagnosis into concrete actions, validation against operational constraints stored in KG, selection of optimal action.

### Communication (Communication Agent)
Synthesis of perception-decision pipeline into user-readable explanation with causal argumentation.

### Memory
Persistence of state and history via Eclipse Ditto + Neo4j.

### Learning / Adaptation
Continuous evolution of KG and decision-making parameters (out of scope for MVP, defined as future work).

---

## Terminologia Dominio 5G

### gNB (gNodeB)
5G base station antenna. In simulator: 3GPP metrics generator.

### RSRP (Reference Signal Received Power)
Received reference signal power. Signal quality metric.

### SINR (Signal-to-Interference-plus-Noise Ratio)
Signal-to-interference-plus-noise ratio. Indicator of congestion and channel degradation.

### Handover
Transition of a communication from one cell to another. Failure rate is an indicator of instability.

### Throughput Downlink/Uplink
Data transfer speed. Degradation indicates resource anomalies or congestion.

### Latency
End-to-end delay. Critical metric for real-time services (eMBB, URLLC).

### KPI (Key Performance Indicator)
Aggregate performance metric. In thesis context: composite of RSRP, SINR, throughput, latency.

---

## Terminologia Architetturale

### Eclipse Ditto
Platform for digital twin management: state synchronization, WebSocket notifications, REST API. In context: backbone of digital representation (layers 2/3 of architecture).

### Neo4j
Graph database for Knowledge Graph. In context: storage of 5G operational constraints and Planning validation rules.

### LangGraph
Framework for orchestration of multi-step agents with explicit state management (LangChain + Langgraph). In context: runtime of cognitive pipeline.

### Supervisor Agent (LangGraph)
Coordination agent that routes incoming tasks to specialized agents. Implements routing, state management, decision tree. In context: central orchestrator of cognitive pipeline.

### StateGraph (LangGraph)
Data structure that represents the state graph of multi-agent pipeline. Each node is an agent/tool, each arc is a conditional transition.

### DKR (Dynamic Knowledge Repository)
Static offline knowledge graph that stores stable operational constraints (3GPP schema, safety rules). In context: Neo4j with 5G ontology. Contrast with DIKG.

### DIKG (Dynamic Instance Knowledge Graph)
Dynamic knowledge graph updated in real-time with the instantaneous state of the physical system. In context: Eclipse Ditto replica of gNB state. Contrast with DKR.

### Decision Sandbox
Pre-execution validation paradigm: the DT is not a passive mirror but a **test environment** where proposed actions are evaluated before execution on the real system. In context: Planning Agent verifies actions against KG.

### Ollama
Local LLM server with Q4/Q5 quantization. In context: hosting of Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B on M4 Pro.

### 3GPP
Telecommunication standard. In context: specification of simulated metrics format.

---

## Metodologia Valutazione

### LLM-as-Judge
Use of an LLM as evaluator of output quality from another LLM. In thesis context: Llama 3.1 70B evaluates causal coherence of Reasoning Agent diagnosis on a 1-5 scale (rubric-based). Mitigation: multiple judges, reference examples, confidence calibration.

### Multi-Model Agreement
Validation strategy through consensus among multiple LLMs on identical tasks. If Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B converge on the same root cause diagnosis, correctness probability → high. Disagreement = low confidence. In context: triangulation without external ground truth.

### Outcome Validity
Definitive metric: did the action proposed by the agent solve the real problem in the system? In thesis context: were simulator KPIs recovered beyond target threshold post-action? Binary Pass/Fail. This is the king metric of the entire evaluation.

### Verifiable vs Non-Verifiable Tasks
**Verifiable (Explicit Ground Truth):** Ditto API calls, KG constraint violations, JSON schema validation — answers are binary.  
**Non-Verifiable (LLM-as-Judge Necessary):** Root cause diagnosis, causal explanation — answers are qualitative, require evaluation.  
In context: maximize verifiable tasks with external ground truth, use LLM-as-judge only where necessary.

### Milestone-Based KPI
Decomposition of each task into flexible milestones monitored in real-time. In thesis context: each fault injection scenario has 6 milestones (perceived anomaly → root cause → diagnosis confidence → proposed action → KG validation → improvement). Partial score per milestone, not all-or-nothing.

### Task Score (TS)
Quality of an agent's final output. In context: Accuracy of Reasoning Agent diagnosis, feasibility of Planning Agent action, coherence of Communication Agent. Evaluated vs ground truth (simulator) or LLM-as-judge.

### Coordination Score (CS)
Quality of interaction between agents. In context: Perception→Reasoning→Planning→Communication pipeline state passage without context loss? Token efficiency? Graph traversal correctness? Separate from Task Score — you can have high TS but low CS (right agent, wrong coordination).

### Outcome Validity Metric
Pass → KPIs recovered > target threshold; Fail → KPIs stagnant or degraded. Evaluated post-action by Planning Agent on 3GPP simulator. It is the absolute ground truth of evaluation.

---

## Noted Terminological Variants

- **"Gemello Digitale Cognitivo"** vs **"Cognitive Digital Twin"** — use CDT as canonical acronym in English text, translate to Italian only when necessary.
- **"Agente"** vs **"Agent"** — Italian preference "agente" in thesis body, "agent" in code comments and papers.
- **"Knowledge Graph"** vs **"Knowledge Base"** — use KG for graph-oriented structures (Neo4j), KB for flat vocabularies. In thesis context: KG.

---

## Related Pages
- [[overview]]
- [[scaffolding-tesi]]
