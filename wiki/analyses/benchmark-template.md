---
title: Benchmark Template — CDT LLM Agent Evaluation Protocol
type: analysis
created: 2026-04-14
updated: 2026-04-14
sources: [sources/multiagent-bench-2025, sources/berkeley-cs294-llm-eval, sources/al-haj-ali-2025-mmci, sources/wireless-agent-hkust-2025]
tags: [benchmark, evaluation, methodology, experimental-design]
---

# Benchmark Template — LLM Agent Reasoning Evaluation

**Scopo:** Protocollo sperimentale end-to-end per valutare CDT reasoning (Blocco D dal paper). Combina MMCI framework (Al-Haj Ali) + LLM eval best practices (Berkeley) + Task/Coordination Score (MultiAgentBench).

---

## Part 1: System Under Test (SUT)

### SUT Specification

**System:** Cognitive Digital Twin for 5G Network Slicing  
**Running on:** 
- **Backend:** Python 3GPP simulator + Eclipse Ditto + Neo4j KG + LangGraph
- **LLM Stack:** 4 open-weight models running locally via Ollama
  - Model A: Llama 3.1 (8B)
  - Model B: Mistral (7B)
  - Model C: Phi-3 Mini (3.8B)
  - Model D: Qwen (3B)

**Agent Decomposition:**
- **Perception Agent** — Queries simulator KPI (RSRP, SINR, throughput, latency, handover_count) → stores in Domain KG (DKR)
- **Reasoning Agent** — Analyzes DKR + Intent KG (DIKG) → outputs diagnosis (e.g., "UE-123 poor coverage due to interference, recommend gNB migration")
- **Planning Agent** — Generates action plan constrained by KG shapes (e.g., "migrate UE-123 to gNB-B only if gNB-B has capacity and RSRP > -105dB")
- **Communication Agent** — Issues RAN commands (assign UE to gNB, adjust slice throughput) → sends to simulator

**Loop:** Perception (tick t) → Reasoning (t) → Planning (t) → Communication (t) → observe outcome (t+1) → loop

---

## Part 2: Fault Injection Scenarios

### Scenario Design

Each scenario injects a synthetic fault into simulator. Ground truth is known (simulator KPI delta post-fault). Test: does Agent reasoning correctly diagnose and plan recovery?

#### **Scenario A: Single-Point Failure (UE Poor Coverage)**

```
Fault: Inject RSRP drop on UE-123 (-105dB → -115dB) simulating interference

Phases:
1. Perception (t=0): Detect RSRP drop
   - Ground Truth: RSRP drop is real (simulator confirms)
   - Metric: Detection latency (time from fault to perception alert) ← target <100ms

2. Reasoning (t=1): Diagnose root cause
   - Ground Truth: Interference or gNB far, not UE malfunction
   - Test: Does Reasoning Agent suggest "gNB migration" or "increase TX power"?
   - Metric: Diagnosis accuracy = cosine(suggested_reason, ground_truth_reason) ← target >0.8
   - Metric: Outcome Validity (Berkeley) = does diagnosis suggest valid actions?

3. Planning (t=2): Generate recovery action
   - Ground Truth: Valid recovery: migrate to gNB-B (if available, capacity ok, RSRP improves)
   - Test: Does Planning Agent check KG constraints before proposing?
   - Metric: KG Constraint Compliance = % of actions passing Neo4j shape validation ← target 100%
   - Metric: Task Completion Score (MultiAgentBench) = did recovery action improve RSRP? ← target >0.7

4. Communication (t=3): Execute command
   - Metric: Latency = time from Planning output to Communication execution ← target <50ms
   - Metric: Command validation = does command match plan (no hallucination)? ← yes/no

5. Observe (t+1): Did recovery work?
   - Ground Truth: New RSRP (post-migration) should be >-105dB
   - Metric: Recovery Effectiveness = (new_rsrp - fault_rsrp) / expected_rsrp ← target >0.8
```

**Fault Parameters:**
- **Severity:** -10dB drop (moderate)
- **Duration:** 5 simulator ticks (500ms real time if tick=100ms)
- **Recovery Window:** 10 ticks deadline (1 second) to recover RSRP or declare failure
- **Repetitions:** N=10 (10 different UEs, different fault timings)
- **Expected Outcome:** 80%+ recovery success rate across all models (consensus threshold 3/4 models succeed)

