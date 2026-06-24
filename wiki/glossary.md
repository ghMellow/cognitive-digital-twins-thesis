---
title: Thesis Glossary
type: concept
created: 2026-04-14
updated: 2026-04-20
sources: [2026-03-31-seconda-call.md, 2026-04-15-terza-call.md]
tags: [terminology, reference, semantics, formal-logic, ontologies]
---

# Glossary — Cognitive Digital Twins

Canonical nomenclature and definitions established by the thesis.

---

## Core Concepts

### Digital Twin (DT)
Synchronized digital representation of a physical entity or process, capable of storing state, history, and enabling simulations.

### Cognitive Digital Twin (CDT)
Digital Twin augmented with cognitive capabilities (perception, reasoning, memory, learning) that operates autonomously and evolves throughout the entity's lifecycle. Canonical reference: **Zheng et al. (2022)**.

### Knowledge Graph (KG)
Semantic structure (graph of nodes and labeled edges) that represents facts, relationships, and operational constraints of a domain. In thesis context: representation of 5G constraints and validation rules for the Planning Agent.

### Multi-Agent System (MAS)
Collection of specialized autonomous agents coordinated to achieve a common objective through structured communication.

### LLM (Large Language Model)
Neural model trained on text corpus, exposed as API or hosted locally (Ollama + quantization).

---

## Formal Knowledge Representation & Semantic Ontologies

Foundation of explicit, machine-readable knowledge formalization. Distinguishes **explicit semantics** (ontologies, rules, graphs) from **implicit semantics** (embedded in LLM embeddings). Cross-referenced with Contribution 2 of the thesis: the bridge between symbolic reasoning and neural approaches.

### Core Knowledge Representation Concepts

#### Ontology
Formal structure composed of concepts linked through rules. Enables explicit, machine-readable representation of domain knowledge. In CDT context: formalizes system knowledge and enables automated inference. Enables reusability and interoperability across cognitive modules.

#### Semantics
Formal meaning attributed to data and relationships. Can be **explicit** (formalized in ontologies, KGs, logical rules) or **implicit** (embedded in LLM weights without declaration). Mario Beltrani distinguishes these as two alternative epistemological approaches to knowledge representation, foundational to Contribution 2.

#### Knowledge Representation and Reasoning (KRR)
Scientific area studying how to represent knowledge formally and how to reason over it. Theoretical foundation of ontologies, KGs, and cognitive architectures. Referenced in the doctoral thesis as one of the enabling technologies for cognition in CDTs.

### Logical Foundations

#### First-Order Logic (FOL)
Formal system for expressing propositions about objects and their relationships via quantifiers (∀, ∃) and predicates. Provides the logical foundation for OWL and most formal ontologies. Referenced by Mario Beltrani as explicit formal reference for his work.

#### Descriptive Logic (DL)
Family of formal languages for representing terminological knowledge. Balances expressivity with decidability of reasoning. Theoretical foundation of OWL and automated reasoners. Enables tractable inference while maintaining semantic rigor.

#### Inference
Process of deriving new knowledge from existing knowledge by following logical rules. In CDT: enables the system to reason about situations not explicitly coded. Executed by reasoners over ontologies and KGs.

### Semantic Standards & Technologies

#### RDF — Resource Description Framework
W3C standard model for representing information as subject-predicate-object triples. Base data structure for knowledge graphs and OWL ontologies. Enables semantic web interoperability.

#### OWL — Web Ontology Language
W3C standard language for defining ontologies. Based on Descriptive Logic (DL) subset of FOL. Defines classes, properties, constraints, and enables automated reasoning via reasoners (e.g., HermiT, Pellet). Allows both human-readable and machine-processable knowledge.

#### SPARQL
Query language for RDF-based knowledge graphs. Functional equivalent of SQL for semantic graphs. Enables structured pattern extraction from graphs. Standard W3C protocol.

#### Reasoner
Inferential engine that, given an ontology, automatically derives implicit knowledge and verifies model consistency. Examples: HermiT, Pellet, FaCT++. Enables automated validation and discovery in ontology-driven systems.

