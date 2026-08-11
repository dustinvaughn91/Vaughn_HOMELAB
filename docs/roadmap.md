# Roadmap

## Completed Baseline

- Created public-safe documentation baseline.
- Set up the public GitHub repository structure.
- Added sanitized architecture, inventory, security model, audit, roadmap, and WARPi runbook documents.
- Added initial Mermaid architecture source.
- Documented private/public separation expectations.
- Documented Guardian defensive monitoring, OpenWrt routed lab segmentation, AdGuard DNS policy, K.E.R.N.E.L. key-based administrative model, and current always-on/on-demand power posture.
- Added a maintainable architecture diagram showing the control plane, routed lab segments, DNS policy, monitoring flows, core services, on-demand systems, and Tailscale at a public-safe abstraction level.
- Added a branded WARPi project overview with its dedicated platform logo, operating model, security boundaries, remote-operation wrappers, and public-safe mode-dispatcher documentation.
- Refreshed the WARPi remote-operations runbook around approved wrappers, safe-stop behavior, dry-run mode planning, and public repository boundaries.

## Near Term

- Strengthen the public release gate with automated checks.
- Keep public docs free of exact host-level private addresses, live service URLs, credentials, Tailscale hostnames, and raw scan output.
- Keep WARPi mode-dispatcher and remote-operations documentation synchronized with validated implementation milestones.
- Expand WARPi documentation as additional field workflows reach stable checkpoints.
- Add repeatable environment audit scripts that produce redacted public output.
- Add rendered architecture and workflow diagrams.
- Add a public-safe restoration and power-state operations summary.
- Add a public-safe Guardian overview that explains telemetry sources and visibility limits without exposing private logs.

## Medium Term

- Improve Mission control documentation.
- Add read-only audit coverage for protected operations systems where approved.
- Build better asset inventory export from K.E.R.N.E.L.
- Add a homelab service catalog.
- Add restoration and rebuild runbooks.
- Add screenshots and diagrams suitable for public showcase.
- Add a sanitized OpenWrt/AdGuard segmentation runbook describing design intent, not live secrets.

## Long Term

- Local-first AI operations where practical.
- Dedicated AI hardware for larger local models.
- Stronger secrets management.
- Automated documentation drift detection.
- Safer public demo environment for AI security workflows.
