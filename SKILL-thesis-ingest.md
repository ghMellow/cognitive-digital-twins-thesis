# SKILL: thesis-ingest

## Purpose
Ingest a research paper (raw PDF/text or pre-processed "Value for thesis" file) into the thesis wiki and update the central Scaffolding document.

---

## Trigger phrases
- "ingest paper [name]"
- "add paper [name]"
- "update scaffolding with [name]"
- User passes a file from `raw/papers/` or a pre-processed `value-*.md`

---

## Directory layout expected

```
raw/
  papers/
    <paper-slug>/
      paper.pdf (or .md)        ← original
      riassunto.md               ← optional: already produced
      yt.md                      ← optional: outreach version
      valore-tesi.md             ← THE MOST IMPORTANT FILE — may be missing
  calls/
    <call-slug>.md
  project/
    proposta/
      proposta-tesi.md
      feedback-claude.md
      base-teorica.md
    approfondimenti/
      <theme>.md

wiki/
  index.md
  log.md
  overview.md
  glossary.md
  scaffolding-tesi.md            ← central document, updated every ingest
  sources/
  concepts/
  analyses/
```

---

## Workflow

### Step 0 — Read the context
First of all:
1. Read `wiki/index.md` to orient yourself
2. Read `wiki/scaffolding-tesi.md` to understand the current state of the thesis
3. Read `wiki/glossary.md` for canonical terms already defined

### Step 1 — Determine entry point

**Case A — you have raw paper only (PDF or text)**

Generate the three layers using exactly the instructions below as internal prompts.

**Layer 1 — `yt`** (tone: engaging engineer explainer):
Analyze the paper by answering these points:
1. **"Here's what they did"** — explain the central idea simply but technically. What is the "trick" or intuition that solves the problem? Use engineer language (weights, architectures, data, reward signals…) but avoid unnecessary mathematical proofs.
2. **"Why it matters"** — what is the real novelty? Is it a breakthrough or just incremental improvement? Why should someone care?
3. **"How do we use it?"** — can I use it to optimize an existing architecture? Does it reduce inference or training costs? Enable previously impossible things?
4. **"Under the hood"** — summarize the technical pipeline. If you had to code it in Python tomorrow, what are the key components?
5. **"The catches"** — where does it struggle? Too resource-heavy? Dataset too specific? Production-ready or lab research only?

**Layer 2 — `riassunto`** (for future reference):
Produce a structured academic summary: problem → method → results → limitations. Must be self-contained and consultable without re-reading the paper.

**Layer 3 — `valore-tesi`** (see full instructions in Step 2 below):
Generate the most important layer by contextualizing the paper against the thesis proposal. See Step 2 for complete instructions.

After generating the three layers, create `wiki/sources/<paper-slug>.md`.

**Case B — you already have the `valore-tesi.md` file**
1. Read the file directly
2. Skip generator for riassunto/yt (already done manually)
3. Go to Step 2

