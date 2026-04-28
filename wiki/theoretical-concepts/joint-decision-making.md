---
title: Joint Decision-Making (MMCI Level 4)
type: concept
created: 2026-04-28
updated: 2026-04-28
sources: [wiki/sources/al-haj-ali-2025-mmci.md]
tags: [mmci, evaluation, autonomy, decision-making]
---

Joint Decision-Making is the MMCI Level 4 capability: the CDT and the operator (or a reference decision policy) coordinate decisions with shared rationale and explicit uncertainty handling.

## Definition
A system supports joint decision-making when it can:
- Propose actions with rationale and confidence
- Incorporate feedback or constraints from an external authority (human, policy, KG)
- Track when autonomy must be reduced (fallback/escalation)

## Role in this thesis
- Primary mapping: **Planning Agent** + **Communication Agent**.
- Key tension: autonomy capability vs reliability; this is where MMCI connects to autonomy progression.

## Practical operationalization
- Action proposals include: expected KPI impact, constraints checked, confidence, and rollback/fallback triggers
- Escalation policy: when disagreement/low confidence occurs, shift from autonomous to human-in-the-loop

## Related pages
- [[mmci-framework]]
- [[closed-loop-autonomy]]
- [[sources/al-haj-ali-2025-mmci]]
- [[benchmark-template]]
- [[scaffolding-tesi]]
