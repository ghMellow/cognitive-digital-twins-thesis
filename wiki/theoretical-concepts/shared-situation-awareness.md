---
title: Shared Situation Awareness (MMCI Level 1)
type: concept
created: 2026-04-28
updated: 2026-04-28
sources: [wiki/sources/al-haj-ali-2025-mmci.md]
tags: [mmci, evaluation, human-in-the-loop, situation-awareness]
---

Shared Situation Awareness is the MMCI Level 1 capability: the Cognitive Digital Twin (CDT) and the human operator (or reference model) agree on the observed state of the system.

## Definition
A system achieves shared situation awareness when it can:
- Observe relevant signals (e.g., KPIs, alarms, context)
- Normalize and represent them consistently
- Present an interpretation of the current state that matches an external reference (human expert or ground-truth source)

## Role in this thesis
- Primary mapping: **Perception Agent** (structured 3GPP KPIs from simulator/Ditto)
- Evaluation strategy: where possible, use **external ground truth** (simulator truth) rather than LLM judgement.

## Practical operationalization
Typical checks:
- KPI extraction correctness (schema + units + time alignment)
- Anomaly flag correctness against injected faults
- Consistency between state in Ditto and the agent’s structured output

## Related pages
- [[mmci-framework]]
- [[sources/al-haj-ali-2025-mmci]]
- [[benchmark-template]]
- [[scaffolding-tesi]]
