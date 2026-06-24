# Recursive Multi-Agent Systems (RecursiveMAS)

**Authors:** Xiyuan Yang, Jiaru Zou, Rui Pan, Ruizhong Qiu, Pan Lu, Shizhe Diao, Jindong Jiang, Hanghang Tong, Tong Zhang, Markus J. Buehler, Jingrui He, James Zou
**Affiliations:** UIUC, Stanford University, NVIDIA, MIT
**arXiv:** 2604.25917v1 [cs.AI] — 28 Apr 2026
**Project Page:** https://recursivemas.github.io

---

## Abstract

Recursive or looped language models have recently emerged as a new scaling axis by iteratively refining the same model computation over latent states to deepen reasoning. RecursiveMAS extends such scaling principle **from a single model to multi-agent systems**, asking: *Can agent collaboration itself be scaled through recursion?*

RecursiveMAS casts the entire MAS as a unified latent-space recursive computation. It connects heterogeneous agents as a collaboration loop through the lightweight **RecursiveLink** module, enabling:
- In-distribution latent thoughts generation
- Cross-agent latent state transfer

An **Inner-Outer Loop** learning algorithm enables iterative whole-system co-optimization through shared gradient-based credit assignment across recursion rounds.

**Key results (vs. text-based MAS baselines):**
- +8.3% average accuracy improvement
- 1.2×–2.4× end-to-end inference speedup
- 34.6%–75.6% token usage reduction

---

## 1. Introduction

### Motivation

Single LLMs fail at complex tasks due to limited capacity, myopic generation, or inefficient solution-space exploration. Multi-agent systems (MAS) address this by assigning complementary roles to heterogeneous agents. However:

- Prompt-based adaptation can improve context but agents cannot truly improve
- Training entire agents is hard (non-trivial parameter update, sequential latency bottleneck)

### Core Idea

Recast agent collaboration through the lens of **Recursive Language Models (RLMs)**, where each agent acts as an RLM layer, iteratively passing latent representations to the next and forming a looped interaction process.

### RecursiveMAS Components

1. **RecursiveLink (ℛ):** A two-layer residual projection module connecting agents in latent space
   - **Inner RecursiveLink (ℛ_in):** consolidates latent thoughts within each agent between input and output spaces during autoregressive generation
   - **Outer RecursiveLink (ℛ_out):** bridges hidden representations across heterogeneous agents with different model types and sizes

2. **Inner-Outer Loop Training:**
   - *Inner loop:* warm-starts each agent to align latent thoughts with semantic distributions
   - *Outer loop:* trains the outer RecursiveLink at system level via gradients recursively back-propagated across full recursion rounds

---

## 2. Preliminary

### Auto-regressive Generation in Latent Space

Standard transformer $f_\theta(\cdot)$ maps input embeddings $E = [e_1, \ldots, e_t] \in \mathbb{R}^{t \times d_h}$ to last-layer hidden state $h_t$. Latent generation keeps recurrence entirely in continuous representation space:

$$h_{t+1} = f_\theta([E_{\leq t}; h_t])$$

The newly generated $h_{t+1}$ is the model's **latent thought**.

### Recursive Computation (RLM)

A Recursive Language Model reuses the same transformer stack for $n$ forward iterations:

$$H^{(0)} = E, \quad H^{(r)} = f_\theta(H^{(r-1)}), \quad r = 1, \ldots, n$$

### LLM-based Multi-Agent Evolution (Definition 2.1)

A *recursive evolution* is the progressive refinement of $\mathcal{H} = \{H_1, \ldots, H_N\}$, where each agent adjusts its latent representation through iterative interaction with others and its own reasoning state:

$$\mathcal{S}^{(0)} \xrightarrow{\text{Evolve}} \mathcal{S}^{(1)} \xrightarrow{\text{Evolve}} \cdots \xrightarrow{\text{Evolve}} \mathcal{S}^{(n)}$$

