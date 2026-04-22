---
title: Agentic Pipeline Architecture — 4-Agent Cognitive Model
type: synthesis
status: pending-advisor-review
created: 2026-04-20
updated: 2026-04-20
sources_raw: [raw/project/approfondimenti/Ruolo degli Agenti nel CDT.md]
papers_supporting: [zheng-et-al-2022-cdt, al-haj-ali-2025-mmci, hasan-nguyen-2026-agentic-dt, biju-2024-langgraph]
related_gaps: [Gap 1.1, Gap 1.3]
tags: [architecture, agents, cognitive-functions, 4-agent-pipeline]
---

# Agentic Pipeline Architecture — 4-Agent Cognitive Model

**Status:** 🔄 Pending advisor feedback  
**Author synthesis:** Nicolò Termine  
**Basis:** Deep dive analysis of CDT architecture from literature integration + implementation feasibility

---

## 🎯 Central Thesis (Personal Contribution)

The six cognitive functions of a CDT (perception, reasoning, memory, learning, adaptation, decision-making) do **not** require six separate agents. A **4-agent pipeline** can efficiently cover all six functions through:

1. Dedicated primary responsibility per agent
2. Secondary/emergent coverage through agent interaction
3. Externalized memory (Eclipse Ditto + Neo4j KG) rather than agent-internal memory
4. Stateless agent design that maximizes robustness

This reduces architectural complexity while maintaining cognitive completeness. Represents **intentional design choice**, not a limitation.

---

## 📐 The 4-Agent Pipeline

### Architecture Diagram

```
Eclipse Ditto ──→ [Perception] ──→ [Reasoning] ──→ [Planning] ←→ Neo4j KG
                      ↓              ↓              ↓
                   Normalized    Diagnosis +    Validated
                   KPI state     Anomalies      Actions
                                                    ↓
                              [Communication]
                                    ↓
                            Operator Report
```

---

### Agent 1: Perception Agent

**Primary responsibility:** Acquisition and normalization of physical state

- Queries Eclipse Ditto (REST/WebSocket) for 3GPP metrics (RSRP, SINR, throughput, latency, handover rate)
- Normalizes values numerically (min-max on [0,1] or z-score)
- Enriches with semantic metadata (threshold_warning, threshold_critical, status flags)
- Outputs structured JSON context

**Cognitive function covered:** **Perception** (primary)

**Evaluation method:** Classical metrics (Precision, Recall, F1) — ground truth available from simulator

**Why separate?** Decouples data quality from reasoning quality. Early error detection.

---

### Agent 2: Reasoning Agent

**Primary responsibility:** Anomaly detection and root cause inference

Operates on three levels:

1. **Anomaly detection** — Identifies KPI values outside thresholds
2. **Multi-KPI correlation** — Detects systemic patterns (e.g., low RSRP + degraded SINR + high handover rate → coverage issue)
3. **Root cause inference** — Produces diagnosis in natural language via LLM

**Cognitive functions covered:** **Reasoning** (primary), **Learning** (secondary via contextual accumulation)

**Evaluation method:** LLM-as-Judge + multi-agent consensus (see [[statistical-rigor-synthesis]])

**Critical point to argue:** Not a simple threshold system, but contextual causal inference requiring natural language reasoning. This is what justifies LLM usage.

---

### Agent 3: Planning Agent

**Primary responsibility:** Action generation with validation

Translates diagnosis into concrete actions across three categories:

- Radio parameter reconfiguration (TX power, antenna tilt)
- Slice resource reallocation
- Escalation to human operator

**Validation loop (CRITICAL):** Before proposing any action, validates against Neo4j KG. If action violates constraints → rejects or escalates.

**Cognitive functions covered:** **Adaptation** (primary), **Decision-making autonomy** (primary)

**Evaluation method:** KG-based validation (objective, automated) + multi-agent consensus