### Formal Analysis Tools

#### Formal Concept Analysis (FCA)
Mathematical tool for extracting conceptual structures from data. Identifies groupings of objects sharing common attributes, producing a formal hierarchy of concepts (lattice). Mario Beltrani cites this as one of his primary research tools. Bridges statistical data exploration and logical structure.

### Cognitive Architectures & Memory

#### Cognitive Architecture
Computational framework modeling basic cognitive functions of an intelligent system: perception, memory, reasoning, planning. Examples: ACT-R, Soar, CLARION. In CDT: used as external module interacting with the DT via communication protocols. Provides a principled, theory-grounded approach to knowledge-based inference.

#### Memory (Cognitive Context)
Core function of a cognitive system. In CDT architecture distinguished into:
- **Static Memory**: rules, ontologies, formal constraints (stored in DKR)
- **Episodic Memory**: history of events, observed patterns over time (stored in DIKG)
Integrates persistent knowledge with dynamic situational awareness.

### Advanced Integration Concepts

#### Symbol Grounding
Process linking formal symbols (e.g., KG nodes) to real-world data (e.g., sensor measurements). One of the open problems in neuro-symbolic systems: ensuring abstract symbols have concrete anchoring in physical reality.

#### Neuro-Symbolic Approach
Paradigm combining neural networks (statistical learning, LLMs) with symbolic reasoning (logic, ontologies). The meeting point between implicit semantics of LLMs and explicit semantics of KGs. **Directly relevant to thesis Contribution 2**: the methodological bridge proposed.

#### Embedding
Vector representation of concepts or entities in continuous mathematical space. Enables LLMs to operate on semantics implicitly. In knowledge graphs: techniques like TransE or Node2Vec embed nodes and relations, enabling hybrid reasoning (symbolic + statistical).

#### Closed World Assumption vs Open World Assumption
Two opposite reasoning hypotheses:
- **CWA** (typical of databases): what is not known is false.
- **OWA** (typical of OWL ontologies): what is not known is simply not yet known.
Relevant when integrating a KG with an agentic system operating in partially observable environments. CDT framework adopts OWA to handle sensor uncertainty and incomplete observations.

---

## Cognitive Functions (Six CDT Pillars)

Follow the taxonomy of **Zheng et al. (2022)** and **Al-Haj Ali et al. (2025)**.

### Perception (Perception Agent)
Acquisition, normalization, and structuring of observational data from the physical system. Output: canonical 3GPP metrics.

### Reasoning (Reasoning Agent)
Inference on anomalies, correlations, root causes. Uses natural logic + KG. Output: structured diagnosis with confidence levels.

### Planning (Planning Agent)
Translation of diagnosis into concrete actions, validation against operational constraints stored in KG, selection of optimal action.

### Communication (Communication Agent)
Synthesis of perception-decision pipeline into user-readable explanation with causal argumentation.

### Memory
Persistence of state and history via Eclipse Ditto + Neo4j.

### Learning / Adaptation
Continuous evolution of KG and decision-making parameters (out of scope for MVP, defined as future work).

---

## Terminologia Dominio 5G

### gNB (gNodeB)
5G base station antenna. In simulator: 3GPP metrics generator.

### RSRP (Reference Signal Received Power)
Received reference signal power. Signal quality metric.

### SINR (Signal-to-Interference-plus-Noise Ratio)
Signal-to-interference-plus-noise ratio. Indicator of congestion and channel degradation.

### Handover
Transition of a communication from one cell to another. Failure rate is an indicator of instability.

### Throughput Downlink/Uplink
Data transfer speed. Degradation indicates resource anomalies or congestion.

### Latency
End-to-end delay. Critical metric for real-time services (eMBB, URLLC).

### KPI (Key Performance Indicator)
Aggregate performance metric. In thesis context: composite of RSRP, SINR, throughput, latency.

---

## Terminologia Architetturale

### Eclipse Ditto
Platform for digital twin management: state synchronization, WebSocket notifications, REST API. In context: backbone of digital representation (layers 2/3 of architecture).

