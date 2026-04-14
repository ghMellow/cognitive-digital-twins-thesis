---
title: Agentic Digital Twin Risk Taxonomy
type: concept
created: 2026-04-14
updated: 2026-04-14
sources: [burr-et-al-2026-agentic-dt]
tags: [agentic-systems, governance, risk-framework, classification]
---

# Agentic Digital Twin Risk Taxonomy

Tassonomia di **27 configurazioni possibili** per Digital Twin agentivi, organizzate in 3 cluster temporali e 3 dimensioni di design.

## Il Framework: 3 Dimensioni × 3 Livelli

Ogni DT agentivo è classificato da una tripla `(Agency, Coupling, Evolution)`:

### Agency — Dove si decide

| Livello | Codice | Descrizione |
|---|---|---|
| **External** | `E` | Umani prendono tutte le decisioni; DT solo osserva |
| **Internal** | `I` | Agenti autonomi prendono decisioni senza intervento umano |
| **Distributed** | `D` | Agency emerge dall'interazione tra multipli agenti; nessuno controlla |

### Coupling — Quanto spesso si aggiornano

| Livello | Codice | Descrizione |
|---|---|---|
| **Loose** | `L` | Batch processing; ore o giorni tra aggiornamenti |
| **Tight** | `T` | Real-time; millisecondi tra osservazione e decisione |
| **Constitutive** | `C` | Il DT non solo osserva — co-definisce la realtà che misura |

### Evolution — Quanto cambia il modello

| Livello | Codice | Descrizione |
|---|---|---|
| **Static** | `S` | Parametri fissi; nessun apprendimento |
| **Adaptive** | `A` | Parametri si aggiornano in base ai dati; struttura invariata |
| **Reconstructive** | `R` | Il sistema ridefinisce le sue stesse categorie e ontologie |

---

## Le 9 Configurazioni Principali

```
(Agency:3 × Coupling:3 × Evolution:3 = 27 totali)
    ↓
Selezione: 9 configurazioni chiave ordinate per maturità
```

### Cluster 1 — The Present (Esiste Oggi, Deployato)

| # | Nome | Codice | Caratteristica | Esempio Reale | Risk Level |
|---|---|---|---|---|---|
| 1 | Computational Tool | `(E,L,S)` | Passivo, batch, fisso | Google Maps | 🟢 Basso |
| 2 | Adaptive Monitor | `(E,T,A)` | Real-time, but human commands, adapts params | Fabbrica con ML online | 🟡 Medio |
| 3 | **Active Steering** | `(I,T,A)` | **TESI** — Autonomo, real-time, adattivo | Manifattura con agenti | 🟠 Medio-Alto |

### Cluster 2 — The Threshold (Raggiungibile a Breve, Pressione verso)

| # | Nome | Codice | Caratteristica | Pericolo | Risk Level |
|---|---|---|---|---|---|
| 4 | Symbiotic | `(D,T,A)` | Agency emerge, nessuno comanda | Smart city incontrollata | 🔴 Alto |
| 5 | **Governor** | `(I,C,A)` | **MASSIMO RISCHIO** — Autonomo, continuo, ridefinisce metriche | Performative lock-in | 🔴🔴 Critico |
| 6 | Swarm | `(D,T,S)` | Fleet autonomo, comportamenti statici | Phantom traffic jams | 🔴 Alto |

### Cluster 3 — The Frontier (Principalmente Teorico)

| # | Nome | Codice | Caratteristica | Status |
|---|---|---|---|---|
| 7 | Worldbuilder | `(E,L,R)` | Ricostituisce ontologia, human-in-loop | Teorico |
| 8 | **Voyager** | `(I,T,R)` | Autonomo, ricostruisce categorie | Fantascienza |
| 9 | Reconstructive Assemblage | `(D,C,R)` | Multipli sistemi si ridefiniscono reciprocamente | Fantascienza |

---

## Dynamics di Transizione

I sistemi non rimangono in una configurazione statica. Il framework identifica **pressioni** che spingono l'evoluzione:

```
(E,L,S) --[efficiency↑ cost↓]--> (E,T,A) --[tight-coupling]--> (I,T,A) --> ... --> (D,C,R)
│                                                                      │
└──────────────────────────────────── Threshold (I,C,A) ─────────────┘
```

### Fattori Acceleratori (↑ spingono avanti)

- Competizione di mercato
- Pressioni di crisi (es. pandemia, emergenza di rete)
- Investimenti tecnici e capital disponibile
- Feedback positivi da successi precedenti

