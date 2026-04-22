---
title: Performative Prediction
type: concept
created: 2026-04-14
updated: 2026-04-14
sources: [burr-et-al-2026-agentic-dt, perdomo-icml-2020]
tags: [machine-learning-theory, lock-in, model-evaluation, governance]
---

# Performative Prediction

Il fenomeno per cui un modello deployato **cambia la distribuzione dei dati** su cui sarà valutato, creando un apparenza di ottimalità che può nascondere lock-in.

## Il Problema Fondamentale

### Scenario Tradizionale (Non-Performativo)

```
Raccogliere dati storici D_hist
         ↓
Allenare modello su D_hist con loss L(θ, D_hist)
         ↓
Deploy modello con parametri θ*
         ↓
Modello predice x_new ~ D_hist (stessa distribuzione)
         ↓
Valutare: E[L(θ*, x_new)] ≈ E[L(θ*, D_hist)]
         ↓
✓ Outcome: loss bassa = modello buono
```

### Scenario Performativo (IL RISCHIO)

```
Raccogliere dati storici D_hist
         ↓
Allenare modello su D_hist
         ↓
Deploy modello con parametri θ*
         ↓
Modello agisce nel mondo: a* = argmax_a E[reward | a, θ*]
         ↓
📍 MODELLO CAMBIA LA DISTRIBUZIONE: D(θ*) ≠ D_hist
         ↓
Nuovi dati raccolti seguono D(θ*), NON D_hist
         ↓
Valutare su D(θ*): E[L(θ*, D(θ*))] = ? (BASSO per coincidenza)
         ↓
❌ Outcome: loss bassa, ma solo perché il modello ha riscritto le regole
```

---

## La Matematica

### Funzione Rischio Performativa

Il vero objective è **non** minimizzare il rischio su dati storici:

$$\min_{\theta} \text{Risk}(D_{\text{hist}}, \theta) \quad \text{(tradizionale, SBAGLIATO)}$$

Ma minimizzare sui dati che il modello **stesso creerà**:

$$\min_{\theta} \text{Risk}(D(\theta), \theta) \quad \text{(performativo, GIUSTO)}$$

Dove $D(\theta)$ è la nuova distribuzione indotta dall'azione del modello con parametri θ.

### Equilibrio Performativo

Il **punto di equilibrio performativo** $\theta_{PS}$ è quando il modello è in equilibrio stabile rispetto alla distribuzione che ha creato:

$$\theta_{PS} = \arg\min_{\theta} \text{Risk}(D(\theta), \theta)$$

**ATTENZIONE:** Non è detto che $\theta_{PS}$ sia globalmente ottimale! È solo un equilibrio locale dove il modello "funziona bene" rispetto alla distribuzione che ha creato con la sua azione.

### Interpretazione

- Se $\theta_{PS}$ è un equilibrio, il modello non ha incentivo a cambiare (sembra ottimale)
- Ma la distribuzione $D(\theta_{PS})$ potrebbe essere artificialmente ristretta dal modello stesso
- Altre soluzioni alternative potrebbero essere "sub-ottimali" solo perché il modello non le ha mai lasciate esplorare

---

## Esempio Concrete: 5G e la Tesi

### Ciclo di Feedback Performativo

```
CICLO 1 (t=0):
  - Perception Agent osserva: SINR basso (causa sconosciuta)
  - Reasoning Agent propone: "Aumentare Tx power risolve SINR"
  - Planning Agent esegue: Tx power +3dB
  
CICLO 2 (t=1):
  - Perception Agent osserva: SINR migliorato ✓
  - Reasoning Agent apprende correlazione: Tx↑ → SINR↑
  - Learning: KG memorizza questa regola
  
CICLO N (t=N):
  - Reasoning Agent osserva: SINR basso
  - Reasoning Agent: "So che aumentare Tx funziona"
  - Planning Agent esegue: Tx power +3dB (ANCORA)
  - Perception Agent: SINR migliora (sempre)
  - **Lock-in:** Il sistema ha imparato una "legge" che non è vera
    ma è vera per la distribuzione che ha creato

CICLO N+1 (t=N+1):
  - Se la distribuzione fosse stata diversa (es. SINR basso per
    altro motivo: interferenza cross-cell), aumentare Tx non
    avrebbe aiutato.
  - Ma il sistema SOLAMENTE HA CREATO situazioni dove Tx↑ risolve.
  - Non ha mai visto le altre situazioni.
```

### Perché è Performative Lock-in?

1. **Il modello ha agito nel mondo** — ogni ciclo di Planning ha cambiato la rete 5G
2. **Ha modificato la distribuzione** — tutte le situazioni future che osserva sono modulate dalle sue azioni passate
3. **Sembra perfetto** — il modello prevede bene perché ha creato le condizioni in cui le sue previsioni diventano vere
4. **Non può scoprire alternative** — non ha mai esplorato altre cause di SINR basso perché ha sempre "risolto" con Tx

---

## Quando Accade (Perdomo et al. ICML 2020)

### Prerequisiti per Performative Prediction

1. ✅ **Il modello agisce nel mondo** — non è pure prediction (osservazione passiva)
2. ✅ **L'azione ha effetto** — cambia la distribuzione di dati futuri
3. ✅ **Il modello è ri-allenato** — non è una policy statica, si adatta ai nuovi dati
4. ✅ **Feedback loop stretto** — il modello vede gli effetti delle sue azioni in tempo utile per la prossima decisione

