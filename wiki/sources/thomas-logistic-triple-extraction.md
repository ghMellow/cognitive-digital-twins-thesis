---
title: Thomas — Ontology-Guided Triple Extraction for Logistics (Interscambio Calls 2026-05-18 & 2026-05-21)
type: source
created: 2026-05-20
updated: 2026-05-21
sources: [raw/calls/2026-05-18-interscambio-call.md, raw/calls/2026-05-21-interscambio-2-call.md]
tags: [knowledge-graph, triple-extraction, ontology, transformers, logistics, interscambio]
---

# Thomas — Ontology-Guided Triple Extraction for Logistics

**One-line summary:** French student (Epitech/French engineering school) building a pipeline to extract RDF-style subject-relation-object triples from text using a logistics-domain ontology combined with transformer models, supervised by Mario and Diego Porres (Argentina).

---

## Context

Thomas presented his research during the interscambio call (2026-05-18), organized by Mario to create cross-fertilization between his research group. Thomas is:
- A French student working **in partnership with a logistics company** (referred to as "MJB")
- Co-supervised by **Diego Porres** (researcher in knowledge representation and semantic web, based in Argentina)
- Working in the **logistics domain** with a company-specific ontology

---

## Research Goal

**Extract structured knowledge triples from raw text in the form:**

```
Subject → Relation → Object
```

This is the foundation of knowledge graph construction: take unstructured text, identify entities and their relationships, and output a structured RDF-compatible representation.

**Why this matters:** In the logistics domain, large volumes of unstructured text (emails, reports, specifications) contain domain knowledge that is hard to query or reason over. By extracting triples and feeding them into a knowledge graph, the information becomes machine-readable and semantically queryable.

---

## Technical Approach

### Core Idea

Combine two complementary technologies:

- **Ontology** → provides the structured schema (what entities and relations are valid in the logistics domain)
- **Transformer models** → provide linguistic flexibility and the ability to understand context in natural language

Neither alone is sufficient: ontology alone is too rigid; transformers alone produce outputs inconsistent with the domain schema.

### Domain Ontology

- Based on a **logistics-specific ontology**, starting from **FACIT** (a top-level ontology framework used as base) and extended with company-specific concepts
- The ontology defines: valid **entity types**, valid **relation types**, and semantic constraints
- The ontology acts as a **guide and validator** throughout the pipeline — not just at the end

**Key entity types identified in the logistics ontology:**

| Concept | Definition |
|---|---|
| Materiality | Any object that can be moved or stored (e.g., items in racks or shelves) |
| Physical Location | Where objects are placed (warehouses, shelves, racks) |
| Agent | Persons or systems moving goods |
| Process | Transport, storage, or breaking/preparation processes |

**Key relations:** `move`, `perform`, `located_in`, `as_origin`, `as_destination` (and their inverse properties).

### Ontology Construction Methodology

Thomas builds the ontology following these explicit steps:

1. **Scope definition** — what domain phenomena must be representable
2. **Competency questions** — natural language questions the ontology must be able to answer
3. **Concept definition** — identify entity classes
4. **Relationship definition** — identify valid relations between concepts
5. **Constraint definition** — semantic constraints (e.g., which relations are valid between which entity types)
6. **Tool:** Protégé (standard ontology editor) + reuse of existing upper-level ontologies

**Two-level adaptation process** (applied to the client-specific domain):

- **Schema-level adaptation** — extract triples from client documentation (interviews, process descriptions) to adapt the ontology to the specific client's vocabulary and domain concepts. Input: written documentation from client about how their data is organized.
- **Instance-level population** — once the schema is finalized, populate the ontology with concrete instances from real operational data (e.g., specific products, locations, agents).

This separation matters: schema adaptation requires domain expert validation; instance population can be more automated.

### Extraction Pipeline (5 Steps)

```text
Input Text
    │
    ▼
1. MENTION DETECTION
   Ontology vocabulary used as a lexicon to identify candidate entity spans
    │
    ▼
2. ENTITY LINKING
   Detected mentions are linked to ontology concepts (disambiguation)
    │
    ▼
3. CANDIDATE TRIPLE GENERATION
   NLP preprocessing + ontology-constrained relation candidates
    │
    ▼
4. TRIPLE VALIDATION (transformer)
   Binary classification: valid / invalid triple
   Special E1/E2 entity tokens injected into sentence input
    │
    ▼
5. KNOWLEDGE GRAPH CONSTRUCTION
   Validated triples → graph
```

### Transformer Input Format — E1/E2 Entity Tokens

The key design choice that proved most effective is a **special tokenization scheme** for the triple validation step:

