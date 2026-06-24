---
title: "RecursiveMAS: Recursive Multi-Agent Systems"
type: source
created: 2026-05-23
updated: 2026-05-23
sources: [raw/papers/a.11_Recursive Multi-Agent Systems/paper.md, raw/papers/a.11_Recursive Multi-Agent Systems/valore-tesi.md]
tags: [multi-agent-systems, latent-space, recursive-computation, scaling, MAS-architecture, 2026]
---

# RecursiveMAS — Recursive Multi-Agent Systems

**One-line summary:** First paper to extend recursive language model scaling from single-model to multi-agent systems, enabling heterogeneous agents to collaborate entirely in latent space via a lightweight RecursiveLink module, achieving +8.3% accuracy, 2.4× speedup, and 75.6% token reduction vs text-based MAS.

---

## Metadata

| Field | Value |
|---|---|
| **Authors** | Xiyuan Yang, Jiaru Zou, Rui Pan, et al. |
| **Affiliations** | UIUC, Stanford, NVIDIA, MIT |
| **arXiv** | 2604.25917v1 [cs.AI] |
| **Date** | 28 Apr 2026 |
| **Type** | Methods + Empirical + Theoretical |
| **Domain** | Multi-agent systems, recursive computation, latent-space communication |

---

## Core Contribution

RecursiveMAS casts an entire heterogeneous MAS as a unified latent-space recursive computation. Each agent acts as an RLM (Recursive Language Model) layer, passing hidden states — not text — to the next agent. The loop closes after the last agent feeds its latent outputs back to the first agent, iterating for `n` recursion rounds. Only the final round produces textual output.

**RecursiveLink (ℛ):** The connecting module — a 2-layer residual MLP:
- **Inner link** (`ℛ_in`): feeds last-layer hidden states back as input embeddings within the same agent during autoregressive generation (latent thoughts generation)
- **Outer link** (`ℛ_out`): bridges hidden representations across heterogeneous agents with different embedding dimensions

**Training:** 2-phase Inner-Outer Loop — inner loop warm-starts each agent independently via cosine regression; outer loop trains the full system via cross-entropy backpropagated through all recursion rounds. Only RecursiveLink weights are updated (13.12M params, 0.31% of total).

---

## Four Collaboration Patterns

| Pattern | Agents | Description |
|---|---|---|
| **Sequential** | Planner → Critic → Solver | Chain-of-agents for progressive decomposition |
| **Mixture** | Math + Code + Science + Summarizer | Parallel domain specialists + aggregator |
| **Distillation** | Expert + Learner | Knowledge transfer from large to small model |
| **Deliberation** | Reflector + Tool-Caller | Inner thinking + external tool invocation |

---

## Key Results

**Accuracy vs Recursive-TextMAS baseline (9 benchmarks):**

| Round | Accuracy gain | Speedup | Token reduction |
|---|---|---|---|
| r=1 | +3.4% | 1.2× | 34.6% |
| r=2 | +6.0% | 1.9× | 65.5% |
| r=3 | +7.2% | 2.4× | 75.6% |

**Training cost:** $4.27 (RecursiveMAS) vs $6.64 (LoRA) vs $9.67 (Full-SFT) — lowest cost, highest accuracy.

**Cross-pattern results (r=3):**
- Mixture: +6.2% over best domain specialist
- Deliberation: +4.8% over standalone tool-caller
- Distillation: +8.0% for learner, retaining 1.5× speedup over expert

---

## Theoretical Results

**Runtime complexity:** RecursiveMAS O(N·m·d_h²) vs text-based O(N·m·|V|·d_h). Since d_h ≪ |V|, latent communication replaces expensive vocabulary-space decoding.

**Gradient Stability Theorem (4.1):** Text-based MAS training during recursion → gradient vanishing (‖∂/∂h‖ → 0). RecursiveLink → near-constant gradients (‖∂/∂h‖ ≈ 1). Formally proven, not just empirical.

---

## Limitations

- Requires access to hidden states → **incompatible with cloud API** (OpenAI, Anthropic, Ollama API-only). Needs full local deployment with direct model access.
- Latent thoughts are not human-interpretable — communication happens entirely in embedding space.
- Tested only on closed-form benchmarks (MATH, science, medicine, code). No real-world production tasks.
- No per-agent quality evaluation — only end-to-end output measured.

---

## Value for Thesis

**Relevant for:**
1. **Ch. 3 — Related Work:** MAS 2026 taxonomy reference; Sequential pattern validates my pipeline architecture classification; small-model (1-10B) multi-agent performance confirms thesis hypothesis.
2. **Ch. 5 — Evaluation Methodology:** The absence of per-agent evaluation in RecursiveMAS is a direct motivation for Contribution 2 — cite explicitly as a gap this paper leaves open.
3. **Ch. 8 — Future Work:** Latent-space communication as potential evolution once explainability requirement is relaxed (fully-autonomous regime).

**Not applicable for:**
- Direct implementation (no hidden state access via Ollama)
- Domain-specific 5G benchmark comparison (no telco domain)
- CDT architecture reference (no Digital Twin layer, no persistent state)

**Relator answer:** RecursiveMAS operates on an orthogonal axis to my CDT — it optimizes inter-agent communication for closed reasoning tasks; I design a cognitive loop with persistent state, physical-world synchronization (Eclipse Ditto), constraint validation (Neo4j), and explainability for human operators. The methodological gap it leaves open (no per-agent evaluation) directly motivates my Contribution 2.

---

## Related Pages

- [[multi-agent-systems]]
- [[mas-patterns]]
- [[mas-agent-patterns]]
- [[multi-agent-frameworks]]
- [[scaffolding-tesi]]
- [[gap-analysis]]