### Neo4j
Graph database for Knowledge Graph. In context: storage of 5G operational constraints and Planning validation rules.

### LangGraph
Framework for orchestration of multi-step agents with explicit state management (LangChain + Langgraph). In context: runtime of cognitive pipeline.

### Supervisor Agent (LangGraph)
Coordination agent that routes incoming tasks to specialized agents. Implements routing, state management, decision tree. In context: central orchestrator of cognitive pipeline.

### StateGraph (LangGraph)
Data structure that represents the state graph of multi-agent pipeline. Each node is an agent/tool, each arc is a conditional transition.

### DKR (Dynamic Knowledge Repository)
Static offline knowledge graph that stores stable operational constraints (3GPP schema, safety rules). In context: Neo4j with 5G ontology. Contrast with DIKG.

### DIKG (Dynamic Instance Knowledge Graph)
Dynamic knowledge graph updated in real-time with the instantaneous state of the physical system. In context: Eclipse Ditto replica of gNB state. Contrast with DKR.

### Decision Sandbox
Pre-execution validation paradigm: the DT is not a passive mirror but a **test environment** where proposed actions are evaluated before execution on the real system. In context: Planning Agent verifies actions against KG.

### Ollama
Local LLM server with Q4/Q5 quantization. In context: hosting of Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B on M4 Pro.

### 3GPP
Telecommunication standard. In context: specification of simulated metrics format.

---

## Cognitive Architecture Patterns

These are reasoning and control flow patterns for LLM agents, from Hintze et al. (2025) taxonomy. Each represents a trade-off in token complexity vs accuracy vs latency.

### ReAct (Reasoning + Acting)

**Definition:** Agent loop where LLM produces both thoughts (reasoning steps) and actions (tool calls) in alternation. Cycle: Thought → Action → Observation → Thought → ...

**Token complexity:** Linear ($O(n)$ tokens for $n$ steps). Grounded in external feedback per action.

**Applicability to thesis:**
- **Best for:** Perception Agent (grounded in simulator data), Reasoning Agent (diagnoses cause via feedback)
- **Why:** Latency budget (5G <50ms SLA) requires linear complexity; exponential backtracking too slow
- **Source:** Yao et al., "ReAct: Synergizing Reasoning and Acting in LLMs" (2022)

---

### Reflexion (Self-Correction Loop)

**Definition:** Agent loop where LLM produces output, then generates a self-critique, then revises based on critique. Cycle: Initial Output → Self-Critique (LLM-generated) → Revision → (repeat if low confidence).

**Token complexity:** Higher than ReAct ($O(kn)$ for $k$ critique-revision rounds).

**Applicability to thesis:**
- **Best for:** Reasoning Agent (self-correct diagnosis before passing to Planning Agent)
- **Why:** Verbal self-correction reduces cascade errors without requiring external evaluator
- **Source:** Shinn et al., "Reflexion: Verbal Reinforcement Learning by Exploration" (2023)

---

### CRITIC (Tool-Interactive Validation)

**Definition:** Agent produces output (reasoning or action), then queries external tools (APIs, databases, KGs) to validate before committing. Cycle: Generate → Query Tools → Validate → (Accept/Reject/Revise).

**Applicability to thesis:**
- **Best for:** Planning Agent (validates proposed action against Neo4j KG before execution)
- **Why:** Closes the loop between neural (LLM reasoning) and symbolic (KG constraints)—neuro-symbolic approach
- **Mechanism:** Planning Agent queries Neo4j shape validators; if constraint violation → rejects action and proposes alternative
- **Source:** Gao et al., "CRITIC: Large Language Models Can Self-Correct with Tool-Interactive Critiquing" (2023)

---

### MAKER (Multi-Agent Worker + Verifier)

**Definition:** Specializes agents into Workers (who produce output) and Verifiers (who check output). Workers and Verifiers are separate agents with different system prompts and can be run in sequence or parallel.

**Error reduction:** Empirically reduces error accumulation on long chains (million-step reasoning tasks → near-zero hallucination vs single monolithic agent).