Given a sentence like `"A product is stored at location X"`, the input to the transformer is augmented with special entity markers:

```text
[E1] product [/E1] is stored at [E2] location X [/E2]
```

The E1/E2 tokens explicitly **mark which entities are being evaluated** for a given relation candidate. This tells the transformer precisely which relation to score (valid/invalid), without relying on the model to re-discover the entities from context.

**Why this works:** Transformers have limited context windows; providing explicit entity boundaries reduces the ambiguity the model must resolve. In Thomas's experiments, this format consistently outperformed giving the model full sentence-level context without entity markers.

**Tradeoff:** Adding E1/E2 tokens for every relation candidate multiplies the number of model calls. Thomas notes this is one source of the pipeline's computational cost.

### Models Tested

Thomas compared multiple architectures for the triple validation step:

| Model Family | Examples Tested |
|---|---|
| Encoder-only | BERT, RoBERTa, ALBERT |
| Encoder-decoder (generative) | BART, T5 |

**Finding:** Encoder-only models with the E1/E2 token format performed best for binary classification (valid/invalid triple). The generative models added overhead without meaningful accuracy gains for this specific task.

### Training Data

Because annotated logistics-domain corpora are scarce, Thomas uses **synthetic data generation**:

- **Source:** Client documentation (operational transcripts originally in French, translated to English)
- **Scale:** ~693 labeled sentence pairs
- **Augmentation:** Paraphrase generation to multiply training examples; synonym substitution
- **Hard negatives:** Deliberately crafted "difficult" sentences where the relation is implicit or ambiguous (e.g., `"The rack must be emptied before departure"` — transport relation is implied, not stated)
- **Result:** High train/validation performance — but Thomas cautions this reflects synthetic data similarity more than true generalization

**Robustness evaluation:** Thomas supplemented standard metrics with harder held-out examples to get a more realistic picture of real-world performance.

---

## Current Status & Limitations

As of May 2026, Thomas's pipeline is **work in progress**:

| Limitation | Detail |
|---|---|
| **Computational complexity** | Combining ontology + transformers is expensive; exploring SLM (Small Language Model) alternatives to reduce cost |
| **Dynamic ontology management** | Logistics domain knowledge changes over time; how to update the ontology without re-training is unsolved |
| **Real data validation** | Pipeline validated mostly on synthetic data; needs real company data to confirm generalization |
| **Polysemy / ambiguity** | Transformers still struggle when 2–3 concepts share overlapping meaning in short context windows |

---

## Future Direction

Thomas plans to explore **LLM integration at every stage** of the pipeline:
- LLMs for mention detection (replacing rule-based ontology matching)
- LLMs for relation extraction
- LLMs for semantic validation of triples

This shifts the architecture from a hybrid rule+transformer system toward a more fully LLM-driven pipeline, with the ontology serving as a constraint layer rather than as the primary engine.

---

## Relation to Nicolò's Thesis

Mario explicitly identified **cross-fertilization potential** between Thomas's work and Nicolò's thesis:

| Dimension | Thomas | Nicolò |
|---|---|---|
| **Layer** | Knowledge representation (ontology → knowledge graph) | Cognitive reasoning (CDT agent behavior evaluation) |
| **Domain** | Logistics | 5G network management |
| **LLM role** | Triple extraction and validation | Cognitive agent (perceive-reason-act cycle) |
| **Evaluation** | Transformer validation on synthetic triples | LLM-as-judge with rubric-based scoring |
| **Ontology** | Central (logistics-specific, guides extraction) | Background (CDT knowledge model, less central currently) |

**Potential synergies:**
1. Thomas's ontology-guided extraction could feed structured knowledge into a CDT's knowledge layer — making the CDT's knowledge base dynamic and text-derived rather than manually curated
2. Nicolò's LLM-as-judge evaluation methodology (rubric-based) could be applied to validate Thomas's triple extraction outputs
3. Both work with the tension between **structured schema** (ontology) and **flexible language understanding** (transformers/LLMs)

---

## Key People

| Person | Role |
|---|---|
| Thomas | French student, main researcher |
| Diego Porres | Co-supervisor (Argentina), knowledge representation & semantic web expert |
| Mario | Overall advisor, organized the interscambio, sees the big picture |
| Karin | PhD student, also co-supervised by Mario and Diego, working on continual learning in industry |

---

## Related Pages

- [[knowledge-graph-in-cdt]] — knowledge graphs as a component of cognitive digital twins
- [[glossary]] — ontology, RDF, triple, knowledge graph definitions
- [[scaffolding-tesi]] — thesis structure and where ontology/KG fit in CDT architecture
