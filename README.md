# Vaughn_HOMELAB

Public documentation for VaughnLab: a home AI, cybersecurity, and infrastructure lab built around practical engineering, recoverable operations, and security-first automation.

This repository is intentionally sanitized for public sharing. It documents architecture, operating patterns, and project direction without publishing live secrets, private network details, customer data, or credentials.

## Start Here

- [Architecture](docs/architecture.md) - how the lab is organized.
- [Security model](docs/security-model.md) - trust boundaries, approvals, and safety rules.
- [Sanitized inventory](docs/inventory.md) - public-safe system roles.
- [Roadmap](docs/roadmap.md) - completed work and next priorities.
- [WARPi remote operations](docs/runbooks/warpi-remote-ops.md) - approved field-device command pattern.
- [Security policy](SECURITY.md) - responsible disclosure and scope.

## What This Lab Is

VaughnLab is a personal research and operations environment for:

- AI-assisted infrastructure operations
- Proxmox-based homelab virtualization
- Portable cybersecurity field tooling
- Local and hybrid AI workflows
- Secure automation and documentation practices

The central AI operator is **K.E.R.N.E.L.**:

> Knowledge Engine for Reasoning, Engineering, Networking, Execution, and Learning

K.E.R.N.E.L. helps maintain documentation, inspect approved systems, coordinate lab workflows, and recommend safe operational changes.

## Core Systems

- **Proxmox host** - virtualization platform for lab services and experiments
- **OpenClaw/K.E.R.N.E.L. node** - AI operations and orchestration workspace
- **WARPi** - portable Raspberry Pi/Kali-style cybersecurity field platform
- **Mission control backend** - service layer for WARPi and future field operations
- **AI lab VM** - isolated development and local model experimentation
- **DERP** - deliberately vulnerable AI/security training target

## Design Values

- Least privilege by default
- Private-first infrastructure
- Explicit approval for risky changes
- Snapshot before experiments
- Public docs are sanitized
- Offensive tooling stays on approved security platforms
- Human operator remains final authority

## Repository Layout

```text
SECURITY.md                 Responsible disclosure and project security scope
docs/
  architecture.md          High-level lab architecture
  inventory.md             Sanitized system inventory
  security-model.md        Trust boundaries and safety rules
  audit-findings.md        Current audit snapshot
  roadmap.md               Near-term milestones
  diagrams/                Mermaid diagram source
  runbooks/
    warpi-remote-ops.md    Approved WARPi remote operations
```

## Public Safety Note

This repo intentionally avoids:

- Real secrets or tokens
- Private IP addresses and live DNS values
- Customer or employer data
- Raw security scan dumps against private systems
- Rebuild-sensitive access details

The goal is to show the architecture and engineering process without exposing the lab.

## Repository Topics

Suggested GitHub topics:

```text
homelab, ai-ops, cybersecurity, raspberry-pi, proxmox, documentation, security-automation, warpi, openclaw, ai-governance
```