---

#### **Scenario B: Resource Contention (RANSlice Overload)**

```
Fault: Inject load on RANSlice-1 (throughput_available = 1000 Mbps → 500 Mbps) affecting 5 UEs

Phases:
1. Perception: Detect load increase
   - Ground Truth: Simulator reports <throughput_target on 3/5 UEs
   - Metric: Detection accuracy = % of under-target UEs identified

2. Reasoning: Diagnose bottleneck
   - Ground Truth: RANSlice capacity issue, not individual gNB or UE problem
   - Test: Does Reasoning Agent identify RANSlice as root cause (not UE antenna or gNB hardware)?
   - Metric: Root Cause Accuracy ← target >0.75

3. Planning: Coordinate rebalancing
   - Ground Truth: Valid recovery: migrate 2 UEs to RANSlice-2 (reduce contention)
   - Test: Does Planning Agent propose multi-UE migration? Does it check SLAs of affected UEs?
   - Metric: **Coordination Score** (MultiAgentBench) = do planned actions reduce contention without violating SLAs? ← target >0.8
   - Complexity: Requires Planning Agent to reason about multi-objective: maximize throughput AND minimize inter-slice migration cost AND maintain other SLAs

4. Communication: Execute batch migration
   - Metric: Atomicity = all 2 migrations succeed or none (no partial state)
   - Metric: Latency = time from Planning to all commands executed ← target <150ms (higher than single action due to batch coordination)

5. Observe: Did rebalancing work?
   - Ground Truth: All UEs should reach throughput_target (or within 5% per MMCI L3)
   - Metric: SLA Compliance = % of UEs with throughput ≥ target ← target 100%
```

**Fault Parameters:**
- **Severity:** 50% capacity reduction (high)
- **Duration:** Persistent (throughout test, not self-recovery)
- **Recovery Window:** 20 ticks (2 seconds)
- **Repetitions:** N=8 (different slice configurations)
- **Expected Outcome:** Coordination Score >0.8; all UEs SLA-compliant post-recovery

---

#### **Scenario C: Multi-Fault (Cascading Failures)**

```
Fault: Simultaneous RSRP drop (Scenario A) + load spike (Scenario B) on overlapping UE set

Phases:
1-4. Same as Scenario A + Scenario B concurrently
   - Two faults independent sources vs. two faults cascade?
   - Metric: multi-fault resilience = % successful recovery on both dimensions

5. Observe: Robustness under stress
   - Ground Truth: No SLA breach despite dual fault
   - Metric: System stability = variance in recovery latency across models ← lower = more robust
   - Metric: Hallucination detection = does any model propose invalid (contradictory) actions? ← 0% expected
```

**Fault Parameters:**
- **Severity:** Double (A + B simultaneous)
- **Duration:** 5 ticks (both faults) + mandatory recovery within 2 seconds
- **Complexity:** Tests multi-objective reasoning + consensus stability when models disagree
- **Repetitions:** N=5 (lower reps due to complexity)
- **Expected Outcome:** 70%+ recovery success; <5% model disagreement rate

---

## Part 3: Metrics Framework

### 3.1 Individual Model Metrics

For each model (Llama, Mistral, Phi-3, Qwen) on each scenario:

| Metric | Definition | Formula | Target | Source |
|---|---|---|---|---|
| **Detection Latency** | Time from fault injection to Perception Alert | latency_ms = t_alert - t_fault | <100ms | Custom |
| **Diagnosis Accuracy** | Cosine similarity between suggested root cause and ground truth | cos(embedding(suggested), embedding(truth)) | >0.80 | Berkeley eval best practice |
| **KG Constraint Compliance** | % of Planning outputs passing Neo4j shape validation | compliance = pass_count / total_count | 100% | Custom (Dual-KG operationalization) |
| **Task Completion Score** | Fraction of goal achieved (e.g., RSRP recovery: (new-fault)/(pre-fault-fault)) | score = (achieved_kpi - fault_kpi) / (pre_fault_kpi - fault_kpi) | >0.70 | MultiAgentBench |
| **Coordination Score** | Multi-agent action coherence (do planned actions achieve multi-objective goals without conflict?) | measured via constraint satisfaction + SLA meet | >0.80 | MultiAgentBench |
| **Command Execution Latency** | Time from Planning output to Communication action on simulator | latency_ms = t_executed - t_planned | <50ms (single) / <150ms (batch) | Custom |
| **Recovery Effectiveness** | Post-recovery KPI vs. expected (best-case) KPI | effectiveness = new_kpi / expected_kpi | >0.80 | Custom |
| **Outcome Validity** | % of recovery actions that actually improve KPI (vs. harm it) | validity = beneficial_actions / total_actions | 100% | Berkeley |
| **SLA Compliance** | % of users with all SLAs met post-recovery | compliance = sla_met_count / total_users | 100% | Custom |

