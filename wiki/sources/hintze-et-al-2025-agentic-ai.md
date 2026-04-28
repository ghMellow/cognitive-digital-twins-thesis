---
title: Agentic AI Architectures, Taxonomies & Evaluation
type: source
created: 2026-04-28
updated: 2026-04-28
authors: [Hintze et al.]
year: 2025
tags: [agentic-ai, architecture, evaluation, taxonomy, multi-agent-systems, cognitive-architecture, LLM-agents, POMDP, CLASSic-framework]
thesis-contribution: 2-evaluation
---

## Main Contribution

Survey paper providing a unified 6-dimensional taxonomy of agentic AI architectures and formalizing agents as POMDP loops with a production-ready evaluation framework (CLASSic: Cost, Latency, Accuracy, Security, Stability).

---

## Summary

**Problem:** Agentic AI systems are proliferating without unified design principles or evaluation standards. Teams build autonomous loops with LLMs as control centers, but architectural decisions (memory strategy, reasoning depth, orchestration pattern) are scattered across frameworks (AutoGen, LangGraph, CrewAI, MetaGPT).

**Method:** Taxonomy decomposes any agent system into 6 modular dimensions:
- **Core Components** — Perception, Memory (dual-stream: working + long-term), Action, Profiling
- **Cognitive Architecture** — Planning strategies (ReAct → Tree of Thoughts → LATS → reasoning models), Reflection mechanisms (Reflexion, CRITIC)
- **Learning** — In-context learning, fine-tuning, RLHF, skill libraries
- **Multi-Agent Systems** — Orchestration topologies (Chain/Waterfall, Star/Hub-and-spoke, Mesh/Swarm)
- **Environments** — Practical domains (Web, OS/Desktop, Software Engineering, Enterprise, Healthcare, Finance, Robotics)
- **Evaluation Framework** — CLASSic: Cost (token complexity), Latency (response time), Accuracy (success rate), Security (robustness), Stability (variance across runs)

Agents formalized as $(S, O, M, T, \pi)$ — POMDP with cycle: **Perception → Memory Update → Cognitive Planning → Action Execution → Feedback**.

**Results:** 
- Demonstrates trade-off curves: ReAct achieves medium token complexity with grounded reasoning; Tree of Thoughts has exponential token complexity $b^d$ but enables backtracking; reasoning models (o1/o3) shift compute to inference with variable success; CRITIC pattern (tool-interactive validation before action) reduces hallucination-in-action risk.
- Multi-agent patterns: MAKER (Worker + Verifier separation) reduces error accumulation on long chains; DyLAN (importance routing) reduces costs by silencing irrelevant agents.
- Cross-domain benchmarks: WebArena (~15% long-horizon success), OSWorld (60.76% CoAct1), SWE-Bench (repository-scale), GAIA (multi-step tool use), Robotouille (async penalty: 47% → 11%).

**Limitations:**
- 60% lab research vs. production reality (dynamic DOM, auth flows, network errors not covered by benchmarks)
- Hierarchical agents exponentially expensive in token budget
- Hallucination-in-action irresolved despite CRITIC and validation patterns
- Security: prompt injection bypassed by adaptive attackers; MCP expands attack surface
- Long-horizon tasks suffer infinite loops without metacognitive exit criteria
- Async environments catastrophic: 11% success vs 47% in synchronous settings

---

## yt

**"Here's what they did"** — Unified formalism for agentic systems: every agent is a **POMDP control loop** where LLM occupies only the local reasoning node. Orchestration, memory retention, action verification, and tool governance are **first-class citizens**, not afterthoughts.

**"Why it matters"** — Most agent systems treat the LLM as the center and bolt on memory/tools. This paper says the opposite: the **system is the center**, and the LLM is one component. This flip in thinking explains why LangGraph (explicit state machine) wins over free-form loops in production.

**"How do we use it?"** — Direct application to your CDT:
- **Cost optimization**: Trade-off curves show ReAct (linear) dominates Tree of Thoughts (exponential) on constrained hardware (M4 Pro).
- **Reasoning validation**: CRITIC pattern (tool-interactive before committing) is your Planning Agent checking Neo4j before proposing actions.
- **Evaluation schema**: CLASSic framework is your Contribution 2 operational metrics—you have Cost (token usage), Latency (5G SLA), Accuracy (fault detection), Stability (run-to-run variance).

**"Under the hood"** — 6 modular dimensions that decompose any architecture. Memory is the critical lever: dual-stream (context window + external store with retention policy), not just single buffer. Multi-agent topologies: Chain (your Perception→Reasoning→Planning→Communication waterfall), Star (with controller), Mesh (swarm, not applicable).

**"The catches"** — Latency in async environments is catastrophic (11% vs 47% success). Long-horizon tasks loop infinitely without metacognitive exit. Reasoners (o1/o3) are opaque and expensive. Security still unresolved. But these are meta-problems, not blockers for thesis.

---

## Value for Thesis

**Areas deepened:**

1. **Evaluation Framework (Contribution 2)** — CLASSic provides operational structure for your multi-dimensional evaluation. You already had Cost/Latency/Accuracy; CLASSic adds Security (intentionally deprioritized in 5G context) and **Stability** (critical for critical infrastructure—must report variance, not just mean). This is your exact contribution: embedding autonomy progression **within** CLASSic's stability dimension.

2. **Cognitive Architecture Justification** — Table 4 shows ReAct as optimal for 7-8B local models. You defend this choice explicitly: Tree of Thoughts exponential cost makes it infeasible on consumer hardware; reasoning models require inference-time compute you don't budget; Reflexion is feasible but secondary to ReAct baseline. **This answer satisfies advisor push-back on "why not o1?"**

