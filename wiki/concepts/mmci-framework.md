---
title: MMCI Framework — Multi-Modal Cognitive Interoperability
type: concept
created: 2026-04-14
updated: 2026-04-14
sources: [al-haj-ali-2025-mmci]
tags: [evaluation, framework, levels, maturity]
---

# MMCI Framework — Multi-Modal Cognitive Interoperability

**Five-level maturity model for evaluating cognitive alignment between CDT and human operator/domain constraints. Core evaluation framework for the thesis.**

---

## Definition

**Al-Haj Ali et al. (2025):**

> "Multi-Modal Cognitive Interoperability is the degree to which a CDT's cognitive processes are aligned with the mental models and decision-making patterns of human operators and domain standards."

Formalized as a 5-level maturity scale, from passive observation to fully autonomous cognition.

---

## Five Levels of Maturity

### Level 1 — Shared Situation Awareness (SSA)

**Definition:** CDT and human operator agree on the current state of the system.

**Metrics:**
- Do system observations match operator's interpretation?
- Are all relevant KPIs accurately perceived?
- Is there latency/lag that breaks synchronization?

**Tesis mapping:**
- **Agente:** Perception Agent
- **Misura:** Accuracy of Perception Agent output vs. simulator ground truth
- **Target 5G:** CDT and operator agree on gNB state (RSRP, SINR, throughput), anomaly detection

### Level 2 — Shared Mental Models (SMM)

**Definition:** CDT internally represents the domain knowledge in a form compatible with human mental models.

**Metrics:**
- Are the system's internal representations (KG, schema) interpretable?
- Can operators understand the model's assumptions and constraints?
- Are assumptions explicitly declared vs. hidden?

**Thesis mapping:**
- **Agente:** Neo4j KG + Planning Agent
- **Misura:** Can operators verify KG constraints? Are they aligned with 3GPP policies?
- **Target 5G:** KG codifies 5G operational rules; operators can audit and validate

### Level 3 — Intent & Reasoning Alignment

**Definition:** The CDT's problem-solving approach is explainable and aligned with human reasoning strategies.

**Metrics:**
- Are diagnoses interpretable (why does the system think X is the root cause)?
- Do explanations follow domain-standard reasoning patterns?
- Can operators follow the causal chain?

**Thesis mapping:**
- **Agente:** Reasoning Agent
- **Misura:** LLM-as-judge, multi-agent agreement, explanation quality
- **Target 5G:** Reasoning Agent explains root causes in LLM-generated natural language; operators can understand and verify

### Level 4 — Joint Decision-Making + Metacognition

**Definition:** CDT proposes actions with full justification; it monitors its own cognitive quality and alerts when uncertain.

**Metrics:**
- Are decisions traceable to reasoning?
- Does the system know when it's uncertain?
- Is confidence calibrated (confidence ~ accuracy)?
- Can operators veto or override with justification?

**Thesis mapping:**
- **Agenti:** Planning Agent + Communication Agent
- **Misura:** Confidence calibration, audit trail, override rate
- **Target 5G:** Planning Agent proposes actions with KG-validated constraints and confidence levels; Communication Agent explains decisions and uncertainty

### Level 5 — Full Autonomous Cognition

**Definition:** CDT operates fully autonomously, monitoring itself, learning from feedback, evolving its knowledge.

**Metrics:**
- Does the system self-correct?
- Does it learn from mistakes?
- Can it explain its evolution?

**Thesis mapping:**
- **Status:** Out of scope for MVP (future work)
- **Future:** Fine-tuning of LLM on domain-specific task, continuous KG update

---

## MMCI as Evaluation Grid for the Thesis

**Mapping to contributions:**

| Agent | Level 1 (SSA) | Level 2 (SMM) | Level 3 (Intent) | Level 4 (Joint) | Level 5 (Autonomous) |
|---|---|---|---|---|---|
| **Perception** | ✅ Ground truth vs. simulator | N/A | N/A | N/A | N/A |
| **Reasoning** | N/A | ✅ KG interpretability | ✅ Explanation quality | ⚠️ Confidence calibration | ⚠️ Learning rate |
| **Planning** | N/A | ✅ KG validates | ✅ Audit trail | ✅ Override handling | ⚠️ Adaptation |
| **Communication** | N/A | N/A | N/A | ✅ Explainability | ⚠️ Proactive uncertainty |

---

## Quantitative Metrics for Each Level

MMCI is primarily a **qualitative framework**, but can be operationalized:

### Level 1 — SSA Metrics
- Perception accuracy: `accuracy = TP / (TP + FP)` vs. simulator truth
- Latency: time from state change to CDT perception
- Coverage: % of observable KPIs successfully captured

### Level 2 — SMM Metrics
- KG schema completeness: % of domain concepts represented
- Constraint validation rate: % of detected anomalies match KG patterns
- Explainability: operator can verify 70%+ of KG edges on audit

### Level 3 — Intent Alignment Metrics
- **LLM-as-judge:** Larger model evaluates diagnosis coherence (0–1 score)
- **Multi-agent agreement:** consensus rate among Llama/Mistral/Phi-3/Qwen (% agreement)
- **Readability:** Flesch-Kincaid grade level of explanation (operator-comprehensible?)
- **Actionability:** % of diagnoses lead to valid action proposals

### Level 4 — Joint Decision-Making Metrics
- **Confidence calibration:** Expected Calibration Error (ECE) between predicted confidence and actual accuracy
- **Audit trail completeness:** 100% of decisions traceable to reasoning + KG
- **Override rate:** % of operator overrides (should be low if system is well-calibrated)
- **Human-system disagreement resolution rate:** when operator and CDT disagree, how often is operator right?

### Level 5 — Autonomous Metrics
- **Learning curve:** improvement in task accuracy over time
- **Stability:** variance of performance on repeated tasks
- **KG evolution:** rate of constraint updates without divergence

---

## Why MMCI Resolves the Thesis's Critical Gap

**The problem:** How do you measure reasoning quality of a Reasoning Agent when there's no "ground truth" for root cause diagnosis in 5G?

**MMCI's solution:** Don't measure reasoning in isolation. Measure **alignment**: how well does the system's model of the domain (KG) and its diagnosis process match what human experts would do?

**In practice:**
- Level 1 validates Perception (easy, ground truth available)
- Level 2 validates KG (harder, but scheme is auditable)
- Level 3 validates Reasoning (hardest, uses multi-model agreement as proxy for ground truth)
- Levels 4–5 validate decision-making and adaptation

By the time you reach Level 4, you've built enough indirect validation that the system's reasoning is credible, even without explicit ground truth.

---

## Limitation of MMCI (Honest Disclosure)

MMCI in Al-Haj Ali et al. (2025) is:
- Qualitative and preliminary, not fully quantified
- Validated only on HRC (human-robot collaboration), not on network operations
- Not empirically tested at scale with LLM-based reasoning

**Your thesis contribution:** You adapt MMCI to the 5G domain and add quantitative operationalization for Levels 3–4 (LLM-as-judge, confidence calibration, agreement metrics).

---

## Related Pages

- [[sources/al-haj-ali-2025-mmci]] — Foundational paper
- [[sources/zheng-et-al-2022-cdt]] — Six functions baseline
- [[glossary]] — Definitions
- [[scaffolding-tesi]] — Integration in Chapter 5
- [[concepts/six-cognitive-functions]] — Mapping to agents
