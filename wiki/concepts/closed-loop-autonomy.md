---
title: Closed-Loop Autonomy
type: concept
created: 2026-04-14
updated: 2026-04-14
sources: [restart-2024-ndt]
tags: [feedback, autonomic-control, adaptation]
---

# Closed-Loop Autonomy

The pattern where an autonomic system continuously observes outcomes of its actions, adjusts its internal model, and improves future decisions based on feedback.

## Canonical Loop

```
Perception (observe state)
    ↓
Reasoning (diagnose problem)
    ↓
Planning (select action)
    ↓
Execution (apply to system)
    ↓
Monitoring (observe outcome)
    ↓
Learning (update internal model)
    ↓
→ back to Perception (next cycle)
```

## Definition (RESTART 2024)

Closed-loop autonomy enables a system to:

1. Act on the network (not just observe)
2. Measure the consequences of actions in real-time
3. **Adapt internally** based on outcome (reward/penalty signal)
4. Improve future action selection through accumulated feedback

## Key Difference from Open-Loop

| Open-Loop | Closed-Loop |
|---|---|
| Action → hope it works | Action → measure result → verify improvement |
| No feedback | Feedback is core |
| Static strategy | Adaptive strategy |
| Cannot correct mistakes | Corrects trajectory in real-time |

## Thesis Implementation

**Architecture:** Full pipeline LangGraph

| Loop Stage | Thesis Component | Implementation |
|---|---|---|
| **Perception** | Perception Agent | Queries Ditto, normalizes metrics |
| **Reasoning** | Reasoning Agent | LLM diagnoses root cause |
| **Planning** | Planning Agent | LLM proposes actions, validates via KG |
| **Execution** | Communication Agent + Ditto | Logs decision and sends to monitoring |
| **Monitoring** | Perception Agent (next cycle) | Observes KPI change in simulatore Python |
| **Learning** | NEO4j KG update | Correlation stored for future pattern matching |

**Time scale:** Full cycle 500ms–2s (vs. cloud deployments which are 10s).

---

## Feedback Mechanisms

1. **Immediate feedback** — Did the action succeed? (KPI improved within SLA?)
2. **Lagged feedback** — What are side effects? (Did load shift elsewhere? Did latency change?)
3. **Comparative feedback** — Is this action better than last time? (Vs. history in KG)
4. **Adversarial feedback** — Does the action conflict with simultaneous actions on adjacent cells?

## Challenges in 5G Context

1. **Latency constraints** — Full cycle must complete in <100ms for URLLC; typical CDT needs 500ms+
2. **Partial observability** — Cannot measure all system state; some effects hidden
3. **Non-stationarity** — Environment changes (users move, traffic pattern shifts) making learned correlations stale
4. **Interference** — Multiple CDTs on neighboring cells may have conflicting actions

---

## Why Important for Thesis

Closed-loop autonomy is the **conceptual justification** for why you need continuous evaluation (Contribution 2):

- If CDT only acted once per day, evaluation would be batch/offline (easy)
- Because CDT acts continuously and adapts, you need **online evaluation** that doesn't require ground truth but can validate alignment
- This is **exactly what your MMCI framework does**: measures alignment between CDT's internal model (KG) and observed outcomes

---

## Related Pages

- [[sources/restart-2024-ndt]] — Foundational paper
- [[six-cognitive-functions]] — The cycle mapped to agents
- [[mmci-framework]] — Evaluation framework that monitors alignment in closed loop
- [[glossary]] — Closed-loop definition
