---
title: Glossario della Tesi
type: concept
created: 2026-04-14
updated: 2026-04-14
sources: []
tags: [terminology, reference]
---

# Glossario — Cognitive Digital Twins

Nomenclatura canonica e definizioni stabilite dalla tesi.

---

## Core Concepts

### Digital Twin (DT)
Rappresentazione digitale sincronizzata di un'entità o processo fisico, in grado di memorizzare stato, cronologia e abilitare simulazioni.

### Cognitive Digital Twin (CDT)
Digital Twin aumentato con capacità cognitive (percezione, ragionamento, memoria, apprendimento) che opera autonomamente e evolve lungo il lifecycle dell'entità. Riferimento canonico: **Zheng et al. (2022)**.

### Knowledge Graph (KG)
Struttura semantica (grafo di nodi e archi etichettati) che rappresenta fatti, relazioni e vincoli operativi di un dominio. Nel contesto della tesi: rappresentazione dei vincoli 5G e delle rule di validazione sul Planning Agent.

### Multi-Agent System (MAS)
Insieme di agenti autonomi specializzati coordinati per raggiungere un obiettivo comune tramite comunicazione strutturata.

### LLM (Large Language Model)
Modello neurale addestrato su corpus di testo, esposto come API o ospitato localmente (Ollama + quantizzazione).

---

## Funzioni Cognitive (sei pilastri CDT)

Seguono la tassonomia di **Zheng et al. (2022)** e **Al-Haj Ali et al. (2025)**.

### Percezione (Perception Agent)
Acquisizione, normalizzazione e strutturazione dei dati di osservazione dal sistema fisico. Output: metriche 3GPP canoniche.

### Ragionamento (Reasoning Agent)
Inference su anomalie, correlazioni, cause radice. Utilizza logica naturale + KG. Output: diagnosi strutturata con gradi di confidenza.

### Pianificazione (Planning Agent)
Traduzione di diagnosi in azioni concrete, validazione contro vincoli operativi memo nel KG, selezione dell'azione ottimale.

### Comunicazione (Communication Agent)
Sintesi della pipeline percezione-decisione in esplicazione leggibile all'utente con argumentazione causale.

### Memoria
Persistenza dello stato e della cronologia tramite Eclipse Ditto + Neo4j.

### Apprendimento / Adattamento
Evoluzione continua del KG e dei parametri di decision-making (out of scope per MVP, definito come future work).

---

## Terminologia Dominio 5G

### gNB (gNodeB)
Antenna base 5G. Nel simulatore: generatore di metriche 3GPP.

### RSRP (Reference Signal Received Power)
Potenza del segnale di riferimento ricevuto. Metrica di qualità del segnale.

### SINR (Signal-to-Interference-plus-Noise Ratio)
Rapporto segnale-interferenza-rumore. Indicatore di congestione e degradazione di canale.

### Handover
Transizione di una comunicazione da una cella a un'altra. Tasso di fallimento è indicatore di instabilità.

### Throughput Downlink/Uplink
Velocità di trasferimento dati. Degradazione indica anomalie di risorse o congestione.

### Latenza
Ritardo end-to-end. Metrica critica per servizi real-time (eMBB, URLLC).

### KPI (Key Performance Indicator)
Metrica aggregata di performance. Nel contesto tesi: composite su RSRP, SINR, throughput, latenza.

---

## Terminologia Architetturale