**Applicability to thesis:**
- **Architecture instantiation:** Reasoning Agent = Worker (diagnoses root cause); Planning Agent = Verifier (checks diagnosis against KG and proposes verified action)
- **Why:** Separation of concerns reduces error propagation; each agent specializes on one task
- **Token efficiency:** Worker focuses on generating ideas; Verifier focuses on validation (different token budgets)
- **Source:** Meyerson et al., "MAKER: A Benchmark of Multi-Agent Collaboration" (2024)

---

### Tree of Thoughts (ToT)

**Definition:** Agent explores a tree of reasoning paths, where each node is a thought and edges are possible continuations. Uses a value function to prune low-probability branches. Backtracking and exploration.

**Token complexity:** Exponential ($O(b^d)$ for branching factor $b$ and depth $d$). Examples: GPT-4 on coding tasks: 1M+ tokens for complex problems.

**Applicability to thesis:**
- **NOT used in MVP** — exponential token cost prohibitive on 7-8B models + M4 Pro hardware
- **Why not:** 5G reasoning deadline <50ms; Tree of Thoughts can take 5-10 seconds on small models
- **Future work:** Consider for offline analysis (post-incident root cause deep dive) with compute budget relaxed
- **Source:** Yao et al., "Tree of Thoughts: Deliberate Problem Solving with LLMs" (2023)

---

### LATS (LLM Agent Tree Search)

**Definition:** Combines tree search (explore multiple reasoning paths) with an external evaluator (LLM-as-judge or reward model) to guide search. Smarter version of ToT: prunes aggressively.

**Token complexity:** Still exponential but mitigated by pruning. Requires external evaluator (adds latency).

**Applicability to thesis:**
- **NOT used** — requires external evaluator LLM (adds latency); incompatible with local-only constraint
- **Future work:** If moving to cloud-capable model, LATS becomes viable for high-stakes decisions
- **Source:** Zhou et al., "LATS: Learning to Solve by Trial and Error" (2023)

---

### Reasoning Models (o1, o3 inference-time reasoning)

**Definition:** LLM models that spend extra inference-time compute thinking through the problem before answering. Internal computation budget $B$ (hidden from user). Not interpretable reasoning chain (opaque).

**Token complexity:** Variable (model-dependent). Can be very high for complex tasks.

**Applicability to thesis:**
- **NOT used** — requires paid API access (GPT-4o, o1) or large private model; incompatible with open-source local constraint
- **Why not:** Thesis requirement = local-only, open-weight models (Llama, Mistral, Phi, Qwen)
- **Comparison baseline:** Can compare thesis results against o1 as upper bound in Related Work
- **Source:** OpenAI (2024) — o1 model release notes

---

## CLASSic Evaluation Framework

**Complete definition:** See [[classic-evaluation-framework]]

Five-dimensional evaluation for agentic systems (Hintze et al., 2025):
- **C**ost — token complexity
- **L**atency — response time
- **A**ccuracy — success rate
- **S**ecurity — robustness against attacks/errors
- **S**tability — run-to-run variance

In thesis context: operationalized per agent (Perception, Reasoning, Planning, Communication) across all five dimensions.

---

## Metodologia Valutazione

### LLM-as-Judge
Use of an LLM as evaluator of output quality from another LLM. In thesis context: Llama 3.1 70B evaluates causal coherence of Reasoning Agent diagnosis on a 1-5 scale (rubric-based). Mitigation: multiple judges, reference examples, confidence calibration.

### Multi-Model Agreement
Validation strategy through consensus among multiple LLMs on identical tasks. If Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B converge on the same root cause diagnosis, correctness probability → high. Disagreement = low confidence. In context: triangulation without external ground truth.

### Outcome Validity
Definitive metric: did the action proposed by the agent solve the real problem in the system? In thesis context: were simulator KPIs recovered beyond target threshold post-action? Binary Pass/Fail. This is the king metric of the entire evaluation.

### Verifiable vs Non-Verifiable Tasks
**Verifiable (Explicit Ground Truth):** Ditto API calls, KG constraint violations, JSON schema validation — answers are binary.  
**Non-Verifiable (LLM-as-Judge Necessary):** Root cause diagnosis, causal explanation — answers are qualitative, require evaluation.  
In context: maximize verifiable tasks with external ground truth, use LLM-as-judge only where necessary.

