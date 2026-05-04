---
title: Multi-Agent Frameworks (JADE, JaCaMo, SPADE)
type: concept
created: 2026-05-04
updated: 2026-05-04
sources: [kalyani-collier-2024-mas-dt]
tags: [mas, frameworks, jade, jacamo, spade, implementation]
---

# Multi-Agent Frameworks (JADE, JaCaMo, SPADE)

A pragmatic overview of common **MAS implementation frameworks** frequently cited in Digital Twin + Multi-Agent literature, and why they matter (or do not matter) for a thesis that uses LLM agents.

## What “MAS Framework” Means

A MAS framework typically provides:
- **Agent lifecycle** (start/stop, containers, registries)
- **Messaging** (often FIPA-ACL inspired)
- **Directory / discovery** (finding other agents)
- **Coordination primitives** (behaviors, schedulers)
- (sometimes) **reasoning abstractions** (BDI, norms)

This is distinct from the *agent logic* itself (rules/ML/LLM).

## Three Canonical Names in DT+MAS Surveys

### JADE

**JADE** (Java Agent DEvelopment Framework) is a mature Java-based platform widely used as a reference implementation for MAS.

- Strengths: stable runtime; messaging patterns; ecosystem familiarity
- Typical use: coordination and communication substrate
- Common limitation in modern stacks: integration overhead with polyglot toolchains and data platforms

### JaCaMo

**JaCaMo** is a MAS meta-framework that combines:
- **Jason** (BDI agents)
- **CArtAgO** (artifacts / environment)
- **Moise** (organizations and norms)

It is often chosen when a paper needs explicit modeling of:
- organizational structure
- normative constraints
- deliberative BDI reasoning

### SPADE

**SPADE** (Smart Python Agent Development Environment) is a Python-based MAS framework.

- Strengths: Python ecosystem integration; easier prototyping
- Typical use: lightweight agent communication and orchestration

## Comparison (High-Level)

| Framework | Primary language | Main differentiator | Best fit when |
|---|---:|---|---|
| JADE | Java | Mature runtime + messaging | You need a stable, classic MAS substrate |
| JaCaMo | Java | BDI + norms + environment artifacts | You want explicit organizational / normative modeling |
| SPADE | Python | Simple Python-based agents | You want fast prototypes and Python integration |

## Mapping to This Thesis (Why These Are Still Useful)

Even if the thesis does not implement agents with JADE/JaCaMo/SPADE, they help in **Related Work** to show:

- DT+MAS is an established pattern with recurring implementation substrates
- the thesis chooses a different execution layer (LLM orchestration + DT platform + KG) while preserving MAS design principles

A reasonable framing is:

- Frameworks like JADE/JaCaMo/SPADE mostly address **agent runtime + messaging**.
- The thesis’ stack emphasizes **cognitive decision-making** (LLM agents), explicit **constraint validation** (KG), and tight synchronization with the DT.

## Practical Guidance (How to Cite Without Overclaiming)

- Cite these frameworks as examples of **MAS implementation approaches** in the surveyed literature.
- Avoid implying they provide guarantees about safety or evaluation quality; they are infrastructure.
- Keep the comparison focused on what the thesis needs: coordination substrate vs cognitive reasoning layer.

---

## Related Pages

- [[sources/kalyani-collier-2024-mas-dt]] — Survey citing these frameworks
- [[multi-agent-systems]] — MAS definition
- [[mas-agent-patterns]] — Role patterns independent of framework choice
- [[glossary]] — Terminology