### Eclipse Ditto
Piattaforma per gestione del digital twin: sincronizzazione stato, WebSocket notifications, API REST. Nel contesto: backbone della représentation digitale (livello 2/3 dell'architettura).

### Neo4j
Database grafo per Knowledge Graph. Nel contesto: memorizzazione vincoli operativi 5G e rule di validazione Planning.

### LangGraph
Framework per orchestrazione di agenti multi-step con state management esplicito (LangChain + Langgraph). Nel contesto: runtime della pipeline cognitive.

### Supervisor Agent (LangGraph)
Agente di coordinamento che instrada task in ingresso agli agenti specializzati. Implementa routing, state management, decision tree. Nel contexto: orchestratore centrale della pipeline cognitiva.

### StateGraph (LangGraph)
Struttura dati che rappresenta il grafo di stato della pipeline multi-agente. Ogni nodo è un agente/tool, ogni arco è une transizione condizionata.

### DKR (Dynamic Knowledge Repository)
Knowledge graph statico offline che memorizza vincoli operativi stabili (schema 3GPP, regole di safety). Nel contexto: Neo4j con ontologia 5G. Contrasto con DIKG.

### DIKG (Dynamic Instance Knowledge Graph)
Knowledge graph dinamico aggiornato real-time con lo stato istantaneo del sistema fisico. Nel contexto: Eclipse Ditto replica dello stato gNB. Contrasto con DKR.

### Decision Sandbox
Paradigma di validazione pre-esecuzione: il DT non è uno specchio passivo ma un **ambiente di test** dove valutare l'azione proposta prima di eseguirla sul sistema reale. Nel contexto: Planning Agent verifica azioni contro KG.

### Ollama
Server locale di LLM with quantizzazione Q4/Q5. Nel contesto: hosting di Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B su M4 Pro.

### 3GPP
Standard di telecomunicazione. Nel contesto: specifica del formato di metriche simulate.

---

## Metodologia Valutazione

### LLM-as-Judge
Utilizzo di un LLM come valutatore di qualità di output di un altro LLM. Nel contesto della tesi: Llama 3.1 70B valuta coerenza causale di diagnosi del Reasoning Agent su scala 1-5 (rubric-based). Mitigation: multiple judges, reference examples, confidence calibration.

### Multi-Model Agreement
Strategia di validazione tramite consensus tra multipli LLM su task identici. Se Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B convergono sulla stessa diagnosi di root cause, la probabilità di correctness → alta. Dissenso = bassa confidenza. Nel contesto: triangolazione senza ground truth esterno.

### Outcome Validity
Metrica definitiva: l'intervento proposto dall'agente ha risolto il problema reale nel sistema? Nel contesto tesi: KPI del simulatore sono recuperati oltre soglia target post-azione? Pass/Fail binario. Questa è la metrica regina dell'intera valutazione.

### Task Verificabili vs Non-Verificabili
**Verificabili (Ground Truth Esplicita):** Ditto API calls, KG constraint violations, JSON schema validation — answer è binarie.  
**Non-Verificabili (LLM-as-Judge Necessario):** Root cause diagnosis, spiegazione causale — answer è qualitativa, richiede valutazione.  
Nel contesto: massimizza task verificabili con ground truth esterno, usa LLM-as-judge solo dove necessario.

### Milestone-Based KPI
Decomposizione di ogni task in milestone flessibili monitorate in real-time. Nel contesto tesi: ogni fault injection scenario ha 6 milestones (anomalia percepta → root cause → diagnosis confidence → azione proposta → KG validation → improvement). Score parziale per ogni milestone, non tutto-o-niente.

### Task Score (TS)
Qualità dell'output finale di un agente. Nel contesto: Accuracy della diagnosi Reasoning Agent, feasibility dell'azione Planning Agent, coerenza Communication Agent. Valutato vs ground truth (simulatore) o LLM-as-judge.

### Coordination Score (CS)
Qualità dell'interazione tra agenti. Nel contesto: Pipeline Perception→Reasoning→Planning→Communication passaggio di stato senza perdita di contesto? Token efficiency? Graph traversal correctness? Separate from Task Score — puoi avere alta TS ma bassa CS (agente giusto, coordinamento sbagliato).

### Outcome Validity Metrica
Pass → KPI recuperati > target soglia; Fail → KPI stagnanti o peggiorati. Valutato post-azione dal Planning Agent sul simulatore 3GPP. È la ground truth assoluta della valutazione.

---

## Varianti Terminologiche Segnalate

- **"Gemello Digitale Cognitivo"** vs **"Cognitive Digital Twin"** — usare CDT come acronimo canonico in testo inglese, traslatare in italiano solo quando necessario.
- **"Agente"** vs **"Agent"** — preferenza italiana "agente" in corpo tesi, "agent" in code comments e paper.
- **"Knowledge Graph"** vs **"Knowledge Base"** — usare KG per strutture orientate a grafi (Neo4j), KB per vocabolari piatti. Nel contesto tesi: KG.

---

## Related Pages
- [[overview]]
- [[scaffolding-tesi]]