### Four Collaboration Patterns

| Pattern | Description | Roles |
|---|---|---|
| **Sequential Style** | Chain of agents that decompose, judge, refine, solve | Planner → Critic → Solver |
| **Mixture Style** | Parallel domain-specialist agents + aggregator | Math/Code/Science Specialists + Summarizer |
| **Distillation Style** | Expert-learner pair for knowledge transfer + efficiency | Expert + Learner |
| **Deliberation Style** | Inner thinker + tool-calling agent, iterative critique | Reflector + Tool-Caller |

---

## 3. Building a Recursive Multi-Agent System

### 3.1 RecursiveLink Design

**Inner Link** — transforms last-layer embedding $h$ within the same agent:

$$\mathcal{R}_\text{in}(h) = h + W_2 \sigma(W_1 h)$$

where $W_1, W_2$ are linear layers, $\sigma(\cdot)$ is GELU activation, and the residual preserves original latent semantics.

**Outer Link** — bridges heterogeneous agents with different hidden dimensions, using an additional linear layer $W_3$:

$$\mathcal{R}_\text{out}(h) = W_3 h + W_2 \sigma(W_1 h)$$

**Why residual connection?** Preserves original semantics, so the network focuses on aligning distributional differences rather than learning a full projection from scratch → more stable and efficient training.

### 3.2 Chain All Agents as a Loop

**Latent Thoughts Generation (inside each agent):**
- Agent $A_1$ receives input context $E_{A_1} = [e_1, \ldots, e_t]$
- Computes $h_t$ at each forward step
- Inner link maps $h_t$ back to input embedding space: $e_{t+1} = \mathcal{R}_\text{in}(h_t)$
- Generates a sequence of latent thoughts $H_{A_1} = [h_t, h_{t+1}, \ldots, h_{t+m}]$

**Cross-Agent Interaction:**
- $H_{A_1}$ is sent to $A_2$ via the outer link: $E_{A_2} \oplus \mathcal{R}_\text{out}(H_{A_1})$
- After all agents complete one pass, the last agent's latent outputs loop back to $A_1$ → closing the recursive loop
- **Only the final recursion round produces textual output** (last agent decodes to text)

### 3.3 Runtime Complexity (Proposition 3.1)

| System | Runtime Complexity |
|---|---|
| Text-based Recursive MAS | $\Theta(N(m|V|d_h + (t+m)^2 d_h))$ |
| RecursiveMAS (latent) | $\Theta(N(md_h^2 + (t+m)d_h^2 + (t+m)^2 d_h))$ |

Since $d_h \ll |V|$ in practice, RecursiveMAS replaces the expensive per-step vocabulary-space decoding cost $m|V|d_h$ with the much more efficient latent-space transformation $md_h^2$.

---

## 4. Learning to Recur as a Whole

### Inner-Loop Training (per agent, parallel)

Objective: train $\mathcal{R}_\text{in}$ to align latent thoughts with semantic distributions from input embeddings:

$$\mathcal{L}_\text{in} = 1 - \cos(\mathcal{R}_\text{in}(H), \text{Emb}_{\theta_i}(y))$$

Cosine regression loss encourages each agent to leverage its inner link to align latent thoughts with ground-truth semantic distributions, eliminating explicit decoding/re-encoding.

### Outer-Loop Training (whole system)

Iteratively optimizes the entire system through outer RecursiveLink $\mathcal{R}_\text{out}$. System unrolled for $n$ forward rounds; cross-entropy loss on final textual prediction:

$$\mathcal{L}_\text{out} = \text{CE}(\mathcal{S}^{(n)}(\mathcal{S}^{(n-1)}(\cdots \mathcal{S}^{(1)}(x))), y)$$

Gradients recursively back-propagated through full computation paths → each outer link gets a shared credit signal based on global contribution to final prediction.

### Gradient Stability (Theorem 4.1)

