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

## � Research Synthesis (Pending Advisor Review) ⏳

Working hypotheses extracted from deep dives and architectural reasoning. Awaiting validation before promotion to canonical wiki.

| Synthesis | Status | Related Gaps | Preview |
|-----------|--------|--------------|---------|
| Agentic Pipeline (4 agents) | 🔄 Pending | Gap 1.1, 1.3 | 4-agent architecture + evaluation methods per agent |
| Statistical Rigor Framework | 🔄 Pending | Gap 2.2, 1.3 | League Training + Paired Variance + Z-score validation |
| Safe-by-Design Firewall | 🔄 Pending | Gap 2.1, 1.1 | Semantic Firewall (Neo4j validator) + Think-Verify-Act |

**Registry:** [[synthesis/index]]

---

## �📚 Sources (Papers, Calls, Deep Dives) — ACTIVE NOW ✅

Ingest raw documents into structured wiki pages.

### Calls and Deep Dives
- [ ] First call (2026-03-17) — Transcript and key decisions
- [ ] Second call (2026-03-31) — Transcript and key decisions
- [x] Berkeley video deep dive — Agentic AI patterns → [[synthesis/statistical-rigor-synthesis]] + [[synthesis/safe-by-design-synthesis]]
- [x] Role of agents in CDT — Architectural deep dive → [[synthesis/agentic-pipeline-synthesis]]
- [ ] Deep dive on Pi usage — (TBD)

---

## 🎯 Concepts (Foundational Theories) — ACTIVE NOW ✅

Concept pages that remain stable throughout the thesis.

### Future Concepts (To Add During Ingest)
- [ ] Digital Twin (traditional) — Definition, contrast vs CDT
- [ ] Multi-Agent Systems — Orchestration patterns, state management
- [ ] LLM Evaluation Methods — LLM-as-judge, confidence calibration, agreement metrics
- [ ] LangGraph Orchestration — Conditional edges, state graph patterns
- [ ] Reasoning without Ground Truth — (Core methodological concept)

---

## 📊 Analyses (Comparative Tables, Gap Analysis) — ACTIVE NOW 

Analytic pages that summarize research and position the thesis's scientific contribution.


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

## 📂 Directory Structure

```
wiki/
├── index.md (this file)
├── scaffolding-tesi.md ✅ central document
├── glossary.md
├── overview.md
├── log.md
├── lint-reports/ ✅ ACTIVE
│   ├── lint-report-2026-04-14.md (pass #1)
│   └── lint-report-2026-04-14-pass2.md (pass #2)
├── synthesis/ ⏳ ACTIVE (pending review)
│   ├── index.md
│   ├── agentic-pipeline-synthesis.md
│   ├── statistical-rigor-synthesis.md
│   └── safe-by-design-synthesis.md
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
