---
title: GHSA-6gxq-gpr8-xgjp — UDR Improper ueId Validation in EE Subscription Handlers
type: source
created: 2026-06-16
updated: 2026-06-16
sources: [https://github.com/free5gc/free5gc/security/advisories/GHSA-6gxq-gpr8-xgjp]
tags: [cve, free5gc, udr, regex, input-validation, 5g-security]
---

CVE-2026-47780: defective regex in UDR EE-subscription handlers allows arbitrary ueId to persist in the database, bypassing 3GPP identifier format restrictions.

---

## Metadata

| Field | Value |
| --- | --- |
| CVE ID | CVE-2026-47780 |
| GHSA ID | GHSA-6gxq-gpr8-xgjp |
| Severity | Moderate |
| CWE | CWE-20 (Improper Input Validation) |
| Affected NF | UDR (Unified Data Repository) |
| Affected file | `api_datarepository.go` |
| Affected versions | free5gc/udr ≤ 4.2.2 |
| Patched version | None at time of advisory |

---

## Vulnerability

The regex used to validate `ueId` in the EE-subscription handlers ends with a trailing `|.+` branch:

```
^(imsi-[0-9]{5,15}|nai-.+|msisdn-[0-9]{5,15}|extid-[^@]+@[^@]+|gci-.+|gli-.+|.+)$
```

The final `|.+` accepts any non-empty string, making all preceding format constraints dead code. The intended pattern should be:

```
^(imsi-[0-9]{5,15}|nai-.+|msisdn-[0-9]{5,15}|extid-[^@]+@[^@]+|gci-.+|gli-.+)$
```

**Affected handlers:**
- `HandleCreateEeSubscriptions` (POST `/nudr-dr/v2/subscription-data/{ueId}/context-data/ee-subscriptions`)
- `HandleQueryeesubscriptions` (GET same endpoint)

Both are in `api_datarepository.go` at approximately lines 2482 and 2569.

---

## Impact

An attacker with SBI network access can submit arbitrary non-compliant identifiers as `ueId`. These persist in the MongoDB data store, enabling:

- Unauthorized data creation under malformed identifiers
- Persistent corruption of subscriber metadata
- Integrity compromise of the UDR data store

---

## Fix

Remove the trailing `|.+` from the regex in both `HandleCreateEeSubscriptions` and `HandleQueryeesubscriptions`.

---

## Relation to the Cross-File Finding

This CVE is officially scoped to UDR only. However, in the free5GC code the same class of defect (inconsistent SUPI/ueId validation) appears across three NFs:

- **PCF**: only empty-check on `supi`, no format validation
- **UDM**: `validator.IsValidSupi()` called in some handlers but absent in others (GHSA-585v-hcgf-jhfr)
- **UDR**: regex present in EE-subscription handlers but defective (`|.+`)

Viewed cross-file, these three are the same systemic vulnerability: SUPI/ueId validation is neither consistent nor correct across the 5G core SBI layer. This cross-NF perspective was identified autonomously by Claude during the free5GC security analysis session (see [[cve-discovery-method]]).

The colleague's static analysis (ANALISI_VULNERABILITA.md, 2026-05-09) had labeled this as V3 ("ineffective regex") — found manually but not yet assigned a CVE ID at the time of that analysis.

---

## Related pages

- [[cve-discovery-method]]
- [[scaffolding-tesi]]