For confident tokens (entropy $\leq \epsilon$, $\epsilon \ll 1$):
- Text-based SFT during recursion: $\left\|\frac{\partial \mathcal{R}_\text{text}(h)}{\partial h}\right\|_2 \leq O(\epsilon) \ll 1$ → **gradient vanishing**
- RecursiveMAS with $\mathcal{R}$: $\left\|\frac{\partial \mathcal{R}(h)}{\partial h}\right\|_2 \geq \Omega\left(1 - \sqrt{\frac{1}{d_h}\log\frac{1}{\delta}}\right)$ → **near-constant gradients**

Latent-space connections maintain stable gradient propagation, avoiding the gradient vanishing induced by text-based interactions.

---

## 5. Empirical Evaluations

### Agent Configurations

| Collaboration Pattern | Role | Model |
|---|---|---|
| Sequential (Light) | Planner / Critic / Solver | Qwen3-1.7B / Llama3.2-1B-Instruct / Qwen2.5-Math-1.5B |
| Sequential (Scaled) | Planner / Critic / Solver | Gemma3-4B / Llama3.2-3B-Instruct / Qwen3.5-4B |
| Mixture | Code / Science / Math / Summarizer | Qwen2.5-Coder-3B / BioMistral-7B / DeepSeek-R1-1.5B / Qwen3.5-2B |
| Distillation | Learner / Expert | Qwen3.5-4B / Qwen3.5-9B |
| Deliberation | Reflector / Tool-Caller | Qwen3.5-4B / Qwen3.5-4B (with tools) |

### Benchmarks (9 total)

- **Math:** MATH500, AIME2025, AIME2026
- **Science/Medicine:** GPQA-Diamond, MedQA
- **Code Generation:** LiveCodeBench-v6, MBPP+
- **Search QA:** HotpotQA, Bamboogle

### Main Results (Table 2 — vs. Recursive-TextMAS)

| Round | Accuracy Improvement | Inference Speedup | Token Reduction |
|---|---|---|---|
| r=1 | +3.4% (avg) | 1.2× | 34.6% |
| r=2 | +6.0% (avg) | 1.9× | 65.5% |
| r=3 | +7.2% (avg) | 2.4× | 75.6% |

Performance and efficiency advantages grow as recursion depth increases.

### Comparison with Other Methods (Table 3, r=3)

| Method | MATH500 | AIME2025 | AIME2026 | GPQA-D | LiveCodeBench | MedQA |
|---|---|---|---|---|---|---|
| Single Agent (LoRA) | 83.1 | 70.0 | 73.3 | 62.0 | 37.4 | 76.1 |
| MoA | 79.8 | 60.0 | 63.3 | 47.6 | 27.0 | 57.5 |
| TextGrad | 84.9 | 73.3 | 76.7 | 62.5 | 39.8 | 77.2 |
| LoopLM | 84.6 | 66.7 | 63.3 | 48.1 | 24.9 | 56.4 |
| Recursive-TextMAS | 85.8 | 73.3 | 73.3 | 61.6 | 38.7 | 77.0 |
| **RecursiveMAS** | **88.0** | **86.7** | **86.7** | **66.2** | **42.9** | **79.3** |

### Generalization across Collaboration Patterns

- **Mixture-style:** +6.2% over strongest domain specialist (non-trivial cross-domain composition)
- **Deliberation-style:** +4.8% over original tool-calling agent
- **Distillation-style:** +8.0% for learner while retaining 1.5× speed advantage over expert

### Training Cost (Table 5)

| Method | GPU Mem. | Trainable Params | Cost | Avg. Acc. |
|---|---|---|---|---|
| LoRA Training | 21.67 GB | 15.92M (0.37%) | $6.64 | 66.9% |
| Full-SFT | 41.40 GB | 4.21B (100%) | $9.67 | 68.6% |
| **RecursiveMAS** | **15.29 GB** | **13.12M (0.31%)** | **$4.27** | **74.9%** |

