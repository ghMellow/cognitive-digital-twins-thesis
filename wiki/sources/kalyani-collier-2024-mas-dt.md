---
title: "The Role of Multi-Agents in Digital Twin Implementation: A Short Survey"
type: source
created: 2026-04-14
updated: 2026-04-14
authors: [Yogeswaranathan Kalyani, Rem Collier]
year: 2024
publication: "ACM Computing Surveys, Vol. 57, No. 3"
sources: [kalyani-collier-2024, valore-tesi-riassunto]
tags: [MAS, DT, survey, systematic-review, multi-agent-patterns]
contributo-tesi: "2-architettura, 3-stato-dell-arte"
---

# Kalyani & Collier (2024) — The Role of Multi-Agents in Digital Twin Implementation

**Autori:** Yogeswaranathan Kalyani, Rem Collier — University College Dublin  
**Pubblicato:** ACM Computing Surveys, Vol. 57, No. 3 — Novembre 2024  
**DOI:** https://doi.org/10.1145/3697350  
**Rilevanza tesi:** **MEDIA-ALTA** — Valida architettura multi-agente + identifica gap metodologico specifico

---

## 🎯 Idea Centrale

Una **Systematic Literature Review (SLR)** che mappa come i **Multi-Agent Systems (MAS)** vengono integrati nei **Digital Twin (DT)** per creare sistemi autonomi e adattativi. A partire da 16.100 risultati su Google Scholar (2020–2024), gli autori selezionano e analizzano **22 paper rilevanti** su 4 Research Questions.

**Tesi del paper:** MAS e DT sono complementari: i DT forniscono simulazione e ancoraggio fisico; i MAS forniscono coordinamento, autonomia e adattabilità. La sinergia produce sistemi intelligenti.

---

## 📋 Le 4 Research Questions

| RQ | Domanda | Risposta Sintetica |
|---|---|---|
| **RQ1** | In quali domini vengono usati agenti nei DT? | Manufacturing domina (10/22); edge computing, agriculture, healthcare emergenti |
| **RQ2** | Quali feature degli agenti vengono sfruttate? | Autonomous decision-making, scheduling, task allocation, real-time processing, simulation & optimization |
| **RQ3** | Quali altre tecnologie si affiancano agli agenti? | DRL, ABS, Ontologie/KG, JADE, JaCaMo, SPADE, WLDT, simulatori 3D |
| **RQ4** | Quali gap rimangono? | Scalabilità, interoperabilità, AI/ML avanzata, privacy/security, valutazione di affidabilità |

---

## 📊 Risultati Chiave

### Domini Coperti

| Dominio | # Paper | Maturity | Note |
|---|---|---|---|
| **Manufacturing** | 10 | Maturo | Factory DT, supply chain, quality control |
| **Edge Computing / CPS** | 5 | Niche | Vehicular DT, air mobility, resource allocation |
| **Smart Agriculture** | 3 | Emergente | Irrigation, crop monitoring, farm optimization |
| **Smart Cities** | 2 | Emergente | Traffic, energy grids |
| **Healthcare** | 2 | Emergente | Patient monitoring, hospital operations |

**Insight per la tesi:** 5G/telecomunicazioni manca completamente → **gap specifico identificato da Pretel et al. (64 paper)**. La tesi riempie questo gap posizionandosi in edge computing / network management.

### Feature degli Agenti Più Usate

1. **Autonomous Decision-Making** — Agenti decidono senza intervento umano
2. **Dynamic Scheduling** — Riallocazione risorse in tempo reale  
3. **Cooperative Task Allocation** — Coordinator agent distribuisce compiti
4. **Real-Time Data Processing** — Feedback loop stretto (millisecondi)
5. **Simulation & Optimization** — Agenti testano scenari prima di eseguire

**Rilevanza per tesi:** I 4 agenti LangGraph (Perception, Reasoning, Planning, Communication) implementano tutte queste feature.

### Stack Tecnologico Ricorrente

