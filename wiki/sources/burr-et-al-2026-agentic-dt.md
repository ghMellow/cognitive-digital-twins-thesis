---
title: "Agentic Digital Twins: A Taxonomy of Capabilities for Understanding Possible Futures"
type: source
created: 2026-04-14
updated: 2026-04-28
authors: [Christopher Burr, Mott MacDonald, Alan Turing Institute]
year: 2026
sources: [burr-2026-agentic-dt, valore-tesi-riassunto]
tags: [agentic-systems, risk-taxonomy, performative-prediction, DT-governance]
thesis-contribution: 1-architecture
---

# Burr et al. (2026) — Agentic Digital Twins: A Taxonomy of Capabilities

**Authors:** Christopher Burr, Mott MacDonald, Alan Turing Institute, Fujitsu, University of Sheffield  
**Published:** January 2026 — arXiv:2601.18799 [cs.CY]  
**Thesis relevance:** **HIGH** — Provides a positioning framework and formalizes key methodological risks

---

## 🎯 Core Idea

An agentic Digital Twin does not merely _represent_ a physical system; it can _co-constitute_ it, changing the reality it measures. This is framed as **performativity**: a deployed model with parameters $\theta$ changes the data distribution it will later observe, $D(\theta)$.

The paper proposes a taxonomy of 27 possible configurations, organized into 3 temporal clusters:
- **Cluster 1 (The Present):** technologically mature, already deployed
- **Cluster 2 (The Threshold):** near-term, with immediate governance risks
- **Cluster 3 (The Frontier):** mostly theoretical

---

## 📐 The Framework: 3 Dimensions × 3 Levels

Each agentic DT is classified by a triple `(Agency, Coupling, Evolution)`:

| Dimension | Level 1 | Level 2 | Level 3 |
|---|---|---|---|
| **Agency** (where decisions are made) | `E` External | `I` Internal | `D` Distributed |
| **Coupling** (interaction frequency) | `L` Loose (batch) | `T` Tight (real-time) | `C` Constitutive (co-definition) |
| **Evolution** (model change) | `S` Static (fixed) | `A` Adaptive (updatable parameters) | `R` Reconstructive (redefines categories) |

---

## 🗺️ The 9 Main Configurations

### Cluster 1 — The Present (Exists Today)

| # | Name | Code | Description | Example |
|---|---|---|---|---|
| 1 | Computational Tool | `(E,L,S)` | Passive tool, no autonomy | Google Maps, cardiac DT |
| 2 | Adaptive Monitor | `(E,T,A)` | Real-time monitoring where humans command; system adapts parameters | Factory DT with online ML |
| 3 | **Active Steering** | `(I,T,A)` | **THESIS HERE** — internal agency, tight coupling, adaptive model | Manufacturing DT with autonomous agents |

### Cluster 2 — The Threshold (Near-Term)

| # | Name | Code | Description | Risk |
|---|---|---|---|---|
| 4 | Symbiotic | `(D,T,A)` | Agency emerges from interaction; no single controller | Ungoverned smart city |
| 5 | **Governor** | `(I,C,A)` | **MAXIMUM RISK** — DT defines what it measures → lock-in | Singapore e-road pricing |
| 6 | Swarm | `(D,T,S)` | Autonomous fleet with static models → chaotic emergence | Phantom traffic jams |

### Cluster 3 — The Frontier (Theoretical)

| # | Name | Code | Description |
|---|---|---|---|
| 7 | Worldbuilder | `(E,L,R)` | Reconstructs ontology with human-in-the-loop | AlphaFold-style |
| 8 | Voyager | `(I,T,R)` | Autonomous + reconstructs categories → inscrutable | Speculative |
| 9 | Reconstructive Assemblage | `(D,C,R)` | Multiple systems that redefine each other | Speculative |

---

## ⚡ Critical Concept: Performative Prediction

Based on **Perdomo et al. (ICML 2020)** and **Hardt & Mendler-Dünner (Statistical Science 2025)**

### The Math

A deployed model with parameters $\theta$ changes the data distribution it will later observe:

$$\text{Distribution} = D(\theta)$$

The true objective is not minimizing risk on historical data, but on the data the model itself will create:

$$\min_{\theta} \text{Risk}(\theta, D(\theta))$$

### Performative Stability Point

The **performative stability point** $\theta_{PS}$ is when the model appears optimal _because it created the distribution on which it is evaluated_:
The **performative stability point** $\theta_{PS}$ is when the model appears optimal _because it created the distribution on which it is evaluated_:

- Model predicts: "action X solves problem Y"
- Model executes X
- Metrics change because of X
- On the next cycle, X appears optimal again
- **Lock-in:** the system cannot distinguish between "X is truly optimal" and "X is optimal for this narrowed, self-induced distribution"

### 5G Example (Thesis-Specific)

```
Cycle 1:
  - Reasoning Agent diagnostica: "SINR basso causa handover failure"
  - Planning Agent propone: "Aumenta Tx power gNB-B1 di 3dB"
  - Azione eseguita

Cycle 2:
  - Perception Agent osserva: SINR migliore, handover failure ridotto ✓
  - Reasoning Agent apprende correlazione: "Aumentare Tx = risolvere SINR"

Cycle N (performative lock-in):
  - System converges on "increasing Tx is always optimal"
  - BUT: the system changed the metric distribution through its actions
  - It cannot tell whether "increase Tx" is optimal for the real network, or only for this altered version
  - It cannot discover alternatives because subsequent cycles see the same self-shaped distribution
```

---

## 🎯 Mapping to the Thesis: Positioning (I,T,A)

**The thesis aims for the Active Steering configuration `(I,T,A)`:**

