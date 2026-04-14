---
title: MultiAgentBench — MARBLE Framework (2025)
type: source
created: 2026-04-14
updated: 2026-04-14
sources: [b.1_Multi Agent Bench/Valore per la mia tesi.md, b.1_Multi Agent Bench/riassunto.md]
tags: [multi-agent-systems, evaluation-framework, LLM-agents, coordination, benchmark, milestone-KPI]
---

# MultiAgentBench — Zhu et al. (2025)

Paper cruciale per **Contributo 2 (Framework di Valutazione)**. Introduce MARBLE (_Multi-agent cooRdination Backbone with LLM Engine_) — framework per misurare non solo task completion ma qualità di collaborazione/competizione tramite KPI basati su milestone. **Posizione nella tesi**: Cap. 5 (Metodologia Valutazione) — fornisce template metodologico per evaluation design.

---

## 🎯 Chi Sono

- **Autori:** Kunlun Zhu et al. — University of Illinois Urbana-Champaign
- **Pubblicato:** 3 Marzo 2025
- **Ref:** arXiv:2503.01935v1
- **Codice:** https://github.com/MultiagentBench/MARBLE

---

## 📋 Framework MARBLE

Architettura di coordinamento per sistemi multi-agente:

```
Task Info + Domain Database
    ↓
Coordination Engine
├── Agent Graph G=(A,E) [tipizzato per relazioni]
├── Cognitive Module (persona + Chain-of-Thought)
└── Memory System (shared/short/long-RAG)
    ↓
Environment + ToolBox
    ↓
Evaluator → Task Score + Coordination Score
```

---

## ✅ Aree Critiche per la Tua Tesi

### 1. **Milestone-Based KPI** (Direttamente Adattabile)

**Il problema:** Come misuri un sistema multi-agente quando l'output non è binario? Response time? Token count? Qualità della spiegazione?

**Loro:** Spezzano ogni task in milestone flessibili monitorate da un LLM evaluator in real-time.

**Applcazione tesi:** Ogni fault injection scenario ha milestones:
1. ✅ Anomalia percepita correttamente da Perception Agent
2. ✅ Root cause identificata dal Reasoning Agent con confidence > threshold
3. ✅ Azione correttiva proposta dal Planning Agent
4. ✅ Azione validata contro Neo4j KG vincoli
5. ✅ Report generato con spiegazione causale dal Communication Agent
6. ✅ KPI del simulatore migliorati post-azione

**Benefit:** Non è tutto-o-niente; ogni milestone raggiunto = progresso misurabile. Puoi assegnare score parziali e identificare dove la pipeline fallisce.

### 2. **Task Score vs Coordination Score** (Separazione Critica)

**Loro:** Due metriche indipendenti:
- **Task Score** — Qualità dell'output finale (accuratezza della diagnosi)
- **Coordination Score** — Qualità dell'interazione tra agenti (passaggio di contesto, consistenza)

**Per tesi:**
- **Task Score (Perception)** → Anomalia rilevata? (ground truth: metriche simulatore)
- **Task Score (Reasoning)** → Root cause corretta? (ground truth: sarebbe da LLM-as-judge)
- **Task Score (Planning)** → Azione feasible? (ground truth: KG validation)
- **Task Score (Communication)** → Spiegazione coerente? (ground truth: LLM-as-judge)
- **Coordination Score** → Pipeline coordinata senza perdita di contesto/token? (graph traversal score)

**Benefit:** Identifichi se il problema è in un agente specifico o nel coordinamento. Rende la diagnostica dell'architettura precisa.

### 3. **LLM-as-Judge per Output Non Strutturati**

**Loro:** Communication Score e Planning Score valutati da LLM evaluator su scala 1-5.

**Per tesi:** 
- **Communication Agent** → Report in linguaggio naturale valutato da Llama 3.1 70B (evaluator) su scala di coerenza causale + completezza
- **Reasoning Agent** → Spiegazione di root cause valutata da LLM evaluator su: plausibilità + alignment con vincoli 3GPP

**Benefit:** A quando manca ground truth esplicito, le metriche LLM-as-judge sono standardizzate e reproducibili. **PERO':** Il paper stesso ammette il rischio di autoreferenzialità (LLM valuta LLM) — la tua mitigazione è affiancare sempre ground truth dove possibile (simulatore, KG, multi-model agreement).

