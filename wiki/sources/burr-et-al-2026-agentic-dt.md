---
title: "Agentic Digital Twins: A Taxonomy of Capabilities for Understanding Possible Futures"
type: source
created: 2026-04-14
updated: 2026-04-14
authors: [Christopher Burr, Mott MacDonald, Alan Turing Institute]
year: 2026
sources: [burr-2026-agentic-dt, valore-tesi-riassunto]
tags: [agentic-systems, risk-taxonomy, performative-prediction, DT-governance]
contributo-tesi: "1-architettura, rischio-metodologico"
---

# Burr et al. (2026) — Agentic Digital Twins: A Taxonomy of Capabilities

**Autori:** Christopher Burr, Mott MacDonald, Alan Turing Institute, Fujitsu, Università di Sheffield  
**Pubblicato:** Gennaio 2026 — arXiv:2601.18799 [cs.CY]  
**Rilevanza tesi:** **ALTA** — Fornisce positioning framework per il sistema + formalizza rischi metodologici critici

---

## 🎯 Idea Centrale

Un Digital Twin agentivo non si limita a _rappresentare_ un sistema fisico; lo _co-costituisce_, cambiando la realtà che misura. Questo processo è formalizzato come **performatività**: il modello deployato con parametri θ cambia la distribuzione dei dati che raccoglierà `D(θ)`.

Il paper propone una tassonomia di 27 configurazioni possibili di DT agentivi, organizzate in 3 cluster temporali:
- **Cluster 1 (The Present):** Tecnologicamente maturo, già deployato
- **Cluster 2 (The Threshold):** Raggiungibile a breve, con rischi di governance immediati
- **Cluster 3 (The Frontier):** Per lo più teorico

---

## 📐 Il Framework: 3 Dimensioni × 3 Livelli

Ogni DT agentivo si classifica con una tripla `(Agency, Coupling, Evolution)`:

| Dimensione | Livello 1 | Livello 2 | Livello 3 |
|---|---|---|---|
| **Agency** (dove si decide) | `E` External | `I` Internal | `D` Distributed |
| **Coupling** (frequenza interazione) | `L` Loose (batch) | `T` Tight (real-time) | `C` Constitutive (co-definizione) |
| **Evolution** (cambiamento modello) | `S` Static (fisso) | `A` Adaptive (parametri aggiornabili) | `R` Reconstructive (ridefinisce categorie) |

---

## 🗺️ Le 9 Configurazioni Principali

### Cluster 1 — The Present (Esiste Oggi)

| # | Nome | Codice | Descrizione | Esempio |
|---|---|---|---|---|
| 1 | Computational Tool | `(E,L,S)` | Strumento passivo, nessuna autonomia | Google Maps, DT cardiaco |
| 2 | Adaptive Monitor | `(E,T,A)` | Real-time ma l'umano comanda, sistema apprende parametri | DT fabbrica con ML online |
| 3 | **Active Steering** | `(I,T,A)` | **TESI QUI** — Agency interna, tight coupling, modello adattivo | DT manifatturiero con agenti autonomi |

### Cluster 2 — The Threshold (Raggiungibile a Breve)

| # | Nome | Codice | Descrizione | Rischio |
|---|---|---|---|---|
| 4 | Symbiotic | `(D,T,A)` | Agency emerge dall'interazione, nessuno controlla | Smart city senza governo |
| 5 | **Governor** | `(I,C,A)` | **MASSIMO RISCHIO** — DT definisce cosa misura → lock-in | Singapore e-road pricing |
| 6 | Swarm | `(D,T,S)` | Fleet autonomo con modelli statici → emergenza caotica | Phantom jams traffico |

### Cluster 3 — The Frontier (Teorico)

| # | Nome | Codice | Descrizione |
|---|---|---|---|
| 7 | Worldbuilder | `(E,L,R)` | Ricostituisce ontologia con human-in-loop | AlphaFold-style |
| 8 | Voyager | `(I,T,R)` | Autonomo + ricostruisce categorie → inscrutable | Fantascienza |
| 9 | Reconstructive Assemblage | `(D,C,R)` | Sistemi multipli che si ridefiniscono reciprocamente | Fantascienza |

---

## ⚡ Concetto Critico: Performative Prediction

Basato su **Perdomo et al. (ICML 2020)** e **Hardt & Mendler-Dünner (Statistical Science 2025)**

### La Matematica

