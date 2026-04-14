---
title: Berkeley CS294 — LLM Agent Evaluations (2026)
type: source
created: 2026-04-14
updated: 2026-04-14
sources: [b.2_Video Berkeley (Agentic AI MOOC) - LLM Agent Evaluations & Project Overview/Valore per la mia tesi.md, b.2_Video Berkeley (Agentic AI MOOC) - LLM Agent Evaluations & Project Overview/riassunto.md]
tags: [LLM-evaluation, agent-arcgitectures, outcome-validity, multi-model-agreement, evaluating-agents]
---

# Berkeley CS294 — LLM Agent Evaluations & Project Overview (2026)

Video MOOC **metodologico** su valutazione di agenti LLM. Informa direttamente il **Contributo 2 (Framework di Valutazione)** della tesi. Fornisce il linguaggio tecnico per: outcome validity, tool-use evaluation, multi-model agreement, LLM-as-judge practices. **Posizione nella tesi**: Cap. 5 (Metodologia) — best practices e anti-patterns nella valutazione agentiche.

---

## 📺 Chi Sono

- **Istituzione:** UC Berkeley, CS294 Advanced Topics
- **Tema:** Metodologia per valutare sistemi di agenti basati su LLM
- **Formato:** Lecture video + case studies
- **YT:** https://www.youtube.com/watch?v=VfOA2a0dj4w
- **Data:** 2026 (parte della Agentic AI curriculum UC Berkeley)

---

## 🔑 Concetti Chiave Estratti

### 1. **Outcome Validity** (La Metrica Vera)

**Il problema:** Un agente genera una spiegazione bellissima, ma l'azione che propone non risolve il problema reale.

**Definizione:** Outcome validity = "L'intervento proposto dall'agente ha risolto il problema nel sistema reale?"

**Per tesi:**
- **False Positive:** Reasoning Agent dichiara diagnosi corretta, ma quando Planning Agent applica l'azione, KPI del simulatore non migliorano
- **Ground Truth:** KPI simulatore = outcome validity definitiva
- **Metrica:** Pass → KPI recuperati oltre soglia target; Fail → KPI stagnanti o peggiorati

**Benefit:** Questa è la tua metrica regina — trasforma "il sistema parla bene" in "il sistema risolve il problema".

### 2. **Task Verificabili vs Non-Verificabili**

**Verificabili (Ground Truth Esplicita):**
- Perception Agent chiama Ditto API per lo stato gNB → Risposta è presente nel DB Ditto? (binario)
- Planning Agent propone azione riconfigurabile → Violazione vincoli KG? (binario)
- Communication Agent genera JSON strutturato → Valida schema? (binario)

**Non-Verificabili (LLM-as-Judge Necessario):**
- Reasoning Agent inferisce "root cause = congestione nella banda low RSRP" → È corretta questa spiegazione? (non-binario, richiede valutazione)

**Per tesi:** Massimizza task verificabili con ground truth esterno (simulatore, KG), usa LLM-as-judge solo dove necessario (Reasoning, Communication).

### 3. **Capacità Specifiche vs Verticali**

**Specifiche:** Può l'agente usare uno specifico tool? (es. può interrogare Ditto API?)  
**Verticali:** Quanto è bravo su un vertical specifico? (es. diagnosi su calo RSRP in dominio 5G)

**Per tesi:**
- **Capacità:** Tool-use (Ditto calls, KG queries, LLM inference chains)
- **Verticali:** 5G fault types (congestione, handover failure, power degradation, latency spike)

**Evaluation Design:** 
- Testa capacità singolarmente (ogni agente isolato)
- Testa su scenari verticali (fault injection controllata per ogni KPI)
- Combina: competenza su verticale + coordinamento tra agenti

### 4. **Multi-Model Agreement** (Quando Manca Ground Truth)

**Strategia:** Se LLM A, LLM B, LLM C concordano sulla stessa diagnosi di root cause, la probabilità di correctness aumenta. Dissenso = bassa confidenza.

**Per tesi:**
- Esecuzione identica su Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B
- Reasoning Agent in ogni modello produce diagnosi
- Stringa diagnosi → embedding + cosine similarity tra diagnosi
- Agreement% = overlap negli embedding
- Soglia: Se agreement > 80%, eleva confidence del Reasoning Agent a "high"; altrimenti, flag per revisione / multi-agent vote

**Benefit:** Migliora robustezza senza dipendere un'unico vendor di LLM.

### 5. **LLM-as-Judge Practices** (Metodologia)

**Setup:**
- Task da valutare: output del Reasoning Agent (diagnosi)
- Judge: Llama 3.1 70B (modello più grande, locale o via API)
- Scala: 1-5 (incoherent → highly sensible)
- Rubric: "La diagnosi spiega causalmente l'anomalia osservata? È consistente con vincoli 3GPP?"

