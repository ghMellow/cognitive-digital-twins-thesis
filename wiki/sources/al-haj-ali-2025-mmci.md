---
title: "Towards Cognitive Interoperability: Cognitive Digital Twin and Cognitive Architecture for Human-CPS Collaboration"
type: source
created: 2026-04-14
updated: 2026-04-14
authors: [Al-Haj Ali et al.]
year: 2025
tags: [CDT, MMCI, evaluation-framework, six-functions, CLARION]
contributo-tesi: "2-valutazione, framework-metodologico"
---

# Al-Haj Ali et al. (2025) — MMCI Framework for CDT

**Framework di valutazione a 5 livelli per agenti cognitivi. Risolve il gap critico della tesi: come misurare reasoning e planning senza ground truth.**

---

## Contributo Principale

Formalizza il **Multi-Modal Cognitive Interoperability (MMCI)** framework — un modello di maturità a 5 livelli per valutare l'allineamento cognitivo tra CDT e operatore umano. Estende le sei funzioni cognitive di Zheng et al. (2022) con una dimensione esplicita di valutazione.

---

## Riassunto

**Problema:** I CDT moderni coordinato con agenti cognitivi, ma manca una metodologia standardizzata per misurare la qualità del ragionamento e dell'allineamento tra il sistema automatico e gli operatori umani.

**Metodo:** Propone il framework MMCI su 5 livelli di maturità:
- Level 1: Shared Situation Awareness
- Level 2: Shared Mental Models
- Level 3: Intent & Reasoning Alignment
- Level 4: Joint Decision-Making + Metacognition
- Level 5: Full Autonomous Cognition

**Architettura:** CDT implementato via CLARION (neuro-symbolic cognitive architecture) per HRC (Human-Robot Collaboration) manifatturiero su un cobot UR5e.

**Risultati:** Validazione empirica del MMCI su scenari di collaborative inspection, con metriche di alignment tra CDT e operatore.

**Limiti:** MMCI non ha ancora metriche quantitative precise per ogni livello (framework qualitativo). Zero trasferibilità al 5G. Non copre LLM o linguaggio naturale (usa CLARION pre-LLM).

---

## Layer Divulgativo (YT)

**La domanda:** Come fai a dire che il tuo sistema cognitivo ragiona "bene"? Se togli gli LLM, cos'è rimasto?

Al-Haj Ali propone una scala di maturità: un CDT "immaturo" riconosce lo stato (Level 1), uno "maturo" ragiona insieme all'operatore e gli spiega il perché (Level 3+). 

Il trick è il **MMCI**: una griglia di valutazione che non richiede ground truth "teorico", ma misura quanto bene il sistema e l'operatore sono "sincronizzati" — quanto concordano su cosa sta succedendo e come agire.

Applicato al 5G, diventa: "Il mio Reasoning Agent spiega le diagnosi? L'operatore capisce e si fida?" Se sì, è Level 3+. Se no, è Level 1.

---

## Valore per la Tesi

### Aree Approfondite

1. **Le Sei Funzioni Cognitive Formalizzate** (Contributo 1 — Architettura)
   - Il paper estende Zheng et al. (2022) aggiungendo una dimensione di **valutazione empirica**
   - Ogni funzione viene misurata lungo il continuum MMCI
   - Mapping esplicito su tuoi agenti LangGraph (vedi tabella sotto)

2. **MMCI Framework — Risoluzione del Gap Critico** (Contributo 2 — Valutazione — FONDAMENTALE)
   - **Level 1:** Shared Situation Awareness — il CDT e l'operatore concordano sullo stato osservato?
   - **Level 2:** Shared Mental Models — il KG Neo4j incarna il modello del dominio?
   - **Level 3:** Intent & Reasoning Alignment — le diagnosi dell'LLM sono interpretabili?
   - **Level 4:** Joint Decision-Making + Metacognition — il sistema spiega le decisioni?
   - **Level 5:** Full Autonomous Cognition — il sistema agisce senza supervisione?
   
   **Questo è lo strumento che mancava.** Invece di inventare metriche custom, usi il MMCI come framework qualitativo e mostri a quale livello arriva il tuo sistema su ciascun agente.

3. **Mapping CLARION → LLM Architecture** (Contributo 1 — Positioning)
   - CLARION è l'architettura cognitiva di riferimento nel paper (subsystem ACS, NACS, GKS, MCS)
   - La tua tesi la sostituisce con LLM + KG — è una scelta di design originale e documentabile
   - Il trade-off: CLARION = more formal, LLM = more flexible + natural language

4. **Dominio Manifatturiero HRC → Tuo Dominio 5G** (Differenziatore)
   - Il paper lavora su Human-Robot Collaboration per ispezione collaborative
   - La tua tesi è su Network Operations (RAN management)
   - Gap aperto: nessun lavoro ha ancora appreso il MMCI al 5G

### Mapping: Funzioni MMCI → Tuoi Agenti