RecursiveMAS achieves the **lowest GPU memory, fewest trainable parameters, and lowest cost**, while achieving the highest accuracy.

---

## 6. In-depth Analyses

### RecursiveLink Architecture Ablation (Table 4)

| Design | MATH500 | GPQA-D | LiveCodeBench |
|---|---|---|---|
| 1-Layer | 84.4 | 63.2 | 40.1 |
| Res+1-Layer | 86.7 | 65.3 | 41.4 |
| 2-Layer | 85.6 | 64.5 | 40.5 |
| **Res+2-Layer (ours)** | **88.0** | **66.2** | **42.9** |

The 2-layer residual design consistently outperforms all alternatives. Residual connection delivers additional gains beyond depth alone.

### Semantic Representations across Recursion

Generated answer distributions progressively align with ground-truth distributions as recursion depth increases (visualized via PCA across 500 QA pairs). At r=1, distributions are visibly shifted; by r=3, they largely overlap.

### Optimal Latent Thoughts Length

Performance improves up to m≈80 tokens per agent, then stabilizes across all benchmarks. RecursiveMAS enables effective collaboration with a modest latent budget — sharp contrast to text-based CoT which requires longer, costlier generation.

### Scaling Law (Training vs. Inference)

Increasing inference recursion depth improves systems trained with fewer rounds. Deeper training shifts the performance frontier upward. Strongest results appear when both training and inference recursion are large — complementary scaling effect.

---

## 7. Related Work

- **LLM-based MAS:** Sequential pipelines (CAMEL, ChatDev), mixture-of-experts (MoA), prompt optimization (TextGrad), agent fine-tuning (MALT). RecursiveMAS treats MAS as a unified whole optimized via latent recursion.
- **Recursive/Looped LMs:** LoopLM, Mixture-of-Recursions, recurrent depth reasoning. RecursiveMAS is the **first** to extend recursive scaling from single-model to system-level.

---

## 8. Conclusion

RecursiveMAS introduces a recursive multi-agent framework that:
1. Supports latent-thoughts generation within each agent (inner RecursiveLink)
2. Connects heterogeneous agents through cross-agent latent state transfer (outer RecursiveLink)
3. Optimizes the whole system with an inner-outer loop training paradigm

Theoretical results establish runtime efficiency and gradient stability advantages over text-based alternatives. Empirical results across 9 benchmarks confirm consistent accuracy improvements, inference speedup, and token reduction — with scaling behavior that improves as recursion depth increases.

---

## Key Terminology

- **RecursiveMAS:** The full framework — heterogeneous LLM agents connected as a recursive latent-space collaboration loop
- **RecursiveLink (ℛ):** Lightweight two-layer residual projection module enabling latent state transfer (inner: within agent; outer: across agents)
- **Latent thought:** The last-layer hidden state $h_t$ generated by a transformer at each autoregressive step, fed back as input instead of being decoded to text
- **Recursion round:** One complete forward pass through all agents in the loop; deeper rounds refine the system's latent state
- **Inner-Outer Loop:** Two-stage training paradigm — inner warms up individual agents, outer co-optimizes the full system
- **Recursive Language Model (RLM):** A model that reuses the same transformer stack for $n$ forward iterations in continuous latent space

---

## Connections to Thesis Topics

- Directly relevant to **latent-space communication** between agents as an alternative to text-mediated interaction
- Demonstrates that **system-level recursion** is a viable scaling axis beyond single-model recursion
- **Gradient stability theorem** provides theoretical grounding for why latent collaboration is preferable to text-based MAS training
- The **collaboration pattern taxonomy** (Sequential, Mixture, Distillation, Deliberation) is a clean structural vocabulary for classifying MAS architectures
- **Cost analysis** shows RecursiveMAS trains on fewer parameters and cheaper than LoRA, relevant for practical deployment arguments
