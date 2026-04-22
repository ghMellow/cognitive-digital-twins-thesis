---
title: Orchestration Framework Decision — LangGraph vs Pi SDK
type: synthesis
status: pending-advisor-review
created: 2026-04-20
updated: 2026-04-20
sources_raw: [raw/project/approfondimenti/Approfondimento uso di Pi.md]
papers_supporting: [biju-2024-langgraph, berkeley-cs294-llm-eval]
references_expert: [Erik Zechner - Pi SDK, LangGraph maintainers]
related_gaps: [Gap 1.1, Gap 2.3, Gap 2.4 (new: architecture choice)]
tags: [architecture-decision, orchestration, langgraph, pi-sdk, performance, explainability]
---

# Orchestration Framework Decision — LangGraph vs Pi SDK

**Status:** 🔄 Pending advisor feedback  
**Author synthesis:** Nicolò Termine  
**Basis:** Deep dive into orchestration frameworks for local LLM agents on M4 Pro hardware

---

## 🎯 Central Thesis (Personal Contribution)

For a **Cognitive Digital Twin on constrained local hardware (M4 Pro 24GB)**, the choice of orchestration framework is not merely implementation detail — it directly impacts:

1. **Prompt efficiency** — Every token saved in framework overhead = more tokens for domain reasoning
2. **Explainability granularity** — Event-driven architecture (Pi SDK) vs state-graph abstraction (LangGraph)
3. **Adaptive resilience** — Rigid state machines vs flexible agent loops for anomaly handling

**Thesis position:** Pi SDK's event-driven, minimalist approach is **scientifically more defensible** for this thesis than LangGraph's standard orchestration pattern, because:

- Maximizes reasoning capacity of small local models (8B-12B)
- Enables granular audit logging required for explainability chapter
- Supports dynamic tool/constraint consultation (Neo4j) without architectural rigidity

**However:** This is a **non-obvious architectural choice** that advisors may challenge. This synthesis documents the trade-offs and decision rationale.

---

## 📊 Framework Comparison

### 1. Prompt Budget and LLM Efficiency

**The Core Problem:** On M4 Pro, every token sent to the LLM is costly. Framework overhead consumes tokens that could be used for domain reasoning.

#### LangGraph Approach (Standard Pattern)

- **System prompt size:** ~500-1500 tokens (state definitions, node instructions, routing logic)
- **Per-call overhead:** Explicit state machine semantics embedded in prompt
- **Token tax:** 30-40% of context window consumed by framework instructions before domain data arrives
- **Effect on small models:** Llama 8B has 4096 token window. With 1500 framework tokens, only ~2500 tokens remain for KPI data + reasoning

```
Input example (LangGraph):
[SYSTEM PROMPT ~1500 tokens describing state machine]
[NODE DEFINITION: "You are the Reasoning Agent in node X"]
[ROUTING INSTRUCTION: "After analysis, return decision in format {...}"]
[USER DATA: ~200 tokens of actual KPI metrics]
```

#### Pi SDK Approach (Event-Driven Minimalist)

- **System prompt size:** <200 tokens (minimal framework instructions)
- **Per-call overhead:** Agent loop is implicit in SDK; instructions focus on task semantics only
- **Token tax:** ~5-10% of context window consumed by framework instructions
- **Effect on small models:** Same Llama 8B. With 150 framework tokens, ~3850 tokens remain for KPI data + reasoning

```
Input example (Pi SDK):
[SYSTEM PROMPT ~150 tokens: "You are a 5G network reasoner. Use tools to analyze"]
[TOOL DEFINITIONS: References to Ditto/Neo4j APIs]
[USER DATA: ~1200 tokens of actual KPI metrics + history]
```

**Impact:** Pi SDK leaves ~1650 more tokens for domain reasoning per call. For small models, this is significant.

---

### 2. Explainability and Audit Trail

**The Thesis Context:** Chapter on "Explainability" must show **why** the CDT made each decision.

#### LangGraph Approach

- **Tracing:** StateGraph provides built-in tracing, but it captures **state transitions**, not reasoning steps
- **Audit log:** "Node X → Node Y" is visible, but what happens *inside* Reasoning Node is a black box
- **Manual logging:** To extract granular reasoning, must add custom logging at each node
- **Cloud dependency:** LangGraph Cloud offers better tracing, but thesis requires **local-only** operation
- **Limitation:** Hard to extract "chain of thought" for explainability without manual intervention

#### Pi SDK Approach

- **Event system:** Native `agent.subscribe()` to all agent events:
  - Tool call (agent requests Ditto data)
  - Tool response (data received)
  - Reasoning step (internal agent thinking, if exposed)
  - Decision point (agent chooses action)
