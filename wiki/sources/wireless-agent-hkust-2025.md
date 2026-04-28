---
title: WirelessAgent — LLM Agents for Intelligent Wireless Networks (2025)
type: source
created: 2026-04-14
updated: 2026-04-28
sources: [b.3_WirelessAgent/Valore per la mia tesi.md, b.3_WirelessAgent/riassunto.md]
tags: [wireless-networks, 5G, LLM-agents, LangGraph, network-slicing, closest-prior-work]
---

# WirelessAgent — Tong et al. HKUST (2025)

**Closest prior work** in the 5G domain with LLM agents. WirelessAgent and the thesis share the **same application domain (5G networks)** and a **very similar orchestration architecture (multi-agent LangGraph)**. Key differentiators: Ditto + Neo4j for state management, an evaluation methodology for reasoning, and local vs cloud LLMs. **Thesis placement**: Ch. 3 (Related Work) — direct benchmark + differentiation on the DT layer and evaluation.

---

## 📋 Metadata

- **Authors:** Tong, Guo, Shao, Wu, Li, Lin, Zhang — HKUST (Hong Kong University of Science and Technology)
- **Published:** arXiv:2505.01074 (May 2025)
- **Code:** https://github.com/jwentong/WirelessAgentR1
- **Task:** Network slicing optimization on dynamic 5G RANs

---

## 🏗️ Architecture

### 4 Cognitive Modules (Very Close to Yours)

| WirelessAgent | Thesis (LangGraph) | Mapping |
|---|---|---|
| Perception | Perception Agent | Multimodal inputs → normalized CQI/SNR/RSRP |
| Memory | Ditto + Neo4j | Persistent state (they use volatile in-memory state) |
| Planning | Reasoning + Planning Agents | CoT, RAG, Reflection |
| Action | Communication Agent (+ execution) | Output + tool manipulation |

### The Pattern Is the Same

```
Input Wireless Data
    ↓
[Perception] — converts metrics into text
    ↓
[Memory] — retrieves history and constraints
    ↓
[Planning] — CoT reasoning over an action
    ↓
[Action] — executes and reflects on outcomes
```

**Critical difference:** they do not have **Eclipse Ditto** as a temporally ordered state layer. State lives in LangGraph `global_state`, which is in-memory and volatile. The thesis adds persistence and temporal semantics.

---

## 🎯 Case Study: Network Slicing

WirelessAgent is tested on a simulated 5G network with 3 slices:
- **eMBB** — enhanced Mobile Broadband (throughput > 100 Mbps)
- **URLLC** — Ultra-Reliable Low-Latency (latency < 1ms)
- **mMTC** — massive Machine-Type Communications (density-focused)

Task: given CQI (Channel Quality Indicator), SNR, and data-rate demands → allocate optimal resources to each slice while minimizing SLA violations.

**Thesis relevance:**
- Similar metrics to your simulator (RSRP, SINR, throughput, latency)
- Ground truth: rule-based optimization (RO) + neural-network baseline
- **Same challenge:** the network is dynamic (channel varies), so ground truth is not static

---

## 📊 Benchmark Results (Paper)

| Model | BW Utilization | User Coverage | Latency |
|---|---|---|---|
| **Rule-Based Optimizer** (ground truth) | 100% (reference) | 100% (reference) | 100% (reference) |
| **Neural Network Baseline** | 87.3% | 89.5% | 103.2% |
| **LLM (Llama3-8B)** | 60.96% | 72.4% | 156.8% |
| **LLM (Deep Seek-R1)** | **96.6%** | **98.2%** | **101.5%** |

**Interpretation:**
- Large models (DeepSeek-R1, Qwen 72B) → 96%+ performance
- Small models (Llama3-8B) → 60% performance
- The gap between small and large is **35.64% BW utilization** — this directly motivates Contribution 3: how to close the gap on consumer hardware?

**Crucial difference:** they test models via **cloud APIs**; you test **local quantized models on an M4 Pro**. This is genuinely different and can be a scientific contribution if you can maintain >80% accuracy (your target).

---

## ✅ Pros — Where It Helps

| Aspect | Use |
|---|---|
| **Domain validation** | Evidence that multi-agent LLMs can work on 5G |
| **LangGraph architecture** | Demonstrates Perception→Memory→Planning→Action on a real case |
| **Benchmark case study** | Network slicing is a close reference use case |
| **Available ground truth** | Rule-based optimizer numbers help calibrate the simulator |
| **Methodology openness** | Paper identifies evaluation gaps — gaps the thesis fills |

---

## ❌ Cons — Where It Doesn’t Help (Your Differentiation)