### 4. **Benchmark Comparativo Modelli** (Contributo 3)

**Loro:** Testano 5 modelli (Llama-3.1-8B, Llama-3.1-70B, Llama-3.3-70B, GPT-3.5, GPT-4o-mini) sugli stessi task con stesso protocollo.

**Per tesi:** 
- Stessa pipeline, modelli diversi (Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B)
- Scenari fissi (fault injection 5G)
- Ground truth dal simulatore

**Differenza chiave:** Loro testano modelli large; tu testast model small locali. Il tuo contributo è dimostrare che agenti su hardware consumer (3-8B quantizzati) possono raggiungere accuracy comparabile su dominio specializzato (5G fault diagnosis), senza cloud.

---

## 📊 Integrazione nello Scaffolding

### Cap. 5 (Metodologia Valutazione)
- Adotta milestone-based KPI framework
- Implementa separazione Task Score / Coordination Score
- Definisci LLM-as-judge come valutatore per output non strutturati
- Documenta ground truth sources (simulatore, KG, multi-agent agreement)

### Cap. 6 (Implementazione)
- Descrivi come MARBLE si istanzia in LangGraph StateGraph
- Spiega milestone per ogni agente
- Definisci score functions

### Cap. 7 (Risultati & Benchmark)
- Tabella: Task Score per modello × scenario
- Tabella: Coordination Score per pipeline configuration
- Grafici di convergenza Task Score vs Coordination Score

---

## ✅ Pro — Dove Ti Aiuta

| Aspetto | Utilità |
|---|---|
| **Evaluation Framework** | Milestone-based KPI + separazione TS/CS direttamente adattabile |
| **Benchmark Template** | Struttura sperimentale: stessa pipeline, modelli diversi, scenari fissi |
| **LLM-as-Judge** | Formalizzazione rigorosa per valutare output non strutturati |
| **Multi-Agent Dynamics** | Cattura non solo task quality ma coordinamento — le tue 4 agenti hanno dipendenze sequenziali |
| **Methodological Rigor** | Paper recente (Mar 2025) con peer review, giustifica scelte architetturali |

---

## ❌ Contro — Dove Non Ti Aiuta

| Aspetto | Limitazione |
|---|---|
| **Domain Specificity** | Le loro metriche sono per task generici; le tue devono essere 5G-specific |
| **Small Model Range** | Non testano Phi-3 3B, Qwen 3B — il tuo contributo è proprio qui |
| **Hardware** | Loro testano su cloud infrastructure; tu su M4 Pro consumer — latency profiles diversi |
| **Ground Truth** | Loro non hanno ground truth esterno (tutto LLM-based); tu hai simulatore + KG |
| **LLM-as-Judge Bias** | Loro usano LLM evaluator senza external ground truth — ammettono il rischio, non lo risolvono |

---

## 🎯 Risposta al Relatore

Se ti chiede: _"Come valuti un sistema di agenti LLM senza ground truth?"_

> _"Seguo l'approccio di MultiAgentBench (Zhu et al., 2025) adattato al mio dominio 5G. Divido il processo in milestone flessibili monitorate da LLM evaluator, ma affianco sempre dove possibile una ground truth esterna: il simulatore 3GPP per il Perception Agent (metriche osservate), il Neo4j KG per il Planning Agent (vincoli rispettati), e LLM-as-judge solo per il Reasoning e Communication Agent. Questo **triangolo di validazione** riduce l'autoreferenzialità che è l'incognita metodologica principale della letteratura su LLM agent evaluation. Per il benchmark comparativo, uso la loro struttura — stessa pipeline, modelli diversi, scenari fissi — ma su modelli small open-weight (3-8B quantizzati su M4 Pro) che nessuno ha testato sistematicamente nel dominio 5G."_

---

## 🔗 Concetti Correlati

- [[mmci-framework]] — Complementare: MMCI è livello più alto di maturità; MultiAgentBench è metrica tattica
- [[cognitive-digital-twin]] — 6 funzioni cognitive → 6 score functions strutturate
- [[biju-2024-langgraph]] — Biju descrive LangGraph; MultiAgentBench descrive come misurarlo
- [[lllm-as-judge]] — Formalizzazione rigorosa della tecnica

---

## Related Pages

[[sources/berkeley-cs294-llm-eval]] | [[sources/mmci-framework]] | [[sources/al-haj-ali-2025-mmci]]
