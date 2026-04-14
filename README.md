# Thesis Wiki: Cognitive Digital Twins

A structured knowledge repository for thesis research on Cognitive Digital Twins (CDT) for 5G networks with LLM-based multi-agent reasoning.

## Purpose

This repository maintains a personal research wiki that:

- Ingests academic sources (papers, transcribed calls, research notes) into structured knowledge pages
- Tracks the thesis argument progression through a central scaffolding document
- Provides query-able references across the research corpus
- Maintains discipline over terminology, concepts, and claims through a shared glossary

The wiki is the single source of truth for thesis structure and research status.

## Structure

```
raw/                    Source materials (read-only)
  papers/               Research papers with pre-processed analysis
  calls/                Transcribed meetings and discussions
  project/              Thesis proposal, feedback, and research notes

wiki/                   Knowledge base (actively maintained)
  scaffolding-tesi.md   Central thesis argument structure
  glossary.md           Canonical terminology and definitions
  index.md              Navigation and status tracking
  log.md                Append-only operation history
  overview.md           High-level thesis summary
  sources/              Summaries of raw documents
  concepts/             Theoretical concepts and frameworks
  analyses/             Comparative tables and gap analysis (deferred)
  style/                Writing conventions (deferred)
  personas/             Target audiences (optional)
```

## Key Documents

- **scaffolding-tesi.md** — Core thesis structure: research question, hypotheses, chapter outline, open tensions, identified gaps
- **glossary.md** — CDT and 5G terminology with canonical definitions
- **index.md** — Complete catalog of wiki pages with progress tracking
- **log.md** — Chronological record of all operations

## Thesis Context

The thesis proposes a Cognitive Digital Twin for 5G base station management with three layers:

1. Physical Simulated (Python 3GPP metrics generator)
2. Digital Twin (Eclipse Ditto)
3. Cognitive (LangGraph + local LLM agents)

Three contributions:

1. Complete CDT architecture with full bidirectionality
2. Evaluation framework for cognitive agents when ground truth is absent (CORE)
3. Benchmark comparison of open-weight LLM models (8B scale) on 5G-specific tasks

## Workflow

Each research artifact follows a standardized ingestion process:

1. Read scaffolding.md to understand current thesis state
2. Ingest paper/call/note and extract value within thesis context
3. Create or update wiki pages (source, concepts, analyses)
4. Update scaffolding with new claims and evidence
5. Update index.md and log.md

Processes are documented in CLAUDE.md and SKILL-thesis-ingest.md.

## Status

Blocco A (Core CDT Theory) — Complete
- Zheng et al. (2022): Foundational CDT definition and six cognitive functions
- Al-Haj Ali et al. (2025): MMCI evaluation framework

Blocco B–E and calls/notes — In progress

See index.md for detailed progress tracking.

## Tools

- Markdown with VS Code
- Git for version control
- Link syntax: [[page-name]] for internal wiki references

## License

Restricted to thesis work. Not a public repository.

## Contact

Nicolò Termine — Politecnico di Torino