### Fattori Frenanti (↓ rallentano)

- Normativa e compliance
- Inerzia istituzionale
- Costi di integrazione
- Incertezza sulla sicurezza

### Soglie di No-Return (Irreversibili)

1. **Agency diventa Internal:** Una volta che gli agenti decidono autonomamente, gli umani non possono facilmente riprendere il controllo (infrastruttura, expertise, reputazione)
2. **Coupling diventa Constitutive:** Quando il DT ridefinisce la realtà che misura, il "reset" è impossibile (lock-in legale, sociale, cognitivo)
3. **Evolution diventa Reconstructive:** Una volta che il sistema ridefinisce le categorie stesse di misurazione, l'ontologia precedente non è più accessibile

---

## Perché (I,T,A) per la Tesi

La configurazione **Active Steering** (I,T,A) è il punto di equilibrio:

✅ **Vantaggi:**
- **Agency:** Autonomia reale senza far aspettare gli operatori
- **Tight Coupling:** Latenza sufficientemente bassa per 5G (millisecondi)
- **Adaptive:** Apprende dai pattern di anomalia

⚠️ **Ma rischia di driftare verso Governor (I,C,A):**

```
(I,T,A) ──[Se coupling diventa constitutive]──> (I,C,A) GOVERNORE
         ──[Se il sistema inizia a ridefinire   (BADè risk di
         ciò che "conta" come metrica]          lock-in performativo)
```

---

## Come Mantenere (I,T,A) Invece di Driftare a (I,C,A)

### Guardrail Architetturale: Knowledge Graph

Il Neo4j KG con vincoli 3GPP immutabili **mantiene il coupling a livello `T` (tight ma reale-time)**:

- **Non Constitutive:** Il KG **non ridefinisce** le metriche KPI; codifica vincoli fisici noti
- **Constraint Checking:** Ogni azione proposta dal Planning Agent va validata contro KG
- **Audit Trail:** Tutte le decisioni rifiutate sono logggate; nessuna metrica sparisce silenziosamente
- **External Reality Check:** Simulatore 3GPP fornisce ground truth che il Planning Agent non controlla

### Mitigazioni Ulteriori

1. **Fault Injection Controllata:** Perturbazioni esterne che il sistema non genera → se impara a "prevedere", è un segnale di performative stability
2. **Multi-Agent Agreement:** Più agenti LLM su stessa diagnosi → decreases likelihood di lock-in su correlazione spuria
3. **Transparent Decision Logging:** Ogni decisione è spiegabile; contromisura per hidden performative redefinition

---

## Mapping Della Tesi

| Elemento Tesi | Mapping Configurazione |
|---|---|
| **Agenti LLM (Perception, Reasoning, Planning, Communication)** | Agency = Internal (`I`) |
| **Eclipse Ditto WebSocket real-time sync** | Coupling = Tight (`T`) |
| **Reasoning Agent apprende pattern; KG si popola** | Evolution = Adaptive (`A`) |
| **Neo4j constraint validation** | Guardrail contro drift a (I,C,A) |
| **Fault injection simulator** | Reality check esterno |

---

## Configurazioni da Evitare

### Governor (I,C,A) — IL RISCHIO PRINCIPALE

```
Autonomo + Co-constitutive coupling + Adaptive
     ↓
DT non solo misura: RIDEFINISCE cosa conta come misurabile
```

**Sintomi:**
- Il sistema pensa: "SINR basso è impossibile, so che ho agito bene"
- Le metriche seguono magicamente quello che l'agente fa
- Nessun segnale di errore emergente (tutte le correlazioni sono "spiegate")
- Umani iniziano a dubitare dei dati fisici, credono al DT

**Esempi Reali:**
- **Singapore E-road Pricing:** Algoritmo che "aggiusta il prezzo per ottimizzare il flusso" ma il flusso è costantemente spostato per allinearlo al price
- **Algorithmic Management:** Manager robots che definiscono "produttività" come "conformità ai KPI che misurano" → lock-in su definizione artificiosa

**Come Evitare:**
- Immutabilità parziale del KG (vincoli 3GPP non ri-scrivibili)
- Reality checks esterni (fault injection)
- Transparency mandate (tutte le decisioni spiegate)

---

## Related Pages

- [[sources/burr-et-al-2026-agentic-dt]] — Paper completo
- [[performative-prediction]] — Rischio di lock-in performativo
- [[governor-configuration]] — Deep dive su (I,C,A)
- [[tight-coupling-risks]] — Rischi di tight coupling
- [[glossary]] — Terminologia