Un modello deployato con parametri θ cambia la distribuzione dei dati che raccoglierà:

$$\text{Distribuzione} = D(\theta)$$

Il vero obiettivo non è minimizzare il rischio su dati storici, ma su quelli che il modello stesso creerà:

$$\min_{\theta} \text{Risk}(\theta, D(\theta))$$

### Il Punto di Performative Stability

Il **punto di equilibrio performativo** θ_PS è quando il modello sembra ottimale _perché ha creato la distribuzione su cui viene valutato_:

- Modello predice: "azione X risolve il problema Y"
- Modello esegue X
- Metriche cambiano a causa di X
- Al ciclo successivo X appare ancora "ottimale"
- **Lock-in:** il sistema non può distinguere tra "X realmente ottimale" e "X ottimale per questa distribuzione ristretta"

### Esempio 5G (Dalla Tesi)

```
Ciclo 1:
  - Reasoning Agent diagnostica: "SINR basso causa handover failure"
  - Planning Agent propone: "Aumenta Tx power gNB-B1 di 3dB"
  - Azione eseguita

Ciclo 2:
  - Perception Agent osserva: SINR migliore, handover failure ridotto ✓
  - Reasoning Agent apprende correlazione: "Aumentare Tx = risolvere SINR"

Ciclo N (performative lock-in):
  - Sistema converge su "aumentare Tx è sempre ottimale"
  - MA: Il sistema ha cambiato la distribuzione delle metriche con le sue azioni
  - Non sa se "aumentare Tx" è ottimale per la rete fisica o solo per questa versione modificata
  - Non può scoprire soluzioni alternative perché tutti i cicli seguenti vedranno la stessa distribuzione
```

---

## 🎯 Mapping Alla Tesi: Positioning (I,T,A)

**La tesi propone esattamente la configurazione Active Steering `(I,T,A)`:**

| Dimensione | Implementazione Tesi |
|---|---|
| **Agency = Internal** | Agenti LLM (Perception, Reasoning, Planning, Communication) decidono autonomamente senza intervento umano; il Planning Agent non attende approvazione |
| **Coupling = Tight** | Eclipse Ditto via WebSocket per sincronizzazione real-time (non batch); ciclo completo ~500ms-2s |
| **Evolution = Adaptive** | Reasoning Agent apprende pattern da anomalie; KG si popola con correlazioni storiche; Planning Agent evolve la selezione di azioni |

---

## 🚨 Rischio Principale: Deriva verso Governor (I,C,A)

Il paper identifica il **Governor** `(I,C,A)` come la configurazione più pericolosa per i DT con agency interna:

| Aspetto | Rischio per la Tesi |
|---|---|
| **Agency interno** | ✅ Intenzionale (tesi) |
| **Coupling tight** | ✅ Intenzionale (tesi) — WebSocket real-time |
| **Constitutive coupling** | ⚠️ **RISCHIO** — Se il Planning Agent inizia a _ridefinire_ le metriche KPI (es. "SINR basso = situazione impossibile", ignorando i dati), il sistema entra nella modalità Governor |
| **Performative lock-in** | ⚠️ **RISCHIO** — Il sistema potrebbe convergere su soluzioni che funzionano _perché ha cambiato la distribuzione_, non perché siano ottimali per la rete reale |

### Guardrail: Il Knowledge Graph

Il **Neo4j KG che valida i vincoli operativi prima dell'esecuzione** è il meccanismo architetturale che impedisce questa deriva:

1. **KG rimane external:** I vincoli 3GPP codificati in KG non verranno riscritti dal Planning Agent
2. **Constraint checking:** Ogni azione del Planning Agent deve rispettare i vincoli KG (limiti termici, limiti backhaul, SLA)
3. **Audit trail:** Tutte le validazioni fallite sono registrate → il sistema non può fingere che un vincolo non esista
4. **Performative boundary:** Il KG mantiene il sistema entro i limiti fisici della rete 5G, impedendo il lock-in su distribuzioni fittizie

---

## 📋 Pro & Contro per la Tesi

### ✅ Aspetti Utili

