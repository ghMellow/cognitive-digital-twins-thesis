---
title: Hasan & Nguyen — Integrating Agentic AI and Digital Twins (2026)
type: source
created: 2026-04-14
updated: 2026-04-28
sources: [a.7_Integrating agentic AI and DT/Valore per la mia tesi.md, a.7_Integrating agentic AI and DT/riassunto.md]
tags: [digital-twins, agentic-AI, 6-layer-architecture, closed-loop, decision-sandbox]
---

# Hasan & Nguyen (2026) — Integrating Agentic AI and DT

A related-work **state-of-the-art (Feb 2026)** paper that validates the research direction: closing the loop between LLM agents and a Digital Twin. It provides a 6-layer architecture that maps closely to the thesis’ 4 agents + supporting components. **Thesis placement**: Related Work + architectural blueprint.

---

## 🏗️ 6-Layer Architecture

The paper formalizes a 6-layer model that supports your decomposition:

| Paper layer | Thesis component | Mapping |
|---|---|---|
| **Multimodal Perception Layer** | Perception Agent (LangGraph) | Queries Ditto; normalizes 3GPP metrics |
| **Knowledge & Data Layer** | Eclipse Ditto + Neo4j KG | State repository + constraint repository |
| **Reasoning & Learning Layer (LLM)** | Reasoning Agent | Root-cause analysis on anomalies |
| **Decision-Making Layer (LLM)** | Planning Agent | KG checks; proposes actions |
| **Action & Execution Layer** | Output to network simulator | Executes corrective actions |
| **Feedback & Adaptation Layer** | Recalibration loop | Multi-model consensus + learning |

---

## 💡 Concetto Chiave: DT come Decision Sandbox

The paper frames the DT as **not a passive mirror** but a **pre-execution validation environment**.

In your case:
- **Sandbox = Neo4j KG**: before proposing an action (e.g., slice reallocation), the Planning Agent checks feasibility against constraints
- **Benefit**: prevents actions that violate 3GPP constraints or cause SLA violations
- **How to cite it**: use the paper to motivate **why validation is separated from reasoning** — a recognized architectural pattern

---

## ✅ Pros — Where It Helps

| Aspect | Use |
|---|---|
| **Related work** | Direct citation for recent CDT + agentic AI state-of-the-art |
| **Architectural blueprint** | 6-layer mapping aligns closely with your decomposition |
| **Paradigm validation** | Confirms multi-agent + DT in real-time cyber-physical contexts |
| **Gap identification** | Uses “knowledge” but not explicit constraint semantics — Neo4j becomes differentiating |
| **Peer-reviewed** | Published in Elsevier Array (Feb 2026) |

---

## ❌ Cons — Where It Doesn’t Help

| Aspect | Limitation |
|---|---|
| **Evaluation methodology** | **None** — your main contribution (evaluating non-deterministic LLM agents) is not addressed; the paper assumes it works |
| **Knowledge graph** | Uses LP (Linear Programming) + RFR (Random Forest Regression); no semantic constraint layer |
| **Multi-model benchmarking** | No comparison across LLMs — your model comparison has no precedent here |
| **Domain** | Power grid ≠ 5G network (metrics, constraints, reaction times, standards differ) |
| **Local deployment** | Nothing on running LLMs on consumer hardware |

---

## 📝 Thesis Positioning

### Ch. 3 (Related Work)
Use as the most recent direct source validating cognitive–physical closed-loop systems.

### Ch. 4 (Architecture)
Use the 6-layer framework to structure your architecture description. Show the decomposition is a consolidated pattern in 2026 peer-reviewed literature.

### Ch. 8 (Discussion)
**Position your differentiating contribution** along three dimensions:
1. **Neo4j Knowledge Graph** (they do not have it; they use LP/RFR)
2. **Evaluation methodology** (MMCI + LLM-as-judge + multi-model agreement)
3. **5G domain + local LLMs**

---

## 🎯 Advisor Answer

If asked: _“Do you know this paper and how does it relate to your thesis?”_

> _“Hasan & Nguyen (2026) is the most direct architectural reference: it formalizes the cognitive–physical closed loop between LLM agents and a Digital Twin, validating the pattern I adopt. Their six-layer decomposition helps justify the separation between Perception, Reasoning, and Planning as motivated architectural choices.”_

**Where the thesis differs:**

> _“Compared to that paper, my work differs in three concrete ways: (1) I introduce a Neo4j Knowledge Graph as a semantic constraints-validation layer, which is absent there; (2) I explicitly address evaluation of non-deterministic LLM agents, which they largely ignore; (3) I operate in the 5G domain on consumer hardware with local LLMs, adding a reproducibility contribution their architecture does not consider.”_

---

## 📊 Gap da Colmare

**Relevant methodological gap:**
> _“The paper evaluates the system mainly via convergence time on synthetic scenarios, without addressing how to validate **LLM reasoning quality**. In my case, this is the central problem — and building a rigorous methodology to answer it is the main scientific contribution of the thesis.”_

---

## 🔗 Related Concepts

- [[cognitive-digital-twin]] — CDT definition
-- [[six-cognitive-functions]] — 6 functions (from Zheng)
- [[knowledge-graph-in-cdt]] — Dual-KG pattern
- [[agentic-dt-risk-taxonomy]] — Governance CDT
-- [[intent-based-networking]] — IBN as a specific use case

---

## Related Pages

[[sources/cogtwin-ijcai-25]] | [[sources/biju-2024-langgraph]] | [[sources/restart-2024-ndt]]