3. **Multi-Agent Pattern (Contribution 1)** — MAKER (Worker + Verifier) validates your Reasoning→Planning separation. The paper proves Worker+Verifier with cross-examination reduces error accumulation vs. single monolithic agent—directly justifies your architecture.

4. **Memory Layer (Architecture Refinement)** — Validates Eclipse Ditto as symbolic state store (ChatDB-style SQL memory for structured KPIs + temporal paging). MemGPT-style external controller for long-term event store complements local LLM context window—this is exactly your MD-based event log + Neo4j.

**Pros:**

- **POMDP formalization** — reframes your CDT as control system, not "prompt pipeline". Scientific credibility boost.
- **LangGraph validation** — explicitly positions flow engineering with state machines as industry standard. Defends your orchestration choice vs. AutoGen free-form.
- **CRITIC pattern** — tool-interactive validation before action commitment is documented, citable design pattern. Your Planning Agent's Neo4j check is CRITIC instantiation.
- **CLASSic framework** — provides operational measurement schema for Contribution 2. Transforms evaluation from ad-hoc to principled.
- **BOLAA empirical** — proves multi-agent specialization beats single large model—justifies 7B multi-agent vs. 70B single model trade-off.
- **Multi-agent agreement validation** — paper documents multi-agent debate as evaluation method for reasoning without ground truth. Your approach (3 LLMs on same fault scenario → consensus) is explicitly supported.

**Cons:**

- **No 5G domain coverage** — paper doesn't include telecom benchmarks. You need RESTART + WirelessAgent for domain specificity.
- **No Eclipse Ditto or KG integration** — memory section covers MemGPT/ChatDB but not how to formalize OWL constraints as action space guards. You build this bridge.
- **Reasoning evaluation gap** — paper explicitly names this as open problem (Section 7). Confirms your Contribution 2 is genuinely novel—no off-the-shelf solution exists.

**Notes for advisor:**

> **Q: "Why ReAct and not Tree of Thoughts or reasoning models?"**
> 
> Table 4 in Hintze et al. shows cognitive architecture token complexity. ReAct is linear (best for latency-constrained tasks like 5G RAN with <50ms SLA), Tree of Thoughts is exponential $b^d$ (prohibitive on 7-8B consumer hardware), and reasoning models require inference-time compute we don't budget. ReAct + Reflexion-style self-correction is the optimal point in the accuracy/latency trade-off for constrained hardware.

> **Q: "How do you evaluate Reasoning Agent output without ground truth?"**
>
> CLASSic framework (Hintze et al., Section 7) names this as critical gap. Our multi-layer solution: Perception Agent uses classical metrics (F1, precision) with simulator ground truth; Reasoning Agent uses **multi-agent agreement** (same fault scenario, 3 LLMs, consensus on root cause) + **KG-based validation** (Neo4j constraints verify internal consistency of diagnosis); Planning Agent's output is verifiable (action against operational KPI bounds); Communication Agent uses readability + completeness scores. This addresses the exact open problem Hintze et al. identifies.

> **Q: "Isn't your multi-agent architecture overcomplicated?"**
>
> MAKER pattern (Hintze et al., Section 5.3) demonstrates Worker+Verifier reduces error accumulation on long reasoning chains. On million-step tasks, separate agents with specialized system prompts achieve near-zero hallucination vs. monolithic agent. Our 4-agent pipeline (Perception→Reasoning→Planning→Communication) is a constrained instantiation of this proven pattern—each agent's output is verifiable before hand-off.

### Structural dimensions

- **Supported topic:** Contributions 1 (CDT architecture validation), 2 (CLASSic evaluation framework), 3 (cognitive architecture choice).
- **Gap closed:** Methodological—provides principled framework for evaluating agentic systems beyond accuracy. Empirical—validates multi-agent specialization vs. monolithic alternatives.
- **Key concepts:** 
  - POMDP (agent control formalization)
  - CLASSic (evaluation dimensions)
  - Cognitive Architectures (ReAct, Tree of Thoughts, LATS, Reflexion, CRITIC)
  - Multi-Agent Topologies (Chain, Star, Mesh)
  - Memory architecture (dual-stream: working + long-term)
  - Tool-interactive validation (CRITIC pattern)
  - Multi-agent agreement (for evaluation without ground truth)
- **Tensions:** None direct contradictions. Complements Zheng et al. (CDT definition) and MultiAgentBench (operational metrics).
- **Scaffolding position:** Contribution 2 (Evaluation Framework) — primary. Contribution 1 (Architecture validation of multi-agent pattern) — secondary.

## Concepts introduced

- [[cognitive-architecture]]
- [[agentic-dt-risk-taxonomy]] (alignment with CLASSic security dimension)
- [[mmci-framework]] (complementary to CLASSic for autonomy progression)
- [[multi-agent-systems]] (theoretical foundation for separation patterns)

## Related pages

- [[scaffolding-tesi]]
- [[sources/multiagent-bench-2025]] (complementary evaluation metrics)
- [[sources/berkeley-cs294-llm-eval]] (multi-agent agreement for reasoning eval)
- [[sources/biju-2024-langgraph]] (orchestration validation)
- [[gap-analysis]] (addresses Gap 1.3 reasoning eval, Gap 2.1 multi-modal validation)
- [[benchmark-template]] (CLASSic instantiation for 5G fault scenarios)
- [[working-hypotheses/agentic-pipeline-synthesis]] (4-agent architecture justification)
