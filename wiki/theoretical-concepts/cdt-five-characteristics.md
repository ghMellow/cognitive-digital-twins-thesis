---
title: CDT Five Characteristics Framework
type: concept
created: 2026-04-28
updated: 2026-04-28
sources: [sources/zheng-et-al-2022-cdt]
tags: [CDT, framework, architecture, evaluation]
---

# CDT Five Characteristics Framework

**Foundational framework defining what constitutes a true Cognitive Digital Twin. From Zheng et al. (2022).**

One-line summary: A CDT must possess cognitive capability, manage full lifecycle, operate autonomously, continuously evolve, and be designed for DT interaction.

---

## The Five Characteristics

### 1. Cognitive Capability

**Definition:** The system has autonomous cognitive abilities to perceive, reason, plan, and decide—not merely reflect or report state.

**Operationalization in thesis:**
- **Perception Agent** — autonomous acquisition and normalization of 5G metrics
- **Reasoning Agent** — autonomous diagnosis of root causes without human intervention
- **Planning Agent** — autonomous generation of corrective actions
- **Communication Agent** — autonomous synthesis of decisions into explanations

**Verification metric:** Can the CDT diagnose and propose actions without human intermediate prompts? Yes → ✅ Cognitive capability verified.

---

### 2. Full Lifecycle Management

**Definition:** The CDT persists and evolves throughout the entire operational lifecycle of the physical system—from commissioning through decommissioning.

**Operationalization in thesis:**
- **Static Memory (DKR):** 3GPP constraints stored in Neo4j—immutable across lifecycle, represent "laws of operation"
- **Dynamic Memory (DIKG):** Eclipse Ditto state history—captures evolution of gNB state over time
- **Learning Loop:** Benchmark evaluates how agents improve on repeated tasks (learning from past cycles)

**Verification metric:** Is historical state preserved? Can the system reference past decisions to improve future ones? Yes → ✅ Full lifecycle management verified.

---

### 3. Autonomy

**Definition:** The system makes decisions and executes actions independently, within governance guardrails—not merely recommendations for human approval.

**Operationalization in thesis:**
- **Autonomy Level 1 (Human-in-the-Loop):** CDT proposes action; human reviews Neo4j constraints + reasoning trace, approves/rejects
- **Autonomy Level 2 (Semi-Autonomous):** CDT executes if action passes KG shape validation; human monitors
- **Autonomy Level 3 (Autonomous):** CDT executes directly; human audits post-hoc via MD event log

**Verification metric:** Which autonomy level does the system achieve? Measured via MMCI maturity progression from Level 1 (SSA) → Level 3+ (autonomous).

---

### 4. Continuous Evolving

**Definition:** The CDT adapts its reasoning and decision-making over time as the physical system's conditions change—not static policies.

**Operationalization in thesis:**
- **Explicit Evolution:** Neo4j KG updated when new 3GPP constraints emerge (e.g., new cell configuration)
- **Empirical Evolution:** Comparative LLM benchmark shows improvement as models specialize on 5G tasks
- **Reactive Evolution:** Planning Agent adjusts action strategy based on past failures (fallback mechanisms)

**Verification metric:** Does the CDT's performance improve on repeated fault scenarios? Does reasoning adapt to new system conditions? Measured via task completion rate trends over benchmark runs.

---

### 5. DT-Based Design

**Definition:** The system is architecturally centered on a Digital Twin representation—not a secondary module—ensuring tight coupling between physical and digital models.

**Operationalization in thesis:**
- **Level 2 (Digital Twin Layer):** Eclipse Ditto maintains bidirectional sync with gNB state (WebSocket updates, REST API)
- **Level 3 (Cognitive Layer):** LangGraph agents query Ditto (not raw API), verify actions against Ditto state before execution
- **Verifiability:** Actions proposed by agents are verifiable against the DT state (Neo4j shape validation)

**Verification metric:** Is every cognitive decision grounded in the DT state? Can actions be traced back to DT observations? Yes → ✅ DT-based design verified.

---

## How the Five Characteristics Map to Thesis Contributions

| Characteristic | Thesis Contribution | Validation Method |
|---|---|---|
| **Cognitive Capability** | Contribution 1 + Contribution 2 | 4-agent architecture covers 6 CDT functions; CLASSic evaluation measures capability |
| **Full Lifecycle Management** | Contribution 1 + Architecture | MD-based event store + Neo4j DKR/DIKG |
| **Autonomy** | Contribution 2 (Evaluation Framework) | MMCI maturity levels measure autonomy progression |
| **Continuous Evolving** | Contribution 3 (Benchmark) | Comparative LLM evaluation shows model specialization |
| **DT-Based Design** | Contribution 1 (Architecture) | Eclipse Ditto bidirectional sync + Neo4j verification |

---

## Checklist: Is This a True CDT?

- [ ] **Cognitive Capability:** System makes autonomous decisions on perception, reasoning, planning
- [ ] **Full Lifecycle Management:** Historical state preserved; system references past for improvement
- [ ] **Autonomy:** Can operate at Level 1+ (human-in-the-loop minimum); can progress to Level 3
- [ ] **Continuous Evolving:** Reasoning adapts to new system conditions; performance improves over time
- [ ] **DT-Based Design:** Architecture is DT-centric; cognitive layer is not standalone module

**Result:** If all 5 are ✅, the system is a true CDT (Zheng et al. definition).

---

## Related Pages

- [[sources/zheng-et-al-2022-cdt]] — source paper
- [[cognitive-digital-twin]] — general CDT concept
- [[six-cognitive-functions]] — the 6 functions a CDT implements
- [[mmci-framework]] — how to measure autonomy progression
- [[scaffolding-tesi]] — thesis architecture mapped to characteristics
