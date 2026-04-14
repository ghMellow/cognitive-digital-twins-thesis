---
title: Risk Profile — Burr Risk Taxonomy + Thesis Guardrails
type: analysis
created: 2026-04-14
updated: 2026-04-14
sources: [sources/burr-et-al-2026-agentic-dt]
tags: [risk-governance, burr-taxonomy, guardrails, safety]
---

# Risk Profile — Agentic DT Risk Governance

**Scopo:** Applicare la tassonomia di rischio Burr (2026) al sistema tesi. Quale configurazione (I, T, A) il sistema realizza? Quali rischi emergono? Come mitigarli?

**Framework:** 27 configurazioni Burr × 3 dimensioni (Intent, Transparency, Agency) = 3×3×3 matrix.

---

## Burr Taxonomy Quick Recap

**3 Dimensioni:**

1. **Intent (I):**
   - **I=0:** No explicit intent (legacy automation)
   - **I=1:** Unclear/brittle intent specification
   - **I=2:** Clear, formal intent (intended state captured in KG)

2. **Transparency (T):**
   - **T=0:** Black box (model behavior opaque)
   - **T=1:** Partial transparency (trace decisions, but why is unclear)
   - **T=2:** Full transparency (explain reasoning in human-readable form)

3. **Agency (A):**
   - **A=0:** No agency (no autonomous decisions)
   - **A=1:** Constrained autonomy (predefined playbooks)
   - **A=2:** Full autonomy (agent decides without constraints)

**27 Configurations = 3^3** with risk profiles:
- ✅ **Safe:** (I:2, T:2, A:0) = "Explicit intent, fully transparent, no autonomy" = reactive system
- ✅ **Safe:** (I:2, T:2, A:1) = "Active Steering" = Zheng CDT ideal; agentic but constrained + explainable
- 🔴 **Unsafe:** (I:2, T:0, A:2) = "Governor Trap" = agent executes unclear decisions autonomously (performative prediction lock-in)
- 🔴 **Unsafe:** (I:0, T:0, A:2) = "Wild Agent" = black-box model with full autonomy (worst case)

---

## Thesis System Configuration (Target)

### Configuration: **(I:2, T:2, A:1)** = Active Steering ✅

| Dimension | Thesis Realization | Evidence |
|---|---|---|
| **Intent (I:2)** | Clear, formal intent in **DIKG (Intent KG)** | User specifies net intent: (:NetIntent {type: "maximize_reliability", target_sinr: -100dB, max_latency: 100ms}) → stored in Neo4j DIKG → Planning Agent queries and constrains decisions |
| **Transparency (T:2)** | Full transparency via **decision traces + KG constraints** | (a) Activity log: each Planning Agent decision logged with source reasoning (which Reasoning Agent output, which KG shape check, which alternative rejected) (b) Explainability: generate human-readable trace ("Selected gNB-B because RSRP > -105dB AND throughput_target not exceeded AND gNB-B has 2 free slots") |
| **Agency (A:1)** | Constrained autonomy via **KG shape validation + multi-agent consensus** | (a) Planning Agent generates decisions autonomously but ALL must pass Neo4j shape validation (b) If consensus vote < 3/4 models agree, decision escalated to human review queue (not auto-executed) (c) Guardrails: latency timeout (if Planning takes >50ms, timeout triggers fallback rule) |

**Burr Risk Profile:** ✅ **SAFE for deployment** as long as guardrails hold.

---

## Risk Cascade: Thesis Threats + Mitigations

### **Risk R1: Intent Specification Brittleness** (Could drift to I:1)

**Threat:** DIKG becomes stale or ambiguous. Example: "maximize_reliability" poorly defined. Does it mean RSRP only? Include handover success? Trading latency for coverage?

| Aspect | Details |
|---|---|
| **Severity** | 🟡 **High** — Leads to misaligned decisions |
| **Trigger** | (a) User intent not updated for new 5G scenario (b) Reasoning Agent infers spurious intent from conflicting KG edges |
| **Cascade** | Drift to (I:1, T:2, A:1) = poorly-defined but transparent autonomy = agent executes unclear commands flawlessly |
| **Mitigation** | ✅ **Multi-level intent validation** (a) Reasoning Agent must parse intent from DIKG and return confidence score (>0.8 required; else error) (b) Planning Agent compares decision against original intent KG edge (traces back reasoning chain to root intent) (c) Quarterly review: audit auto-executed decisions for drift (if >5% mismatch, trigger intent rewrite) |
| **Monitoring** | Monthly drift audit (automated): sample N=100 executed decisions → compare output KPI against stated intent KP target |

