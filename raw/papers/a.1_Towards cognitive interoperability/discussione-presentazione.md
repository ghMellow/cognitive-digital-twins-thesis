# Discussion Notes — Presentation by Jana AL HAJ ALI
**Date:** 2026-05-20
**Context:** Meeting with the author of "Towards Cognitive Interoperability: CDT and Cognitive Architecture for Human-CPS Collaboration"
**Purpose:** Identify connection points with the user's thesis on CDT for 5G radio cell management

---

## 1. The Most Relevant Contributions for This Thesis

### 1.1 MMCI as a Ready-Made Evaluation Metric

**Why it matters most:** The feedback document explicitly identified the evaluation of reasoning and planning agents as the highest-risk open problem. Al Haj Ali's MMCI provides a ready-made, formally grounded framework to measure exactly that — and it already appeared in the feedback as a *"concrete metric for measuring growing autonomy."*

The five levels map directly onto the human-in-the-loop trajectory of this thesis:

| MMCI Level | Al Haj Ali's definition | Mapping to 5G CDT thesis |
|---|---|---|
| L0 | Semantic Interoperability | Eclipse Ditto provides raw metric state |
| L1 | Shared Situation Awareness | Perception Agent normalises and surfaces anomalies |
| L2 | Shared Mental Models | Reasoning Agent correlates KPIs, infers root causes |
| L3 | Intent and Reasoning Alignment | Planning Agent proposes actions verified against Neo4j KG |
| L4 | Joint Decision-Making with Metacognitive Regulation | Full autonomous pipeline with explainable reporting |

**Concrete use:** Evaluating which MMCI level the 5G CDT achieves under different LLM configurations gives a domain-independent yardstick that reviewers can compare across papers. It also formalises the "autonomia crescente" dimension from the feedback.

---

### 1.2 Formal CDT Definition (Emulation + Simulation + Cognition)

The paper defines CDT rigorously as three co-equal functions: **emulation, simulation, cognition**. The feedback document noted that "a lot of literature on Digital Twins does not apply formal rigour to the definition" and that demonstrating the system respects these constraints is itself a scientific contribution.

**Concrete use:** Section 2.1.3 gives the formal definition and the two implementation strategies (externalised vs internalised cognition). This thesis implements **internalised cognition** via the LangGraph agent pipeline — this architectural choice can now be named and justified formally rather than treated as an implementation detail.

---

### 1.3 LLMs Explicitly Listed as a Future Direction

Chapter 6 states:
> *"Deeper integration of LLM-based components for natural language interaction"*

This is significant: Al Haj Ali's thesis opens the door, this thesis walks through it. The 5G CDT can be positioned as a direct empirical response to this stated future direction — replacing the CLARION cognitive architecture with LLM-based agents and evaluating the trade-offs.

**Concrete use:** The thesis introduction can anchor the research in the gap explicitly left open by Al Haj Ali. This is cleaner positioning than claiming novelty in a vacuum.

---

### 1.4 Cognitive Architecture → LangGraph Agent Mapping

Al Haj Ali uses CLARION with four subsystems (ACS, NACS, MS, MCS). The 5G CDT uses LangGraph with four specialised agents. These are different implementations of the same conceptual structure:

| CLARION Subsystem | Function | 5G CDT Agent Equivalent |
|---|---|---|
| ACS (Action-Centred) | Procedural knowledge, action selection | Planning Agent |
| NACS (Non Action-Centred) | Declarative knowledge, world model | Reasoning Agent (with Neo4j KG) |
| MS (Motivational) | Goal and priority management | (embedded in LangGraph graph logic) |
| MCS (Meta-Cognitive) | Monitors, regulates, triggers learning | Communication Agent + human escalation |

**Concrete use:** This mapping allows the thesis to position LangGraph + LLMs as a *modern, LLM-native alternative to CLARION* — preserving the same functional decomposition but replacing neuro-symbolic components with language models. This is a defensible architectural choice, not just a trendy technology swap.

---

### 1.5 Evaluation Framework Structure

The paper evaluates against a **semantic-only baseline** (CDT without cognitive architecture) using MMCI indicators. This comparative approach is directly replicable:

- **Baseline:** Eclipse Ditto alone (L0 — semantic interoperability only)  
- **Experimental:** Full LangGraph pipeline (L1–L4 progression)
- **Metrics:** MMCI level achieved per agent per fault scenario

**Concrete use:** This is the missing evaluation strategy identified in the feedback as the highest-risk gap. Al Haj Ali's methodology provides both the comparison structure and the metric vocabulary.

---

### 1.6 KRR Positioning: Ontology vs Knowledge Graph

