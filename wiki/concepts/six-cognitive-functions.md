---
title: Six Cognitive Functions
type: concept
created: 2026-04-14
updated: 2026-04-14
sources: [zheng-et-al-2022-cdt]
tags: [architecture, functions, cognitive-capabilities]
---

# Six Cognitive Functions

Formalized by Zheng et al. (2022) as the core capabilities of a Cognitive Digital Twin. Each function maps to one or more specialized agents in the thesis.

## 1. Percezione | Perception

**Definizione:** Acquisizione, normalizzazione e strutturazione dei dati osservati dal sistema fisico.

**Nella tesi:**
- **Agente:** Perception Agent
- **Fonte dati:** Eclipse Ditto (Things e Features del gNB simulato)
- **Compiti:** Query Ditto, normalizzazione metriche 3GPP (RSRP, SINR, throughput, latenza, tasso handover), rilevamento di anomalie ovvie (threshold superati)
- **Output:** Struttura standardizzata dello "stato percepito" da passare agli altri agenti

**Metriche di valutazione:**
- Accuracy vs. ground truth (simulatore Python)
- Latency di acquisizione
- Completeness (nessuna metrica persa)

---

## 2. Ragionamento | Reasoning

**Definizione:** Inference su anomalie, correlazioni causali, diagnosi di problemi.

**Nella tesi:**
- **Agente:** Reasoning Agent
- **Metodo:** LLM locale (Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B) + prompt engineering
- **Compiti:** Correlare KPI, identificare pattern anomali, proporre cause radice in linguaggio naturale
- **Output:** Diagnosi strutturata con gradi di confidenza

**Sfida:** Non esiste ground truth ovvio per il reasoning (è il gap critico della tesi).  
**Soluzione proposta:** LLM-as-judge + multi-agent agreement + KG-based validation

**Metriche di valutazione:**
- LLM-as-judge (confronto con modelli più grandi)
- Multi-model agreement (consensus tra Llama/Mistral/Phi-3/Qwen)
- KG-based validation (diagnosi rispetta vincoli Neo4j?)
- Confidence calibration (i gradi di sicurezza sono accurati?)

---

## 3. Memoria | Memory

**Definizione:** Storage a lungo termine di conoscenza strutturata (knowledge) e episodica (storico degli stati e azioni).

**Nella tesi:**
- **Knowledge Graph:** Neo4j con vincoli operativi 3GPP (statico, offline)
  - Schema: nodi (KPI, anomalie, azioni), archi (relazioni causali, vincoli operativi)
  - Ruolo: guardrail di validazione per Planning Agent
- **Episodic History:** Eclipse Ditto history + log applicativo
  - Registrazione cronologica di stati osservati e azioni eseguite
  - Consultabile per pattern matching su scenari storici

**Proprietà:**
- Separazione dura tra KG statico (schema + regole permanenti) e storia dinamica (streaming di osservazioni)
- Entrambi accessibili agli agenti tramite query standardizzate

---

## 4. Apprendimento | Learning

**Definizione:** Evoluzione della knowledge base nel tempo sulla base di nuova esperienza.

**Nella tesi:**
- **Stato MVP:** Benchmark comparativo di come diversi LLM imparano da fault injection scenario
- **Stato Futuro:** Fine-tuning domain-specific su task 5G, aggiornamento incrementale KG

**Metriche di valutazione:**
- Task accuracy su scenari visti vs. unseen
- Convergence speed
- Retention rate (non dimentica scenari passati)

---

## 5. Adattamento | Adaptation

**Definizione:** Evoluzione continua dei parametri di decision-making mentre il CDT opera e il sistema fisico cambia.

**Nella tesi:**
- **Realizzazione:** Planning Agent aggiorna lo schema delle azioni disponibili sulla base del feedback
  - Se un'azione ha successo ripetutamente, viene preferita
  - Se fallisce, vincoli vengono aggiunti al KG
- **Ciclo:** Act → Observe → Update KG → repeat

**Proprietà:**
- Adattamento è _local_ al singolo CDT (no distributed learning)
- Necessita di meccanismi di stabilità (prevent divergence)

---

## 6. Decision-Making | Autonomous Decision-Making

**Definizione:** Selezione autonoma dell'azione ottimale sulla base di diagnosi e vincoli.

**Nella tesi:**
- **Agente:** Planning Agent
- **Input:** Diagnosi del Reasoning Agent
- **Processo:** Generazione azioni candidate → validazione contro KG constraints → selezione best
- **Output:** Piano d'azione eseguibile o escalation all'operatore

**Proprietà:**
- Verificabilità: ogni azione deve poter essere giustificata (audit trail)
- Fattibilità: solo azioni osservabili nel simulatore (nessuna azione fantasma)

---

## Mapping tesi → Sei Funzioni

| Funzione | Agente | LLM? | Ground Truth? | Metrica |
|---|---|---|---|---|
| Percezione | Perception | No (rule-based) | ✅ Simulatore | Accuracy, recall, latency |
| Ragionamento | Reasoning | ✅ | ❌ Assente | LLM-as-judge, agreement, calibration |
| Memoria | KG + Ditto | No | N/A | Query accuracy, schema validity |
| Apprendimento | Benchmark | ✅ | ⚠️ Parziale | Task accuracy, convergence |
| Adattamento | Planning | ✅ | ⚠️ Parziale | Stability, recovery time |
| Decision-Making | Planning | ✅ | ✅ KG constraints | Feasibility, latency, audit trail |

---

## Tensioni Aperte

1. **Reasoning senza ground truth** — Fondamento dell'intero contributo metodologico della tesi
2. **Learning vs. Stability** — Come evitare che il sistema diverga durante l'adattamento?
3. **Real-time constraints** — Tutte le funzioni devono girarsi in millisecond (5G timing critical)

---

## Related Pages

- [[cognitive-digital-twin]] — Concetto parent
- [[sources/zheng-et-al-2022-cdt]] — Fonte
- [[glossary]] — Termini correlati
- [[scaffolding-tesi]] — Sezione Cap. 5 — Metodologia di Valutazione
