---
title: Project Log
type: analysis
created: 2026-04-14
updated: 2026-04-20
sources: []
tags: [project-log, chronology]
---

# Log — Wiki Project Chronology

Append-only log of all wiki operations. **Last 5 logs are detailed; earlier logs are archived in summary form below.**

---

## [2026-04-22] lint | Pass #3 — Post-Folder-Rename Validation

**Operation:** Complete lint pass following folder rename operations (`concepts/` → `theoretical-concepts/`, `synthesis/` → `working-hypotheses/`)

**Results:** 
- **Link validity:** 99%+ (up from 97% in Pass #2)
- **Broken links fixed:** 4 links removed (`[[lllm-as-judge]]` typo ×2, `[[mas-agent-patterns]]`, `[[multi-agent-frameworks]]`)
- **Folder references corrected:** 4 files updated (log.md, scaffolding-tesi.md, working-hypotheses/index.md, lint-report-pass2)
- **Contradictions:** 0 (stable)
- **Orphaned pages:** 0 (stable)
- **Terminology consistency:** 100% (all terms match glossary)

**File created:** `wiki/lint-reports/lint-report-2026-04-22.md`

**Status:** ✅ **Wiki production-ready.** All folder references corrected, link integrity solid, zero contradictions. Ready for thesis writing phase.

---

## [2026-04-20] ingest | 4th Deep Dive → Orchestration Framework Synthesis

**Operation:** Extracted 4th deep dive from `raw/project/approfondimenti/Approfondimento uso di Pi.md` as research synthesis page awaiting advisor validation.

**Synthesis Page Created:**
- `wiki/working-hypotheses/orchestration-framework-synthesis.md` — LangGraph vs Pi SDK trade-offs (token efficiency, explainability, resilience)

**Decision Context:** Choice of orchestration framework directly impacts:
- Prompt efficiency on constrained hardware (M4 Pro: token budget = reasoning capacity)
- Explainability granularity (event-driven vs state-machine)
- Adaptive resilience (Tree Sessions capability)

**Key Argument:** Pi SDK's event-driven minimalist approach is scientifically defensible for this thesis because it maximizes reasoning capacity of 8B-12B models AND enables granular audit logging for explainability chapter. However, LangGraph is industry standard — trade-off must be explicitly defended to advisors.

**Related Gaps:** Gap 1.1 (5G architecture choice) + Gap 2.3 (Decision Latency considerations)

**Status:** 🔄 Pending advisor validation. Includes 5 discussion points ready for next call.

**Files Updated:** `wiki/working-hypotheses/index.md` (+ 4a synthesis row), `wiki/log.md` (this entry)

---

## [2026-04-20] reference | AI Panorama 2025-2026 for Team Alignment

**Type:** Background knowledge document (not research synthesis)

**Purpose:** Establish shared vocabulary for team/advisor discussions on AI landscape without terminology confusion. Documents the invariant structure of agents (LLM + loop + memory + tools) and positions thesis work within current ecosystem.

**Document Location:** `raw/project/approfondimenti/Approfondimento Stato dell'Arte AI.md`

**Key Sections:**
- Transformer mechanics & what LLMs encode
- Agent architecture (ReAct, Reflexion, Tree of Thoughts, RL-based reasoning)
- Three memory paradigms: RAG (scale 1000s docs) vs Wiki (scale 100s, compile-time) vs Palazzo Mentale (emerging hybrid)
- Framework ecosystem comparison (LangChain, LangGraph, CrewAI, Pi, OpenClaw, NVIDIA)
- Practical workflow (Obsidian visualization + VSCode execution + Markdown persistence)

**Relevance to Thesis:**
- Wiki pattern (Section 4.4) validates our `raw/` → `wiki/` architecture
- Skill files pattern (Section 6.3) already in use — confirms best practice
- Framework invariant structure (Section 5.3) informs orchestration-framework-synthesis

**Next Step:** Use as reference during next advisor call. If specific discussion points emerge (e.g., "why not RAG?", "why Markdown over database?"), extract to dedicated synthesis pages for deeper validation.

**Status:** 🎯 Ready for team discussion. No validation required — background material.

---

## [2026-04-20] ingest | Glossary — Formal Knowledge Representation & Semantic Ontologies

**Operation:** Enhanced `glossary.md` with comprehensive semantic foundations following insights from latest advisor call (2026-04-15).

**New Section Added:** "Formal Knowledge Representation & Semantic Ontologies" (11 subsections, 50+ definitions)

**Subsections:**
1. **Core Knowledge Representation Concepts** — Ontology, Semantics (explicit vs implicit), KRR
2. **Logical Foundations** — First-Order Logic (FOL), Descriptive Logic (DL), Inference
3. **Semantic Standards & Technologies** — RDF, OWL, SPARQL, Reasoner
4. **Formal Analysis Tools** — Formal Concept Analysis (FCA)
5. **Cognitive Architectures & Memory** — Cognitive Architecture, Memory (static vs episodic)
6. **Advanced Integration Concepts** — Symbol Grounding, Neuro-Symbolic Approach, Embedding, CWA vs OWA

**Key Definitions Integrated:**
- **Ontology** ← formalization of domain knowledge in machine-readable format (enables inference)
- **Semantics** ← explicit (ontologies/KGs) vs implicit (LLM embeddings) — distinguishes Contribution 1 from Contribution 2
- **Neuro-Symbolic Approach** ← marked as **thesis methodology bridge**: combines neural (LLMs) + symbolic (logic/KGs)
- **Cognitive Architecture** ← theoretical foundation for six cognitive functions (Zheng et al. 2022)
- **FCA** ← Mario Beltrani's primary formal tool for extracting conceptual hierarchies from data

**Relationship to Thesis:** These definitions establish the formal vocabulary layer underlying Contribution 2 (multi-dimensional evaluation framework) and provide theoretical justification for neuro-symbolic design choices in the agentic pipeline. Addresses implicit terminology gap from recent calls.

**Metadata Updated:** Added sources tags linking to recent calls (2026-03-31-seconda-call.md, 2026-04-15-terza-call.md)

**Status:** ✅ Glossary now serves as authoritative reference for both implicit (LLM-based) and explicit (ontology-based) semantics paradigms. Ready for team discussions on Contribution 2 design choices.

---

## [2026-04-20] ingest | 4th Deep Dive → Orchestration Framework Synthesis

**Synthesis Page Created:**
- `wiki/working-hypotheses/orchestration-framework-synthesis.md` — LangGraph vs Pi SDK trade-offs (token efficiency, explainability, resilience)

**Decision Context:** Choice of orchestration framework directly impacts:
- Prompt efficiency on constrained hardware (M4 Pro: token budget = reasoning capacity)
- Explainability granularity (event-driven vs state-machine)
- Adaptive resilience (Tree Sessions capability)

**Key Argument:** Pi SDK's event-driven minimalist approach is scientifically defensible for this thesis because it maximizes reasoning capacity of 8B-12B models AND enables granular audit logging for explainability chapter. However, LangGraph is industry standard — trade-off must be explicitly defended to advisors.

**Related Gaps:** Gap 1.1 (5G architecture choice) + Gap 2.3 (Decision Latency considerations)

**Status:** 🔄 Pending advisor validation. Includes 5 discussion points ready for next call.

**Files Updated:** `wiki/working-hypotheses/index.md` (+ 4a synthesis row), `wiki/log.md` (this entry)

---

## [2026-04-20] ingest | Deep Dives → Research Synthesis (Pending Review)

**Operation:** Extracted 3 deep dives from `raw/project/approfondimenti/` as structured research synthesis pages awaiting advisor validation.

**Synthesis Pages Created:**
- `wiki/working-hypotheses/index.md` — Registry and workflow for synthesis validation
- `wiki/working-hypotheses/agentic-pipeline-synthesis.md` — 4-agent architecture, cognitive function mapping, evaluation methods per agent
- `wiki/working-hypotheses/statistical-rigor-synthesis.md` — League Training + Paired Variance Estimation + Z-score validation + consensus metrics
- `wiki/working-hypotheses/safe-by-design-synthesis.md` — Semantic Firewall pattern, Neo4j validator, Think-Verify-Act cycle, prompt injection defense

**Papers Supporting:** Berkeley CS294, DeepMind (Vinyals), UC Berkeley security (D. Song), Cognition AI architecture patterns

**Related Gaps Addressed:**
- Gap 1.1 (5G-specific architecture) — now detailed in agentic-pipeline-synthesis
- Gap 1.3 (Operational evaluation) — now detailed in statistical-rigor-synthesis + agentic-pipeline-synthesis
- Gap 2.1 (LLM-as-judge + validation) — now detailed in statistical-rigor-synthesis + safe-by-design-synthesis

**Status:** 🔄 **Pending advisor validation.** Each synthesis page includes "Points to Validate" section ready for next advisor meeting. Once validated → content will be promoted to canonical wiki pages (theoretical-concepts/ or analyses/).

**Next Step:** Present 3 syntheses to relatori with specific discussion points highlighted. Record feedback in "Feedback ricevuti" sections.

**Files Updated:** `wiki/index.md` (+ Synthesis registry section), `wiki/log.md` (this entry)

---

## [2026-04-20] align | Scaffolding Updated per Post-Call Feedback

**Operation:** Align `scaffolding-tesi.md` with insights from updated `feedback-claude.md` (post-call review)

**Key Changes to Scaffolding:**

1. **Main Hypothesis** — Added autonomy progression as explicit dimension: "multi-dimensional evaluation framework **with progressive autonomy tracking** — progressing from human-in-the-loop to autonomous operation, measured via MMCI metric and multi-model agreement"

2. **Open Tensions** — Expanded from 4 to 5 tensions; added new tension #5: **"Autonomy Capability vs. Reliability"** → operationalized via MMCI framework across autonomy levels (human-in-the-loop → semi-autonomous → autonomous)

3. **Gap 1.3 (Operational Evaluation)** — Strengthened with explicit mention of KG-based validation for **Planning Agent decisions** (was missing)

4. **Gap 2.2 (Comparative Benchmark)** — Updated from 92–120 runs to **288–360 runs** (3 scenarios × 4 models × **3 autonomy levels** × 8–10 replicates) — autonomy now core benchmark dimension

5. **NEW SECTION — Agentic Memory Architecture** — Documented persistent MD event store + Neo4j KG integration as architectural element Gap 3.2 (TIER-2). Enables temporal anomaly correlation and historical pattern learning for agents.

6. **Contribution 2 CORE designation** — Marked as ⭐ **"CORE: Multi-Dimensional Cognitive Evaluation Framework with Autonomy Progression"** with explicit note: "Gap 2.4 (MMCI as operational metric)" and benchmarking across autonomy levels

7. **Contribution 1** — Updated to include "Gap 3.2 (Persistent memory layer)" and reference to new Memory Architecture section

**Status Implication:** 
- Thesis now has 5 open tensions (was 4)
- Benchmark scope increased: +196 runs due to autonomy dimension
- MMCI becomes operational metric (not just theoretical reference)
- Contribution 2 is now explicitly labeled as **CORE** — evaluation framework with autonomy escalation is the scientific heart
- Memory layer elevated from implementation detail to architectural gap + design choice

**Files Modified:** `scaffolding-tesi.md` (7 replacements: Hypothesis, Open Tensions ×2, Remaining Gaps ×2, Contributions table ×2, NEW section added)

**Status:** ✅ Scaffolding coherent with post-call feedback. Autonomy progression and MMCI operationalization now central to thesis structure. Ready for implementation phase.

---

## 📦 Archive — Summarized Logs (2026-04-14 to 2026-04-15)

**[2026-04-14 AM] setup** — Wiki structure initialization: created folders (`sources/`, `theoretical-concepts/`, `personas/`, `analyses/`, `style/`) and master files (`glossary.md`, `overview.md`, `log.md`, `index.md`). Initialized glossary with 40+ canonical CDT + 5G terms. ✅

**[2026-04-15] translation** — Complete English translation of foundational wiki: CLAUDE.md, SKILL-thesis-ingest.md, glossary.md, index.md, overview.md, scaffolding-tesi.md (413 lines). All Italian replaced with idiomatic English. Language policy: user comms in Italian, wiki storage in English. ✅

**[2026-04-14 PM] ingest | Blocks A–B (6 papers)** — Sequential ingestion: Zheng (CDT theory) → Al-Haj Ali (MMCI) → RESTART (5G NDT) → Burr (risk taxonomy) → Kalyani (22-paper SLR) → Pretel (64-paper SLR). Created 11 source pages, 8 concept pages. Zero contradictions. All claims scaffolding-supported. ✅

**[2026-04-14 evening] lint Pass #1** — 132 links scanned, 91% validity. Fixed 1 typo. 15 zombie links identified (mostly future Block C/D). Zero contradictions. Recommendation: GO for Block C. ✅

**[2026-04-14 late] ingest | Blocks C–E (6 papers)** — Simultaneous: Block C (CogTwin, Hasan&Nguyen, Biju) + Block D (MultiAgentBench, Berkeley CS294) + Block E (WirelessAgent). 12/12 papers ingested same day. Created 6 source pages, 2 new concept pages, 14 glossary terms added. **All blocks completed.** ✅

---

## [2026-04-14] lint | Pass #2 — Post-12-Papers Verification

**Operation:** Complete lint pass after all 12 papers ingested

**Results:** 97%+ link validity (up from 91%), 200+ links scanned, 197 valid, 3 zombie, 0 contradictions. **12/15 zombie links from Pass #1 resolved.** File created: `wiki/lint-reports/lint-report-2026-04-14-pass2.md`. **Status:** Wiki production-ready for analysis phase. ✅

---

## [2026-04-14] analyses | Create 4 Comparative Analysis Pages

**Operation:** Post-lint, create 4 analysis pages to position thesis against 12-paper landscape

**Pages Created:** 
- `comparison-matrix.md` — 12 papers × 9 DT properties + LLM coverage; thesis = 9/9 (8/10 novelty score)
- `gap-analysis.md` — 8 gaps identified (3 critical, 3 high, 2 medium); thesis closes all 8
- `risk-profile.md` — Burr (I,T,A) taxonomy; thesis = Active Steering (I:2,T:2,A:1) with 3-layer guardrails
- `benchmark-template.md` — 3 scenarios, 4 models, 5-phase eval, 19 metrics, 92–120 planned runs

**Pages Updated:** `index.md` — "Analyses" section ✅ ACTIVE

**Status:** ✅ Wiki COMPLETE for literature review phase: 12 papers ingested + analyzed, 97%+ link validity, 0 contradictions, 4 analyses created, 8/10 novelty documented. **Implementation timeline: user-initiated.** ✅

---

## [2026-04-19] admin | Reorganize lint-reports into dedicated folder

**Operation:** Create `wiki/lint-reports/` folder and move existing lint reports for organizational clarity

**Actions performed:**
- Created folder: `wiki/lint-reports/`
- Moved: `wiki/lint-report-2026-04-14.md` → `wiki/lint-reports/lint-report-2026-04-14.md`
- Moved: `wiki/lint-report-2026-04-14-pass2.md` → `wiki/lint-reports/lint-report-2026-04-14-pass2.md`
- Updated: `CLAUDE.md` — no direct references (internal use only)
- Updated: `wiki/index.md` — Directory Structure section updated with new folder location

**Status:** ✅ Wiki housekeeping complete. Lint reports now centralized under `wiki/lint-reports/`

---

## [2026-04-14] ingest | Block C — Architectural Blueprint

**Operation:** Simultaneous ingestion of 3 papers: CogTwin (IJCAI-25), Hasan&Nguyen (6-layer), Biju (LangGraph)

**Pages Created:** 3 source pages, +6 glossary terms (DKR, DIKG, Decision Sandbox, Meta-Cognitive Layer, Supervisor Agent, StateGraph)

**Key Insights:** 
- Dual-KG is architecturally mandatory (CogTwin, Hasan&Nguyen, Biju confirm)
- LLM Reasoning genuinely novel (none of the 3 implement)
- KG Validation differentiating vs prior work
- Meta-Cognitive Supervisor opportunity for thesis implementation

**Status:** ✅ Block C completed (3/3), scaffolding sections touched: Ch. 2, 3, 4, 8. **Total progress: 9/12 papers (75%).** ✅

---

## [2026-04-14] ingest | Block D — Evaluation Methodology

**Operation:** Simultaneous ingestion of 2 papers: MultiAgentBench (Zhu et al., UIUC) + Berkeley CS294 (LLM eval MOOC)

**Pages Created:** 2 source pages, +8 glossary terms (LLM-as-Judge, Multi-Model Agreement, Outcome Validity, Milestone-based KPI, Task Score, Coordination Score)

**Key Insights:**
- MultiAgentBench: MARBLE framework with milestone-based KPI, TS/CS separation on 5 models
- Berkeley: Outcome Validity as absolute metric, ground-truth strategy (simulator + KG + LLM-as-judge), multi-model agreement robustness
- Tensions resolved: None — A+B+C+D forms coherent narrative (theory → domain → blueprint → rigorous metrics)
- **This is Contribution 2:** Not just CDT, but rigorous evaluation framework makes it scientific

**Status:** ✅ Block D completed (2/2), scaffolding sections touched: Ch. 5, 6, 7. **Total progress: 11/12 papers (92%).** ✅


---

## [2026-04-14] ingest | Block E — Closest Prior Work

**Operation:** Ingestion of final paper: WirelessAgent (Tong et al., HKUST, 2025)

**Pages Created:** 1 source page (`wiki/sources/wireless-agent-hkust-2025.md`)

**Key Insights:**
- WirelessAgent validates agentic approach for 5G (proven, not speculation)
- Cognitive loop Perception→Memory→Planning→Action is industry standard (WirelessAgent, CogTwin, Hasan&Nguyen, Biju all implement)
- Evaluation gap universal: WirelessAgent measures only output (BW %), no reasoning assessment
- **Thesis Differentiations:** (1) State: volatile KV-store vs persistent Ditto, (2) KG: flat RAG vs Neo4j constraints, (3) Eval: BW% only vs MMCI+milestone+LLM-as-judge+agreement
- Open research question: can KG+Ditto+coordination close model-size gap (96.6% DeepSeek vs 60.96% Llama-8B)?

**Status:** ✅ Block E completed (1/1). **12/12 papers ingested (100%).** Scaffolding sections touched: Ch. 3, 4, 7. ✅




