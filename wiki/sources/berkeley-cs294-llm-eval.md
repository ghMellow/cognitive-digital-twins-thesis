---
title: Berkeley CS294 — LLM Agent Evaluations (2026)
type: source
created: 2026-04-14
updated: 2026-04-28
sources: [b.2_Video Berkeley (Agentic AI MOOC) - LLM Agent Evaluations & Project Overview/Valore per la mia tesi.md, b.2_Video Berkeley (Agentic AI MOOC) - LLM Agent Evaluations & Project Overview/riassunto.md]
tags: [LLM-evaluation, agent-arcgitectures, outcome-validity, multi-model-agreement, evaluating-agents]
---

# Berkeley CS294 — LLM Agent Evaluations & Project Overview (2026)

A **methodology-focused** MOOC lecture on evaluating LLM-based agents. It directly informs **Contribution 2 (evaluation framework)** of the thesis. Provides vocabulary and practices for: outcome validity, tool-use evaluation, multi-model agreement, and LLM-as-judge. **Thesis placement**: Ch. 5 (Methodology) — best practices and anti-patterns for agent evaluation.

---

## 📺 Who They Are

 - **Institution:** UC Berkeley, CS294 Advanced Topics
 - **Topic:** Methodology for evaluating LLM-based agent systems
 - **Format:** Lecture video + case studies
- **YT:** https://www.youtube.com/watch?v=VfOA2a0dj4w
- **Year:** 2026 (part of the UC Berkeley Agentic AI curriculum)

---

## 🔑 Key Concepts Extracted

### 1. **Outcome Validity** (The Real Metric)

**Problem:** an agent can produce a great explanation, but the action it proposes does not solve the real problem.

**Definition:** outcome validity = “Did the intervention proposed by the agent solve the problem in the real system?”

**For the thesis:**
- **False positive:** Reasoning Agent claims a correct diagnosis, but after the Planning Agent applies the action, simulator KPIs do not improve
- **Ground truth:** simulator KPIs provide the definitive outcome validity signal
- **Metric:** Pass → KPIs recover above a target threshold; Fail → KPIs stagnate or worsen

**Benefit:** this is the flagship metric — it turns “the system speaks well” into “the system solves the problem.”

### 2. **Verifiable vs Non-Verifiable Tasks**

**Verifiable (explicit ground truth):**
- Perception Agent calls Ditto API for gNB state → is the answer in the Ditto DB? (binary)
- Planning Agent proposes a reconfiguration action → does it violate KG constraints? (binary)
- Communication Agent generates structured JSON → does it validate against schema? (binary)

**Non-verifiable (LLM-as-judge needed):**
- Reasoning Agent infers “root cause = congestion in low-RSRP band” → is this explanation correct? (non-binary; needs evaluation)

**For the thesis:** maximize verifiable tasks with external ground truth (simulator, KG), and use LLM-as-judge only where necessary (Reasoning, Communication).

### 3. **Capability-Level vs Vertical-Level Evaluation**

**Capability-level:** can the agent use a specific tool? (e.g., query Ditto API)  
**Vertical-level:** how good is it on a specific vertical? (e.g., diagnosing RSRP drops in 5G)

**For the thesis:**
- **Capabilities:** tool-use (Ditto calls, KG queries, LLM inference chains)
- **Verticals:** 5G fault types (congestion, handover failure, power degradation, latency spikes)

**Evaluation design:**
- Test capabilities in isolation (each agent separately)
- Test vertical scenarios (controlled fault injection per KPI)
- Combine: vertical competence + inter-agent coordination

### 4. **Multi-Model Agreement** (When Ground Truth Is Missing)

**Strategy:** if LLM A, LLM B, LLM C agree on the same root-cause diagnosis, correctness likelihood increases. Disagreement implies low confidence.

**For the thesis:**
- Run the same scenario on Llama 3.1 8B, Mistral 7B, Phi-3 Mini, Qwen 3B
- The Reasoning Agent in each model produces a diagnosis
- Diagnosis string → embeddings + cosine similarity
- Agreement% = overlap in embedding space
- Threshold: if agreement > 80%, raise confidence to “high”; otherwise flag for review / a structured vote

**Benefit:** improves robustness without relying on a single LLM vendor.

### 5. **LLM-as-Judge Practices** (Methodology)

**Setup:**
- Task to evaluate: Reasoning Agent output (diagnosis)
- Judge: Llama 3.1 70B (larger model, local or via API)
- Scale: 1–5 (incoherent → highly sensible)
- Rubric: “Does the diagnosis causally explain the observed anomaly? Is it consistent with 3GPP constraints?”

