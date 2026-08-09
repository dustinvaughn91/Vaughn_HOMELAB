# Vaughn_HOMELAB

Public documentation for VaughnLab: a private AI, cybersecurity, and infrastructure lab built around practical engineering, recoverable operations, and security-first automation.

This repository is intentionally sanitized for public sharing. It documents architecture, operating patterns, and project direction without publishing credentials, private host-level addressing, Tailscale hostnames, customer data, or rebuild-sensitive access details.

## Start Here

- [Architecture](docs/architecture.md) - how Proxmox, OpenWrt, AdGuard, Guardian, core services, and on-demand workloads fit together.
- [Security model](docs/security-model.md) - trust boundaries, approvals, identity model, and safety rules.
- [Sanitized inventory](docs/inventory.md) - public-safe system roles and normal power posture.
- [Roadmap](docs/roadmap.md) - completed work and next priorities.
- [WARPi remote operations](docs/runbooks/warpi-remote-ops.md) - approved field-device command pattern.
- [Security policy](SECURITY.md) - responsible disclosure and public repo scope.

## What This Lab Is

VaughnLab is a personal research and operations environment for:

- AI-assisted infrastructure operations
- Proxmox-based homelab virtualization
- Segmented lab networking with OpenWrt
- Controlled DNS through AdGuard Home
- Defensive monitoring with Guardian/Wazuh
- Portable cybersecurity field tooling through WARPi
- Local and hybrid AI/security experiments
- Secure automation and documentation practices

The central AI operator is **K.E.R.N.E.L.**:

> Knowledge Engine for Reasoning, Engineering, Networking, Execution, and Learning

K.E.R.N.E.L. helps maintain documentation, inspect approved systems, coordinate lab workflows, and recommend or execute safe operational changes within explicit authority boundaries.

## Current Architecture At A Glance

VaughnLab runs on a Proxmox virtualization layer with a small set of always-on services and a larger set of on-demand lab systems.

Always-on services provide the control plane and shared foundations: the OpenClaw/K.E.R.N.E.L. node, Holocron private web UI, AdGuard DNS staging resolver, OpenWrt routed lab boundary, GLPI ticketing, and Guardian defensive monitoring. These systems are private by default and are not documented here as public services.

On-demand systems stay powered off unless needed for a specific workflow: WARPi mission backend development, DERP AI-security testing, local AI/security experiments, workflow automation, malware triage, and Kali-based assessment work. This reduces idle attack surface and keeps the lab easier to reason about.

## Network And Security Shape

The management and recovery plane remains separate from routed lab workloads. Selected core systems intentionally stay on the management LAN for recovery and control-plane availability.

OpenWrt routes the segmented lab networks. Current documented lab segments use private RFC1918 ranges in the `10.66.x.x` space for pentest, security, services, AI/lab, and triage workloads. Routed lab DHCP points workloads at AdGuard DNS, and OpenWrt blocks direct DNS bypass from the routed segments.

Guardian receives local security telemetry, OpenWrt logs, and Proxmox telemetry. Guardian does **not** claim full packet visibility across all bridges; that would require a dedicated mirror, TAP, or sensor design.

## Administrative Model

K.E.R.N.E.L. uses a named `kernel` administrative identity with SSH key-based access where supported. Linux root is preserved as a local/console break-glass identity, not as a routine remote SSH path.

OpenWrt is an appliance exception: it uses the platform-supported root administration model with key-only SSH and password SSH disabled.

Routine Proxmox automation uses least-privilege access scoped to approved lab resources. Protected systems remain outside routine automation unless the human operator explicitly grants a separate authority path.

## Repository Layout

```text
SECURITY.md                 Responsible disclosure and project security scope
docs/
  architecture.md          High-level lab architecture
  inventory.md             Sanitized system inventory
  security-model.md        Trust boundaries and safety rules
  audit-findings.md        Public-safe audit snapshot
  roadmap.md               Near-term milestones
  diagrams/                Mermaid diagram source
  runbooks/
    warpi-remote-ops.md    Approved WARPi remote operations
```

## Public Safety Note

This repo intentionally avoids:

- Real secrets or tokens
- Private host-level IP addresses and live private DNS names
- Tailscale hostnames, auth keys, or session details
- Customer or employer data
- Raw security scan dumps against private systems
- Rebuild-sensitive access details

High-level private RFC1918 lab ranges may be described when needed to explain architecture, but exact host-level operational details remain private.

## Repository Topics

Suggested GitHub topics:

```text
homelab, ai-ops, cybersecurity, raspberry-pi, proxmox, documentation, security-automation, warpi, openclaw, ai-governance
```
