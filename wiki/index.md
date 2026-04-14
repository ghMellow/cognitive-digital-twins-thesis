---
title: Indice Master della Wiki
type: analysis
created: 2026-04-14
updated: 2026-04-14
sources: []
tags: [index, navigation]
---

# Indice Master — Wiki della Tesi

Catalogo completo di tutte le pagine wiki della tesi. Aggiornato incrementalmente ad ogni ingest.

---

## 📋 Documenti Fondamentali — ATTIVO ORA ✅

| Documento              | Tipo     | Scopo                                                                  | Link                 |
| ---------------------- | -------- | ---------------------------------------------------------------------- | -------------------- |
| Scaffolding della Tesi | analysis | Struttura argomentativa centrale della tesi, aggiornata ad ogni ingest | [[scaffolding-tesi]] |
| Glossario              | concept  | Terminologia canonica dominio CDT + 5G                                 | [[glossary]]         |
| Overview Tesi          | analysis | Sintesi problema, ipotesi, contributi scientifici, stack               | [[overview]]         |
| Log Progetto           | analysis | Cronologia append-only di tutte le operazioni                          | [[log]]              |

---

## 📚 Sources (Paper, Call, Approfondimenti) — ATTIVO ORA ✅

Ingest documenti raw in pagine wiki strutturate.

### Blocco A — Teoria CDT
- [x] [[sources/zheng-et-al-2022-cdt]] — Zheng et al. (2022) — Foundational definition, six functions, KG as backbone
- [x] [[sources/al-haj-ali-2025-mmci]] — Al-Haj Ali et al. (2025) — MMCI framework, 5 levels of maturity for evaluation

### Blocco B — Pattern e Contesto
- [x] [[sources/restart-2024-ndt]] — RESTART NDT (2024) — Architettura NDT, 3-tier, IBN, justificazione 5G
- [x] [[sources/burr-et-al-2026-agentic-dt]] — Burr et al. (2026) — Risk taxonomy (I,T,A) vs (I,C,A), performative prediction
- [x] [[sources/kalyani-collier-2024-mas-dt]] — Kalyani & Collier (2024) — SLR 22 paper MAS+DT, architettura multi-agente
- [x] [[sources/pretel-et-al-2024-mas-dt]] — Pretel et al. (2024) — SLR 64 paper MAS+DT, 12 DT properties, gap analysis

### Blocco C — Blueprint Architetturale
- [x] [[sources/cogtwin-ijcai-25]] — CogTwin IJCAI-25 — Dual-KG pattern, CDT architecture
- [x] [[sources/hasan-nguyen-2026-agentic-dt]] — Hasan & Nguyen (2026) — 6-layer agentic architecture
- [x] [[sources/biju-2024-langgraph]] — Biju (2024) — LangGraph supervisor pattern

### Blocco D — Metodologia Valutazione
- [x] [[sources/multiagent-bench-2025]] — MultiAgentBench (2025) — Milestone-based KPI, Task/Coordination Score framework
- [x] [[sources/berkeley-cs294-llm-eval]] — Berkeley CS294 (2026) — LLM Agent Evaluations, outcome validity

### Blocco E — Closest Prior Work
- [x] [[sources/wireless-agent-hkust-2025]] — WirelessAgent HKUST (2025) — LLM agents + LangGraph for 5G network slicing

### Call e Approfondimenti
- [ ] Prima call (2026-03-17) — Transcrizione e decisioni chiave
- [ ] Seconda call (2026-03-31) — Transcrizione e decisioni chiave
- [ ] Approfondimento video Berkeley — Agentic AI patterns
- [ ] Approfondimento uso di Pi — (TBD)
- [ ] Ruolo degli agenti nel CDT — Analisi del ruolo specifico

---

## 🎯 Concepts (Teorie Fondamentali) — ATTIVO ORA ✅

Pagine concettuali che rimangono stabili durante la tesi.

### Concepts Creati (Blocco A-B)
- [x] [[concepts/cognitive-digital-twin]] — Definizione formale, cinque caratteristiche, sei funzioni, mapping agenti
- [x] [[concepts/six-cognitive-functions]] — Percezione, ragionamento, memoria, apprendimento, adattamento, decision-making
- [x] [[concepts/knowledge-graph-in-cdt]] — Ruolo architettuale, pattern Dual-KG, schema 5G, validazione KG
- [x] [[concepts/mmci-framework]] — Multi-Modal Cognitive Interoperability, 5 livelli maturity, operationalization
- [x] [[concepts/network-digital-twin]] — 5G-specific DT, 3-tier architecture (DH, Autonomic, Closed-loop), AI as driver
- [x] [[concepts/digital-hat]] — Interface layer, sincronizzazione real-time, Eclipse Ditto mapping, protocolli
- [x] [[concepts/intent-based-networking]] — IBN flow, translation to actions, KG constraint validation per 5G
- [x] [[concepts/closed-loop-autonomy]] — Feedback loop, adaptation, why MMCI evaluation needed- [x] [[concepts/agentic-dt-risk-taxonomy]] — 27 configurazioni (I,T,A) vs (I,C,A), Burr framework
- [x] [[concepts/performative-prediction]] — Lock-in risk, Perdomo ICML 2020, detection tests
### Concepts Futuri (Da Aggiungere Durante Ingest)
- [ ] Digital Twin (tradizionale) — Definizione, BLOCCOvs CDT
- [ ] Multi-Agent Systems — Orchestration patterns, state management
- [ ] LLM Evaluation Methods — LLM-as-judge, confidence calibration, agreement metrics
- [ ] Agentic AI Risk Taxonomy — (Da Burr et al. 2026, Blocco B)
- [ ] LangGraph Orchestration — Conditional edges, state graph patterns
- [ ] Reasoning without Ground Truth — (Core methodological concept)

