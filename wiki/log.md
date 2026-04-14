---
title: Log di Progetto
type: analysis
created: 2026-04-14
updated: 2026-04-14
sources: []
tags: [project-log, chronology]
---

# Log — Cronologia Progetto Wiki

Registro append-only di tutte le operazioni sulla wiki.

---

## [2026-04-14] setup | Inizializzazione struttura wiki

**Operazione:** Setup completo della struttura wiki secondo CLAUDE.md

**Azioni compiute:**
- Creazione cartelle: `sources/`, `concepts/`, `personas/`, `analyses/`, `style/`
- Creazione file master: `glossary.md`, `overview.md`, `log.md` (questo), `index.md`
- Inizializzazione di glossario con 40+ termini canonici dominio CDT + 5G
- Creazione pagina overview con sintesi tesi, problematica, contributi, stack tecnologico

**File creati:** 5 cartelle + 4 file master  
**File rimangono:** `scaffolding-tesi.md` (già popolato con literature review)

**Prossimo passo:** Ingestare paper raw (blocco A–E da scaffolding) in `sources/` → aggiornare `index.md`

---

## [2026-04-14] ingest | Zheng et al. (2022) — The Emergence of Cognitive Digital Twin

**Punto di ingresso:** Caso B — valore-tesi.md già disponibile  
**Pagine create:** `wiki/sources/zheng-et-al-2022-cdt.md`  
**Pagine aggiornate:** `scaffolding-tesi.md` (checkbox + link), `index.md` (checkbox + link)  
**Tensioni rilevate:** No  
**Sezioni scaffolding toccate:** Cap. 2 — Background Teorico (sezione 2.1 e 2.2)

**Sommario:** Fondazione teorica della definizione di CDT. Il paper formalizza le cinque caratteristiche (cognitive capability, full lifecycle, autonomy, continuous evolving, DT-based design) e le sei funzioni cognitive (percezione, ragionamento, memoria, apprendimento, adattamento, decision-making). Legittima il KG come componente mandatoria. Mapping 1:1 su architettura tesi: ogni agente LangGraph copre una o più funzioni cognitive. **Contributo principale: vocabolario formale e framework teorico per il Background**.  
**Non coperto:** Implementazione, LLM, valutazione del reasoning cognitivo, domini specifici (5G).  
**Prossimo:** Al-Haj Ali et al. (2025) — estensione su MMCI framework e valutazione

---

## [2026-04-14] ingest | Al-Haj Ali et al. (2025) — Towards Cognitive Interoperability

**Punto di ingresso:** Caso B — valore-tesi.md già disponibile  
**Pagine create:** `wiki/sources/al-haj-ali-2025-mmci.md`, `wiki/concepts/mmci-framework.md`  
**Pagine aggiornate:** `scaffolding-tesi.md` (checkbox + link), `index.md` (checkbox + concepts)  
**Tensioni rilevate:** No  
**Sezioni scaffolding toccate:** Cap. 5 — Metodologia di Valutazione (sezione 5.1 e 5.2)

**Sommario:** MMCI framework (Multi-Modal Cognitive Interoperability) — five-level maturity model per valutare allineamento cognitivo tra CDT e operatore/vincoli di dominio. **Risolve il gap critico:** come misurare Reasoning e Planning senza ground truth esplicito? Risposta: misurare alignment tra modello interno (KG) e previsioni/azioni che il sistema fa. Livelli: SSA (situazione) → SMM (modelli mentali) → Intent Alignment (diagnosi) → Joint Decision (azioni + spiegazione) → Full Autonomy (out of scope). **Contributo principale: framework di valutazione qualitativa con possibilità di quantificazione**. Substitution architetturale: CLARION (paper) → LLM pipeline (tesi), HRC manifattura (paper) → RAN 5G (tesi).  
**Non coperto:** Metriche quantitative precise per ogni livello, dominio 5G, LLM, linguaggio naturale.  
**Prossimo:** Blocco B — RESTART NDT (2024) — giustificazione dominio 5G

---
