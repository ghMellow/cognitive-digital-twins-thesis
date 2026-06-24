# RecursiveMAS — Analisi Divulgativa (Stile Simone Rizzo)

---

## 1. "Raga, guardate che hanno fatto"

Il trick è elegante: **trasformate ogni agente in uno strato di una RLM (Recursive Language Model)**. Invece di far parlare gli agenti in testo (genera token → decodifica → re-encoda → passa al prossimo agente — latenza enorme, gradienti che svaniscono), li colleghi direttamente via embeddings nascosti.

Il meccanismo chiave si chiama **RecursiveLink** — un modulo residuale a 2 layer che fa due cose:
- **Inner link** (`R_in`): dentro ogni agente, invece di proiettare `h_t` sul vocabolario per predire il prossimo token, lo riproietta nell'embedding space input e lo ri-inietta come `e_{t+1}`. L'agente "pensa" in latente senza mai decodificare.
- **Outer link** (`R_out`): prende i latent thoughts finali dell'agente `A_i` e li trasforma nell'embedding space di `A_{i+1}`, bridging modelli eterogenei (dimensioni diverse, famiglie diverse — Qwen, Llama, Gemma, tutto insieme).

Poi chiudi il loop: dopo l'ultimo agente, i suoi latent outputs tornano indietro al primo agente → ricorsione. Solo nell'**ultimo round** l'ultimo agente decodifica in testo.

Risultato: hai un sistema multi-agente che ottimizza in modo differenziabile end-to-end, con gradienti stabili (dimostrato formalmente), più veloce (eviti milioni di token intermedi), e migliore.

---

## 2. Perché è una figata

**Novità vera? Sì.** Prima di questo paper, il recursive scaling (LoopLM, Mixture-of-Recursions) esisteva *dentro* un singolo modello. Nessuno l'aveva portato a livello di *sistema* — più modelli eterogenei che si ricorsivano insieme.

Il **Gradient Stability Theorem (Theorem 4.1)** è la parte più solida: dimostra formalmente che il text-based training soffre di gradient vanishing durante la ricorsione (il gradiente della proiezione su vocabolario → 0 per token confident), mentre RecursiveLink mantiene gradienti O(1). Non è una claim empirica — è matematica.

**Numeri pratici su 9 benchmark:**
- +8.3% accuracy media vs text-based MAS
- 2.4× speedup a r=3
- 75.6% riduzione token a r=3
- Costo training: $4.27 vs $9.67 (Full-SFT) — meno della metà, con accuracy più alta

**Scalabilità**: funziona con Sequential, Mixture, Distillation, Deliberation — non è tied a una topologia specifica.

---

## 3. Come lo usiamo a lavoro?

**Ottimizzazione architetture esistenti:**
- Se hai una pipeline multi-agente text-based (tipo LangGraph con agenti che si passano JSON), puoi teoricamente sostituire il "passo messaggi" con un RecursiveLink → latenza -2.4×, token -75%.
- Però: richiede accesso ai last-layer hidden states dei modelli → **non funziona con API cloud** (OpenAI, Anthropic). Devi avere i modelli locali con accesso al forward pass completo.

**Riduce costi inference:** Enormemente, specialmente se hai pipeline con molti round. A r=3 usi il 25% dei token di una pipeline testuale equivalente.

**Cosa diventa possibile:**
- Multi-agent systems con modelli eterogenei piccoli (1-10B) che collaborano in latente → rivaleggia con singoli modelli grandi
- Training del sistema come entità unificata (non agente per agente) senza dover aggiornare tutti i pesi

---

## 4. Cosa c'è "sotto il cofano"

**Pipeline tecnica:**

```python
# Pseudo-implementazione RecursiveMAS

# Inner RecursiveLink (dentro ogni agente, step auto-regressivo)
def R_in(h, W1, W2):
    return h + W2(gelu(W1(h)))  # residual 2-layer MLP

# Outer RecursiveLink (tra agenti, bridging dimensioni diverse)
def R_out(h, W1, W2, W3):
    return W3(h) + W2(gelu(W1(h)))  # W3 allinea dim space

# Loop di ricorsione (n round, solo ultimo produce testo)
for round in range(n_rounds):
    latent = input_embedding
    for agent in agents:
        latent = agent.forward_latent(latent, R_in)  # latent thoughts generation
        latent = R_out(latent)  # cross-agent transfer
    # solo se round == n_rounds - 1: agent_N.decode(latent)
```

**Training in 2 fasi:**
1. **Inner loop** (parallelo per ogni agente): regression loss `L_in = 1 - cos(R_in(H), Emb(y))` — allinea latent thoughts alla distribuzione semantica degli input embeddings
2. **Outer loop** (sistema intero): cross-entropy `L_out = CE(S^(n)(x), y)` con backprop attraverso tutti i round di ricorsione → ogni outer link riceve un credit signal globale

**Componenti chiave da implementare:**
- Freezare tutti i parametri LLM (si aggiornano solo W1, W2, W3 dei RecursiveLinks — 13M params totali)
- AdamW lr=5e-4, cosine scheduler, batch=4
- Latent thoughts length m≈80 è il sweet spot (performance si stabilizza lì)

---

## 5. Il "Ma anche No" — Limiti e Red Flags

**Richiede accesso diretto ai hidden states** — incompatibile con qualsiasi API cloud. Serve Hugging Face + PyTorch + GPU locale. Non è "plug and play" su infrastruttura esistente.

**Non è production-ready in senso classico.** Il paper fa training su s1K + m1k + OpenCodeReasoning + ARPO-SFT — dataset curati. Non dimostrano come generalizza se la distribuzione del task è molto diversa.

**Complessità implementativa alta.** Devi gestire forward pass parziale di LLM eterogenei, passaggio di tensori between modelli con dimensioni diverse, e backprop attraverso N agenti × n round. Il debugging è un incubo.

**Benchmark di scaling**: i risultati migliori sono con modelli 5-10B (Sequential Scaled, Qwen3.5). Con modelli sub-2B (Sequential Light) i gain ci sono ma meno impressionanti. Con modelli piccoli il latent space è meno ricco.

**Nessun test su task reali production** — tutto su benchmark standardizzati (MATH500, GPQA-D, MedQA, LiveCodeBench). Quanto regge su task proprietari con distribuzioni anomale?

**Latent thoughts non interpretabili** — il sistema pensa in embedding, non in testo. Per applicazioni dove serve spiegabilità (tipo la tua, con Communication Agent), questo è un problema strutturale.
