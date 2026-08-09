# Security Model

VaughnLab is designed around least privilege, explicit approval, and recoverable operations.

## Core Rules

- Default exposure is private/LAN-only.
- Remote access uses private overlay networking only when approved.
- Public Internet exposure requires explicit approval.
- Router, NAT, firewall, DNS, and billing changes require explicit approval.
- Destructive actions require explicit approval.
- Real secrets are never committed, pasted into chat, or placed in public docs.
- Always-on systems are limited to the control-plane, routing/DNS, ticketing, UI, and monitoring backbone.
- On-demand lab systems should stay powered off when idle.

## Role Separation

Human operator:

- Final authority
- Approves risky changes
- Owns secrets and external accounts

K.E.R.N.E.L.:

- Documents infrastructure
- Performs approved read-only checks
- Uses least-privilege tokens where available
- Recommends changes before risky operations
- Uses named key-based administrative access where supported

WARPi:

- Runs approved security and field tooling
- Provides structured status through `kernel-report`
- Provides security scans through `kernel-security`

DERP:

- Is an intentionally vulnerable test target
- Must never have real secrets
- Must remain isolated from trusted systems

## Administrative Access Model

Supported Linux guests use a named `kernel` administrative identity with SSH key-based access. Password-based `kernel` access is not the intended routine path.

Linux root is preserved as a local or console break-glass identity. Root SSH is not a routine administrative path, and password-based root SSH should remain disabled.

Appliances may have platform-specific models. OpenWrt, for example, uses the supported root administration model with key-only SSH and password SSH disabled rather than a normal Linux `kernel` plus sudo pattern.

## Network Security Model

The management and recovery plane is separate from routed lab workloads. Selected core systems stay on the management LAN for recovery, DNS staging, SIEM access, and agent control.

OpenWrt routes private VaughnLab lab segments and enforces DNS policy for routed workloads. AdGuard provides controlled DNS for those workloads, and direct DNS bypass from routed lab segments is blocked and logged.

Guardian receives host/security telemetry, OpenWrt logs, and sanitized Proxmox telemetry. Guardian does **not** currently have full packet visibility across all Proxmox bridges; public docs must not imply mirror/TAP coverage that does not exist.

## Power-State Model

Always-on systems provide core lab functions: control plane, private UI, DNS, routed lab boundary, ticketing, and monitoring.

On-demand systems support experiments and higher-risk workflows such as AI security testing, malware triage, workflow automation, and pentest work. They should be stopped when idle to reduce attack surface and resource load.

## Public Repository Policy

Before publishing:

- Run secret scanning
- Remove private host-level addresses and DNS names
- Remove customer or employer details
- Avoid raw logs unless sanitized
- Prefer architecture summaries over operational dumps

## Approved Security Activity Pattern

Security activity should be routed through approved wrappers when available. For WARPi, use:

```text
kernel-security <approved-command> <target>
```

Do not bypass an approved wrapper with raw tooling unless explicitly approved.