---

## 📊 Analyses (Tabelle Comparative, Gap Analysis) — ATTIVO ORA ✅

_Creato al completamento dell'ingest di TUTTI i paper (dopo Blocco E) e Lint Pass #2_

Pagine analitiche che riassumono la ricerca e posizionano il contributo della tesi.

- [x] [[analyses/comparison-matrix]] — 12 papers vs. 9 DT properties + LLM coverage; thesis uniqueness score (8/10)
- [x] [[analyses/gap-analysis]] — 8 critical gaps (LLM agents, 5G domain, agent eval, governance, etc.) con risoluzioni tesi
- [x] [[analyses/risk-profile]] — Burr (I,T,A) taxonomy: tesi = (I:2,T:2,A:1) "Active Steering"; guardrails operationalizzati
- [x] [[analyses/benchmark-template]] — 3 fault injection scenarios (A: single fault, B: contention, C: cascade) con full metrics framework

---

## 📝 Style Rules (Convenzioni Tesi) — DEFERRED ⏳

_Creato quando inizi a scrivere il body chapters (Capitoli 1–8)_

Convenzioni di scrittura, terminologia canonica, formato equazioni, stile citazioni.

**Planned rules:**
- Terminologia e abbreviazioni canoniche (già parzialmente in glossary.md)
- Formato equazioni 3GPP e metriche di rete
- Stile di citazione per paper vs implementazioni vs standard
- Nomenclatura agenti LangGraph
- Convenzione per rappresentare il ciclo cognitivo

---

## 👥 Personas (Audience) — OPTIONAL

_Opzionale — possibile omissione se la tesi è mono-audience_

Target audience della tesi e come personalizzare la spiegazione per ciascuno:
- Relatore (ricercatore in CDT/MAS) — focalizzazione su novità metodologica
- Azienda (Fondazione Ugo Bordoni) — focalizzazione su applicabilità 5G
- Comunità ricerca (pubblicazione) — focalizzazione su benchmark e riproducibilità
- Operatori di rete — focalizzazione su usabilità pratica

**Nota:** Probabilmente non necessario per una tesi magistrale single-authored.

---

## 🚦 Status Ingest — Wiki Literature Review Phase COMPLETE

| Milestone                           | Status | Note                                 |
| ----------------------------------- | ------ | ------------------------------------ |
| Setup wiki                          | ✅      | Struttura, file master, glossario    |
| **Blocco A — Teoria CDT**           | ✅      | 2/2 (Zheng + Al-Haj Ali) — 14 Apr   |
| **Blocco B — Pattern e Contesto**   | ✅      | 4/4 (RESTART, Burr, Kalyani, Pretel) — 14 Apr |
| **Blocco C — Blueprint Archi.**     | ✅      | 3/3 (CogTwin, Hasan&Nguyen, Biju) — 14 Apr |
| **Blocco D — Valutazione**          | ✅      | 2/2 (MultiAgentBench, Berkeley) — 14 Apr |
| **Blocco E — Closest Prior Work**   | ✅      | 1/1 (WirelessAgent) — 14 Apr        |
| **Lint Pass #1**                    | ✅      | 0 contraddizioni, 91% link validity |
| **Lint Pass #2**                    | ✅      | 97%+ link validity, 12 zombies resolved |
| **Creazione analyses/ pages**       | ✅      | 4/4 (comparison, gap, risk, benchmark) — 14 Apr |
| Ingest call 1 + 2                   | ⏳      | Opzionale (bassa priorità) |
| Ingest approfondimenti (3 files)    | ⏳      | Opzionale (bassa priorità) |
| Creazione style/ pages              | ⏳      | Durante scrittura Cap. 1–8          |
| Aggiornamento scaffolding finale    | ⏳      | Review pass prima della tesi         |
| Lint della wiki (pre-submission)    | ⏳      | Before thesis handover               |

---

## 📂 Struttura Directory

```
wiki/
├── index.md (questo file)
├── scaffolding-tesi.md ✅ documento centrale
├── glossary.md
├── overview.md
├── log.md
├── lint-report-2026-04-14.md ✅ (pass #1)
├── lint-report-2026-04-14-pass2.md ✅ (pass #2)
├── sources/ ✅ ATTIVO (12 papers)
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
├── concepts/ ✅ ATTIVO (10 concepts)
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
├── analyses/ ✅ ATTIVO (4 analyses)
│   ├── comparison-matrix.md
│   ├── gap-analysis.md
│   ├── risk-profile.md
│   └── benchmark-template.md
├── style/ ⏳ DEFERRED (writing phase)
└── personas/ (optional — empty)
```

---
