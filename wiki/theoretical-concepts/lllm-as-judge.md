---
title: LLM-as-Judge
type: concept
created: 2026-04-30
updated: 2026-04-30
sources: [multiagent-bench-2025, berkeley-cs294-llm-eval]
tags: [evaluation, methodology, llm-judge, non-verifiable, agentic-systems]
---

# LLM-as-Judge

Evaluation technique that uses a language model to score the output of another model or agent when no deterministic oracle exists. Core component of the thesis evaluation framework for non-verifiable agent dimensions.

## Canonical Definition

**Berkeley CS294 (LLM Agent Evaluation):** Using an LLM (e.g., GPT-4, Llama 3.1 70B) as an automated evaluator for open-ended outputs — outputs where classical metrics (accuracy, F1) fail because no single correct answer exists.

**MultiAgentBench / MARBLE (Zhu et al., 2025):** LLM-based scoring of Communication Score and Planning Score on a 1–5 scale, used alongside deterministic Task Score to capture coordination quality across multi-agent scenarios.

---

## Strict Implementation Principle

> LLM-as-Judge is a **last-resort oracle** — it activates only when no external ground truth is available. Where a simulator, a KG constraint, or an API execution result exists, that external validator takes precedence unconditionally.

This is the key distinction between a rigorous and a naive implementation. Using it everywhere is a methodological weakness; using it only where necessary is a defensible design choice.

---

## Task Taxonomy — Where It Applies

| Task Type | Definition | Evaluation Method |
|---|---|---|
| **Close-ended** | Fixed, discrete answer space (e.g., sentiment classification) | Accuracy, F1 — no judge needed |
| **Verifiable** | Ground truth exists via oracle (simulator, KG, execution) | Rule-based / pass-fail — no judge needed |
| **Open-ended / Non-verifiable** | No single correct answer (e.g., root-cause explanation, report quality) | ✅ LLM-as-Judge applies here |
| **Dynamic benchmark** | Test cases that evolve to prevent data contamination | LLM judge + multi-run consistency |

---

## Strict Implementation Protocol

1. Classify the evaluation dimension as **verifiable** or **non-verifiable**
2. If verifiable → use external oracle; stop here
3. If non-verifiable → define a fixed scoring rubric (per-dimension, not holistic)
4. Anchor the judge prompt with: task description, agent output, relevant evidence, constraint set
5. Require **structured output** from the judge (JSON with per-dimension scores)
6. Run multiple judges or multiple runs — report agreement, not just mean
7. Calibrate against human evaluation on a held-out subset
8. Report judge bias risks explicitly alongside results

---

## Evaluation Rubric — Recommended Dimensions

| Dimension | What It Checks |
|---|---|
| **Factual Grounding** | Consistency of the output with observed signals and retrieved evidence |
| **Causal Coherence** | Logical connection between cause and effect in the reasoning chain |
| **Completeness** | Coverage of relevant factors for the anomaly or task at hand |
| **Constraint Awareness** | Compliance with operational constraints (e.g., 3GPP rules, KG bounds) |
| **Actionability** | Whether the output supports a concrete next step |
| **Clarity** | Internal consistency and absence of contradictory statements |

---

## Thesis Agent Mapping

Where each agent's output lands in the evaluation stack:

| Agent | Output Type | Primary Validator | LLM-as-Judge |
|---|---|---|---|
| **Perception Agent** | Structured anomaly signal | Simulator ground truth | ❌ Not needed |
| **Planning Agent** | Proposed reconfiguration action | KG constraint check (Neo4j) | ❌ Not needed |
| **Reasoning Agent** | Root-cause explanation (NL) | No external oracle | ✅ Required |
| **Communication Agent** | Diagnostic report (NL) | No external oracle | ✅ Required |
| **Whole pipeline** | KPI recovery in simulator | Throughput / RSRP delta | ❌ Outcome validity via simulator |

---

## LLM-as-Judge vs Human Evaluation

| Aspect | Human Evaluation | LLM-as-Judge |
|---|---|---|
| **Speed** | Slow, expensive | Fast, scalable |
| **Reproducibility** | Low (inter-annotator disagreement) | Medium (prompt-sensitive) |
| **Correlation with human judgment** | Gold standard | High (when rubric is explicit) |
| **Interpretability** | High | Low without structured output |
| **Bias** | Subjective; varies by evaluator | Style bias; favors fluency over correctness |
| **Cost** | High | Low (local models viable for judge role) |

---

## Known Biases and Mitigations

| Bias | Description | Mitigation |
|---|---|---|
| **Verbosity bias** | Longer outputs rated higher regardless of quality | Cap output length; evaluate density not volume |
| **Self-similarity bias** | Judge prefers outputs stylistically close to its own training | Use a judge from a different model family than the evaluated agent |
| **Autoreferentiality** | LLM-judged metrics validated only by LLM metrics | Always pair with at least one external outcome metric |
| **Prompt sensitivity** | Score changes with minor prompt rewording | Fix prompt template; run ablation on wording |
| **Hallucinated justifications** | Judge invents reasons for a score | Require evidence anchoring in judge prompt |

---

## MultiAgentBench Connection

MARBLE uses LLM-as-Judge for two coordination metrics:

```
Coordination Score (CS) = (C_score + P_score) / 2
  C_score = communication quality  (1–5, LLM-based)
  P_score = planning quality        (1–5, LLM-based)
```

This is methodologically transferable to the thesis — with the important caveat that MARBLE applies LLM judging to **all** coordination dimensions without an external oracle. The thesis improves on this by using LLM-as-Judge only for Reasoning and Communication, while grounding Perception and Planning in deterministic validators.

---

## Academic Positioning

When asked by the advisor how LLM-based evaluation is justified:

> "LLM-as-Judge is adopted only for evaluation dimensions where no deterministic oracle exists — specifically, Reasoning Agent root-cause explanations and Communication Agent reports. For all other agents, evaluation is grounded in simulator KPIs or KG constraint validation. This hybrid design limits subjectivity to the dimensions where it is unavoidable, and follows the same methodological separation between Task Score and Coordination Score demonstrated in Zhu et al. (2025)."

---

## Related Pages


- [[sources/multiagent-bench-2025]] — Source: MARBLE framework, LLM-based CS scoring
- [[sources/berkeley-cs294-llm-eval]] — Source: Taxonomy verifiable/non-verifiable, outcome validity
- [[theoretical-concepts/cognitive-digital-twin]] — System being evaluated
- [[theoretical-concepts/classic-evaluation-framework]] — Broader evaluation context
- [[scaffolding-tesi]] — Integration in Contribution 2 (Evaluation Framework)
- [[analyses/benchmark-template]] — Operational benchmark design
