---
title: "Towards Cognitive Interoperability: Cognitive Digital Twin and Cognitive Architecture for Human-CPS Collaboration"
type: source
created: 2026-04-14
updated: 2026-04-28
authors: [Al-Haj Ali et al.]
year: 2025
tags: [CDT, MMCI, evaluation-framework, six-functions, CLARION]
thesis-contribution: 2-evaluation
---

# Al-Haj Ali et al. (2025) — MMCI Framework for CDT

**A 5-level evaluation/maturity framework for cognitive agents. It directly supports the thesis’s core gap: evaluating reasoning and planning when explicit ground truth is missing.**

---

## Main Contribution

Formalizes the **Multi-Modal Cognitive Interoperability (MMCI)** framework — a 5-level maturity model to evaluate cognitive alignment between a CDT and a human operator. It extends Zheng et al. (2022) by adding an explicit evaluation dimension.

---

## Summary

**Problem:** Modern CDTs coordinate cognitive agents, but there is no standardized methodology to measure reasoning quality and alignment between the automated system and human operators.

**Method:** Proposes the MMCI framework with 5 maturity levels:
- Level 1: Shared Situation Awareness
- Level 2: Shared Mental Models
- Level 3: Intent & Reasoning Alignment
- Level 4: Joint Decision-Making + Metacognition
- Level 5: Full Autonomous Cognition

**Architecture:** CDT implemented via CLARION (a neuro-symbolic cognitive architecture) for manufacturing Human-Robot Collaboration (HRC) on a UR5e cobot.

**Results:** Empirical validation of MMCI on collaborative inspection scenarios, with alignment metrics between CDT and operator.

**Limitations:** MMCI does not yet define precise quantitative metrics for each level (it is primarily qualitative). Not directly transferable to 5G without adaptation. Does not cover LLMs or natural-language reasoning (pre-LLM CLARION setting).

---

## Outreach Layer (YT)

**The question:** How can you claim a cognitive system “reasons well”? Without explicit ground truth, what remains measurable?

Al-Haj Ali proposes a maturity scale: an “immature” CDT recognizes the state (Level 1), while a “mature” one reasons with the operator and explains why (Level 3+).

The trick is **MMCI**: an evaluation grid that does not require theoretical ground truth, but measures how well the system and operator are “synchronized” — whether they agree on what is happening and what to do.

Applied to 5G, it becomes: “Does my Reasoning Agent explain diagnoses in an interpretable way? Does an operator understand and trust it?” If yes, it’s Level 3+. If not, it’s Level 1.

---

## Value for Thesis

### Areas Deepened

1. **Six Cognitive Functions + Evaluation Lens** (Contribution 1 — Architecture)
   - Extends Zheng et al. (2022) with an explicit **evaluation** perspective
   - Each function can be discussed along the MMCI continuum
   - Direct mapping to the thesis agents (table below)

2. **MMCI Framework — Addressing the Critical Gap** (Contribution 2 — Evaluation — CORE)
   - **Level 1:** Shared Situation Awareness — do the CDT and the operator agree on the observed state?
   - **Level 2:** Shared Mental Models — does the Neo4j KG encode the domain model consistently?
   - **Level 3:** Intent & Reasoning Alignment — are the LLM’s diagnoses interpretable and aligned with intent?
   - **Level 4:** Joint Decision-Making + Metacognition — does the system justify decisions and monitor its own reasoning quality?
   - **Level 5:** Full Autonomous Cognition — can the system act without human supervision?
   
   **This is the missing scaffold.** Instead of inventing ad-hoc metrics, the thesis uses MMCI as a qualitative maturity framework and shows which level each agent reaches.

3. **Mapping CLARION → LLM-Based Architecture** (Contribution 1 — Positioning)
   - CLARION is the paper’s reference cognitive architecture (ACS, NACS, GKS, MCS subsystems)
   - The thesis replaces it with an LLM + KG pipeline — a documentable design choice
   - Trade-off: CLARION = more formal; LLM = more flexible and supports natural language explanations

4. **Manufacturing HRC → 5G Domain** (Differentiator)
   - The paper targets manufacturing Human-Robot Collaboration (collaborative inspection)
   - The thesis targets network operations (RAN management)
   - Open gap: no prior work has applied MMCI to the 5G domain

### Mapping: MMCI Functions → Thesis Agents

