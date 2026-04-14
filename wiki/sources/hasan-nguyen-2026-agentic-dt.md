---
title: Hasan & Nguyen — Integrating Agentic AI and Digital Twins (2026)
type: source
created: 2026-04-14
updated: 2026-04-14
sources: [a.7_Integrating agentic AI and DT/Valore per la mia tesi.md, a.7_Integrating agentic AI and DT/riassunto.md]
tags: [digital-twins, agentic-AI, 6-layer-architecture, closed-loop, decision-sandbox]
---

# Hasan & Nguyen (2026) — Integrating Agentic AI and DT

Paper di related work **stato dell'arte (febbraio 2026)** che valida la direzione di ricerca: chiudere il loop tra agenti LLM e Digital Twin. Fornisce framework architetturale con 6-layer che mappeano quasi perfettamente i tuoi 4 agenti + componenti. **Position nei capitoli della tesi**: Related Work + Blueprint architetturale.

---

## 🏗️ 6-Layer Architecture

Il paper formalizza un modello a 6 strati che valida la tua decomposizione:

| Layer del Paper | Tuo Componente | Mapping |
|---|---|---|
| **Multimodal Perception Layer** | Perception Agent (LangGraph) | Interroga Ditto, normalizza metriche 3GPP |
| **Knowledge & Data Layer** | Eclipse Ditto + Neo4j KG | State repo + constraint repository |
| **Reasoning & Learning Layer (LLM)** | Reasoning Agent | Root cause analysis su anomalie |
| **Decision-Making Layer (LLM)** | Planning Agent | Verifica KG, propone azioni |
| **Action & Execution Layer** | Output verso network simulator | Esecuzione azioni correttive |
| **Feedback & Adaptation Layer** | Loop di ricalibrazione | Multi-agent consensus + learning |

---

## 💡 Concetto Chiave: DT come Decision Sandbox

Il paper formalizza che il DT **non è uno specchio passivo** ma un **ambiente di validazione pre-esecuzione**.

Nel tuo caso:
- **Sanbox = Neo4j KG**: prima di proporre un'azione (es. riallocazione slice), il Planning Agent verifica la fattibilità contro i vincoli
- **Benefit**: evita azioni che violerebbero 3GPP standard o causerebbero SLA violation
- **Citazione**: usa questo paper per motivare **perché hai separato il layer di validazione dal layer di reasoning** — è pattern architetturale riconosciuto

---

## ✅ Pro — Dove Ti Aiuta

| Aspetto | Utilità |
|---|---|
| **Related Work** | Citazione diretta per stato dell'arte recente su CDT + Agentic AI |
| **Blueprint architetturale** | 6-layer mapping allineato 1:1 con la tua decomposizione |
| **Validazione del paradigma** | Confirm multi-agente + DT in contesti cyber-fisici real-time |
| **Gap identification** | Paper USA KG ma non formalizza vincoli — tuo Neo4j è differenziante |
| **Peer review** | Pubblicato su Elsevier Array feb 2026 — la tua tesi è costruita su letteratura peer-reviewed |

---

## ❌ Contro — Dove Non Ti Aiuta

| Aspetto | Limitazione |
|---|---|
| **Evaluation Methodology** | **ZERO** — il contributo principale della tua tesi (come valuti agenti LLM non-deterministici?) non è trattato. Paper assume semplicemente che il sistema funzioni |
| **Knowledge Graph** | Usa LP (Linear Programming) + RFR (Random Forest Regression), nessuna struttura semantica per vincoli operativi |
| **Benchmark Multi-Modello** | Nessun confronto tra LLM diversi — il tuo Contributo 3 (Llama vs Mistral vs Phi-3 vs Qwen) non ha precedente qui |
| **Dominio** | Grid energetico ≠ rete 5G. Metriche, vincoli, tempi di reazione, standard (ENTSO-E vs 3GPP) sono mondi separati |
| **Local Deployment** | Nulla su LLM su hardware consumer — tu hai questo come constraint reale |

---

## 📝 Positioning nella Tua Tesi

### Cap. 3 (Related Work)
Citazione diretta come la fonte più recente che valida il closed-loop cognitivo-fisico.

### Cap. 4 (Architettura)
Usa il 6-layer framework per strutturare la descrizione della tua architettura. Mostra che la decomposizione non è arbitraria, è pattern consolidato in letteratura peer-reviewed 2026.

### Cap. 8 (Discussion)
**Posiziona il tuo contributo differenziante** sulle tre dimensioni:
1. **Knowledge Graph Neo4j** — loro non hanno (loro usano LP/RFR)
2. **Evaluation Methodology** — loro non hanno, tu sì (MMCI + LLM-as-judge + multi-agent union)
3. **Dominio 5G + LLM locali** — loro non hanno, tu sì

---

## 🎯 Risposta al Relatore

Se ti chiede: _"Conosci questo paper e cosa ne pensi rispetto alla tua tesi?"_

> _"Il paper di Hasan & Nguyen (2026) è il riferimento architetturale più diretto: formalizza il closed-loop cognitivo-fisico tra agenti LLM e Digital Twin, validando il pattern che sto adottando. La loro decomposizione in sei layer mi ha aiutato a giustificare la separazione tra Perception Agent, Reasoning Agent e Planning Agent come scelte architetturali motivate, non arbitrarie."_

**Dove ti differenzi:**

> _"Rispetto a quel paper, il mio lavoro si differenzia su tre punti concreti: primo, introduco un Knowledge Graph Neo4j come layer semantico di validazione dei vincoli — qualcosa che nel paper è assente; secondo, affronto esplicitamente il problema della valutazione degli agenti LLM, che loro ignorano completamente assumendo che il sistema funzioni; terzo, opero in dominio 5G su hardware consumer con LLM locali, il che aggiunge un contributo di riproducibilità che la loro architettura non considera."_

---

## 📊 Gap da Colmare

**Gap Metodologico Rilevante:**
> _"Il paper valuta il sistema solo tramite convergence time su scenari sintetici, senza mai affrontare come validare la **qualità del reasoning LLM**. Nel mio caso, questo è esattamente il problema centrale — e costruire una metodologia rigorosa per rispondere a quella domanda è il contributo scientifico principale della mia tesi."_

---

## 🔗 Concetti Correlati

- [[cognitive-digital-twin]] — CDT definition
- [[six-cognitive-functions]] — 6 funzioni (da Zheng)
- [[knowledge-graph-in-cdt]] — Dual-KG pattern
- [[agentic-dt-risk-taxonomy]] — Governance CDT
- [[intent-based-networking]] — IBN come specifico use case

---

## Related Pages

[[sources/cogtwin-ijcai-25]] | [[sources/biju-2024-langgraph]] | [[sources/restart-2024-ndt]]