| Aspetto | Utilità |
|---|---|
| **Framework di positioning** | Consente posizionamento esatto: "Configurazione Active Steering (I,T,A) per evitare deriva verso Governor" |
| **Vocabolario condiviso** | Nel Related Work puoi usare codice (I,T,A) e tutti capiscono immediatamente il livello di autonomia |
| **Formalizzazione del rischio** | Performative prediction fornisce **vocabolario riconosciuto** per spiegare il rischio principale della tesi |
| **Giustificazione architetturale** | Spiega **perché** il Knowledge Graph è mandatorio, non opzionale |
| **Sezione rischi & limitazioni** | Puoi dichiare apertamente: "Il sistema è in configurazione (I,T,A) con guardrail KG per prevenire deriva verso (I,C,A)" |

### ❌ Limitazioni

| Aspetto | Motivo |
|---|---|
| **Zero empirismo** | Nessun esperimento numerico, nessun benchmark; utile come vocabolario, non come guida implementativa |
| **Non copre LLM specificamente** | Tassonomia è agnostica rispetto al technology stack; non parla di Llama, Mistral, quantizzazione |
| **Non copre 5G** | Casi di studio sono traffico stradale (toy model) e manifattura; non telco |
| **Non copre valutazione** | Nessun suggerimento su come misurare se un sistema è realmente in (I,T,A) vs (I,C,A) |

---

## 📝 Appunti per il Relatore

Se il relatore chiede domande critiche sulla governance del sistema:

**D: "Come si è sicuri che il sistema non drifta verso configurazione Governor?"**

R: "Il Knowledge Graph implementa un guardrail architetturale esplicito — i vincoli 3GPP sono codificati in schema Neo4j immutabile dal Planning Agent. Questo mantiene il sistema meccanicamente ancorato al livello (I,T,A) [Burr et al. 2026 Active Steering] e impedisce il lock-in performativo in distribuzioni fittizie."

**D: "Cosa succede se il Reasoning Agent 'impara' correlazioni false?"**

R: "È precisamente il rischio di performative prediction [Burr et al. 2026, Perdomo ICML 2020]: il sistema potrebbe convergere su una soluzione che _sembra ottimale_ perché ha modificato la distribuzione con le sue azioni, non perché sia realmente ottimale per la rete 5G. Questo è uno dei motivi per cui facciamo fault injection controllata — perturbazione esterna del simulatore che il sistema non controlla — per rilevare se il sistema ha effettivamente imparato pattern stabili o se è in lock-in performativo."

**D: "Quindi il rischio principale è performative lock-in?"**

R: "Esattamente. Con il simulatore 3GPP virtuale otteniamo rapidità di ciclo e ripetibilità, ma perdiamo il "reality check" di una rete fisica reale che il sistema non controlla. Abbiamo incorporato tre meccanismi per mitigare: (1) vincoli KG immutabili, (2) fault injection esterna, (3) multi-agent agreement su diagnosi per rilevare divergenza dalle leggi fisiche note."

---

## 🔗 Concetti Introdotti

- [[agentic-dt-risk-taxonomy]] — La tassonomia delle 9 configurazioni
- [[performative-prediction]] — Il rischio di lock-in performativo
- [[governor-configuration]] — Configurazione Governor (I,C,A) e come evitarla
- [[tight-coupling-risks]] — Rischi specifici di tight coupling real-time

---

## 📚 Riferimenti Fondamentali da Approfondire

1. **Performative Prediction:** Perdomo et al., ICML 2020 | Hardt & Mendler-Dünner, _Statistical Science_ 2025
2. **Steering Representations:** Korenhof, Blok & Kloppenburg, _Philosophy & Technology_ 2021
3. **DT Philosophical Foundations:** Wagg et al., _Data-Centric Engineering_ 2025
4. **Algorithmic Governance:** Zuboff, _The Age of Surveillance Capitalism_ (per contesto) + Burr & Gonzalez & Keudel, 2021

---

## 🎬 Ruolo nello Scaffolding

**Sezioni impattate:**
- **Cap. 1 (Introduzione):** Positioning con codice (I,T,A)
- **Cap. 3 (Related Work):** Vocabolario e framework di governance per DT agentivi
- **Cap. 5 (Metodologia):** Performative prediction come rischio metodologico centrale
- **Cap. 8 (Discussione):** Limitazioni del sistema entro frontiera (I,T,A) e prevenzione deriva verso (I,C,A)

---

## Related Pages

- [[sources/restart-2024-ndt]] — 5G domain justification
- [[sources/zheng-et-al-2022-cdt]] — CDT foundational theory
- [[concepts/cognitive-digital-twin]] — CDT definition
- [[glossary]] — Terminology
