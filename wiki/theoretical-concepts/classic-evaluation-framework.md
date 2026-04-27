---
title: CLASSic Evaluation Framework
type: concept
created: 2026-04-28
updated: 2026-04-28
sources: [sources/hintze-et-al-2025-agentic-ai]
tags: [evaluation, framework, methodology, multi-dimensional]
---

# CLASSic Evaluation Framework

**Five-dimensional evaluation framework for agentic systems. From Hintze et al. (2025). Core schema for Thesis Contribution 2: Multi-Dimensional Cognitive Evaluation.**

One-line summary: CLASSic measures Cost, Latency, Accuracy, Security, and Stability—going beyond single-metric evaluation to capture production-readiness.

---

## The Five Dimensions

### C — Cost

**Definition:** Computational resources consumed (tokens, memory, inference time budget).

**Motivation:** Larger reasoning architectures (Tree of Thoughts, reasoning models) have exponential token complexity $\propto b^d$ (branching factor × depth). Trade-off: deeper reasoning vs. latency/cost.

**Operationalization in thesis:**
- **Token consumption per agent:** Measure input+output tokens for Perception, Reasoning, Planning, Communication agents
- **Inference cost per cycle:** Total tokens per cognitive cycle (target: <2000 tokens for <100ms latency on M4 Pro)
- **Model comparison:** Llama 3.1 8B vs Mistral 7B vs Phi-3 Mini 3.8B vs Qwen 3B—rank by token efficiency

**Metric:** Tokens/decision or Inference time / agent. Target: <500ms end-to-end cycle on M4 Pro.

---

### L — Latency

**Definition:** Response time from stimulus to action execution.

**Motivation:** 5G RAN has strict SLAs. Handover decisions must complete in <50ms. Latency in async environments (network delays, buffering) causes 11% vs 47% success rate (Robotouille benchmark).

**Operationalization in thesis:**
- **Hard latency (URLLC-critical):** <50ms for Planning Agent decision
- **Soft latency (eMBB-tolerable):** <200ms for full Perception→Reasoning→Planning→Communication cycle
- **Async penalty measurement:** Inject network delays; measure success rate degradation

**Metric:** p50/p95/p99 latency per stage. Measure jitter (variance) as well as mean.

---

### A — Accuracy

**Definition:** Success rate of the system on well-defined tasks.

**Motivation:** 80% accuracy but with 20% infinite loops is not production-ready. Need outcome-driven metrics.

**Operationalization in thesis:**
- **Task Completion Score (TS):** Percentage of fault scenarios where agent reaches correct diagnosis
- **Outcome Validity:** Final metric—did the recommended action recover KPIs above threshold? (Binary: Pass/Fail)
- **Per-agent accuracy:** Perception F1 (vs simulator truth), Reasoning accuracy (vs ground truth or multi-model consensus), Planning constraint compliance (% actions passing KG validation)

**Metric:** Outcome Validity = primary (verifiable in simulator). Reasoning accuracy = secondary (multi-LLM agreement + KG-grounded).

---

### S — Security

**Definition:** Robustness against adversarial or erroneous inputs.

**Motivation:** Agents can be attacked via prompt injection, malicious tool outputs, or corrupted state. Must measure failure modes.

**Operationalization in thesis:**
- **Constraint verification:** % of proposed actions that pass Neo4j shape validation (should be 100%)
- **Fallback activation:** How often does Planning Agent reject an invalid action? Measure false-accept rate
- **Safety guardrails:** Does the system escalate to human review when confidence is low? (Operationalized via MMCI Level 1)

**Metric:** Security score = (Valid actions / Total actions) × (Fallbacks triggered correctly / Invalid inputs). Target: >99% valid, 100% fallback accuracy.

---

### S — Stability

**Definition:** Consistency of performance across repeated runs (run-to-run variance).

**Motivation:** An agent that succeeds 70% of the time with ±30% variance is unreliable. Stability measures confidence in repeated operation.

**Operationalization in thesis:**
- **Run-to-run variance:** Execute the same fault scenario N=10 times on each model; measure std(accuracy), std(latency)
- **Failure severity distribution:** Not just success rate, but _how badly_ does the system fail? (e.g., does failure cascade or gracefully degrade?)
- **Recovery stability:** If system fails on attempt 1, does it recover on attempt 2+? Measure recovery latency

**Metric:** Coefficient of Variation (CV) = std(accuracy) / mean(accuracy). Target: CV < 0.15 (low variance). Severity distribution histogram.

---

## CLASSic Score Aggregation

**Overall readiness score (not a number, but a decision tree):**

```
if Cost per cycle ≤ SLA
  AND Latency p95 ≤ SLA
    AND Accuracy > threshold
      AND Security > 99%
        AND Stability CV < 0.15
  then "PRODUCTION READY" ✅
  else "RESEARCH PROTOTYPE" 🔄
```

---

## How CLASSic Maps to Thesis Contributions

| CLASSic Dimension | Thesis Operationalization | Contribution |
|---|---|---|
| **Cost** | Token budget per agent (M4 Pro hardware constraint) | Contribution 3: Model benchmark (cost/performance trade-off) |
| **Latency** | Cycle time breakdown (P→R→Pl→C stages) + async penalty | Contribution 3: 5G domain-specific (SLA < 50ms for URLLC) |
| **Accuracy** | Task Score + Outcome Validity + per-agent metrics | Contribution 2: Multi-dimensional evaluation (no single metric) |
| **Security** | KG constraint compliance + fallback mechanisms | Contribution 2: Guardrails against performative prediction |
| **Stability** | Run-to-run variance across N replicates + failure modes | Contribution 2: MMCI autonomy progression (Level 1 = stable human-in-the-loop) |

---

## Why CLASSic Matters for CDT Evaluation

**Traditional evaluation (single accuracy metric):**
- ❌ Misses latency catastrophes (16% success rate in async environments per Robotouille)
- ❌ Ignores stability (70±30% is very different from 70±5%)
- ❌ Conflates cost and capability (expensive ≠ better)

**CLASSic evaluation (five dimensions):**
- ✅ Captures production readiness holistically
- ✅ Enables trade-off analysis (e.g., "accept higher latency if cost drops 40%")
- ✅ Reveals failure modes (cascading vs graceful, reproducible vs random)

---

## Related Pages

- [[sources/hintze-et-al-2025-agentic-ai]] — source paper
- [[mmci-framework]] — how autonomy progression fits within CLASSic dimensions
- [[benchmark-template]] — operationalization protocol for CLASSic metrics
- [[gap-analysis]] — how CLASSic addresses Gap 1.3 (evaluation without ground truth)