**Risk mitigations:**
1. **Diverse judges:** use 2–3 different models and average
2. **Blind evaluation:** judge does not see which agent/model produced the output
3. **Reference outputs:** include 1–2 “correct” diagnosis exemplars from a domain expert
4. **Confidence calibration:** ask the judge to self-rate confidence (“confident”, “somewhat uncertain”)

**For the thesis:**
- Judge = Llama 3.1 70B if available (e.g., via quantized Ollama); otherwise 8B with a stricter rubric
- Rubric should include: causal coherence, 3GPP constraint alignment, completeness
- Record confidence scores for later analysis

---

## 📋 Integration into the Scaffolding

### Ch. 5 (Evaluation Methodology)

**Section 5.1 — Defining evaluation dimensions**
- Outcome validity (KPI improvement in simulator)
- Task completeness (milestone-based)
- Reasoning quality (LLM-as-judge rubric)
- Coordination quality (multi-agent agreement score)

**Section 5.2 — Ground truth strategy**
- Where available (simulator for Perception, KG for Planning): deterministic validation
- Where unavailable (Reasoning, Communication): LLM-as-judge + multi-model agreement mitigations

**Section 5.3 — Evaluation protocols**
- Capability-level: each agent isolated on simple tasks
- Vertical-level: end-to-end pipeline on fault injection scenarios
- Combination: comparative model benchmark on the same scenario set

### Ch. 6 (Experiments)

**Table:** Outcome Validity by Model × Fault Type  
**Table:** Task Score (milestone completeness) by Agent  
**Table:** Multi-Model Agreement % (Llama/Mistral/Phi-3/Qwen consensus on diagnosis)  
**Figure:** Confidence calibration curve (Judge confidence vs actual agreement with external ground truth)

---

## ✅ Strengths

| Aspect | Use |
|---|---|
| **Outcome validity framework** | Definitive metric: “Did the action actually solve the problem?” |
| **Task classification** | Separate verifiable (deterministic) vs non-verifiable (LLM-based) |
| **Multi-model agreement** | Triangulation without external ground truth |
| **LLM-as-judge best practices** | Rubrics, confidence calibration, mitigation patterns |
| **Capability vs vertical** | Separate architectural debugging from domain debugging |
| **Transparent methodology** | Allows an advisor to replicate the evaluation |

---

## ❌ Limitations and Mitigations

| Limitation | Thesis mitigation |
|---|---|
| Does not cover real-time latency constraints | Add a “Decision latency” metric (ms) per agent |
| Examples are software-centric (WebArena, SWE-bench) | Build a 5G-specific benchmark with fault injection |
| LLM-as-judge can have systematic biases | Use multiple judges, reference examples, confidence calibration |
| Does not cover consumer hardware constraints | Measure token throughput, peak memory, power draw on M4 Pro |

---

## 🎯 Advisor Answer

If asked: _“How do you avoid circular evaluation (LLM evaluates LLM)?”_

> _“Following best practices (Berkeley CS294, 2026), I use a three-layer approach: (1) whenever external ground truth exists (3GPP simulator, Neo4j constraints), I use it — deterministic and reproducible; (2) when ground truth is missing for Reasoning, I use multi-model agreement across four local open-weight models (Llama, Mistral, Phi-3, Qwen): convergence increases confidence; (3) I add an LLM judge (e.g., Llama 70B) with a transparent rubric, reference examples, and multiple judges that vote. This is still imperfect, but it is the best available practice for tasks without explicit ground truth. Final outcome validity is always validated on the simulator: if the action restores KPIs, the diagnosis was correct.”_

---

## 🔗 Related Concepts

- [[mmci-framework]] — MMCI is a maturity framework; Berkeley provides tactical evaluation methods
- [[multiagent-bench-2025]] — Complementary: MultiAgentBench focuses on coordination; Berkeley is more general
- [[cognitive-digital-twin]] — 6 cognitive functions → structured evaluation dimensions

---

## Key Takeaway

This lecture shifts the thesis from “I built a CDT that works” to **“I developed a rigorous methodology to evaluate the reliability of cognitive reasoning on a simulated 5G infrastructure.”** That framing is what makes the work scientifically solid and publishable.

---

## Related Pages

[[sources/multiagent-bench-2025]] | [[sources/al-haj-ali-2025-mmci]] | [[mmci-framework]]