### Milestone-Based KPI
Decomposition of each task into flexible milestones monitored in real-time. In thesis context: each fault injection scenario has 6 milestones (perceived anomaly → root cause → diagnosis confidence → proposed action → KG validation → improvement). Partial score per milestone, not all-or-nothing.

### Task Score (TS)
Quality of an agent's final output. In context: Accuracy of Reasoning Agent diagnosis, feasibility of Planning Agent action, coherence of Communication Agent. Evaluated vs ground truth (simulator) or LLM-as-judge.

### Coordination Score (CS)
Quality of interaction between agents. In context: Perception→Reasoning→Planning→Communication pipeline state passage without context loss? Token efficiency? Graph traversal correctness? Separate from Task Score — you can have high TS but low CS (right agent, wrong coordination).

### Outcome Validity Metric
Pass → KPIs recovered > target threshold; Fail → KPIs stagnant or degraded. Evaluated post-action by Planning Agent on 3GPP simulator. It is the absolute ground truth of evaluation.

---

## Noted Terminological Variants

- **"Gemello Digitale Cognitivo"** vs **"Cognitive Digital Twin"** — use CDT as canonical acronym in English text, translate to Italian only when necessary.
- **"Agente"** vs **"Agent"** — Italian preference "agente" in thesis body, "agent" in code comments and papers.
- **"Knowledge Graph"** vs **"Knowledge Base"** — use KG for graph-oriented structures (Neo4j), KB for flat vocabularies. In thesis context: KG.

---

## Recursive MAS & Latent-Space Collaboration

Concepts from Yang et al. (2026) — RecursiveMAS. Source: [[sources/recursive-mas-2026]].

### Recursive Language Model (RLM)

A language model that reuses the same transformer stack for `n` forward iterations in continuous latent space, refining the hidden representation without decoding to text at each step. Formula: H^(r) = f_θ(H^(r−1)), r=1,...,n. Foundation of RecursiveMAS architecture.

### Latent Thought

The last-layer hidden state `h_t` generated by a transformer at each autoregressive step, fed back as next-step input embedding instead of being decoded to a token. Enables reasoning entirely in continuous representation space.

### RecursiveLink (ℛ)

Lightweight 2-layer residual MLP module connecting agents in latent space. Two variants:

- **Inner link (ℛ_in):** `ℛ_in(h) = h + W2·σ(W1·h)` — feeds latent thoughts back within same agent
- **Outer link (ℛ_out):** `ℛ_out(h) = W3·h + W2·σ(W1·h)` — bridges heterogeneous agents with different embedding dimensions

Only RecursiveLink weights are trained (frozen LLM parameters).

### Latent-Space MAS Communication

Paradigm where agents exchange hidden states (embeddings) rather than decoded text. Reduces runtime from O(N·m·|V|·d_h) to O(N·m·d_h²) since d_h ≪ |V|. Trade-off: higher efficiency but zero interpretability of inter-agent messages.

### Inner-Outer Loop Training

Two-phase training paradigm for RecursiveMAS:

- **Inner loop** (per agent, parallel): cosine regression loss aligning latent thoughts to semantic input distributions — warms up ℛ_in
- **Outer loop** (full system): cross-entropy loss on final text output, gradients backpropagated through all recursion rounds — trains ℛ_out with global credit assignment

### Recursion Round

One complete forward pass through all agents in the loop. Performance scales monotonically with recursion depth (scaling law: more rounds → better accuracy, more speedup, fewer tokens). Only the final round produces textual output.

---

## Related Pages
- [[overview]]
- [[scaffolding-tesi]]
- [[classic-evaluation-framework]] — CLASSic evaluation dimensions explained
- [[cdt-five-characteristics]] — Zheng et al. five CDT characteristics framework
- [[mmci-framework]] — MMCI maturity levels for cognitive interoperability
- [[sources/recursive-mas-2026]] — RecursiveMAS paper source page