---

### **Risk R2:Transparency Degradation** (Could drift to T:1 or T:0)

**Threat:** LLM reasoning becomes opaque. Model hallucination occurs but hard to detect because explanation looks plausible.

| Aspect | Details |
|---|---|
| **Severity** | 🔴 **Critical** — Governor trap entry point |
| **Trigger** | (a) LLM model degrades (quantization artifacts) (b) Ensemble consensus masks disagreement → majority vote hides dissent (c) KG validation catches structural errors but not semantic hallucinations (e.g., "select gNB-C" for reasons not in KG) |
| **Cascade** | (I:2, T:1, A:1) or worse (I:2, T:0, A:1) = Agent fully autonomous but reasons are unclear → operator trust erodes → force manual override (defeats CDT purpose) OR operator blindly trusts = Governance mode (I,C,A) entrenchment |
| **Mitigation** | ✅ **Multi-stage explainability** (a) **Stage 1 (Semantic):** Reasoning Agent outputs reasoning chain (chain-of-thought) — compare chain tokens to KG facts (using vector similarity: do key entities in chain exist in KG?) (b) **Stage 2 (Consensus):** If 2+ models disagree in chain, escalate; if all 4 agree, proceed. (c) **Stage 3 (Grounding):** Execute decision, observe outcome (KPI delta). Do outcomes match prediction in reasoning chain? If actual_kpi ≠ predicted_kpi by >ε, log as "transparency failure" for audit. |
| **Monitoring** | Real-time: measure "reasoning-outcome alignment" = cosine(predicted_kpi_in_chain, actual_kpi_post_execution). Target >0.8. If <0.7 for 3+ consecutive cycles, escalate to manual oversight. |

---

### **Risk R3: Agency Overreach** (Could drift to A:2)

**Threat:** Constraints become lax; Planning Agent bypasses guardrails. Example: timeout fires too often → fallback rule starts executing without Planning Agent cognition → system drifts to reactive mode OR Planning learns to avoid timeout by making faster but wrong decisions.

