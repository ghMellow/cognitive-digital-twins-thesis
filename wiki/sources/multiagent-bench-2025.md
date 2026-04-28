---
title: MultiAgentBench — MARBLE Framework (2025)
type: source
created: 2026-04-14
updated: 2026-04-28
sources: [b.1_Multi Agent Bench/Valore per la mia tesi.md, b.1_Multi Agent Bench/riassunto.md]
tags: [multi-agent-systems, evaluation-framework, LLM-agents, coordination, benchmark, milestone-KPI]
---

# MultiAgentBench — Zhu et al. (2025)

A crucial paper for **Contribution 2 (evaluation framework)**. It introduces MARBLE (_Multi-agent cooRdination Backbone with LLM Engine_) — a framework to measure not only task completion but also the quality of collaboration/competition via milestone-based KPIs. **Thesis placement**: Ch. 5 (Evaluation Methodology) — provides a methodological template for evaluation design.

---

## 🎯 Metadata

- **Authors:** Kunlun Zhu et al. — University of Illinois Urbana-Champaign
- **Published:** March 3, 2025
- **Ref:** arXiv:2503.01935v1
- **Code:** https://github.com/MultiagentBench/MARBLE

---

## 📋 Framework MARBLE

Coordination architecture for multi-agent systems:

```
Task Info + Domain Database
    ↓
Coordination Engine
├── Agent Graph G=(A,E) [tipizzato per relazioni]
├── Cognitive Module (persona + Chain-of-Thought)
└── Memory System (shared/short/long-RAG)
    ↓
Environment + ToolBox
    ↓
Evaluator → Task Score + Coordination Score
```

---

## ✅ What Matters for the Thesis

### 1. **Milestone-Based KPI** (Directly Adaptable)

**Problem:** how do you measure a multi-agent system when the output is not binary? Response time? Token count? Explanation quality?

**Their approach:** split each task into flexible milestones monitored by an LLM evaluator in real-time.

**Thesis adaptation:** each fault-injection scenario becomes a milestone sequence:
1. ✅ Anomaly correctly perceived by the Perception Agent
2. ✅ Root cause identified by the Reasoning Agent with confidence > threshold
3. ✅ Corrective action proposed by the Planning Agent
4. ✅ Action validated against Neo4j KG constraints
5. ✅ Report generated with a causal explanation by the Communication Agent
6. ✅ Simulator KPIs improve after the action

**Benefit:** not all-or-nothing; each achieved milestone is measurable progress. You can assign partial scores and locate where the pipeline fails.

### 2. **Task Score vs Coordination Score** (Critical Separation)

**Their framework:** two independent metrics:
- **Task Score** — final output quality (e.g., diagnosis correctness)
- **Coordination Score** — interaction quality between agents (context passing, consistency)

**For the thesis:**
- **Task Score (Perception)** → anomaly detected? (ground truth: simulator metrics)
- **Task Score (Reasoning)** → correct root cause? (ground truth: often needs LLM-as-judge)
- **Task Score (Planning)** → feasible action? (ground truth: KG validation)
- **Task Score (Communication)** → coherent explanation? (ground truth: LLM-as-judge)
- **Coordination Score** → coordinated pipeline without context/token loss? (graph traversal score)

**Benefit:** you can tell whether the issue is in a specific agent or in coordination. It makes architectural debugging more precise.

### 3. **LLM-as-Judge for Non-Structured Outputs**

**Their approach:** Communication Score and Planning Score are rated by an LLM evaluator on a 1–5 scale.

**For the thesis:**
- **Communication Agent** → natural-language report rated by Llama 3.1 70B (evaluator) on causal coherence + completeness
- **Reasoning Agent** → root-cause explanation rated for plausibility + alignment with 3GPP constraints

**Benefit:** when explicit ground truth is missing, LLM-as-judge metrics are standardized and reproducible. **However:** the paper acknowledges the self-referentiality risk (LLM evaluates LLM). The thesis mitigation is to pair external ground truth whenever possible (simulator, KG, multi-model agreement).

### 4. **Comparative Model Benchmark** (Contribution 3)

**Their setup:** test 5 models (Llama-3.1-8B, Llama-3.1-70B, Llama-3.3-70B, GPT-3.5, GPT-4o-mini) on the same tasks with the same protocol.

**For the thesis:**
- Same pipeline, different models (Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B)
- Fixed scenarios (5G fault injection)
- Ground truth from the simulator

**Key difference:** they emphasize large models; the thesis targets small local models. The contribution is showing that agents on consumer hardware (quantized 3–8B) can achieve comparable accuracy on a specialized domain (5G fault diagnosis) without cloud.

---

## 📊 Integrazione nello Scaffolding

### Ch. 5 (Evaluation Methodology)
- Adopt a milestone-based KPI framework
- Implement the Task Score / Coordination Score separation
- Define LLM-as-judge for non-structured outputs
- Document ground truth sources (simulator, KG, multi-model agreement)

### Ch. 6 (Implementation)
- Describe how MARBLE is instantiated in LangGraph `StateGraph`
- Specify milestones per agent
- Define scoring functions

### Ch. 7 (Results & Benchmark)
- Table: Task Score by model × scenario
- Table: Coordination Score by pipeline configuration
- Plots: Task Score vs Coordination Score convergence

---

## ✅ Pros — Where It Helps

| Aspect | Use |
|---|---|
| **Evaluation framework** | Milestone-based KPIs + TS/CS separation is directly adaptable |
| **Benchmark template** | Experimental structure: same pipeline, different models, fixed scenarios |
| **LLM-as-judge** | A structured way to evaluate non-structured outputs |
| **Multi-agent dynamics** | Captures coordination, not only task output quality |
| **Methodological rigor** | Recent (Mar 2025) peer-reviewed framing for evaluation choices |

---

## ❌ Cons — Where It Doesn’t Help

| Aspect | Limitation |
|---|---|
| **Domain specificity** | Their metrics target generic tasks; yours must be 5G-specific |
| **Small-model coverage** | They do not test Phi-3 3B / Qwen 3B — the thesis contribution is here |
| **Hardware** | They run on cloud infra; you run on consumer M4 Pro — different latency profiles |
| **Ground truth** | They often lack external ground truth; you have simulator + KG |
| **LLM-as-judge bias** | Evaluator without external ground truth — they acknowledge the risk but do not solve it |

---

## 🎯 Advisor Answer

If asked: _“How do you evaluate an LLM-agent system without ground truth?”_

> _“I follow MultiAgentBench (Zhu et al., 2025) adapted to the 5G domain. I split the process into flexible milestones monitored by an LLM evaluator, but I always add external ground truth where possible: the 3GPP simulator for the Perception Agent (observed metrics), the Neo4j KG for the Planning Agent (constraint satisfaction), and LLM-as-judge only for the Reasoning and Communication agents. This **validation triangle** reduces self-referentiality, the main methodological unknown in LLM-agent evaluation literature. For comparative benchmarking, I reuse their structure — same pipeline, different models, fixed scenarios — but focus on small open-weight models (quantized 3–8B on M4 Pro) that have not been systematically tested in the 5G domain.”_

---

## 🔗 Related Concepts

- [[mmci-framework]] — Complementary: MMCI is higher-level maturity; MultiAgentBench is tactical evaluation
- [[cognitive-digital-twin]] — 6 cognitive functions → structured score functions
- [[biju-2024-langgraph]] — Biju describes LangGraph; MultiAgentBench describes how to measure it

---

## Related Pages

[[sources/berkeley-cs294-llm-eval]] | [[mmci-framework]] | [[sources/al-haj-ali-2025-mmci]]
