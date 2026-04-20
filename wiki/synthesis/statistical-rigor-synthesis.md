---
title: Statistical Rigor Framework for Multi-Agent LLM Evaluation
type: synthesis
status: pending-advisor-review
created: 2026-04-20
updated: 2026-04-20
sources_raw: [raw/project/approfondimenti/Approfondimento dai video Berkeley.md]
papers_supporting: [berkeley-cs294-llm-eval, multiagent-bench-2025, burr-et-al-2026-agentic-dt]
references_expert: [Sida Wang - Berkeley, Oriol Vinyals - DeepMind, Noam Brown - OpenAI]
related_gaps: [Gap 1.3, Gap 2.2, Gap 2.3]
tags: [evaluation, statistical-rigor, benchmark, hypothesis-testing]
---

# Statistical Rigor Framework for Multi-Agent LLM Evaluation

**Status:** 🔄 Pending advisor feedback  
**Author synthesis:** Nicolò Termine  
**Basis:** Deep dive into Berkeley CS294 (Agentic AI) + DeepMind/OpenAI expert patterns

---

## 🎯 Central Thesis (Personal Contribution)

Improvements in LLM agent performance **can be statistical noise**, not genuine capability gain. The thesis must apply rigorous hypothesis testing to distinguish:

- **Signal** — Reproducible performance improvement across diverse scenarios and model pairs
- **Noise** — Random variation within measurement error bounds

This applies **Transitive Strength** framework (DeepMind AlphaStar lineage) + **Paired Variance Estimation** (Sida Wang, Berkeley) to 5G network management domain.

---

## 📊 Framework Components

### 1. Transitive Strength (League Training Model)

_Reference: Oriol Vinyals, DeepMind_

For each scenario, classify agent behavior along robustness spectrum:

| Classification | Definition | Example in 5G Context |
|---------------|-----------|----------------------|
| **Adversarial** | Susceptible to malformed inputs or simulator glitches | LLM hallucinates on corrupted RSRP values |
| **Exploiter** | Fails against specifically adversarial test cases designed to break logic | Saturate a slice to see if agent escalates correctly |
| **Cheese** | Proposes "lucky" but unsustainable solutions (extreme reconfigurations) | Proposes extreme TX power increase instead of load balancing |
| **Normal Policy** | Robust behavior under realistic conditions | Handles standard fault scenarios correctly |
| **Optimal Policy** | Performs at expert level (human baseline) with autonomous precision | Root cause inference + corrective action, both sound |

**Why it matters:** Moving from Adversarial → Optimal characterizes robustness **trajectory**, not just "accuracy at finish line".

**For thesis:** Benchmark systematically across this spectrum. Report which models reach which level.

---

### 2. Paired Variance Estimation

_Reference: Sida Wang, UC Berkeley_

**The Problem:** Comparing Llama 8B vs Mistral 7B on aggregate metrics (e.g., "accuracy: 78% vs 76%") is misleading. Natural variance in test selection can account for 5-10% swing.

**The Solution:** Head-to-head comparison on **identical scenarios**:

1. Fix a set of K identical fault injection scenarios
2. Run both models on each scenario
3. Compute paired differences: $d_i = \text{score}_{\text{Model A}, i} - \text{score}_{\text{Model B}, i}$
4. Estimate variance of differences: $\text{Var}(D) = \frac{1}{K-1}\sum(d_i - \bar{d})^2$
5. Compute t-statistic: $t = \frac{\bar{d}}{\sqrt{\text{Var}(D)/K}}$
6. Test significance at $\alpha = 0.05$

**Implication:** Do not compare aggregates. Compare pairs head-to-head on shared scenarios.

**For thesis:** Requires N × M × K experimental matrix:
- N scenarios (3 planned)
- M models (4 planned: Llama, Mistral, Phi-3, Qwen)
- K replicates per scenario (8-10 planned)
- **3 autonomy levels** (human-in-the-loop, semi-auto, autonomous)

