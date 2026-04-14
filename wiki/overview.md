---
title: Thesis Overview
type: analysis
created: 2026-04-14
updated: 2026-04-14
sources: [proposta-tesi.md, feedback-claude.md]
tags: [thesis, summary, architecture]
---

# Overview — Cognitive Digital Twins

High-level summary of the thesis and its scientific contribution.

---

## Title and Scope

**Title:** Cognitive Digital Twins  
**Author:** Nicolò Termine  
**Institution:** Politecnico di Torino  
**Partner:** Fondazione Ugo Bordoni / CINI  
**Date:** April 2026

---

## Central Problem

5G networks are too dynamic for passive management tools. Current Digital Twins are static mirrors; AI agents are isolated modules. **How do we combine distributed cognition with digital representation to achieve autonomous decision-making on 5G infrastructure?**

---

## Main Hypothesis

A local Cognitive Digital Twin (CDT), reproducible on consumer hardware (M4 Pro 24GB), can support the six foundational cognitive functions identified in literature (perception, reasoning, memory, learning, adaptation, decision-making) by coordinating open-source LLM agents orchestrated via LangGraph.

---

## Scientific Contributions

### Contribution 1 — CDT Architecture (Engineering)

**What:** Complete design and implementation of a three-layer system:
- **Simulated Physical Layer** — 3GPP metrics generator with anomaly injection
- **DT Layer** — Eclipse Ditto as backbone for synchronized digital representation
- **Cognitive Layer** — LangGraph + specialized LLM agents (Perception, Reasoning, Planning, Communication)

**Why relevant:** Demonstrates end-to-end feasibility and architectural maturity.

### Contribution 2 — Evaluation Framework for Cognitive Agents (Methodological — CORE)

**What:** Systematic methodology for evaluating specialized cognitive agents when ground truth is absent:
- **Perception Agent** → classical structured metrics (accuracy vs. simulator)
- **Reasoning Agent** → LLM-as-judge + multi-agent agreement + KG-based validation
- **Planning Agent** → validation against KG constraints + operational feasibility
- **Communication Agent** → readability + completeness + causal fidelity

**Why relevant:** Addresses open problem of LLM evaluation in specialized contexts. It is the **scientific center of gravity of the thesis**, suggested by Andrea's feedback in the call.

### Contribution 3 — Comparative Benchmark of Models (Empirical)

**What:** Systematic evaluation of open-source LLMs on 5G-specific tasks:
- Models: Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B
- Tasks: reasoning on KPI anomalies, corrective planning, diagnostic communication
- Metrics: accuracy, latency, token efficiency, memory

**Why relevant:** Publishable output. Empirical contribution complementary to the previous two.

---

## Technology Stack

| Layer | Technology | Role |
|---|---|---|
| Simulated Physical | Python + 3GPP metrics generator | Data source, ground truth |
| Digital Twin | Eclipse Ditto + REST API | State synchronization, event stream |
| Knowledge Graph | Neo4j + Cypher | Operational constraints, validation |
| Agent Orchestration | LangGraph + LangChain | State management, routing |
| LLM | Ollama (Q4 quantization) | Local models: Llama, Mistral, Phi-3, Qwen |
| User Interface | Textual report + graphical metrics | Diagnostic explanation |

---

## Critical Research Hypotheses

1. **An autonomous open-source LLM can infer root causes of 5G anomalies with sufficient reliability to support decision-making** → Tested via benchmark
2. **Multi-agent agreement significantly increases confidence in LLM diagnoses in the absence of ground truth** → Tested via Reasoning Agent evaluation
3. **Operational constraints stored in KG are sufficient to validate Planning actions** → Tested via fault injection
4. **Consumer hardware (M4 Pro) with quantized models supports end-to-end pipeline in real-time** → Tested via latency and throughput benchmark

---

## Scope NOT Included (Future Work)

- Fine-tuning training of models on 5G-specific tasks
- Continuous learning and dynamic adaptation of KG
- Multi-domain CDT (only 5G in this thesis)
- Orchestration on distributed clusters

---

## Related Pages
- [[scaffolding-tesi]]
- [[glossary]]
