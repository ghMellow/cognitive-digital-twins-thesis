---
title: Agreement as an Evaluation Signal (Multi-model / Multi-agent agreement)
type: concept
created: 2026-04-28
updated: 2026-04-28
sources: [wiki/sources/pretel-et-al-2024-mas-dt.md, wiki/sources/berkeley-cs294-llm-eval.md]
tags: [evaluation, agreement, reliability, llm-as-judge]
---

Agreement is an evaluation signal for systems where direct ground truth is absent: if independent agents (or models) converge on the same diagnosis/action, confidence can increase; systematic disagreement indicates uncertainty or ambiguity.

## Definition
Agreement can be operationalized as:
- Exact-match agreement on labels (when outputs are structured)
- Semantic agreement (embedding similarity) for natural-language rationales
- Voting/consensus procedures across heterogeneous models

## Role in this thesis
- Applies primarily to the **Reasoning Agent** where ground truth for root-cause explanations is limited.
- Used as a mitigation for LLM-as-judge circularity: agreement complements external truth sources (simulator/KG) where available.

## Related pages
- [[sources/berkeley-cs294-llm-eval]]
- [[sources/pretel-et-al-2024-mas-dt]]
- [[sources/multiagent-bench-2025]]
- [[benchmark-template]]
- [[scaffolding-tesi]]