| Aspect | Gap | Thesis solution |
|---|---|---|
| **No Digital Twin layer** | In-memory state; no ordered persistence | Ditto + temporal semantics |
| **Flat knowledge base** | RAG vector store; no structured constraints | Neo4j KG with operational constraints |
| **No evaluation methodology** | Intent accuracy only; no reasoning quality | MMCI + LLM-as-judge + multi-model agreement |
| **Cloud LLM only** | DeepSeek, Qwen-72B, Llama-70B via API | Thesis: local Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B |
| **No explainability** | Outputs yes, causal rationale no | Communication Agent with explanations + confidence |
| **Monolithic evaluation** | BW utilization only; no process breakdown | Separate Task Score / Coordination Score |

---

## 📐 Thesis Positioning

### Ch. 3 (Related Work)

**Subsection:** _“Closest Prior Work: LLM Agents for 5G Networks”_

> _“The most directly related work is WirelessAgent (Tong et al., 2025), which orchestrates LLM agents with LangGraph for 5G network slicing. Their core result — that models like DeepSeek-R1 reach 96.6% of the theoretical optimum vs 60% for small models — validates the agentic approach for wireless domains. However, it exposes key methodological gaps that this thesis addresses…”_

### Ch. 4 (Architecture)

Show how the thesis design extends WirelessAgent:

| Layer | WirelessAgent | Thesis | Benefit |
|---|---|---|---|
| State Management | In-memory volatile | Ditto + temporal | Reproducibility, debugging, historical analysis |
| Knowledge Base | RAG vector store | Neo4j KG | Constraint verification, semantic queries |
| Evaluation | Intent accuracy only | MMCI + multi-agents | Process transparency, reasoning validity |

### Ch. 7 (Results)

**Table: WirelessAgent vs Thesis**

| Aspect | WirelessAgent (theirs) | Thesis (your results) | Notes |
|---|---|---|---|
| Models tested | Llama3-8B, DeepSeek-R1, ... (cloud) | Llama 3.1 8B, Mistral 7B, Phi-3 Mini (local) | Contribution: local deployment |
| Performance range | 60–96% BW utilization | [TBD] — your benchmark | Differentiation on small-model quantization |
| Task score | Not measured | [TBD] — milestone-based | More rigorous evaluator |
| Decision latency | Not reported | [TBD] ms per cycle | Critical for real-time 5G |

---

## 🎯 Advisor Answer (if asked)

If asked: _“Do you know WirelessAgent? What do you think?”_

> _**“WirelessAgent (Tong et al., 2025) is the closest prior work in 5G with LLM agents. Their main validation is showing that a multi-agent LangGraph architecture reaches 96.6% of the theoretical optimum on network slicing, validating the approach itself. I adopt their Perception→Memory→Planning→Action pattern as a reference architecture for the cognitive layer of my thesis.**

**Where the thesis differs:**

1. **State management:** they use in-process memory; I add Eclipse Ditto as a persistent, temporally ordered DT layer, decoupling cognitive producers from infrastructure consumers.

2. **Knowledge representation:** they use flat RAG (vector store); I use a Neo4j Knowledge Graph to encode verifiable 5G operational constraints (3GPP). The Planning Agent does not “hope” to satisfy constraints — it checks them before execution.

3. **Evaluation methodology:** they mainly measure final correctness (BW utilization). They **do not evaluate natural-language reasoning quality** (which they flag as future work). I build a multi-dimensional evaluation framework (MMCI, milestone-based KPIs, Task Score / Coordination Score, LLM-as-judge with multi-model agreement) to validate the cognitive process, not only the final outcome.

4. **Local vs cloud LLMs:** they test DeepSeek-R1, Llama-70B via cloud. Contribution 3 asks the inverse: what can be achieved with quantized models on consumer hardware (Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B on M4 Pro)? This is not an obvious question and is publishable.”_

---

## 📚 Honest Critique (for the Advisor)

A weakness worth flagging:

> _“WirelessAgent measures only the final output (BW utilization, latency). The intermediate reasoning — why it allocated that resource, how it justified that decision — remains a black box. Their main ‘accuracy’ signal is agreement with a rule-based optimizer. This is the classic methodological gap in LLM-agent evaluation literature, and it is exactly the gap this thesis aims to fill with a structured evaluation framework.”_

---

## 🔗 Related Concepts

- [[cognitive-digital-twin]] — CDT definition; generalized beyond WirelessAgent
- [[six-cognitive-functions]] — WirelessAgent’s 4 modules vs the canonical 6 functions
- [[knowledge-graph-in-cdt]] — Neo4j differentiation vs WirelessAgent RAG
- [[mmci-framework]] — Cognitive evaluation that WirelessAgent does not provide
- [[multiagent-bench-2025]] — Coordination metrics (WirelessAgent does not measure)
- [[biju-2024-langgraph]] — Same LangGraph pattern

---

## Related Pages

[[sources/multiagent-bench-2025]] | [[sources/berkeley-cs294-llm-eval]] | [[sources/hasan-nguyen-2026-agentic-dt]]