| Dimension | Thesis Implementation |
|---|---|
| **Agency = Internal** | LLM agents (Perception, Reasoning, Planning, Communication) decide autonomously; the Planning Agent does not wait for approval |
| **Coupling = Tight** | Eclipse Ditto via WebSocket for real-time synchronization (not batch); full loop ~500ms–2s |
| **Evolution = Adaptive** | Reasoning Agent learns patterns from anomalies; KG accumulates historical correlations; Planning Agent evolves action selection |

---

## 🚨 Main Risk: Drift toward Governor (I,C,A)

The paper identifies **Governor** `(I,C,A)` as the most dangerous configuration for DTs with internal agency:

| Aspect | Thesis Risk |
|---|---|
| **Internal agency** | ✅ Intentional (thesis) |
| **Tight coupling** | ✅ Intentional (thesis) — real-time WebSocket |
| **Constitutive coupling** | ⚠️ **RISK** — if the Planning Agent starts to _redefine_ KPI meaning (e.g., "low SINR is impossible", ignoring data), the system drifts toward Governor |
| **Performative lock-in** | ⚠️ **RISK** — the system may converge on solutions that work _because it changed the distribution_, not because they are optimal for the real network |

### Guardrail: The Knowledge Graph

The **Neo4j KG that validates operational constraints before execution** is the architectural mechanism that helps prevent this drift:

1. **KG stays external:** 3GPP constraints encoded in the KG cannot be rewritten by the Planning Agent
2. **Constraint checking:** every proposed action must satisfy KG constraints (thermal limits, backhaul limits, SLAs)
3. **Audit trail:** failed validations are logged → the system cannot “pretend” constraints do not exist
4. **Performative boundary:** the KG keeps the system within physical/operational boundaries, reducing lock-in to artificial distributions

---

## 📋 Pros & Cons for the Thesis

### ✅ Useful Aspects

| Aspect | Use |
|---|---|
| **Positioning framework** | Enables precise positioning: “Active Steering (I,T,A) while avoiding drift toward Governor” |
| **Shared vocabulary** | In Related Work you can use (I,T,A) and readers immediately understand autonomy level |
| **Risk formalization** | Performative prediction gives recognized vocabulary for the thesis’s main methodological risk |
| **Architectural justification** | Explains why a Knowledge Graph guardrail is mandatory, not optional |
| **Risks & limitations section** | Lets you state: “System is (I,T,A) with KG guardrails to prevent drift toward (I,C,A)” |

### ❌ Limitations

| Aspect | Rationale |
|---|---|
| **No empirical results** | No numerical experiments/benchmarks; useful as vocabulary, not as implementation guidance |
| **Not LLM-specific** | The taxonomy is stack-agnostic; it does not discuss Llama, Mistral, quantization |
| **No 5G coverage** | Case studies focus on road traffic (toy model) and manufacturing; not telecom |
| **No evaluation method** | No guidance on how to measure whether a system is truly (I,T,A) vs (I,C,A) |

---

## 📝 Notes for Advisor

If the advisor raises governance-critical questions:

**Q: "How do you ensure the system does not drift toward the Governor configuration?"**

A: "The Knowledge Graph is an explicit architectural guardrail: 3GPP constraints are encoded in an immutable Neo4j schema that the Planning Agent cannot change. This mechanically anchors the system to (I,T,A) (Burr et al., 2026 Active Steering) and reduces performative lock-in to artificial distributions."

**Q: "What if the Reasoning Agent learns spurious correlations?"**

A: "That is exactly the performative prediction risk (Burr et al., 2026; Perdomo ICML 2020): the system may converge on a solution that _appears optimal_ because it reshaped the distribution through its actions, not because it is truly optimal for a real 5G network. This motivates controlled fault injection — external perturbations the system does not control — to detect whether it learned stable patterns or is stuck in performative lock-in."

**Q: "So is the main risk performative lock-in?"**

A: "Yes. With a virtual 3GPP simulator we gain fast cycles and repeatability, but we lose the ‘reality check’ of a physical network the system cannot control. Mitigations include: (1) immutable KG constraints, (2) external fault injection, and (3) multi-model agreement on diagnoses to detect divergence from known physical constraints."

---

## 🔗 Concepts Introduced

- [[agentic-dt-risk-taxonomy]] — The 9-configuration taxonomy
- [[performative-prediction]] — Performative lock-in risk

---

## 📚 References Worth Following Up

1. **Performative Prediction:** Perdomo et al., ICML 2020 | Hardt & Mendler-Dünner, _Statistical Science_ 2025
2. **Steering Representations:** Korenhof, Blok & Kloppenburg, _Philosophy & Technology_ 2021
3. **DT Philosophical Foundations:** Wagg et al., _Data-Centric Engineering_ 2025
4. **Algorithmic Governance:** Zuboff, _The Age of Surveillance Capitalism_ (per contesto) + Burr & Gonzalez & Keudel, 2021

---

## 🎬 Role in the Scaffolding

**Impacted sections:**
- **Ch. 1 (Introduction):** positioning with (I,T,A)
- **Ch. 3 (Related Work):** vocabulary + governance framing for agentic DTs
- **Ch. 5 (Methodology):** performative prediction as a central methodological risk
- **Ch. 8 (Discussion):** limitations of operating at (I,T,A) and preventing drift toward (I,C,A)

---

## Related Pages

- [[sources/restart-2024-ndt]] — 5G domain justification
- [[sources/zheng-et-al-2022-cdt]] — CDT foundational theory
- [[theoretical-concepts/cognitive-digital-twin]] — CDT definition
- [[glossary]] — Terminology
