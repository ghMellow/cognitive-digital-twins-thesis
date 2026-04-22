---
title: Cognitive Digital Twin (CDT)
type: concept
created: 2026-04-14
updated: 2026-04-14
sources: [zheng-et-al-2022-cdt]
tags: [definition, architecture, cognitive]
---

# Cognitive Digital Twin (CDT)

Central concept of the thesis. A digital twin augmented with cognitive capabilities for autonomous reasoning and decision-making.

## Canonical Definition

**Zheng et al. (2022):** "Una rappresentazione digitale aumentata con capacità cognitive, semanticamente interconnessa, che evolve lungo il lifecycle dell'entità fisica."

---

## Five Fundamental Characteristics (Zheng et al., 2022)

1. **Cognitive Capability** — Capacità di percezione, ragionamento, memoria e apprendimento
2. **Full Lifecycle Management** — Gestione completa dal design alla dismissione dell'asset
3. **Autonomy** — Capacità di prendere decisioni senza intervento umano (con supervisione)
4. **Continuous Evolving** — Il CDT si adatta e migliora nel tempo
5. **DT-based Design** — Il ciclo di design è informato dal digital twin, feedback loop chiuso

---

## Six Cognitive Functions

Mapping funzioni CDT → architettura tesi:

| Funzione | Descrizione | Realizzazione Tesi |
|---|---|---|
| **Percezione** | Acquisizione e normalizzazione dati da sistema fisico | Perception Agent → Eclipse Ditto |
| **Ragionamento** | Inference su anomalie, correlazioni, cause radice | Reasoning Agent → LLM locale |
| **Memoria** | Storage a lungo termine di knowledge e storia episodica | Neo4j KG + Ditto history |
| **Apprendimento** | Evoluzione della knowledge base nel tempo | Benchmark comparativo LLM (MVP) |
| **Adattamento** | Evoluzione continua dei parametri di decision-making | Planning Agent + feedback loop |
| **Decision-Making** | Selezione azione ottimale | Planning Agent + KG constraints |

---

## CDT vs DT Tradizionale

| Aspetto | Digital Twin | Cognitive Digital Twin |
|---|---|---|
| **Stato** | Riflette passivamente lo stato fisico | Riflette + interpreta + prevede + pianifica |
| **Reasoning** | Nessuno (o rule-based statico) | Autonomo, context-aware, adattivo |
| **Memoria** | Registrazione eventi | Knowledge graph + learning loop |
| **Azione** | Nessuna (observer pattern) | Decision-making autonomo con feedback |
| **Evoluzione** | Statico nel tempo | Evoluzione continua del comportamento |

---

## Architettura CDT a 3 Layer (Tesi)

```
Layer 3 — Cognitive (LangGraph + LLM agents)
                ↕ (WebSocket, state polling)
Layer 2 — Digital Twin (Eclipse Ditto)
                ↕ (REST API, simulatore)
Layer 1 — Fisico Simulato (Python 3GPP simulator)
```

Ogni layer ha responsabilità distinta ma interconnessa:
- **Layer 1** — Emula il comportamento del sistema fisico, genera metriche
- **Layer 2** — Sincronizza lo stato tra fisico e cognitivo
- **Layer 3** — Raccoglie informazioni, ragiona, pianifica azioni e le comunica

---

## CDT come Veicolo per il Contributo Scientifico della Tesi

Il sistema CDT descritto è il **veicolo implementativo**. Il vero contributo scientifico della tesi non è il CDT stesso (già studiato in letteratura) ma:
1. La metodologia di valutazione degli agenti cognitivi quando ground truth è assente
2. Il benchmark comparativo di modelli LLM locali su task 5G-specifici
3. La dimostrazione di eseguibilità su hardware consumer

---

## Related Pages

- [[sources/zheng-et-al-2022-cdt]] — Fonte principale
- [[sources/cogtwin-ijcai-25]] — Implementazione teorica
- [[glossary]] — Termini correlati
- [[scaffolding-tesi]] — Integrazione nella tesi