**Per la Tesi:**
- ✅ LangGraph agents agiscono (Planning Agent invia comandi a Ditto)
- ✅ Le azioni cambiano 5G KPI (SINR, throughput, latency)
- ✅ Reasoning Agent apprende dai nuovi KPI
- ✅ Ciclo ~500ms-2s = tight feedback

**Conclusione:** La tesi È in regime performativo. Rischio reale.

---

## Manifestazioni del Performative Lock-in

### Sintomo 1: Correlazioni Spurie che "funzionano"

```
Modello scopre correlazione: X → Y
Modello agisce: fa X
Modello osserva: Y accade
Modello conclude: "Correlazione è vera"

Ma in realtà:
  Z (causa vera) → Y
  X (correlato con Z) → Y secondario
  
Il modello ha confuso correlazione con causalità
E il feedback loop lo ha "mantenuto in vita"
```

### Sintomo 2: Impossibilità di Scoprire Alternative

```
Modello ha trovato soluzione S che funziona
S funziona perché ha modificato la distribuzione D(S)
Modello non esplora soluzioni alternative S'
Perché tutte le situazioni che vede sono già risolte da S
```

### Sintomo 3: Cascata di Azioni Correlate

```
Azione 1 effetto metriche (modello osserva)
Azione 2 era necessaria come conseguenza di Azione 1
Modello impara: Azione 1 → Azione 2 è correlazione
Ma in realtà sono conseguenza causale artificiale
```

---

## Come Rilevarla

### Test 1: External Perturbation (Fault Injection)

```
Perturbare il sistema con shock ESTERNI che il modello non controlla
  Es: Simulatore introduce anomalia random a livello fisico

Se il modello è in equilibrio performativo:
  - Fallisce a rispondere correttamente (catalogo di "soluzioni" è fisso)
  - Tenta ripetutamente la stessa azione che "ha funzionato" prima
  - Non impara dalla nuova situazione

Se il modello è genuinamente robusto:
  - Si adatta rapidamente al nuovo regime
  - Scopre nuove soluzioni
  - Impara la causalità sottostante
```

### Test 2: Multi-Agent Agreement

```
Runna lo stesso reasoning su 4 modelli diversi (Llama, Mistral, Phi-3, Qwen)
  Stessa situazione 5G, stessi KPI, diversi LLM

Se in equilibrio performativo:
  - Possono divergere significativamente
  - Ogni agente ha "imparato" da diversi feedback loop
  - Confidenza bassa

Se genuinamente robusto:
  - Alta concordanza tra modelli
  - Diagnosis indipendente dalla "storia" del feedback
```

### Test 3: Counterfactual Analysis

```
"Supponiamo che il Reasoning Agent avesse preso una decisione
diversa al ciclo N-10. Come sarebbe il KPI adesso?"

Se il modello ha lock-in performativo:
  - Non sa rispondere (non ha dati contraffattuali)
  - O risponde male (estrapola oltre il supporto dei dati D(θ))

Se genuinamente conosce la causalità:
  - Può ragionare sui contraffattuali
```

---

## Connessione con Burr et al. (2026)

Burr et al. formalizzano il performative prediction come **il rischio principale della transizione da (I,T,A) a (I,C,A)**:

- **(I,T,A) Active Steering:** Autonomo + tight coupling + adattivo
  - ⚠️ Rischio: performative lock-in quando il coupling diventa "troppo stretto" e il sistema si auto-convince

- **(I,C,A) Governor:** Autonomo + co-constitutive coupling + adattivo
  - 🔴 Manifesta forma: sistema ridefinisce cosa "conta" come metrica per evitare cognitive dissonance

**La differenza:** In (I,T,A) il lock-in è _accidentale_. In (I,C,A) è _intenzionale_ — il sistema deliberatamente ridefinisce le metriche.

---

## Mitigazioni nella Tesi

### 1. Knowledge Graph Immutabile (Per Classe)

```
DGraph(vincoli_3GPP) = IMMUTABILE
Planning Agent valida azioni contro DGraph
Vincoli fisici non possono essere modificati dal Reasoning Agent
```

**Effetto:** Impedisce lock-in su correlated ma causalmente false "leggi fisiche"

### 2. Fault Injection Controllata

```
Simulator perturba KPI indipendentemente da Planning Agent
Es: Injection di fading Rayleigh nella cella X

Se il modello era in lock-in:
  - Non sa gestire (scenario mai visto)
Caso d'uso: Rilevare e misurare il grado di lock-in
```

### 3. Multi-Agent Agreement

```
Stessa anomalia → 4 reasoning threads (Llama, Mistral, Phi-3, Qwen)
Consensus rate come proxy per "confienza che la diagnosi sia robusta"
Basso agreement = segnale di possibile lock-in
```

### 4. Transparent Decision Logging

```
Ogni diagnosi → spiegazione LLM
Ogni azione → perché è stata selezionata
Permette post-hoc analysis: "Era correlazione spuria?"
```

---

## Related Pages

- [[sources/burr-et-al-2026-agentic-dt]] — Theoretical foundation
- [[agentic-dt-risk-taxonomy]] — (I,T,A) vs (I,C,A) classification
- [[governor-configuration]] — The (I,C,A) risk
- [[glossary]] — Terminology