**Agent Frameworks:** JADE, JaCaMo, SPADE, custom frameworks  
**DT Platforms:** WLDT, Unity3D, Microsoft AirSim, custom simulators  
**Learning:** Deep Reinforcement Learning (DRL) dominante; alcuni rule-based e ontology-based  
**Knowledge:** Ontologie Semantic Web (RDF/OWL), Knowledge Graphs, domain-specific rule sets

**Differenza con tesi:** Tutti i 22 paper usano **DRL classico** o **rule-based agents**. **NESSUNO usa LLM** come layer cognitivo. Questa è la novità della tesi.

---

## 🏗️ Architettura Proposta (Smart Agriculture Showcase)

Gli autori propongono un **Web of Digital Twins** per open-environment arable farming con questa struttura:

```
User Interface (input: farm_id, field_id, sowing_date)
    ↓
Microservices Layer
    ├── Weather Forecasting Service
    ├── Soil Analysis Service
    ├── Crop Growth Model (ML)
    └── Irrigation Scheduling Service
    ↓
Agent Layer
    ├── Manager Agent          — Orchestrazione
    ├── Farm Agent             — DT della farm
    ├── Field Agent            — Monitoraggio + sensori
    └── Recommendation Agent   — Output verso utente
    ↓
Knowledge Layer
    └── Semantic Web + Domain Ontologies (AGROVOC)
```

**Mapping alla tesi:**
- Manager Agent ← Planning Agent (overall orchestration)
- Farm Agent ← Perception Agent (DT state)
- Field Agent ← Perception Agent (sensor data)
- Recommendation Agent ← Planning + Communication (actionable decisions)
- Knowledge Layer ← Neo4j KG (domain knowledge, constraints)

---

## 🔴 Gap Identificati (Future Work)

| Gap | Descrizione | Rilevanza per Tesi |
|---|---|---|
| **Scalabilità & Adattabilità** | Non risolta in nessuno dei 22 paper | 🟡 Media — tesi locale M4 Pro è micro-scale, non è il focus |
| **Interoperabilità & Standardizzazione** | Ogni paper usa stack diverso; nessuno standard | 🔴 Alta — tesi usa exact stack (LangGraph+Ditto+Neo4j) potrebbe proporre pattern |
| **Integrazione avanzata AI/ML** | Ancora superficiale; DRL prevalente, no LLM | 🔴 **MASSIMA** — Questo è esattamente il gap che riempie la tesi |
| **Valutazione di Affidabilità** | Come misurare che l'agente sia "affidabile"? | 🔴 **MASSIMA** — MMCI framework risolve questo |
| **Privacy & Security** | Menzionate ma non affrontate | 🟡 Media — out of scope per la tesi |
| **Domains beyond Manufacturing** | Edge computing, network management inesplorati | 🟡 Media-Alta — La tesi esplora questo spazio |

---

## ✅ Aspetti Utili per la Tesi

### 1. Validazione Architetturale

Il tuo design a 4 agenti (Perception, Reasoning, Planning, Communication) rispecchia esattamente il pattern che il survey consolida come standard nei 22 paper. Nel Related Work puoi citare: _"Our agent taxonomy aligns with established MAS+DT patterns (Kalyani & Collier, 2024)"_.

### 2. Knowledge Graph è Letteralmente Standard

Kalyani et al. identificano **Ontologie e Knowledge Graphs** come componente chiave ricorrente in più paper. Questo ti dà citazione diretta per Neo4j; non è innovazione, è best practice già validata.

### 3. Gap Esplicito su Valutazione

Il paper ammette: _"Evaluation methodologies for trustworthiness and reliability of multi-agent systems in DT are not adequately addressed"_. La tesi dichiara esattamente questo come suo focus principale (MMCI + multi-agent agreement + KG validation).

### 4. LLM come Cognitive Layer è Genuinamente Nuovo

