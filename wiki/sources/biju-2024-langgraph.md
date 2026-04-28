---
title: Biju (2024) — Implementing MAS via LangGraph
type: source
created: 2026-04-14
updated: 2026-04-28
sources: [b.4_Implementing MAS via LangGraph/Valore per la mia tesi.md, b.4_Implementing MAS via LangGraph/riassunto.md]
tags: [LangGraph, MAS, multi-agent-systems, supervisor-pattern, state-management]
---

# Biju (2024) — Implementing MAS via LangGraph

An applied paper that validates the **Supervisor + specialized agents** pattern in LangGraph — the same topology used in the thesis’ cognitive layer. Value: architectural justification for LangGraph + a baseline for comparative benchmarking. **Thesis placement**: Background + implementation comparison.

---

## 🎯 Supervisor Pattern

Biju uses the same pattern you implement:

```
Supervisor Agent (LangGraph)
    ├── Perception Agent (tool: query Ditto)
    ├── Reasoning Agent (tool: LLM inference)
    ├── Planning Agent (tool: KG constraint check)
    └── Communication Agent (tool: action output)
```

Flow: the Supervisor receives a task → routes it to a specialist agent → the agent uses its tool → final response.

**Your version is more advanced**:
- Adds **KG-based validation** in the Planning Agent (absent in Biju)
- Integrates a **feedback loop** with anomaly detection (absent in Biju)
- Uses **local LLMs** vs hard-coded GPT-4o (absent in Biju)

---

## 📊 Baseline Comparativo

The paper reports numbers you can use as a reference baseline:

| Metric | Biju value | Notes for the thesis |
|---|---|---|
| **Task completion accuracy** | 92–98% | Your benchmark should be ≥ this |
| **Latency per task** | 2–4s | Your 5G cognitive loop should be ≤ 1s to be competitive |
| **Task complexity** | FAQs, database queries | Your tasks (fault diagnosis) are more complex |
| **Models used** | GPT-4o hard-coded | Your multi-model comparison (Llama/Mistral/Phi-3/Qwen) |

**How to position results**: “On tasks of similar complexity to Biju (2024), our system achieves X% accuracy with Y ms average latency, using quantized open-weight models that Biju does not consider.”

---

## ✅ Pros — What You Reuse

| Aspect | Use |
|---|---|
| **Validated architecture** | Supervisor + specialist agents is a mature pattern |
| **Same stack** | `StateGraph`, `langchain` — same framework; you extend it |
| **Numeric baseline** | Comparison metrics (92–98% accuracy, 2–4s) |
| **Applied example** | Shows LangGraph works on heterogeneous real tasks |
| **Tool pattern** | Supervisor routes to specialized tools — aligns with your KG-check pattern |

---

## ❌ Cons — Where It Doesn’t Help

| Aspect | Limitation |
|---|---|
| **Evaluation methodology** | **None** for LLM reasoning. Biju assumes obvious ground truth (FAQ right/wrong); you do not have that luxury for root-cause inference |
| **Local LLMs** | Hard-coded GPT-4o; your open-source/on-prem (quantized Llama 3.1 8B) scenario is different |
| **Knowledge graph** | No KG layer; relies on direct DB queries. You add KG constraints — missing there |
| **Advanced state management** | No episodic memory, session persistence, long-term learning |
| **Domain** | Generic tasks (FAQ); no specialized verticals (telecom, IIoT, etc.) |
| **Ablations** | None — unclear which agent contributes what |

---

## 🔴 Red Flags to Avoid

**Do not cite Biju as CDT theory**
- It does not cover Digital Twins, 3GPP, or cognitive DT literature
- Treat it as an applied reference, not a theoretical foundation

**Do not treat code snippets as pseudocode**
- `StateGraph` snippets are teaser-level — rely on official LangGraph docs for real implementation

**Do not use it as a direct benchmark**
- Tasks differ too much (FAQ vs fault diagnosis)
- Results are not directly comparable

---

## 📝 Thesis Positioning

### Ch. 4 (Architecture)
Use Biju’s supervisor pattern as **justification for the LangGraph topology** you chose. Show the decomposition is a recognized pattern, not an invention.

### Ch. 6 (Implementation)
Use Biju’s numeric baseline (92–98% accuracy, 2–4s latency) as a **comparison point** for your results on specialized 5G tasks.

### Ch. 8 (Discussion)
**Position your contribution beyond Biju**:
1. Rigorous evaluation methodology (LLM-as-judge + multi-model agreement)
2. Knowledge Graph integration as a constraints layer
3. Local open-weight LLMs instead of GPT-4o → reproducibility

---

## 🎯 Advisor Answer

If asked: _“Do you know Biju? What do you think?”_

> _“Biju (2024) is a useful applied reference for the Supervisor + specialist-agents pattern in LangGraph, which matches the topology I adopt in my cognitive layer. However, it has two key limitations: (1) it evaluates tasks with explicit ground truth (FAQ, databases), whereas my Reasoning Agent must infer root causes from 5G radio anomalies without ground truth — which requires LLM-as-judge or multi-model consensus; (2) it does not include a knowledge graph as a constraints layer — my Planning Agent checks each corrective action against Neo4j constraints before execution. Biju supports my Background section, but my scientific contribution goes beyond it.”_

---

## 📚 Related Concepts

- [[cognitive-digital-twin]] — CDT architecture
- [[six-cognitive-functions]] — Agent decomposition rationale
- [[knowledge-graph-in-cdt]] — KG constraint validation (not in Biju)
- [[mmci-framework]] — Evaluation methodology (missing in Biju)
- [[agentic-dt-risk-taxonomy]] — Safety guardrails

---

## 🔍 Alternatives to Consider (Future Comparison)

To make the analysis even more rigorous, you could compare against:
- **AutoGen** — agent framework Microsoft
- **CrewAI** — higher-level MAS framework
- **JADE** — mature classical MAS platform

But **LangGraph is still the right choice** for this thesis (local execution, control over graph visibility, state management).

---

## Related Pages

[[sources/hasan-nguyen-2026-agentic-dt]] | [[sources/cogtwin-ijcai-25]] | [[sources/kalyani-collier-2024-mas-dt]]