---

### 3.2 Ensemble (Multi-Model) Metrics

Combine 4 models via consensus voting:

| Metric | Definition | Formula | Target |
|---|---|---|---|
| **Consensus Rate** | % of decisions where ≥3/4 models agree | consensus = unanimous / total_decisions | >90% |
| **Disagreement Resolution** | When models disagree, does tie-breaker (Llama priority) lead to good outcomes? | tie_breaker_success = beneficial_outcomes / tie_breaker_calls | >80% |
| **Ensemble Robustness** | Variance in recovery latency across 4 models (lower = more robust) | robustness = 1 / (1 + std_dev(latencies)) | >0.85 (normalized) |
| **Hallucination Detection** | % of invalid/contradictory actions flagged by consensus (any model outputs action violating another model's constraint?) | detection = caught_invalid / total_invalid | 100% (ideal) / >95% (realistic) |
| **Multi-Model Agreement Reliability** | Given 4 models agree, what % are actually correct? (calibration measure) | reliability = correct_unanimous / total_unanimous | >95% |

---

### 3.3 MMCI Alignment Metrics (Al-Haj Ali)

For each recovery phase, assess MMCI maturity level:

| MMCI Level | Focus | Metric | Thesis Target |
|---|---|---|---|
| **L1: Shared Situation Awareness** | All agents perceive same facts (no perception disagreement) | perception_alignment = 1 - (disagreement_count / total_observations) | >95% |
| **L2: Mental Model Alignment** | All agents build consistent world model (KG-grounded) | kg_alignment = consistent_edge_count / total_edges_queried | >90% |
| **L3: Intent Alignment** | Agents agree on goals (diagnosis and recovery plan) | intent_alignment = cosine(reasoning_outputs_across_models) | >85% |
| **L4: Joint Decision Making** | Agents coordinate on actions (Planning consensus) | decision_alignment = consensus_rate (>3/4) | >90% |
| **L5: Full Autonomy** | System executes recovery without human input and validates effectiveness | autonomy_score = (execution_success × transparency_score) | >80% |

**Operationalization:** For each scenario, measure L1-L5 alignment. Plot recovery curve: latency to reach each level.

---

## Part 4: Experimental Design

### 4.1 Test Matrix

```
Scenarios:      A (single fault), B (contention), C (cascade)
Models:         Llama 3.1-8B, Mistral-7B, Phi-3 Mini-3.8B, Qwen-3B
Repetitions:    A: N=10, B: N=8, C: N=5
Total runs:     (10 + 8 + 5) × 4 models = 92 model-scenario pairs

Duration:       2 hours wall-clock (parallelizable via Ollama multi-model)
Data captured:  Per model × scenario: latencies, accuracy, KG compliance, MMCI levels
```

### 4.2 Execution Protocol

```
# Setup
1. Initialize Ollama with 4 models
2. Warm up each model (inference cache priming)
3. Initialize Neo4j with baseline 5G schema (20 UEs, 3 gNBs, 2 RANSlices)
4. Initialize simulator KPI baselines (RSRP, SINR, throughput, latency, handover)

# Per Scenario
5. For fault in [A, B, C]:
   6. For i in 1..N_reps:
      7. Reset simulator to baseline
      8. Inject fault at t=0
      9. Run 4-agent loop with timeout=2s per loop
      10. Collect metrics: detection, diagnosis, planning, execution, recovery
      11. Log all traces (model outputs, KG queries, decisions, outcomes)
      12. Repeat with each model

# Analysis
13. Aggregate metrics:
    - Per-model: mean, std, percentiles (P50, P95, P99)
    - Ensemble: consensus rate, agreement reliability, hallucination rate
    - MMCI: L1-L5 progression curves
14. Generate report: comparison table, radar plots, latency CDF
15. Identify outliers: which (model, scenario) pairs fail? Root cause analysis.

# Artifacts
- benchmark_results.csv (90+ rows × 20+ metrics)
- latency_cdf.png (cumulative distribution)
- consensus_heatmap.png (4 models × agreement rates)
- mmci_levels_progression.png (latency to reach each MMCI level)
- failure_analysis.md (outlier cases documented)
```

---

## Part 5: Expected Results & Interpretation

### Hypothesis

**H1:** Ensemble consensus improves reliability vs. single model  
**H2:** Latency scales with model size (Llama > Mistral > Phi-3 > Qwen)  
**H3:** MMCI L4 (joint decision) is bottleneck; L5 (autonomy) depends on guardrails  
**H4:** Multi-fault (Scenario C) reduces consensus; quorum voting catches disagreements  

### Interpretation Rubble

| Result | Meaning | Next Action |
|---|---|---|
| **Consensus >90% across scenarios** | ✅ Models reliably agree; ensemble is robust | Proceed to deployment |
| **Consensus 70-90%** | ⚠️ Frequent disagreements; watch for patterns | Investigate disagreement types; consider model retraining |
| **Consensus <70%** | ❌ Ensemble unreliable; single model may be better | Debug: which model diverges? Why? |
| **Latency <100ms for all models** | ✅ Edge SLA met; all models deployable | Prioritize by accuracy, not speed |
| **Latency 100-200ms** | ⚠️ Edge SLA tight; consider model pruning or offloading | Trade accuracy vs. latency |
| **Latency >200ms** | ❌ Edge SLA violated; model too slow | Reject model or upgrade edge hardware |
| **KG Compliance 100%** | ✅ Guardrails work; no invalid actions | Validate guardrail covers all fault types |
| **KG Compliance 95-99%** | ⚠️ Rare edge cases violate constraints | Audit violations; update schema if needed |
| **KG Compliance <95%** | ❌ Guardrails failing; system unsound | Stop; redesign KG schema or agent logic |
| **MMCI L5 achieved in <200ms** | ✅ Full autonomy + recovery feasible | Deploy with guardrails |
| **MMCI L5 blocked at L4** | ⚠️ Planning consensus bottleneck | Investigate: model disagreement or timeout? |
| **MMCI L5 never achieved** | ❌ System cannot operate autonomously | Fallback to reactive mode or human oversight |

---

## Part 6: Deliverables

```
📁 thesis/experiments/benchmark/
  ├── scenarios/
  │   ├── scenario_a_single_fault.py
  │   ├── scenario_b_contention.py
  │   ├── scenario_c_cascade.py
  │   └── scenario_runner.py
  ├── models/
  │   ├── llama_agent.py
  │   ├── mistral_agent.py
  │   ├── phi3_agent.py
  │   ├── qwen_agent.py
  │   └── ensemble.py
  ├── metrics/
  │   ├── individual_metrics.py
  │   ├── ensemble_metrics.py
  │   ├── mmci_alignment.py
  │   └── analysis.py
  ├── results/
  │   ├── benchmark_results.csv
  │   ├── latency_cdf.png
  │   ├── consensus_heatmap.png
  │   ├── mmci_progression.png
  │   └── failure_log.txt
  ├── config/
  │   ├── simulator_config.yaml
  │   ├── kg_schema.yaml
  │   └── benchmark_config.yaml
  └── README.md (this template, expanded with actual code)
```

---

## Related Pages

- [[analyses/comparison-matrix]] — Where thesis fits in 12-paper corpus
- [[analyses/gap-analysis]] — What gaps this benchmark tests
- [[analyses/risk-profile]] — How guardrails are validated
- [[sources/multiagent-bench-2025]] — Task/Coordination Score details
- [[sources/berkeley-cs294-llm-eval]] — LLM eval best practices
- [[sources/al-haj-ali-2025-mmci]] — MMCI framework levels