**Total runs:** $3 \times 4 \times 3 \times 8 = 288$ baseline + replicates

---

### 3. Multi-Agent Consensus as Robustness Metric

_Reference: Sida Wang, Noam Brown_

When ground truth is absent (especially for Reasoning Agent), **high agreement among models suggests robustness**; **disagreement signals ambiguity or hallucination**.

$$\text{Consensus Score} = \frac{\text{# models agreeing on diagnosis}}{\text{Total models tested}}$$

**Three interpretations:**

| Score | Interpretation | Action |
|-------|----------------|--------|
| 1.0 (100%) | All 4 models agree | Very robust; high confidence in diagnosis |
| 0.75 (75%) | 3 of 4 agree | Acceptable; minor model uncertainty |
| ≤0.5 (50%) | Tie or minority agrees | Ambiguous task; requires human review |

**Why it works:** Independent models (same architecture family) are unlikely to hallucinate identically on the *same wrong diagnosis*. Convergence = signal.

**For thesis:** Report consensus score alongside accuracy metrics. This becomes a **second dimension of robustness**.

---

### 4. Z-Score Validation for KPI Impact

_Reference: Statistical hypothesis testing, generalized to network metrics_

When Planning Agent proposes an action (e.g., "increase TX power"), validate the KPI improvement against null hypothesis:

$$H_0: \text{(Mean KPI after action) = (Mean KPI before action)}$$

Compute z-score:

$$z = \frac{\bar{X}_{\text{after}} - \bar{X}_{\text{before}}}{\sqrt{\sigma^2_{\text{before}} + \sigma^2_{\text{after}}}}$$

**Threshold:** If $|z| > 1.96$, reject $H_0$ at $\alpha = 0.05$ (95% confidence that improvement is real, not noise).

**For thesis:** Report z-scores for each Planning Agent action. This proves improvements are not chance artifacts.

---

### 5. Multi-Model Agreement as Consensus

When testing multiple model sizes (Llama 3.1 8B vs Phi-3 Mini 3.8B), **agreement among models is stronger evidence than single-model accuracy**.

**Protocol:**

1. Present identical scenario to 4 models in parallel
2. Measure: % models proposing same diagnosis / action
3. Average agreement across test suite

**Implications:**
- High agreement (>75%) → diagnosis is robust across model architectures
- Low agreement (<50%) → task requires better specification or ground truth clarification

**For thesis:** Contributes to Contribution 2 (evaluation framework) as **multi-dimensional robustness metric**.

---

## 🔐 Safe-by-Design Integration

These statistical methods are **prerequisites for claims of autonomous operation** in critical infrastructure:

- **Paired testing** ensures comparisons don't overstate gains
- **Consensus metrics** catch hallucinations independent models would all make
- **Z-score validation** proves real-world KPI impact, not statistical noise
- **Transitive strength** tracks when system becomes unsafe (Adversarial) vs robust (Optimal)

---

## ⚠️ Points to Validate with Advisors

1. **Benchmark scope:** Is 288 runs (3 scenarios × 4 models × 3 autonomy × 8 replicates) feasible within thesis timeline? Trade-offs to reduce?

2. **Statistical power:** For small models (Phi-3 Mini), will we have sufficient variance in outputs to make paired t-tests meaningful? Or will results be too deterministic?

3. **Autonomy dimension:** Is "measuring performance across increasing autonomy levels" a novel contribution, or is this already standard in HRI (human-robot interaction) literature?

4. **Null hypothesis selection:** Is $H_0 = \text{no difference}$ the right null for CDT? Or should we test against "human operator baseline"?

5. **Consensus vs. ground truth:** If 4 models agree on wrong diagnosis, does consensus mislead? How to mitigate?

---

## 📚 Feedback Ricevuti

_To be completed after advisor meeting_

---

## Related Pages

- [[agentic-pipeline-synthesis]] — 4 agents evaluated via these statistical methods
- [[benchmark-template]] — Operational implementation of this framework
- [[safe-by-design-synthesis]] — Integration with architectural validation