**Why validation is architectural:** See [[safe-by-design-synthesis]] for Semantic Firewall pattern. This creates "safe-by-design" autonomy.

---

### Agent 4: Communication Agent

**Primary responsibility:** Cognitive cycle synthesis for human operator

Aggregates entire pipeline (perception → reasoning → planning) into interpretable report:

- Causal explanations of reasoning
- Confidence levels
- Action justifications
- Alternative actions considered

**Cognitive functions covered:** **Decision-making autonomy** (secondary, via explainability)

**Evaluation method:** Human evaluation (clarity, completeness, actionability) + LLM-as-Judge

**Why separate?** Explainability (XAI) is increasingly recognized as essential to "responsible autonomy" in literature (Burr et al., Al-Haj Ali).

---

## 🧠 Memory Architecture (Distributed, Not Agent-Local)

### Why No Dedicated Memory Agent?

**Deliberate architectural choice:**

- **Short-term:** LangGraph state persistence across agent calls within single cognitive cycle
- **Long-term:** Eclipse Ditto maintains complete temporal history (with timestamps)
- **Structured knowledge:** Neo4j KG holds stable relational facts

**Rationale:** Stateless agents + externalized memory maximizes:
- **Robustness** — No agent-local state corruption
- **Auditability** — All decisions traceable to external stores
- **Scalability** — Memory not replicated per agent

This is legitimate pattern already in literature (Kalyani & Collier, CogTwin).

---

## 📊 Evaluation Methods by Agent

| Agent | Method (Primary) | Method (Secondary) | Output Validation |
|-------|------------------|-------------------|-------------------|
| Perception | Classical metrics (F1, MAE) | — | Ground truth from simulator |
| Reasoning | LLM-as-Judge | Multi-agent consensus | Semantic consistency check |
| Planning | KG-based validation | Multi-agent consensus | Constraint satisfaction proof |
| Communication | Human evaluation | LLM-as-Judge | Operator comprehension test |

**Insight:** Different agents → different evaluation paradigms. This is **not a weakness**, but **methodological rigor** — choosing the right metric for the right task.

---

## 🔀 Mapping: 6 Cognitive Functions → 4 Agents

| Cognitive Function | Primary Agent | Secondary Contribution | Coverage |
|-------------------|---------------|----------------------|----------|
| Perception | Perception | — | Direct, total |
| Reasoning | Reasoning | Planning (via KG validation) | Direct via inference, validated via constraints |
| Memory | *Distributed* (Ditto + LangGraph + Neo4j) | All agents access | Not agent-local; external memory pattern |
| Learning | *Partial* — few-shot in context | Planning (via KG updates) | Session-local + manual KG refinement |
| Adaptation | Planning | Reasoning (quality of diagnosis) | Immediate reactive response |
| Decision-making | Planning + Communication | Reasoning (quality of reasoning) | Verified + explained autonomy |

---

## ⚠️ Points to Validate with Advisors

1. **Completeness of 6 functions:** Are all six functions adequately covered by 4 agents? Is "partial learning" acceptable as thesis contribution?

2. **Stateless vs. Stateful:** Is externalized memory sufficient for CDT definition (Zheng et al., Al-Haj Ali)? Or does a CDT require agent-internal state?

3. **Evaluation rigor:** Is different metric per agent academically rigorous, or does it weaken the evaluation framework? How to present this as strength not weakness?

4. **Scalability:** Does 4-agent pattern scale to more agents later? Is it an intentional constraint or design limitation?

5. **Communication Agent necessity:** Is Communication Agent scientifically necessary, or is it just "interface layer"? How to position it as cognitive function, not implementation detail?

---

## 📚 Feedback Ricevuti

_To be completed after advisor meeting_

---

## Related Pages

- [[safe-by-design-synthesis]] — KG validation as Planning Agent supervisor
- [[benchmark-template]] — How each agent is benchmarked
- [[scaffolding-tesi]] — Architecture now specified with 4-agent model
