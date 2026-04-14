---
title: Digital Hat (DH)
type: concept
created: 2026-04-14
updated: 2026-04-14
sources: [restart-2024-ndt]
tags: [NDT, interface, synchronization, Ditto]
---

# Digital Hat (DH)

The interface layer between physical network infrastructure and the cognitive/autonomic control layer in an NDT.

## Definition (RESTART 2024)

The Digital Hat is:

- A protocol-agnostic abstraction of physical asset state
- Real-time synchronized with the physical asset
- Standard representation for cognitive algorithms to query and act upon
- Persistent state store with historical tracking

## Functional Requirements

1. **Synchronization** — State changes from physical asset are mirrored with minimal latency
2. **Abstraction** — Protocol details hidden; unified API exposed upward
3. **Query Interface** — Cognitive layer can efficiently query current and past state
4. **Action Interface** — Cognitive layer can safely propose and execute actions
5. **Versioning** — Maintains temporal history of state for trend analysis

## Thesis Implementation

**Technology:** Eclipse Ditto

**Mapping:**

| DH Concept | Ditto Equivalent |
|---|---|
| Physical asset representation | Thing (device) |
| State properties | Features |
| Synchronization protocol | REST API + WebSocket |
| Real-time change feed | Change notifications |
| Historical state query | Feature history API |
| Action safeguard | Thing metadata policies |

**Example (5G gNB):**

```
Asset: gNB (physical radio node)

DH Thing:
  ID: "gNB-cell-1"
  Features:
    - rsrp: -120 dBm (RSRP KPI)
    - sinr: 15 dB (SINR KPI)
    - throughput_dl: 150 Mbps (downlink throughput)
    - handover_failure_rate: 0.5%
    - load_cell: 65%
  
  Metadata: SLA targets, constraints, capabilities
```

The Reasoning Agent queries this DH (via Ditto API) to analyze state, and the Planning Agent updates DH to signal corrective actions.

---

## Design Benefits

1. **Decoupling** — Cognitive algorithms don't need to know physical asset protocols
2. **Testability** — Can mock DH without physical infrastructure (thesis simulator)
3. **Standardization** — Same approach works for any physical asset exposing DH interface
4. **Debuggability** — Full history of DH state available for audit trails

---

## Challenges in Practice

1. **Latency** — DH synchronization must be sub-millisecond for 5G latency-critical decisions
2. **Completeness** — What properties to expose? Too many = overhead; too few = blind spots
3. **Consistency** — Handling temporal gaps between physical state and DH mirror
4. **Safety** — Preventing cognitive layer from proposing unsafe actions to DH

---

## Related Pages

- [[sources/restart-2024-ndt]] — Foundational paper
- [[network-digital-twin]] — Parent concept
- [[intent-based-networking]] — How Planning Agent uses DH
- [[glossary]] — DH definition