| Funzione (Al-Haj Ali) | Tuo Agente | Livello MMCI Target |
|---|---|---|
| **Situation Awareness** | Perception Agent | Level 1: Operatore e CDT concordano su RSRP/SINR/throughput? |
| **Mental Model** | Neo4j KG + Planning Agent | Level 2: KG codifica policy 3GPP e constraints? |
| **Intent Alignment** | Reasoning Agent | Level 3: Spiegazioni dell'LLM sono interpretabili e actionable? |
| **Joint Decision-Making** | Planning Agent | Level 4: Le azioni proposte includono justificazione e gradi di confidenza? |
| **Metacognition** | Communication Agent | Level 4: Il sistema monitora la qualità del suo ragionamento? |
| **Autonomy** | (Future work) | Level 5: No supervisione umana (out of scope tesi MVP) |

### Pro / Contro Come Fonte

| Dimensione | Pro | Contro |
|---|---|---|
| **Framework Valutazione** | MMCI risolve il gap principale della tesi (come misurare reasoning senza ground truth) | Metriche quantitative ancora non definite — framework è qualitativo/preliminare |
| **Sei Funzioni** | Estende Zheng et al. con dimensione di valutazione empirica | Non aggiunge novità rispetto a Zheng per l'architettura pura |
| **CLARION vs LLM** | Chiarisce il trade-off architetturale: simbolico vs neural | Pre-LLM, quindi niente su valutazione output linguaggio naturale, allucinazioni, etc. |
| **Dominio HRC** | Metodologia di valutazione è domain-agnostic, trasferibile a 5G | Zero trasferibilità verticale (HRC ≠ RAN management per specifiche politiche) |
| **Human Alignment** | Introduce la dimensione operatore umano (good for CDT+human) | Tua tesi è autonomismo puro (Perception→Reasoning→Planning autonomo), non collaborative |

### Appunti Contestualizzati per il Relatore

**Se chiede: "Come valuti il Reasoning Agent?"**

> "Adotto il framework MMCI proposto da Al-Haj Ali et al. (2025) come griglia di valutazione qualitativa. Per il Reasoning Agent, miro a Level 3 (Intent & Reasoning Alignment): le spiegazioni causali prodotte dall'LLM devono essere interpretabili da un operatore esperto e congruenti con il modello di dominio (KG Neo4j). Le metriche sono: LLM-as-judge (modello più grande valuta coerenza della diagnosi), multi-agent agreement (consensus tra Llama/Mistral/Phi-3/Qwen), calibration confidence (i gradi di sicurezza stimati corrispondono all'accuracy reale)."

**Se chiede: "Perché MMCI?"**

> "Il paper identifica il problema centrale della mia tesi: non esiste ground truth 'oggettivo' per valutare il reasoning cognitivo. MMCI non risolve questo completamente, ma propone di misurare l'allineamento tra il modello interno del sistema (KG) e le previsioni/azioni che il sistema fa — è un proxy credibile di qualità di reasoning senza dover aspettare outcome fisici."

**Se chiede: "Quanto di Al-Haj Ali applichi davvero?"**

> "Applico il framework MMCI come struttura di valutazione qualitativa, non la specifiche implementazione (CLARION + robot UR5e + HRC). La mia tesi sostituisce CLARION con una pipeline multi-agente LLM-based e adatta il framework al dominio 5G. Il paper valida il concetto; la mia tesi lo implementa con tecnologie contemporanee (LLM locali) e lo misura su task telecom."

---

### Dimensioni Strutturali

- **Argomento supportato:** Framework di valutazione MMCI per agenti cognitivi; sei funzioni cognitive estese con dimensione di valutazione
- **Gap colmato:** Metodologico — risolve il rischio critico di valutazione, fornisce griglia qualitativa quando ground truth è assente
- **Posizione scaffolding:** **Capitolo 5 — Metodologia di Valutazione**, sezione 5.1 (MMCI framework) e 5.2 (mapping su agenti)
- **Tensioni:** No contraddizioni, è una estensione naturale di Zheng et al. (2022)
- **Concetti introdotti:** MMCI framework, five levels of maturity, shared situation awareness, intent alignment, metacognition

---

## Concetti Introdotti

- [[mmci-framework]] — Multi-Modal Cognitive Interoperability, 5 livelli di maturità
- [[shared-situation-awareness]] — Level 1 di MMCI
- [[mental-model-alignment]] — Level 2–3 di MMCI
- [[joint-decision-making]] — Level 4–5 di MMCI

---

## Related Pages

- [[scaffolding-tesi]] — Articolo centrale
- [[sources/zheng-et-al-2022-cdt]] — Fondazione teorica (sei funzioni)
- [[glossary]] — MMCI, LLM-as-judge, confidence calibration
- [[concepts/six-cognitive-functions]] — Estensione valutazione
- [[sources/multiagent-bench-2025]] — Metriche concrete per agenti multi-agent
- [[concepts/knowledge-graph-in-cdt]] — Dual-KG come implementazione di Mental Models