| Function (Al-Haj Ali) | Thesis Agent | Target MMCI Level |
|---|---|---|
| **Situation Awareness** | Perception Agent | Level 1: CDT and operator agree on RSRP/SINR/throughput state |
| **Mental Model** | Neo4j KG + Planning Agent | Level 2: KG encodes 3GPP policies and constraints |
| **Intent Alignment** | Reasoning Agent | Level 3: explanations are interpretable and actionable |
| **Joint Decision-Making** | Planning Agent | Level 4: actions include justification + confidence |
| **Metacognition** | Communication Agent | Level 4: system monitors reasoning quality |
| **Autonomy** | (Future work) | Level 5: no human supervision (out of scope for MVP) |

### Pros / Cons as a Source

| Dimension | Pro | Con |
|---|---|---|
| **Evaluation framework** | MMCI addresses the thesis’s core gap (how to assess reasoning without ground truth) | Quantitative metrics are still under-defined; largely qualitative/preliminary |
| **Six functions** | Extends Zheng et al. with an empirical evaluation lens | Limited novelty vs Zheng on pure architecture |
| **CLARION vs LLM** | Clarifies the symbolic vs neural trade-off | Pre-LLM context: does not address natural-language outputs, hallucinations, etc. |
| **HRC domain** | Evaluation methodology is domain-agnostic and transferable | Low vertical transferability (HRC ≠ RAN ops policies/constraints) |
| **Human alignment** | Explicitly includes the human operator dimension | Your thesis is primarily autonomous (Perception→Reasoning→Planning), not collaborative |

### Notes for Advisor

**If asked: "How do you evaluate the Reasoning Agent?"**

> "I adopt MMCI (Al-Haj Ali et al., 2025) as a qualitative evaluation grid. For the Reasoning Agent, the target is Level 3 (Intent & Reasoning Alignment): the LLM’s causal explanations should be interpretable to an expert operator and consistent with the domain model (Neo4j KG). Practical signals include: LLM-as-judge (a stronger model scores coherence), multi-model agreement (consensus across Llama/Mistral/Phi-3/Qwen), and confidence calibration (estimated confidence tracks empirical accuracy)."

**If asked: "Why MMCI?"**

> "The paper identifies the thesis’s central problem: there is no fully objective ground truth to evaluate cognitive reasoning. MMCI does not solve this completely, but proposes measuring alignment between the system’s internal model (KG) and the predictions/actions it produces — a credible proxy for reasoning quality without waiting for physical outcomes."

**If asked: "How much of Al-Haj Ali do you actually apply?"**

> "I apply MMCI as a qualitative evaluation scaffold, not the specific implementation (CLARION + UR5e robot + HRC). The thesis replaces CLARION with an LLM-based multi-agent pipeline and adapts MMCI to the 5G domain. The paper validates the framework idea; the thesis implements it with modern tooling (local LLMs) and evaluates it on telecom tasks."

---

### Structural Dimensions

- **Supported topic:** MMCI evaluation/maturity framework for cognitive agents; evaluation lens over six cognitive functions
- **Gap closed:** Methodological — provides a qualitative scaffold when explicit ground truth is absent
- **Scaffolding position:** **Chapter 5 — Evaluation Methodology**, sections on MMCI + agent mapping
- **Tensions:** None; a natural extension of Zheng et al. (2022)
- **Concepts introduced:** MMCI framework, five maturity levels, shared situation awareness, mental model alignment, joint decision-making

---

## Concepts Introduced

- [[mmci-framework]] — Multi-Modal Cognitive Interoperability (5 maturity levels)
- [[shared-situation-awareness]] — MMCI Level 1
- [[mental-model-alignment]] — MMCI Level 2
- [[joint-decision-making]] — MMCI Level 4

---

## Related Pages

- [[scaffolding-tesi]] — Central thesis argument
- [[sources/zheng-et-al-2022-cdt]] — Theoretical foundation (six functions)
- [[glossary]] — MMCI, LLM-as-judge, confidence calibration
- [[theoretical-concepts/six-cognitive-functions]] — Function-level evaluation lens
- [[sources/multiagent-bench-2025]] — Concrete evaluation metrics for agents
- [[theoretical-concepts/knowledge-graph-in-cdt]] — Dual-KG as an implementation of shared mental models