- **Granularity:** Captures every "impulse" of the cognitive cycle
- **Audit trail:** Naturally produces a queryable log of all decisions
- **Local-native:** All events are local; no cloud dependency
- **Explainability benefit:** For thesis Chapter "Causality of Decisions", the event stream is the primary artifact

**Quote for thesis:** "The event-driven architecture of Pi SDK provides native explainability through an ordered sequence of tool consultations and reasoning steps, enabling post-hoc causal analysis without additional instrumentation."

---

### 3. Resilience and Adaptive Behavior

**The 5G Context:** Network anomalies are often unpredictable. CDT must adapt dynamically.

#### LangGraph Approach (Rigid State Machine)

- **Architecture:** Predefined directed acyclic graph (DAG) or cyclic graph with fixed nodes/edges
- **Adaptation:** If anomaly doesn't match predefined nodes/edges, agent is constrained by graph structure
- **Example:** If a critical warning arrives during Planning phase, the only way to "escalate" is via a predefined edge back to Reasoning. No side paths.
- **Robustness:** Robust for expected scenarios; fragile for novel scenarios

#### Pi SDK Approach (Flexible Event Loop)

- **Architecture:** Agent operates in a loop: perceive → reason → decide → act → repeat
- **Adaptation:** Agent can call any tool at any moment; not constrained by predefined graph
- **Dynamic reasoning:** If Reasoning Agent wants to re-query Ditto mid-analysis, it can. If it wants to check Neo4j multiple times, it can.
- **Tree Sessions:** Pi SDK supports "branching" sessions — agent can simulate hypothetical actions on a separate branch without losing the main thread
- **Example:** Scenario: "What if we reduced slice X power by 5%?" Agent can explore this in a side branch without affecting the main decision thread

**For thesis:** "The event-driven loop architecture of Pi SDK enables the CDT to dynamically adapt to anomalies beyond predefined state transitions, simulating hypothetical scenarios (Tree Sessions) without architectural constraint."

---

### 4. Development Trade-offs (Implementation Speed)

For thesis timeline:

| Factor | LangGraph | Pi SDK |
|--------|-----------|--------|
| **Learning curve** | Medium (extensive docs, many abstractions) | Low (TypeScript, ~200 lines for simple agent) |
| **Time to working prototype** | 2-3 weeks | 1-2 weeks |
| **Debugging complexity** | High (state machine semantics) | Low (simple event log) |
| **Integration with Neo4j** | Via custom nodes | Direct tool integration |
| **Local LLM integration** | Requires careful prompt engineering | Optimized for local inference |
| **Peer familiarity** | High (industry standard) | Low (emerging, niche) |

---

## ⚠️ Points to Validate with Advisors

1. **Framework maturity:** Pi SDK is newer (Zechner, recent). Is it academically "safe" to base thesis on emerging framework, or should we use established LangGraph to minimize risk?

2. **Local reasoning quality:** Does reducing framework prompt overhead actually improve reasoning quality of Llama 8B on 5G tasks? Or is the difference negligible? (Requires empirical testing)

3. **Explainability vs. Structure:** Is "event-driven explainability" as rigorous as "state-graph transparency"? Can we formally argue causality from event logs?

4. **Tree Sessions validity:** For thesis purposes, can we use Tree Sessions to generate synthetic "what-if" scenarios for evaluation? Or is that circular (testing on data the system itself generated)?

5. **Hybrid approach:** If advisors prefer LangGraph for stability, can we implement **Pi SDK's event semantics *inside* LangGraph nodes** to get best of both (stability + explainability)?

---

## 💡 Recommended Talking Points (For Call)

1. **Efficiency on M4 Pro:** Emphasize token budget — with Llama 8B at 4K window, LangGraph overhead (1500 tokens) vs Pi SDK overhead (150 tokens) is a real 30% vs 3% trade-off.

2. **Thesis novelty:** Using Pi SDK shows critical evaluation of standard frameworks. It's not "just using LangGraph like everyone else" — it's a **justified architectural choice**.

3. **Explainability as thesis core:** If explainability is central contribution, the framework must enable granular auditing. Pi SDK's event system is inherently better suited than state machine abstraction.

4. **Fallback position:** If advisors push for LangGraph stability, propose implementing "event subscription" layer *within* LangGraph to retain explainability benefits without switching frameworks.

5. **Empirical validation:** Suggest benchmarking both frameworks on same scenario (Llama 8B, same KPI input) and measuring reasoning quality. Let data guide decision, not tribal knowledge.

---

## 📚 Feedback Ricevuti

_To be completed after advisor meeting_

---

## Related Pages

- [[agentic-pipeline-synthesis]] — The 4 agents that need orchestration
- [[scaffolding-tesi]] — Architecture Chapter 4 will reference this decision