The paper uses OWL/SWRL ontology (CDTO) for formal reasoning. This thesis uses Neo4j knowledge graph. These are two valid KRR strategies — the paper's Chapter 1 explicitly discusses both as dominant approaches in CDT literature.

**Concrete use:** The thesis does not need to apologise for choosing Neo4j over OWL. The paper provides the theoretical justification for KGs as a valid alternative: "contextual linking, extensible knowledge base." The trade-off (formal completeness vs. pragmatic queryability) can be stated explicitly.

---

## 2. Questions to Ask the Author

These are questions where Al Haj Ali's experience directly informs open problems in this thesis.

### On Evaluation

> 1. **"How did you operationalise MMCI levels as measurable indicators in the use case? What evidence mapped to each level?"**  
>   *Why ask:* The feedback identified this as the hardest problem. The paper mentions evaluation but does not detail the specific indicators — the presentation may clarify this.

> 2. **"For the Reasoning and Planning components, how did you handle cases where the system's output was difficult to evaluate against a ground truth?"**  
>   *Why ask:* In 5G the same problem exists — root cause inference has no obvious ground truth. Her experience in HRC (where the human can validate the robot's decision) may offer transferable strategies.

3. **"The MMCI extension with more measurable indicators is listed as future work — do you have a direction in mind for that?"**  
   *Why ask:* If this is actively being worked on, it could become a collaboration point or a reference to cite for ongoing work.

### On Architecture

4. **"How does CLARION handle the latency requirements of real-time scenarios? In 5G, decisions may need to happen in milliseconds — was this a constraint in your use case?"**  
   *Why ask:* LLMs introduce latency too, but differently. Understanding her experience with CLARION timing helps position the comparison fairly.

5. **"In your framework, cognition is either externalised (strongly coupled to the physical system) or internalised (in the CDT). In 5G the CDT is the network management plane — is there a third position where the CDT IS the operational system?"**  
   *Why ask:* In telecoms, the CDT and the managed system boundary is blurrier than in HRC. Her definition might need to be extended or the 5G case justified as a variant.

> 6. **"What were the main limitations you encountered in integrating the ontology with CLARION at runtime?"**  
>   *Why ask:* The 5G thesis integrates a knowledge graph with LLM agents in a similar coupling pattern (Neo4j → Planning Agent). Her pain points are likely relevant.

### On LLMs

7. **"You mention LLM integration as a future direction. Did you experiment with LLMs at all during the project, even informally? What concerns shaped the decision to use CLARION instead?"**  
   *Why ask:* Her answer reveals whether the future direction is a genuine gap or a deliberate exclusion. Either answer is useful.

8. **"For the natural language explanation component, did the Communication equivalent in your system produce explanations a domain expert found usable? What made them credible or not?"**  
   *Why ask:* The Communication Agent in the 5G CDT faces the same problem. Credibility of natural language explanations is non-trivial.

### On Positioning

9. **"How do you differentiate CDT from a standard autonomous agent system? What makes the Digital Twin framing necessary rather than optional?"**  
   *Why ask:* This is a question reviewers will ask both theses. Her answer may reveal arguments this thesis has not yet formalised.

---

## 3. How This Work Positions the 5G CDT Thesis

| Dimension | Al Haj Ali's thesis | 5G CDT thesis |
|---|---|---|
| Domain | Human-robot collaboration, manufacturing | 5G radio cell network management |
| CDT implementation | CLARION (neuro-symbolic cognitive architecture) | LangGraph + local LLMs |
| KRR approach | OWL/SWRL ontology (CDTO) | Neo4j knowledge graph |
| Evaluation framework | MMCI levels, semantic baseline comparison | MMCI levels (reusing the model), LLM model comparison |
| Physical layer | UR5e cobot, screwing task | Python 5G metrics simulator, 3GPP KPIs |
| Human-in-the-loop | Human operator in HRC loop | Escalation to network operator (growing autonomy) |
| Future directions opened | LLM integration, multi-agent, more measurable MMCI indicators | This thesis |

**The 5G CDT thesis is a direct empirical follow-up to Al Haj Ali's framework:**
- Same formal CDT definition and cognitive functions
- Same MMCI evaluation model (applied to a new domain)
- CLARION replaced by LLM agents — explicit architectural comparison
- LLM integration (her future work) — the central contribution

---

## 4. What to Read Before the Presentation

If time allows, prioritise:

1. **Section 2.4** — MMCI levels in detail (most directly reusable)
2. **Section 5.5** — Evaluation framework and metrics (how she measures MMCI in practice)
3. **Section 3.2** — CLARION selection criteria (maps to LangGraph positioning)
4. **Chapter 6** — Future directions (frames where this thesis fits)
