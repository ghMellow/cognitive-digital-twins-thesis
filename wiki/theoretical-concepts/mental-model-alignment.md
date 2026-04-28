---
title: Mental Model Alignment (MMCI Level 2)
type: concept
created: 2026-04-28
updated: 2026-04-28
sources: [wiki/sources/al-haj-ali-2025-mmci.md]
tags: [mmci, evaluation, knowledge-graph, alignment]
---

Mental Model Alignment is the MMCI Level 2 capability: the CDT and the operator share compatible internal models of how the system works (entities, causal relations, constraints).

## Definition
A system is aligned at the mental-model level when it:
- Encodes domain structure (entities, relations, constraints)
- Uses that structure consistently while reasoning and planning
- Produces explanations and actions that are compatible with the operator’s domain assumptions

## Role in this thesis
- Primary mapping: **Neo4j Knowledge Graph (DKR)** + Planning validation.
- Purpose: provide a **symbolic anchor** for reasoning and constraint checking to reduce hallucination-in-action.

## Practical operationalization
- Constraint satisfaction checks for candidate actions (CRITIC-style validation)
- Schema coverage checks (are the constraints needed for the scenarios represented?)
- Consistency checks between KG constraints and observed state

## Related pages
- [[mmci-framework]]
- [[knowledge-graph-in-cdt]]
- [[sources/al-haj-ali-2025-mmci]]
- [[sources/hintze-et-al-2025-agentic-ai]]
- [[scaffolding-tesi]]
