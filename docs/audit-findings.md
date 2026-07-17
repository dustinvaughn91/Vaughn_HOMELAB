# Audit Findings

Snapshot date: 2026-07-17 UTC

This is a public-safe summary of the current environment audit. Live operational details, service discovery output, and private telemetry remain in private notes only.

## Healthy Signals

| Finding | Severity | Risk | Recommendation | Owner | Status | Date Reviewed |
| --- | --- | --- | --- | --- | --- | --- |
| Public documentation is separated from private operational notes. | Info | Reduces accidental exposure. | Keep public/private review in the release gate. | K.E.R.N.E.L. | In progress | 2026-07-17 |
| WARPi uses approved wrappers for reporting and security activity. | Low | Direct raw-tool usage could bypass guardrails. | Keep runbooks centered on approved wrappers. | K.E.R.N.E.L. | In progress | 2026-07-17 |
| DERP is intentionally vulnerable and isolated by design. | Medium | Misunderstanding DERP scope could create unsafe assumptions. | Continue labeling DERP as a controlled training target. | K.E.R.N.E.L. | In progress | 2026-07-17 |
| Local AI/memory workflows reduce avoidable external dependency for embeddings. | Info | External APIs can increase cost and data movement. | Prefer local-first where practical. | K.E.R.N.E.L. | In progress | 2026-07-17 |

## Current Gaps

| Finding | Severity | Risk | Recommendation | Owner | Status | Date Reviewed |
| --- | --- | --- | --- | --- | --- | --- |
| WARPi documentation drift exists around older mode-script paths. | Medium | Operators may follow stale paths. | Update WARPi docs from the device-local source of truth. | K.E.R.N.E.L. | Open | 2026-07-17 |
| Some detailed scan and service-discovery output is private-only. | High | Publishing exact services or ports can expose unnecessary attack detail. | Keep raw scan reports out of the public repository. | K.E.R.N.E.L. | Open | 2026-07-17 |
| Public release checks need automation. | High | Manual review alone can miss secrets or private infrastructure details. | Add automated release-gate checks for secrets, private network indicators, and documentation quality. | K.E.R.N.E.L. | Open | 2026-07-17 |

## Notes

This report avoids private network identifiers, exact service discovery, and raw operational logs. Full details remain local.
