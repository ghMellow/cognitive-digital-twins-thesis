---
title: Cognitive Architecture (for Agentic Systems)
type: concept
created: 2026-04-28
updated: 2026-04-28
sources: [wiki/sources/hintze-et-al-2025-agentic-ai.md, wiki/glossary.md]
tags: [agentic-ai, cognitive-architecture, evaluation, patterns]
---

A cognitive architecture is the control-logic pattern that structures how an intelligent system cycles through perception, memory update, reasoning/planning, action, and feedback.

## Why it matters
In agentic LLM systems, the cognitive architecture determines:
- Token and time complexity (cost/latency)
- Robustness and stability across runs
- Whether reasoning is grounded (tool feedback) vs purely generative

## Common patterns (high level)
- **ReAct** — linear Thought→Action→Observation loops
- **Reflexion** — self-critique and revision loops
- **CRITIC** — tool-interactive validation before committing actions
- **Tree of Thoughts / LATS** — tree search variants (higher cost)

## Role in this thesis
- Constrained-hardware setting favors **linear-cost** architectures (ReAct baseline), with selective self-correction.
- Planning uses CRITIC-style validation against Neo4j constraints.

## Related pages
- [[sources/hintze-et-al-2025-agentic-ai]]
- [[classic-evaluation-framework]]
- [[glossary]]
- [[scaffolding-tesi]]
