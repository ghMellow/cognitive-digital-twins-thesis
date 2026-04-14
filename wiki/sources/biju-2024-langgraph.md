---
title: Biju (2024) — Implementing MAS via LangGraph
type: source
created: 2026-04-14
updated: 2026-04-14
sources: [b.4_Implementing MAS via LangGraph/Valore per la mia tesi.md, b.4_Implementing MAS via LangGraph/riassunto.md]
tags: [LangGraph, MAS, multi-agent-systems, supervisor-pattern, state-management]
---

# Biju (2024) — Implementing MAS via LangGraph

Paper applicativo che valida il **pattern Supervisor + Agenti Specializzati** su LangGraph — esattamente la topologia che usi nel tuo livello cognitivo. Utilità: giustificazione architetturale di LangGraph + baseline di benchmark comparativo. **Posizione nella tesi**: Background + confronto implementativo.

---

## 🎯 Supervisor Pattern

Biju usa il pattern che tu implementi:

```
Supervisor Agent (LangGraph)
    ├── Perception Agent (tool: query Ditto)
    ├── Reasoning Agent (tool: LLM inference)
    ├── Planning Agent (tool: KG constraint check)
    └── Communication Agent (tool: action output)
```

Il flow è: Supervisor riceve task in input → instrada a agente specializzato → agente usa tool proposito → risposta finale.

**Tua versione è più sofisticata**:
- Aggiungi **verifica KG-based** nel Planning Agent (Biju non ha)
- Integri **feedback loop** con anomaly detection (Biju non ha)
- Usi **LLM locali** vs GPT-4o hard-coded (Biju no)

---

## 📊 Baseline Comparativo

Il paper riporta numeri che puoi usare come reference:

| Metrica | Valore Biju | Note per la Tua Tesi |
|---|---|---|
| **Task Completion Accuracy** | 92–98% | Tuo benchmark dovrebbe essere >= di questo |
| **Latenza per Task** | 2–4s | Tuo ciclo cognitivo 5G deve essere <= 1s per dominare |
| **Task Complexity** | FAQ, database queries | Tuoi task (fault diagnosis) sono più complessi |
| **Modelli Usati** | GPT-4o hard-coded | Tua comparison Llama/Mistral/Phi-3/Qwen multi-model |

**Posizionamento nei risultati**: "Su task di complessità simile a Biju (2024), il nostro sistema raggiunge X% accuracy con Y ms latenza media, usando modelli open-source quantizzati che Biju non considera."

---

## ✅ Pro — Cosa Prendi

| Aspetto | Utilità |
|---|---|
| **Architettura validata** | Supervisor + agenti specializzati = pattern maturo |
| **Stack identico** | `StateGraph`, `langchain` — stesso framework, tu lo estendi |
| **Baseline numerico** | Ti dà metriche di confronto (92-98% accuracy, 2-4s) |
| **Example applicativo** | Mostra che LangGraph funziona su task reali eterogenei |
| **Tool pattern** | Supervisor instradata a tool specializzati — exact mapping con il tuo KG check predictor |

---

## ❌ Contro — Dove Non Ti Aiuta

| Aspetto | Limitazione |
|---|---|
| **Evaluation Methodology** | **ZERO** rigor metodologico per valutare reasoning LLM. Biju assume ground truth ovvio (FAQ: risposta giusta/sbagliata); tu non hai questo lusso per root cause inference |
| **LLM Locali** | Hard-coded su GPT-4o; il tuo scenario open-source/on-premise (quantized Llama 3.1 8B) è completamente diverso |
| **Knowledge Graph** | Biju non ama KG; usa database query diretto. Tu aggiungi KG come layer di vincoli — loro non lo hanno |
| **State Management Avanzato** | Nulla su memory episodica, session persistence, long-term learning — i tuoi problemi aperti |
| **Dominio** | Task generici (FAQ); non tocca CAse d'uso specializzati (telecom, IIoT, etc.) |
| **Ablation Study** | Nessuno — non sai quale agente contribuisce quanto al risultato finale |

---

## 🔴 Red Flag da Evitare

**NON citare Biju come base teorica per CDT**
- Non tratta Digital Twins, non sa nulla di 3GPP, nessuna letteratura cognitiva
- È reference applicativa, non teorica

**NON fidarti del codice come pseudocode**
- Le snippet `StateGraph` nel paper sono teaser — leggi documentazione ufficiale LangGraph per implementazione reale

**NON usarlo come benchmark diretto**
- Task troppo diversi (FAQ vs fault diagnosis) per confronto significativo
- Risultati non sono direttamente comparabili

---

## 📝 Positioning nella Tua Tesi

### Cap. 4 (Architettura)
Cita il supervisor pattern di Biju come **giustificazione della topologia LangGraph** che hai scelto. Mostra che la decomposizione non è inventata, è pattern riconosciuto.

### Cap. 6 (Implementazione)
Usa il baseline numerico di Biju (92-98% accuracy, 2-4s latenza) come **punto di comparazione** per i tuoi risultati su task 5G specializzati.

### Cap. 8 (Discussion)
**Posiziona il tuo contributo oltre Biju**:
1. Metodologia di valutazione rigorosa (LLM-as-judge + multi-agent agreement) — loro non hanno
2. Integration con Knowledge Graph come layer di vincoli — loro non hanno
3. LLM locali open-source invece di GPT-4o — contributo di reproducibility

---

## 🎯 Risposta al Relatore

Se ti chiede: _"Conosci Biju? Cosa ne pensi?"_

> _"Il paper di Biju (2024) è un utile reference applicativo per il pattern Supervisor+Agenti specializzati su LangGraph, che è la stessa topologia che adotto nel mio livello cognitivo. Tuttavia ha due limitazioni rilevanti: primo, valuta solo agenti con ground truth esplicito (FAQ, database), mentre il mio Reasoning Agent deve inferire root cause da anomalie radio 5G senza ground truth — qui mi serve LLM-as-judge o multi-agent consensus; secondo non gestisce knowledge graph come layer di vincoli — il mio Planning Agent verifica ogni azione correttiva contro Neo4j prima di eseguirla, che è contribution assente nella letteratura applicativa che ho trovato. Biju mi è utile per la sezione Background, ma il mio contributo scientifico si posiziona un livello sopra."_

---

## 📚 Concetti Correlati

- [[cognitive-digital-twin]] — CDT architecture
- [[six-cognitive-functions]] — Agent decomposition rationale
- [[knowledge-graph-in-cdt]] — KG constraint validation (non in Biju)
- [[mmci-framework]] — Evaluation metodology (Biju non ha)
- [[agentic-dt-risk-taxonomy]] — Safety guardrails

---

## 🔍 Alternative da Considerare (Future Comparison)

Per rendere l'analisi ancora più rigorosa, potresti confrontare con:
- **AutoGen** — agent framework Microsoft
- **CrewAI** — higher-level MAS framework
- **JADE** — mature classical MAS platform

Ma **LangGraph è la scelta corretta** per il tuo caso (local, control graph visibility, state management).

---

## Related Pages

[[sources/hasan-nguyen-2026-agentic-dt]] | [[sources/cogtwin-ijcai-25]] | [[sources/kalyani-collier-2024-mas-dt]]
