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
- [ ] RESTART NDT (2024) — Justificazione dominio 5G
- [ ] Burr et al. (2026) — Agentic AI Risk Taxonomy
- [ ] Kalyani (2024) — SLR 22 paper MAS+DT
- [ ] Pretel (2024) — SLR 64 paper MAS+DT

### Blocco C — Blueprint Architetturale
- [ ] CogTwin IJCAI-25 — Dual-KG pattern, CDT architecture
- [ ] Hasan & Nguyen (2026) — 6-layer agentic architecture
- [ ] Biju (2024) — LangGraph supervisor pattern

### Blocco D — Metodologia Valutazione
- [ ] MultiAgentBench (2025) — Multi-agent metric framework
- [ ] Berkeley CS294 (2025) — LLM agents evaluation (MOOC video)

### Blocco E — Closest Prior Work
- [ ] WirelessAgent HKUST (2025) — LangGraph + 5G wireless domain

### Call e Approfondimenti
- [ ] Prima call (2026-03-17) — Transcrizione e decisioni chiave
- [ ] Seconda call (2026-03-31) — Transcrizione e decisioni chiave
- [ ] Approfondimento video Berkeley — Agentic AI patterns
- [ ] Approfondimento uso di Pi — (TBD)
- [ ] Ruolo degli agenti nel CDT — Analisi del ruolo specifico

---

## 🎯 Concepts (Teorie Fondamentali) — ATTIVO ORA ✅

Pagine concettuali che rimangono stabili durante la tesi.

### Concepts Creati (Blocco A)
- [x] [[concepts/cognitive-digital-twin]] — Definizione formale, cinque caratteristiche, sei funzioni, mapping agenti
- [x] [[concepts/six-cognitive-functions]] — Percezione, ragionamento, memoria, apprendimento, adattamento, decision-making
- [x] [[concepts/knowledge-graph-in-cdt]] — Ruolo architettuale, pattern Dual-KG, schema 5G, validazione KG
- [x] [[concepts/mmci-framework]] — Multi-Modal Cognitive Interoperability, 5 livelli maturity, operationalization

### Concepts Futuri (Da Aggiungere Durante Ingest)
- [ ] Digital Twin (tradizionale) — Definizione, BLOCCOvs CDT
- [ ] Multi-Agent Systems — Orchestration patterns, state management
- [ ] LLM Evaluation Methods — LLM-as-judge, confidence calibration, agreement metrics
- [ ] Agentic AI Risk Taxonomy — (Da Burr et al. 2026, Blocco B)
- [ ] LangGraph Orchestration — Conditional edges, state graph patterns
- [ ] Reasoning without Ground Truth — (Core methodological concept)

---

## 📊 Analyses (Tabelle Comparative, Gap Analysis) — DEFERRED ⏳

_Creato al completamento dell'ingest di TUTTI i paper (dopo Blocco E)_

Pagine analitiche che riassumono la ricerca e posizionano il contributo della tesi.

**Planned analyses:**
- Comparison matrix: MAS+DT state-of-art (Pretel 64, Kalyani 22, WirelessAgent, CogTwin, Hasan&Nguyen)
- Gap analysis: cosa copre la tesi vs cosa rimane open
- Risk profile della tesi secondo Burr taxonomy
- Benchmark template (Llama/Mistral/Phi-3/Qwen su fault injection scenarios)

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

## 🚦 Status Ingest

| Milestone                           | Status | Note                                 |
| ----------------------------------- | ------ | ------------------------------------ |
| Setup wiki                          | ✅      | Struttura, file master, glossario    |
| **Blocco A — Teoria CDT**           | ✅      | Zheng + Al-Haj Ali completati        |
| Ingest paper Blocco B               | ⏳      | Prossimo: RESTART NDT (2024)         |
| Ingest paper Blocco C               | ⏳      | Dopo B                               |
| Ingest paper Blocco D               | ⏳      | Dopo C                               |
| Ingest paper Blocco E               | ⏳      | Dopo D                               |
| Ingest call 1 + 2                   | ⏳      | In parallelo con paper               |
| Ingest approfondimenti (3 files)    | ⏳      | In parallelo con paper               |
| Creazione analyses/ pages           | ⏳      | Dopo ingest completo (post-Blocco E) |
| Creazione style/ pages              | ⏳      | Quando inizi a scrivere corpo (Cap.1) |
| Aggiornamento scaffolding finale    | ⏳      | Dopo tutti gli ingest (review pass)  |
| Lint della wiki                     | ⏳      | Prima di consegna tesi               |

---

## 📂 Struttura Directory

```
wiki/
├── index.md (questo file)
├── scaffolding-tesi.md ✅ documento centrale
├── glossary.md
├── overview.md
├── log.md
├── sources/ ✅ ATTIVO
│   ├── zheng-et-al-2022-cdt.md
│   └── al-haj-ali-2025-mmci.md
├── concepts/ ✅ ATTIVO
│   ├── cognitive-digital-twin.md
│   ├── six-cognitive-functions.md
│   ├── knowledge-graph-in-cdt.md
│   └── mmci-framework.md
├── analyses/ ⏳ DEFERRED (post-ingest)
├── style/ ⏳ DEFERRED (writing phase)
└── personas/ (optional)
```

---
