# Valore per la Mia Tesi — RecursiveMAS

**Paper:** Yang et al. — "Recursive Multi-Agent Systems" (2026)  
**Tesi di riferimento:** Cognitive Digital Twin per 5G Radio Network — CDT con pipeline multi-agente LangGraph + LLM locali

---

## Aree in cui il paper approfondisce (rispetto alla mia tesi)

### 1. Architettura MAS e pattern di collaborazione
Il paper formalizza una tassonomia pulita di 4 pattern MAS (Sequential, Mixture, Distillation, Deliberation) con configurazioni agente esplicite. La mia pipeline è **Sequential Style** (Perception → Reasoning → Planning → Communication), esattamente il pattern "Chain-of-agents" del paper. Questo mi dà un vocabolario teorico per classificare la mia architettura in letteratura e citare un paper 2026 che lo valida.

### 2. Valutazione di sistemi MAS (rilevante per Contributo 2)
Il paper misura accuracy end-to-end del sistema su task specifici per dominio (math, code, medicine) — non valuta i singoli agenti intermedi. Interessante per contrasto: la *mia* valutazione deve essere più granulare (per-agent evaluation) perché il mio contributo scientifico è *come valuti* ogni anello della catena, non solo l'output finale. Il paper dimostra involontariamente il gap che colmo.

### 3. Scaling via ricorsione
Il paper mostra che aumentare i round di ricorsione migliora monotonicamente le performance (scaling law su training e inference). Nel mio sistema non faccio ricorsione esplicita, ma questo è un riferimento per discutere il concetto di "iterative refinement" nella cognitive loop (ogni tick del ciclo cognitivo CDT è già una forma di recursion applicativa, anche se non latente).

### 4. Costo training e parametri trainabili
Il cost analysis (Tabella 5: $4.27, 13.12M params, 15.29GB GPU) è utile come riferimento per la discussione sul deployment locale. Dimostra che ottimizzare solo i moduli di connessione (non i pesi LLM) è sufficiente per performance superiori — principio trasferibile alla mia architettura KG-based dove il "training" è nella struttura del grafo, non nei pesi.

---

## Pro (utilità per la tesi)

**✅ Vocabolario MAS aggiornato (2026):** Formalizza pattern MAS che uso senza nominarli. Posso citarlo in Ch. 3 (Related Work) per classificare la mia architettura nel panorama MAS 2026.

**✅ Benchmark numeri di riferimento:** Tabella 3 mostra performance di single agent (LoRA 83.1% MATH500), MoA (79.8%), TextGrad (84.9%) su benchmark standard. Utile per avere senso della scala delle performance in sistemi agentic comparabili.

**✅ Gradient stability proof:** Dimostrazione formale che text-based MAS training soffre di vanishing gradients in pipeline ricorsive. Rafforza teoricamente la scelta di LangGraph stateful (con memory layer) vs pipeline puramente testuale stateless. Citabile in Ch. 5 (Evaluation Methodology) per motivare perché la qualità del ciclo cognitivo non si misura solo dall'output finale.

**✅ Conferma indipendente dell'approccio locale:** Il paper usa modelli 1-10B (stesso range mio: Llama 3.1 8B, Qwen 3B, etc.) e dimostra che pipeline multi-agente con modelli piccoli e ottimizzazione sistemica batte singoli agenti grandi. Rafforza la mia ipotesi centrale sul valore dell'architettura CDT vs singolo LLM.

**✅ Cost comparison pulita:** $4.27 per training RecursiveMAS vs $9.67 Full-SFT. Posso usare questo come benchmark di confronto per giustificare approcci leggeri (es. prompt engineering + KG constraints vs fine-tuning) in Ch. 6.

---

## Contro (limiti di utilità per la tesi)

**❌ Non applicabile direttamente:** RecursiveMAS richiede accesso ai hidden states dei modelli. La mia architettura usa LangGraph con LLM via Ollama (API-based, nessun accesso ai pesi durante inference). Non posso implementare RecursiveLink nella mia tesi.

**❌ Comunicazione non interpretabile:** Il punto centrale di RecursiveMAS è comunicare in embedding space — latent thoughts non leggibili. La mia Communication Agent deve produrre output spiegabili per operatori 5G. Filosoficamente opposto al mio approccio.

**❌ Nessun Digital Twin Layer:** Il paper non ha nessun layer di persistent state, nessuna sincronizzazione con una controparte fisica. È un sistema di ragionamento puro, non un CDT. Il gap che la mia tesi colma non viene nemmeno sfiorato.

**❌ Nessuna valutazione per-agent:** Il paper misura solo accuracy dell'output finale. Non valuta la qualità di ogni agente nella pipeline — precisamente il gap metodologico che il mio Contributo 2 risolve.

**❌ Domain non telco:** I benchmark sono matematica, scienza, medicina, codice. Zero 5G, zero network management, zero KPI telco. Non è un baseline diretto comparabile.

---

## Appunti per il relatore — "Cosa ne pensi?"

Se il relatore chiede cosa penso di RecursiveMAS rispetto alla mia tesi, rispondo così:

> *"RecursiveMAS è un lavoro teoricamente elegante che risolve il problema della comunicazione latente tra agenti eterogenei, con proof formale di gradient stability e risultati empirici convincenti su 9 benchmark. È rilevante per la mia tesi come punto di confronto architetturale: dimostra che pipeline multi-agente con modelli 1-10B, ottimizzate a livello sistemico, superano approcci single-agent più grandi — confermando la direzione generale della mia ipotesi.*
>
> *Tuttavia, RecursiveMAS e il mio CDT operano su assi ortogonali. RecursiveMAS ottimizza la comunicazione tra agenti nel ragionamento su task chiusi (math, code). Il mio sistema affronta il problema del ciclo cognitivo in un sistema aperto con stato persistente (Eclipse Ditto), vincoli operativi verificabili (Neo4j), e un requisito di spiegabilità per operatori umani che è strutturalmente incompatibile con la comunicazione in latent space.*
>
> *Il limite più interessante di RecursiveMAS dalla prospettiva della mia tesi è l'assenza di valutazione per-agent: il paper non risponde alla domanda 'quale agente nella pipeline sta degradando la qualità?' — che è esattamente il vuoto metodologico che il mio Contributo 2 colma."*

---

## Collocazione consigliata nella tesi

| Capitolo | Uso |
|----------|-----|
| **Ch. 3 — Related Work** | Citare come esempio di MAS 2026 che valida Sequential pattern + modelli 1-10B per task complessi. Posizionare come lavoro complementare (different axis: latent communication vs explainable CDT). |
| **Ch. 5 — Evaluation** | Citare Tabella 3 come benchmark di riferimento per accuracy range su sistemi MAS multi-model. Usare l'assenza di per-agent evaluation come motivazione esplicita per il mio framework. |
| **Ch. 8 — Future Work** | Menzionare RecursiveLink come possibile evoluzione: se in futuro si abbandona il requisito di spiegabilità (es. regime fully-autonomous senza human-in-the-loop), un'architettura latente potrebbe essere un'estensione naturale per ridurre latency. |

---

## Classificazione finale

| Dimensione | Valutazione |
|-----------|-------------|
| Rilevanza diretta (implementazione) | ❌ Bassa — non implementabile nel mio stack |
| Rilevanza come citazione bibliografica | ✅ Alta — MAS 2026 con small models |
| Utilità per contrasto metodologico | ✅ Alta — rafforza il gap che colmo (per-agent eval) |
| Utilità per risposta al relatore | ✅ Alta — posizionamento chiaro e articolabile |
| Priorità di lettura | Media — non urgente, ma utile prima di Ch. 3 |