Nessuno dei 22 paper usa LLM agents. Tutti usano DRL o regole. Questo significa:
- ✅ La tesi è innovativa (primo a combinare LLM + MAS + DT in questo modo)
- ⚠️ Ma non hai letteratura per guidare le decisioni (perché Llama vs. Mistral? Perché 8B?)
- 🟠 Dipendi da letteratura su LLM agents (Berkeley MOOC, MultiAgentBench, WirelessAgent)

---

## ❌ Limitazioni per la Tesi

| Limitazione | Impatto |
|---|---|
| **Zero empirismo** | È una SLR, no esperimenti propri; non puoi estrarre metriche quantitative |
| **Nessun LLM** | Tutti i 22 paper usano DRL classico; Kalyani non può guidare scelte su modelli |
| **Dominio Manufacturing** | 45% dei paper è manufacturing; tua 5G è niche, difficulta il confronto diretto |
| **No 5G/Telecom** | Completamente assente dalla SLR; devi trovare altri punti di contatto |
| **Valutazione rimane aperta** | La SLR identifica il gap ma non lo risolve; la tesi deve farlo |

---

## 📝 Appunti per il Relatore

**D: "Avete verificato che il vostro design multi-agente è validato dalla letteratura?"**

R: "Sì — Kalyani & Collier (2024) analizzano 22 paper sui MAS+DT e identificano un pattern ricorrente di agent-per-funzione (manager, data, processing, recommendation). Il nostro design istanzia questo pattern con Perception, Reasoning, Planning, Communication agents, che sono una mappatura diretta delle feature riconosciute dalla SLR."

**D: "Il Knowledge Graph — perché Neo4j e non un'ontologia Semantic Web?"**

R: "Entrambi gli approcci (Semantic Web vs. property graphs) sono coperti da Kalyani et al. come best practice. Abbiamo scelto Neo4j per scalabilità in real-time (Cypher vs. SPARQL latency) e perché i vincoli 3GPP si representano più naturalmente come grafo di dipendenze (nodo=KPI, arco=causalità) che come assiomi OWL."

**D: "Quali sono i gap che state riempiendo rispetto alla SLR?"**

R: "Tre gap principali: (1) Kalyani et al. ammettono che AI/ML avanzata (in particolare LLM) è superficialmente integrata — nessuno dei 22 paper usa agenti LLM; (2) Valutazione della trustworthiness rimane aperta — la SLR non fornisce metodologia; (3) Dominio 5G/network manca completamente. La tesi affronta tutti e tre."

---

## 🔗 Concetti Introdotti / Collegati

- [[mas-agent-patterns]] — Architettura ricorrente nei 22 paper
- [[knowledge-graph-in-cdt]] — KG come standard di best practice
- [[multi-agent-frameworks]] — JADE, JaCaMo, SPADE overview
- [[sources/pretel-et-al-2024-mas-dt]] — SLR complementare (64 paper vs. 22)

---

## 📚 Paper Interni al Survey da Approfondire

| Autori | Titolo | Perché Leggere |
|---|---|---|
| **Zhang et al., 2021** | Adaptive DT + Multi-agent DRL for vehicular edge computing | Più vicino al tuo dominio: edge network, resource allocation, adaptive agents |
| **Xu et al., 2023** | DT-driven collaborative scheduling via MAS, edge computing | Quasi identico al tuo use case: resource scheduling su edge |
| **Latsou et al., 2023** | Automated anomaly detection + bottleneck ID con MAS | Pattern per il tuo Reasoning Agent; baseline rule-based |
| **Galuzin et al., 2022** | Knowledge-Based multi-agent adaptive management | KG + agents per decision-making real-time |

---

## Related Pages

- [[sources/restart-2024-ndt]] — 5G domain context
- [[sources/burr-et-al-2026-agentic-dt]] — Risk taxonomy and governance
- [[sources/pretel-et-al-2024-mas-dt]] — Companion SLR (64 papers, 7 DT properties analysis)
- [[concepts/knowledge-graph-in-cdt]] — KG as standard component
- [[glossary]] — Terminology