| Aspect | Details |
|---|---|
| **Severity** | 🟡 **High** — Leads to unsafe decisions |
| **Trigger** | (a) Latency pressure: 5G SLA <100ms but Planning Agent routinely takes 60ms (timeout=50ms) → fallback triggers often (b) Operator disables guardrails temporarily for emergency; never re-enables (c) Adversarial: attacker crafts inputs that repeatedly trigger timeout → learns system will fallback → injects fallback command |
| **Cascade** | (I:2, T:2, A:2) = fully autonomous without constraints = dangerous |
| **Mitigation** | ✅ **Layered timeout + escalation** (a) **Soft timeout (40ms):** If Planning takes >40ms, log warning but continue (don't interrupt) (b) **Hard timeout (50ms):** If still running at 50ms, escalate to Supervisor Agent (not fallback rule) (c) **Supervisor logic:** Can choose (1) fallback, or (2) defer decision to next cycle (queued), or (3) ask for human input. (d) **Learning:** Track timeout frequency; if >20% of planning calls timeout, alert operator ("latency pressure detected; consider increasing Planning compute or simplifying constraint set") |
| **Monitoring** | Real-time: timeout frequency + escalation reasons. If timeouts >20/hour, manual investigation. |

---

### **Risk R4: KG Constraint Capture Incompleteness** (Intent Drift)

**Threat:** VValid decision in practice but violates KG shape → Planning rejects it → System appears inflexible or broken.

| Aspect | Details |
|---|---|
| **Severity** | 🟡 **High** — UX/trust issue |
| **Trigger** | (a) New 5G scenario (edge case) not covered by training KG schema (b) Operator wants to override constraint for legitimate reason (emergency) but system refuses |
| **Cascade** | Operator loses trust → manually overrides repeatedly → system downgraded to manual-only (CDT purpose defeated) |
| **Mitigation** | ✅ **Constraint override + audit** (a) Planning Agent can propose override with explanation ("violating throughput_max because emergency slice requires X") (b) Override logged and flagged for post-hoc review (c) If override is legitimate, update KG schema for future (d) If override causes problems, revert and block similar overrides |
| **Monitoring** | Weekly override audit: how many overrides? What % were beneficial vs. harmful? If beneficial rate >10%, schema is too strict → relax constraints. |

---

## Risk Matrix: Thesis vs. Base Case

**Scenario 1: Baseline System (No CDT)**
- Config: (I:1, T:0, A:1) = Rule-based automation
- RSRP_target = -100dB? → fixed rule "if RSRP < -105, migrate UE" → executes without reasoning
- Risk: brittle, cannot adapt to new failures

| Risk | Severity | Baseline | Thesis |
|---|---|---|---|
| Intent brittleness | 🟡 High | ❌ High (rules hard-coded) | ✅ Low (KG update propagates) |
| Transparency | 🟡 High | ❌ Low (why rule fired?) | ✅ High (trace reasoning) |
| Hallucination | 🟢 Low | ✅ None (no reasoning) | ⚠️ Medium (mitigated by KG + consensus) |
| Autonomy overreach | 🟡 High | ❌ High (rules run blind) | ✅ Low (guardrails enforced) |
| **Overall Risk** | – | 🔴 **High** | ✅ **Low** |

**Scenario 2: LLM-Only (No KG Guardrails)**
- Config: (I:2, T:1, A:2) = Agent fully autonomous, but reasoning opaque
- LLM outputs decision; humans trust it or not
- Risk: Governor trap

| Risk | Severity | LLM-Only | Thesis |
|---|---|---|---|
| Intent brittleness | 🟡 High | ❌ LLM can misinterpret intent | ✅ KG validates intent |
| Transparency | 🟡 High | ❌ LLM chain-of-thought hard to verify | ✅ Chain grounded in KG facts |
| Hallucination | 🔴 Critical | ❌ LLM can fabricate reasoning | ✅ Consensus + KG validation catches |
| Autonomy overreach | 🔴 Critical | ❌ No guardrails; LLM decides freely | ✅ Hard constraints (KG shapes) |
| **Overall Risk** | – | 🔴 **Critical** | ✅ **Low** |

---

## Guardrails Implementation Checklist

| Guardrail | Thesis Implementation | Verification |
|---|---|---|
| **KG Shape Validation** | Neo4j APOC shape constraints on every Planning Agent output | Unit test: invalid output rejected; valid output passes |
| **Multi-Agent Consensus** | 4-model ensemble with ≥3/4 agreement required for execution | Integration test: disagreement triggers escalation |
| **Latency Timeout** | Planning hard timeout at 50ms; escalates to Supervisor | Performance test: timeout under synthetic load; escalation logs |
| **Transparency Log** | Every decision traces (model, reasoning chain, constraints checked, overrides) | Audit test: log all fields; replay decision from log |
| **Intent Drift Detection** | Quarterly audit comparing executed decisions vs. intent KG | Compliance test: automated drift scoring |
| **Emergency Override** | Human can override with logged justification + mandatory audit | Access control test: override requires auth; audit trail intact |

---

## Operational Prerequisites for Deployment

| Prerequisite | Owner | Timing |
|---|---|---|
| **Regular KG Review** | Domain expert (5G telecom) | Monthly |
| **Transparency Audit** | Operations team | Weekly |
| **Intention Audit** | Stakeholders (e.g., network operator) | Quarterly |
| **Incident Review** | Security + ops | As-needed (any override or escalation) |
| **Model Update Protocol** | ML team | Every 6 months or post-incident |

---

## Summary: Risk Profile Verdict

**Configuration:** (I:2, T:2, A:1) = **Active Steering** ✅  
**Risk Level:** 🟢 **Low** (with guardrails in place)  
**Deployment Readiness:** ✅ **Yes** (prerequisites must be met)  
**Comparison to Baseline:** 🔴 Baseline (I:1,T:0,A:1) has HIGH risk due to brittle rules  
**Comparison to Alternative LLM-Only:** 🔴 LLM-only (I:2,T:1,A:2) has CRITICAL risk (Governor trap)

---

## Related Pages

- [[sources/burr-et-al-2026-agentic-dt]] — Burr taxonomy details
- [[analyses/gap-analysis]] — How thesis operationalizes governance
- [[analyses/benchmark-template]] — Fault injection verifies guardrails
- [[scaffolding-tesi]] — Cap. 4 architecture with guardrails embedded
