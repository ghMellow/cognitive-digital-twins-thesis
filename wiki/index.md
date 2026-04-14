---
title: Master Index of Wiki
type: analysis
created: 2026-04-14
updated: 2026-04-14
sources: []
tags: [index, navigation]
---

# Master Index — Thesis Wiki

Complete catalog of all thesis wiki pages. Updated incrementally with each ingest.

---

## 📋 Foundational Documents — ACTIVE NOW ✅

| Document               | Type     | Purpose                                                                | Link                 |
| ---------------------- | -------- | ---------------------------------------------------------------------- | -------------------- |
| Thesis Scaffolding     | analysis | Central argumentative structure of thesis, updated every ingest        | [[scaffolding-tesi]] |
| Glossary               | concept  | Canonical terminology CDT + 5G domain                                 | [[glossary]]         |
| Thesis Overview        | analysis | Summary problem, hypothesis, scientific contributions, stack           | [[overview]]         |
| Project Log            | analysis | Append-only chronology of all operations                               | [[log]]              |

---

## 📚 Sources (Papers, Calls, Deep Dives) — ACTIVE NOW ✅

Ingest raw documents into structured wiki pages.

### Block A — CDT Theory
- [x] [[sources/zheng-et-al-2022-cdt]] — Zheng et al. (2022) — Foundational definition, six functions, KG as backbone
- [x] [[sources/al-haj-ali-2025-mmci]] — Al-Haj Ali et al. (2025) — MMCI framework, 5 maturity levels for evaluation

### Block B — Pattern and Context
- [x] [[sources/restart-2024-ndt]] — RESTART NDT (2024) — NDT architecture, 3-tier, IBN, 5G justification
- [x] [[sources/burr-et-al-2026-agentic-dt]] — Burr et al. (2026) — Risk taxonomy (I,T,A) vs (I,C,A), performative prediction
- [x] [[sources/kalyani-collier-2024-mas-dt]] — Kalyani & Collier (2024) — SLR 22 papers MAS+DT, multi-agent architecture
- [x] [[sources/pretel-et-al-2024-mas-dt]] — Pretel et al. (2024) — SLR 64 papers MAS+DT, 12 DT properties, gap analysis

### Block C — Architectural Blueprint
- [x] [[sources/cogtwin-ijcai-25]] — CogTwin IJCAI-25 — Dual-KG pattern, CDT architecture
- [x] [[sources/hasan-nguyen-2026-agentic-dt]] — Hasan & Nguyen (2026) — 6-layer agentic architecture
- [x] [[sources/biju-2024-langgraph]] — Biju (2024) — LangGraph supervisor pattern

### Block D — Evaluation Methodology
- [x] [[sources/multiagent-bench-2025]] — MultiAgentBench (2025) — Milestone-based KPI, Task/Coordination Score framework
- [x] [[sources/berkeley-cs294-llm-eval]] — Berkeley CS294 (2026) — LLM Agent Evaluations, outcome validity

### Block E — Closest Prior Work
- [x] [[sources/wireless-agent-hkust-2025]] — WirelessAgent HKUST (2025) — LLM agents + LangGraph for 5G network slicing

### Calls and Deep Dives
- [ ] First call (2026-03-17) — Transcript and key decisions
- [ ] Second call (2026-03-31) — Transcript and key decisions
- [ ] Berkeley video deep dive — Agentic AI patterns
- [ ] Deep dive on Pi usage — (TBD)
- [ ] Role of agents in CDT — Analysis of specific role

---

## 🎯 Concepts (Foundational Theories) — ACTIVE NOW ✅

Concept pages that remain stable throughout the thesis.

### Concepts Created (Block A-B)
- [x] [[concepts/cognitive-digital-twin]] — Formal definition, five characteristics, six functions, agent mapping
- [x] [[concepts/six-cognitive-functions]] — Perception, reasoning, memory, learning, adaptation, decision-making
- [x] [[concepts/knowledge-graph-in-cdt]] — Architectural role, Dual-KG pattern, 5G schema, KG validation
- [x] [[concepts/mmci-framework]] — Multi-Modal Cognitive Interoperability, 5 maturity levels, operationalization
- [x] [[concepts/network-digital-twin]] — 5G-specific DT, 3-tier architecture (DH, Autonomic, Closed-loop), AI as driver
- [x] [[concepts/digital-hat]] — Interface layer, real-time synchronization, Eclipse Ditto mapping, protocols
- [x] [[concepts/intent-based-networking]] — IBN flow, translation to actions, KG constraint validation for 5G
- [x] [[concepts/closed-loop-autonomy]] — Feedback loop, adaptation, why MMCI evaluation needed
- [x] [[concepts/agentic-dt-risk-taxonomy]] — 27 configurations (I,T,A) vs (I,C,A), Burr framework
- [x] [[concepts/performative-prediction]] — Lock-in risk, Perdomo ICML 2020, detection tests

### Future Concepts (To Add During Ingest)
- [ ] Digital Twin (traditional) — Definition, contrast vs CDT
- [ ] Multi-Agent Systems — Orchestration patterns, state management
- [ ] LLM Evaluation Methods — LLM-as-judge, confidence calibration, agreement metrics
- [ ] LangGraph Orchestration — Conditional edges, state graph patterns
- [ ] Reasoning without Ground Truth — (Core methodological concept)

