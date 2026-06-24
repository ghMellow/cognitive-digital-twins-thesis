# Riassunto — Recursive Multi-Agent Systems (RecursiveMAS)

**Paper:** Yang et al., arXiv:2604.25917v1 [cs.AI], 28 Apr 2026  
**Affiliazioni:** UIUC, Stanford, NVIDIA, MIT

---

## Idea Centrale

RecursiveMAS estende il paradigma dei Recursive Language Models (modelli che raffinano iterativamente il proprio stato latente) dal livello di singolo modello al livello di sistema multi-agente. Il sistema tratta l'intera pipeline di agenti eterogenei come un unico processo ricorsivo nello spazio latente, eliminando la comunicazione testuale intermedia tra agenti.

---

## Problema Affrontato

Nei sistemi multi-agente text-based:
- Ogni agente deve decodificare output testuali → re-encodare → passare al successivo → latenza alta
- Il training agente-per-agente non ottimizza il sistema come entità unificata
- I gradienti vaniscono durante backpropagation attraverso step testuali (vocabolario ≫ hidden dim)

---

## Soluzione: RecursiveLink

Un modulo leggero a 2 layer residuali che connette gli agenti in due modalità:

| Tipo | Funzione | Formula |
|------|----------|---------|
| **Inner** | Latent thoughts generation dentro ogni agente | `R_in(h) = h + W2·σ(W1·h)` |
| **Outer** | Trasferimento cross-agente tra modelli eterogenei | `R_out(h) = W3·h + W2·σ(W1·h)` |

Il loop ricorsivo: A1 → A2 → ... → AN → (torna ad A1). Solo l'ultimo round dell'ultimo agente produce output testuale.

---

## Training in 2 Fasi

1. **Inner loop** (parallelo, per ogni agente): regressione coseno per allineare latent thoughts alla distribuzione semantica dell'input embedding
2. **Outer loop** (sistema intero): cross-entropy sul testo finale, con backprop attraverso tutti i round di ricorsione → credit assignment globale per ogni outer link

Solo RecursiveLink viene aggiornato (13.12M parametri, 0.31% del totale). I pesi LLM rimangono frozen.

---

## Risultati Principali (9 benchmark, matematica/scienza/medicina/codice/ricerca)

| Round | Accuracy vs text-MAS | Speedup | Token ridotti |
|-------|---------------------|---------|---------------|
| r=1 | +3.4% | 1.2× | 34.6% |
| r=2 | +6.0% | 1.9× | 65.5% |
| r=3 | +7.2% | 2.4× | 75.6% |

**Costo training:** $4.27 (vs $6.64 LoRA, $9.67 Full-SFT) con accuracy più alta di entrambi.

---

## 4 Pattern di Collaborazione Testati

| Pattern | Agenti | Risultato chiave |
|---------|--------|-----------------|
| Sequential | Planner → Critic → Solver | Scaling law stabile con recursion depth |
| Mixture | Math/Code/Science + Summarizer | +6.2% vs miglior specialista |
| Distillation | Expert + Learner | +8% learner, 1.5× speedup vs expert |
| Deliberation | Reflector + Tool-Caller | +4.8% vs tool-caller standalone |

---

## Risultati Teorici

- **Runtime complexity**: RecursiveMAS O(N·m·d_h²) vs text-based O(N·m·|V|·d_h) — risparmio dove d_h ≪ |V|
- **Gradient Stability Theorem**: RecursiveLink mantiene gradienti ≈ costanti durante ricorsione; text-based soffre di vanishing gradients → vantaggio di apprendimento dimostrabile formalmente

---

## Limiti

- Richiede accesso ai hidden states → solo modelli locali (Hugging Face), incompatibile con API cloud
- Non testato su distribuzioni fuori dai benchmark standard
- Latent thoughts non interpretabili (la comunicazione avviene in embedding space)
- Overhead implementativo: gestione forward pass eterogeneo, tensori cross-modello, backprop multi-round

---

## Posizione nel Panorama

- **Prima proposta** di recursive scaling a livello di sistema (non solo single-model)
- Supera: Single Agent (LoRA/Full-SFT), MoA, TextGrad, LoopLM, Recursive-TextMAS
- Compatibile con qualsiasi topologia MAS (non tied a struttura sequenziale)
