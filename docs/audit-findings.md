# Audit Findings

Snapshot date: 2026-08-28 UTC

This is a public-safe summary of the current environment audit. Live operational details, service discovery output, and private telemetry remain in private notes only.

## Healthy Signals

| Finding | Severity | Risk | Recommendation | Owner | Status | Date Reviewed |
| --- | --- | --- | --- | --- | --- | --- |
| Public documentation is separated from private operational notes. | Info | Reduces accidental exposure. | Keep public/private review in the release gate. | K.E.R.N.E.L. | In progress | 2026-07-17 |
| WARPi uses approved wrappers for reporting and security activity. | Low | Direct raw-tool usage could bypass guardrails. | Keep runbooks centered on approved wrappers. | K.E.R.N.E.L. | In progress | 2026-07-17 |
| DERP is intentionally vulnerable and isolated by design. | Medium | Misunderstanding DERP scope could create unsafe assumptions. | Continue labeling DERP as a controlled training target. | K.E.R.N.E.L. | In progress | 2026-07-17 |
| Local AI/memory workflows reduce avoidable external dependency for embeddings. | Info | External APIs can increase cost and data movement. | Prefer local-first where practical. | K.E.R.N.E.L. | In progress | 2026-07-17 |
| Routed lab segmentation is documented at a public-safe level. | Low | Clear architecture reduces accidental cross-boundary changes. | Keep exact host-level details private. | K.E.R.N.E.L. | In progress | 2026-08-09 |
| AdGuard DNS policy is documented for routed lab workloads. | Low | DNS expectations are clearer for lab systems. | Avoid publishing admin credentials or live service paths. | K.E.R.N.E.L. | In progress | 2026-08-09 |
| Guardian defensive monitoring is documented with its visibility limits. | Low | Avoids overstating IDS/SIEM coverage. | Do not claim full packet visibility without mirror/TAP design. | K.E.R.N.E.L. | In progress | 2026-08-09 |
| K.E.R.N.E.L. key-based admin and root break-glass model is documented. | Low | Reduces confusion between routine admin and emergency recovery. | Keep private keys and recovery secrets out of public docs. | K.E.R.N.E.L. | In progress | 2026-08-09 |
| Always-on versus on-demand power posture is documented. | Low | Reduces idle attack surface and resource drift. | Keep docs aligned with Proxmox policy. | K.E.R.N.E.L. | In progress | 2026-08-09 |
| Proxmox autostart behavior has a private forensic audit trail. | Low | Recovery planning is stronger when autostart failures are tied to evidence instead of assumptions. | Keep explicit startup order, dependency validation, and reboot proof-test notes in private operational documentation. | K.E.R.N.E.L. | In progress | 2026-08-28 |

## Current Gaps

| Finding | Severity | Risk | Recommendation | Owner | Status | Date Reviewed |
| --- | --- | --- | --- | --- | --- | --- |
| WARPi documentation drift exists around older mode-script paths. | Medium | Operators may follow stale paths. | Update WARPi docs from the device-local source of truth. | K.E.R.N.E.L. | Open | 2026-07-17 |
| Some detailed scan and service-discovery output is private-only. | High | Publishing exact services or ports can expose unnecessary attack detail. | Keep raw scan reports out of the public repository. | K.E.R.N.E.L. | Open | 2026-07-17 |
| Public release checks need automation. | High | Manual review alone can miss secrets or private infrastructure details. | Add automated release-gate checks for secrets, private network indicators, and documentation quality. | K.E.R.N.E.L. | Open | 2026-07-17 |
| Guardian does not have full bridge-wide packet visibility. | Medium | Overstating visibility could weaken detection assumptions. | Add mirror/TAP/sensor design only after explicit approval. | K.E.R.N.E.L. | Open | 2026-08-09 |
| Protected systems need separately approved documentation/audit depth. | Medium | Public docs should not imply routine agent control where the authority boundary is intentionally limited. | Document protected roles at a high level until access is approved. | K.E.R.N.E.L. | Open | 2026-08-09 |
| Autostart needs an approved recovery hardening pass. | Medium | A host can appear recovered while individual workloads remain stopped if guest-start failures are only visible in private task logs. | Apply explicit startup ordering and a controlled reboot validation plan only during a separately approved maintenance window. | K.E.R.N.E.L. | Open | 2026-08-28 |

## Notes

This report avoids private host-level identifiers, exact service discovery, raw operational logs, credentials, and Tailscale hostnames. Full operational details remain local.