**Mitigazioni ai rischi:**
1. **Diverse judges:** Usa 2-3 modelli diversi, calcola media
2. **Blind evaluation:** Judge non vede nome dell'agente che ha generato
3. **Reference outputs:** Includi nella prompt alcuni riferimenti di diagnosi "correct" dal domain expert (1-2 esempi)
4. **Confidence calibration:** Chiedi al judge di auto-stimare la sua confidenza ("confident", "somewhat uncertain")

**Per tesi:**
- Judge = Llama 3.1 70B se available via Ollama quantized; altrimenti 8B ma con rubric più rigido
- Rubric dovrebbe includere: coerenza causale, alignment 3GPP constraints, completezza della spiegazione
- Documentare confidence scores per analisi later

---

## 📋 Integrazione nello Scaffolding

### Cap. 5 (Metodologia Valutazione)

**Section 5.1 — Defining Evaluation Dimensions**
- Outcome validity (KPI improvement in simulator)
- Task completeness (milestone-based)
- Reasoning quality (LLM-as-judge rubric)
- Coordination quality (multi-agent agreement score)

**Section 5.2 — Ground Truth Strategy**
- Where available (simulatore for Perception, KG for Planning): deterministic validation
- Where unavailable (Reasoning, Communication): LLM-as-judge with multi-model agreement mitigation

**Section 5.3 — Evaluation Protocols**
- Capacità-level: Each agent isolated on simple tasks
- Verticale-level: End-to-end pipeline on fault injection scenarios
- Combination: Benchmark comparativo modelli su same scenario set

### Cap. 6 (Esperimenti)

**Table:** Outcome Validity by Model × Fault Type  
**Table:** Task Score (milestone completeness) by Agent  
**Table:** Multi-Model Agreement % (Llama/Mistral/Phi-3/Qwen consensus on diagnosis)  
**Figure:** Confidence calibration curve (Judge confidence vs actual agreement with external ground truth)

---

## ✅ Aree di Forza

| Aspetto | Utilità |
|---|---|
| **Outcome Validity Framework** | Metrica definitiva: "L'azione ha davvero risolto il problema?" |
| **Task Classification** | Distinguere verificabili (deterministic) vs non-verificabili (LLM-based) |
| **Multi-Model Agreement** | Triangolazione senza ground truth esterno |
| **LLM-as-Judge Best Practices** | Rubrics, confidence calibration, mitigation patterns |
| **Capacity vs Vertical** | Separare debug architetturale da debug domeniale |
| **Metodologia Trasparente** | Consente al relatore di replicare l'evaluation |

---

## ❌ Limitazioni e Loro Mitigazioni

| Limitazione | Mitigation in Tesi |
|---|---|
| Non copre real-time latency constraints | Aggiungi metrica di "Decision Latency" (ms) per ogni agents |
| Esempi su dominio informatico (WebArena, SWE-bench) | Crea tuo benchmark 5G-specific con fault injection |
| LLM-as-Judge può avere bias sistematici | Usa multiple judges, includi reference examples nel prompt, confidence calibration |
| Non coprire hardware consumer constraints | Misura token throughput, memory peak, power draw su M4 Pro |

---

## 🎯 Risposta al Relatore

Se chiede: _"Come garantisci che la valutazione non è circolare (LLM valuta LLM)?"_

> _"Seguendo le migliori pratiche dalla letteratura recente (Berkeley CS294, 2026), applico un approccio a tre strati: primo, dove ho ground truth esterno (simulatore 3GPP, vincoli Neo4j), lo uso — è deterministic e reproducibile. Secondo, per il Reasoning Agent dove manca ground truth, uso multi-model agreement tra 4 modelli locali open-weight: se Llama, Mistral, Phi-3, Qwen convergono sulla stessa diagnosi, la confidenza sale. Terzo, affianco un LLM evaluator (Llama 70B) ma con rubric trasporente, reference examples, e multiple judges che votano. È ancora una triangolazione parziale su LLM, ma è il meglio che la letteratura agentiche oggi offre per task senza ground truth esplicito. La outcome validity finale è sempre validata sul simulatore: se l'azione riporta i KPI alla normalità, il Reasoning Agent ha indovinato."_

---

## 🔗 Concetti Correlati

- [[mmci-framework]] — MMCI è framework di maturità; Berkeley fornisce metriche tattiche
- [[multiagent-bench-2025]] — Complementare: MultiAgentBench è specifico per coordinamento; Berkeley è più generale
- [[cognitive-digital-twin]] — 6 funzioni cognitive → 6 evaluation dimensions strutturate
- [[lllm-as-judge]] — Implementazione rigorosa della tecnica

---

## Key Takeaway

Il video trasforma la tua tesi da "Ho costruito un CDT che funziona" a **"Ho sviluppato una metodologia rigorosa per valutare l'affidabilità del ragionamento cognitivo su infrastruttura simulata 5G"**. Questo è ciò che la rende scientificamente solida e pubblicabile.

---

## Related Pages

[[sources/multiagent-bench-2025]] | [[sources/al-haj-ali-2025-mmci]] | [[sources/mmci-framework]]