---

## 📊 Analyses (Comparative Tables, Gap Analysis) — ACTIVE NOW ✅

_Created upon completion of ingest of ALL papers (after Block E) and Lint Pass #2_

Analytic pages that summarize research and position the thesis's scientific contribution.

- [x] [[analyses/comparison-matrix]] — 12 papers vs. 9 DT properties + LLM coverage; thesis uniqueness score (8/10)
- [x] [[analyses/gap-analysis]] — 8 critical gaps (LLM agents, 5G domain, agent eval, governance, etc.) with thesis resolutions
- [x] [[analyses/risk-profile]] — Burr (I,T,A) taxonomy: thesis = (I:2,T:2,A:1) "Active Steering"; operationalized guardrails
- [x] [[analyses/benchmark-template]] — 3 fault injection scenarios (A: single fault, B: contention, C: cascade) with full metrics framework

---

## 📝 Style Rules (Thesis Conventions) — DEFERRED ⏳

_Created when you begin writing thesis body chapters (Chapters 1–8)_

Writing conventions, canonical terminology, equation format, citation style.

**Planned rules:**
- Canonical terminology and abbreviations (already partially in glossary.md)
- 3GPP equations format and network metrics
- Citation style for papers vs implementations vs standards
- LangGraph agent nomenclature
- Convention for representing the cognitive cycle

---

## 👥 Personas (Audience) — OPTIONAL

_Optional — possible omission if thesis is mono-audience_

Target audience of thesis and how to customize explanation for each:
- Advisor (researcher in CDT/MAS) — focus on methodological novelty
- Company (Fondazione Ugo Bordoni) — focus on 5G applicability
- Research community (publication) — focus on benchmark and reproducibility
- Network operators — focus on practical usability

**Note:** Probably not necessary for a single-authored master's thesis.

---

## 🚦 Ingest Status — Wiki Literature Review Phase COMPLETE

| Milestone                           | Status | Note                                 |
| ----------------------------------- | ------ | ------------------------------------ |
| Setup wiki                          | ✅      | Structure, master files, glossary    |
| **Block A — CDT Theory**           | ✅      | 2/2 (Zheng + Al-Haj Ali) — 14 Apr   |
| **Block B — Pattern & Context**    | ✅      | 4/4 (RESTART, Burr, Kalyani, Pretel) — 14 Apr |
| **Block C — Arch. Blueprint**      | ✅      | 3/3 (CogTwin, Hasan&Nguyen, Biju) — 14 Apr |
| **Block D — Evaluation**           | ✅      | 2/2 (MultiAgentBench, Berkeley) — 14 Apr |
| **Block E — Closest Prior Work**  | ✅      | 1/1 (WirelessAgent) — 14 Apr        |
| **Lint Pass #1**                    | ✅      | 0 contradictions, 91% link validity |
| **Lint Pass #2**                    | ✅      | 97%+ link validity, 12 zombies resolved |
| **Creation of analyses/ pages**     | ✅      | 4/4 (comparison, gap, risk, benchmark) — 14 Apr |
| Ingest call 1 + 2                   | ⏳      | Optional (low priority) |
| Ingest deep dives (3 files)         | ⏳      | Optional (low priority) |
| Creation of style/ pages            | ⏳      | During writing Ch. 1–8              |
| Final scaffolding update            | ⏳      | Review pass before thesis           |
| Wiki lint (pre-submission)          | ⏳      | Before thesis handover               |

---

## 📂 Directory Structure

```
wiki/
├── index.md (this file)
├── scaffolding-tesi.md ✅ central document
├── glossary.md
├── overview.md
├── log.md
├── lint-report-2026-04-14.md ✅ (pass #1)
├── lint-report-2026-04-14-pass2.md ✅ (pass #2)
├── sources/ ✅ ACTIVE (12 papers)
│   ├── zheng-et-al-2022-cdt.md
│   ├── al-haj-ali-2025-mmci.md
│   ├── restart-2024-ndt.md
│   ├── burr-et-al-2026-agentic-dt.md
│   ├── kalyani-collier-2024-mas-dt.md
│   ├── pretel-et-al-2024-mas-dt.md
│   ├── cogtwin-ijcai-25.md
│   ├── hasan-nguyen-2026-agentic-dt.md
│   ├── biju-2024-langgraph.md
│   ├── multiagent-bench-2025.md
│   ├── berkeley-cs294-llm-eval.md
│   └── wireless-agent-hkust-2025.md
├── concepts/ ✅ ACTIVE (10 concepts)
│   ├── cognitive-digital-twin.md
│   ├── six-cognitive-functions.md
│   ├── knowledge-graph-in-cdt.md
│   ├── mmci-framework.md
│   ├── network-digital-twin.md
│   ├── digital-hat.md
│   ├── intent-based-networking.md
│   ├── closed-loop-autonomy.md
│   ├── agentic-dt-risk-taxonomy.md
│   └── performative-prediction.md
├── analyses/ ✅ ACTIVE (4 analyses)
│   ├── comparison-matrix.md
│   ├── gap-analysis.md
│   ├── risk-profile.md
│   └── benchmark-template.md
├── style/ ⏳ DEFERRED (writing phase)
└── personas/ (optional — empty)
```

---
