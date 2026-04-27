
---

# 📄 Riassunto — "Agentic AI Architectures, Taxonomies & Evaluation"

**Tipo:** Survey paper — architettura & ingegneria dei sistemi agentici basati su LLM[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)  
**Focus:** Non "cosa fanno gli agenti", ma **come si costruiscono, si orchestrano e si valutano in produzione**[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)

---

## 🧱 Contributo Centrale

Il paper propone una **tassonomia unificata a 6 dimensioni** e formalizza l'agente come loop POMDP:[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)

A=(S,O,M,T,π)A = (S, O, M, T, \pi)A=(S,O,M,T,π)

Il ciclo ad ogni timestep ttt: **Percezione → Memory Update → Planning → Azione → Feedback**.[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)

Le 6 dimensioni della tassonomia sono:[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)

|Dimensione|Cosa copre|
|---|---|
|**Core Components**|Perception, Memory, Action, Profiling|
|**Cognitive Architecture**|Planning (ReAct → LATS → reasoning models), Reflection|
|**Learning**|In-context, fine-tuning, RLHF/RLAIF, skill libraries|
|**Multi-Agent Systems**|Topologie Chain/Star/Mesh, CAMEL/AutoGen/MetaGPT/LangGraph|
|**Environments**|Web, OS, Robotics, Enterprise, Healthcare, Finance|
|**Evaluation**|Framework **CLASSic**: Cost, Latency, Accuracy, Security, Stability|

---

## ⚙️ Architettura Unificata — Componenti Chiave

**Memory** — Dual-stream: context window (short-term) + VectorDB/SQL (long-term) con retention policy obbligatoria (forget / summarize / prune) per evitare context overflow. Sistemi chiave: MemGPT (paging), MemInsight (episodic → semantic compression), MemAgent (policy-learned retrieval).[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)

**Action Space** — Evoluzione in ordine di rischio/flessibilità crescente:[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)

- API calls (sicuro, rigido)
    
- Code-as-Action / CodeAct (flessibile, richiede sandbox)
    
- ACI / SWE-agent (IDE-friendly shell)
    
- Computer Use (mouse/keyboard/screenshot — generico ma pericoloso)
    
- VLA (robotica, motor control)
    

**Planning** — Trade-off token cost vs accuracy:[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)

|Metodo|Topologia|Token complexity|Pro|Contro|
|---|---|---|---|---|
|CoT|Lineare|Bassa|Veloce|No recovery|
|ReAct|Loop lineare|Media ×N|Grounded|Myopic, looping|
|Reflexion|Loop ciclico|Alta ×kN|Self-correction|Hallucinated critiques|
|Tree of Thoughts|Albero|Molto alta b^d|Backtracking|Latency esplosiva|
|LATS (MCTS)|Grafo/albero|Molto alta|Accuracy hard tasks|Dipende da evaluator|
|Reasoning models (o1/o3)|Albero implicito|Variabile B|Compute-quality tradeoff|Opaco, costoso|
|ReAcTree|Albero gerarchico|Media-alta|Long-horizon modulare|State sync complesso|

**Orchestration** — Il pattern vincente in produzione: **flow engineering** con LangGraph (state machine esplicita, checkpoints, guard nodes) invece di loop autonomi free-form. MCP standardizza tool discovery e governance (allowlist, audit logging).[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)

---

## 🤝 Multi-Agent Systems

Tre topologie principali:[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)

- **Chain/Waterfall** (MetaGPT, ChatDev) — SOP rigide, ottimo per software eng, ChatDev -30% bug vs single-agent
    
- **Star/Hub-and-spoke** (AutoGen, Swarm) — controller centrale con worker specializzati, supporta human-in-the-loop
    
- **Mesh/Swarm** (CAMEL, GenerativeAgents) — decentralizzato, ottimo per simulazioni sociali e ideazione
    

Pattern chiave: **MAKER** con cross-examination (Worker + Verifier separati) riduce error accumulation su million-step chains. **DyLAN** usa importance scoring per silenziare agenti non rilevanti → riduzione costi.[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)

---

## 🌍 Environments & Benchmark di Riferimento

|Dominio|Benchmark|Top result|
|---|---|---|
|Web|WebArena, Mind2Web|~15% long-horizon|
|OS/Desktop|OSWorld Verified|CoAct1: 60.76%|
|Software Eng.|SWE-Bench Verified/Pro|Repository-scale|
|General assistant|GAIA|Multi-step tool use gap|
|Async planning|Robotouille|47% sync → 11% async|

---

## 🛡️ Evaluation Framework — CLASSic

**C**ost — token complexity esponenziale per architetture gerarchiche[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)  
**L**atency — agenti async crollano all'11% di success rate in ambienti con delay variabili[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)  
**A**ccuracy — success rate medio spesso sotto 15% su long-horizon tasks[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)  
**S**ecurity — prompt injection irrisolta, "adaptive attackers bypass static guards"[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)  
**S**tability — variance run-to-run non riportata nella maggior parte dei benchmark; necessario failure severity distribution, non solo mean success[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)

---

## 🚩 Limiti & Open Challenges

- **Hallucination-in-Action** — in chat è testo sbagliato, in un agente è un file cancellato[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)
    
- **Infinite loops** — mancanza di moduli metacognitivi per capire quando fermarsi[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)
    
- **Costo computazionale** — ToT/LATS richiedono call LLM multiple per ogni query[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)
    
- **Sicurezza** — PromptArmor riduce il rischio, ma non è sufficiente contro attacchi adattativi[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)
    
- **Latency in real-time** — robot e autonomous driving richiedono <100ms, incompatibile con reasoning pesante senza distillation[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)
    
- **Open-ended learning** — agenti ancora statici post-deploy; Voyager è l'eccezione, non la regola[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)
    

---

## 💡 Takeaway per l'Ingegnere

> _"La domanda centrale si è spostata da 'come promptare un modello' a 'come programmare e controllare un sistema agente completo'"_[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)

La ricetta pratica consigliata dal paper: **LLM per reasoning locale + graph controller (LangGraph) per orchestrazione + MCP per tool governance + retention policy esplicita per la memoria** = sistema debuggabile e sicuro per la produzione.[Agentic-AI-Architectures-Taxonomies-Evaluation.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/146803486/ef8a0d38-5202-481d-9349-6d3df0e7b5bd/Agentic-AI-Architectures-Taxonomies-Evaluation.pdf)