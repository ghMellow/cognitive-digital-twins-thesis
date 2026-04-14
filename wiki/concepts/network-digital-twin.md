---
title: Network Digital Twin (NDT)
type: concept
created: 2026-04-14
updated: 2026-04-14
sources: [restart-2024-ndt]
tags: [5G, architecture, digital-twin, network-operations]
---

# Network Digital Twin (NDT)

Digital twin specialized for 5G network infrastructure management. Extends DT with AI-driven autonomic control and closed-loop automation.

## Definition (RESTART 2024)

An NDT is a synchronized digital representation of a 5G network infrastructure that:

1. Mirrors the state of physical assets (gNB, slices, spectrum) in real-time
2. Implements autonomic control logic (AI layer) for decision-making
3. Executes decisions through closed-loop feedback to physical network
4. Continuously evolves its model based on outcomes

## Differ from Traditional DT

| Aspetto | Traditional DT | NDT |
|---|---|---|
| **Observations** | Passive monitoring | Active monitoring + decision |
| **AI Role** | Optional, supporting | Mandatory, core driver |
| **Control** | Manual operator intervention | Autonomic, loop-closed |
| **Reactivity** | Human timescale (minutes) | Millisecond timescale |
| **Target** | Design/simulation | Operational management |

## Three-Tier Architecture (RESTART)

### Tier 1 — Digital Representation (DH — Digital Hat)
- Synchronized replica of network state
- Protocol-agnostic interface to physical assets
- Real-time synchronization via APIs
- **Thesis mapping:** Eclipse Ditto

### Tier 2 — Autonomic Control Layer (AI)
- Reasoning on anomalies and policy violations
- Decision-making for corrective actions
- Intent-based translation (high-level goals → concrete configs)
- **Thesis mapping:** LangGraph (Reasoning + Planning agents)

### Tier 3 — Closed-loop Automation
- Feedback from physical network post-action
- KPI monitoring vs. SLA targets
- Continuous adaptation of control logic
- **Thesis mapping:** Perception Agent + history tracking

---

## Role in the Thesis

The NDT concept provides the **architectural framing** for the entire thesis:

- **What:** Why is a cognitive layer mandatory for 5G?
  - Answer: Dynamic workloads require autonomic decision-making at millisecond scale
  
- **Why:** How is autonomy achieved?
  - Answer: Closed-loop automation + AI-driven orchestration
  
- **How:** How do you implement it practically?
  - Answer: DT layer (Ditto) + cognitive agents (LangGraph) + KG constraints (Neo4j)

---

## Limitations of NDT Concept (as stated in literature)

1. **Evaluation gap:** NDT papers describe architecture, not measurement methodology for AI quality
2. **Vendor specificity:** NDT usually assumes enterprise infrastructure (telecom operators)
3. **Implementation gap:** Few production NDT systems exist; most are research prototypes
4. **Local execution:** NDT literature assumes cloud/edge deployment; local edge execution rare

**Thesis contribution:** Addresses evaluation gap (Contribution 2) and enables local execution on consumer hardware (M4 Pro).

---

## Related Pages

- [[sources/restart-2024-ndt]] — Foundational paper
- [[digital-hat]] — DH interface
- [[intent-based-networking]] — IBN layer
- [[closed-loop-autonomy]] — Feedback mechanism
- [[concepts/cognitive-digital-twin]] — Extension of NDT with cognition
