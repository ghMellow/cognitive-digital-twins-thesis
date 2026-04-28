---
title: MAS Patterns in Digital Twins (MAS-with-DT vs MAS-for-DT)
type: concept
created: 2026-04-28
updated: 2026-04-28
sources: [wiki/sources/pretel-et-al-2024-mas-dt.md, wiki/sources/kalyani-collier-2024-mas-dt.md]
tags: [multi-agent-systems, digital-twin, patterns, architecture]
---

Two high-level architectural patterns used to describe how Multi-Agent Systems (MAS) relate to Digital Twins (DT), distilled from systematic literature reviews.

## Pattern 1 — MAS-with-DT
Agents **use** the DT as an information source (sensing, state queries, simulation outputs).

## Pattern 2 — MAS-for-DT
Agents **constitute** or orchestrate the DT’s behavior (coordination, decision-making, adaptation).

## Thesis positioning
This thesis intentionally combines both:
- MAS-with-DT: Perception agent consumes DT state (Ditto)
- MAS-for-DT: orchestration layer coordinates cognitive cycle (LangGraph)

## Related pages
- [[sources/pretel-et-al-2024-mas-dt]]
- [[sources/kalyani-collier-2024-mas-dt]]
- [[scaffolding-tesi]]