**Case C — you have `valore-tesi.md` but missing `riassunto` and/or `yt`**
1. Use the existing `valore-tesi.md` for Step 2 (don't re-generate it)
2. Generate only the missing layers with Case A prompts
3. Flag to the user which layers you generated and which were already present

### Step 2 — Extract thesis value

The `valore-tesi.md` should be generated (Case A) or read (Case B/C) keeping the specific thesis context always in mind:

**Fixed thesis context** (always in mind during this analysis):
> The thesis proposes a Cognitive Digital Twin (CDT) for a 5G radio cell on three layers: simulated physical (3GPP metric generator), digital twin (Eclipse Ditto), cognitive (LangGraph + local LLMs). The main scientific contribution is not the system itself but the **evaluation framework for specialized cognitive agents** (Perception, Reasoning, Planning, Communication). Critical current gap: evaluate Reasoning and Planning without obvious ground truth — candidate strategies: LLM-as-judge, multi-agent agreement, KG-based validation. Second contribution: comparative benchmark Llama 3.1 8B / Mistral 7B / Phi-3 Mini / Qwen 3B on 5G-specific tasks.

For each paper, answer:
1. **Which areas does it deepen** — relative to the three thesis contributions (CDT architecture, evaluation framework, model benchmark)
2. **Pros/cons** — strengths and limitations of the paper in our use context
3. **Contextual notes for the advisor** — if the advisor asked "what do you think of this paper relative to your thesis?", what would you answer? Include: how you'd cite it, where it enters the argument, what you take and what you leave. If the paper is not useful, explain explicitly why.

Then extract the structural dimensions for the scaffolding:

| Dimension | Guiding question |
|---|---|
| **Supported topic** | Which claim of the proposal does it support or challenge? |
| **Gap closed** | Methodological, empirical, or theoretical? |
| **Key concepts** | Which terms/frameworks enter the glossary? |
| **Tensions** | Contradicts anything already in scaffolding or other papers? |
| **Scaffolding position** | Contribution 1 (architecture), 2 (evaluation) or 3 (benchmark)? |

If any of these points is ambiguous, ask **at most 2 questions** to the user before proceeding.

### Step 3 — Update `wiki/scaffolding-tesi.md`

Update rules:
- **Don't rewrite** existing sections: add, annotate, integrate
- Insert the paper's contribution in the relevant section with this format:
  ```
  > **[Author, Year]** — <contribution in 1-2 lines>. [[sources/<paper-slug>]]
  ```
- If the paper opens a new section not foreseen, add it with `###` heading and flag it explicitly to the user
- If the paper contradicts something existing, add a `⚠️ TENSION:` block before updating

### Step 4 — Update or create secondary wiki pages

- `wiki/sources/<paper-slug>.md` — always, even if it exists (update)
- `wiki/concepts/<concept>.md` — for each new or deepened concept
- `wiki/glossary.md` — add canonical terms with definition and source

### Step 5 — Update `wiki/index.md`

Add or update the source row. Update rows for each modified page.

### Step 6 — Write entry in `wiki/log.md`

```
## [YYYY-MM-DD] ingest | <Paper Title — Author, Year>
Entry point: raw | value-thesis
Pages created: ...
Pages updated: scaffolding-tesi, ...
Tensions detected: yes/no — <description if yes>
Scaffolding sections touched: ...
```

---

## Expected output per ingest

| File | Action |
|---|---|
| `wiki/scaffolding-tesi.md` | Updated with paper's contribution |
| `wiki/sources/<slug>.md` | Created or updated |
| `wiki/concepts/*.md` | 0–3 pages created/updated |
| `wiki/glossary.md` | New terms added |
| `wiki/index.md` | Rows updated |
| `wiki/log.md` | Entry appended |

---

## Source page format

```yaml
---
title: <Paper Title>
type: source
created: YYYY-MM-DD
updated: YYYY-MM-DD
authors: [Author1, Author2]
year: YYYY
tags: [method, domain, key-concepts]
contributo-tesi: 1-architecture | 2-evaluation | 3-benchmark | none
---
```

**Main contribution** — 1 line

## Summary
<problem → method → results → limitations>

## yt
<outreach layer: central trick, why it matters, practical applications, under the hood, limitations>

## Value for thesis

**Areas deepened:** ...
**Pros:** ...
**Cons:** ...

**Notes for advisor:**
> <If advisor asked: what would you answer? How you'd cite it, where it enters the argument, what you take and what you leave. If not useful: why.>

### Structural dimensions
- Supported topic: ...
- Gap closed: ...
- Scaffolding position: Contribution [1/2/3] — <specific section>
- Tensions: ...

## Concepts introduced
- [[concept-1]], [[concept-2]]

## Related pages
- [[scaffolding-tesi]]
- [[concepts/...]]
```

---

## Operational notes

- **Never modify files in `raw/`**
- If `valore-tesi.md` is already excellent, trust it — don't re-analyze the paper from scratch
- Always use terms from `wiki/glossary.md`; if you add a new one, flag it
- The scaffolding is the living central document: every paper must leave a trace there
- If the user passes multiple papers in one session, process one at a time and update the log for each
