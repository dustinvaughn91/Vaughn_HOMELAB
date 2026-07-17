# Architecture

VaughnLab is organized as a small operations platform with a clear separation between control-plane services, experiment systems, and approved security tooling.

## Logical Layers

```text
Human Operator
      |
      v
K.E.R.N.E.L. / OpenClaw
      |
      +-- Proxmox lab inventory and VM lifecycle operations
      +-- WARPi read-only reporting and approved security wrappers
      +-- Documentation and runbook maintenance
      +-- Local memory and automation tooling

Proxmox Host
      |
      +-- Mission Control Backend
      +-- AI Lab VM
      +-- DERP Security Target
      +-- Automation VM

WARPi
      |
      +-- Normal Mode
      +-- Field Mode
      +-- Kismet-on-demand
      +-- GPS and display collectors
      +-- Approved security command wrapper
```

## Control Plane

K.E.R.N.E.L. runs from the OpenClaw operations environment and acts as the documentation and automation coordinator. It uses least-privilege access where possible and avoids direct control of protected systems unless explicitly approved.

K.E.R.N.E.L. is allowed to inspect approved lab resources, maintain documentation, and run specific approved operational commands. It does not make public exposure, billing, router, firewall, DNS, or destructive changes without explicit human approval.

## Virtualization Layer

The lab uses Proxmox to host small purpose-built VMs and containers. Routine automation uses a limited Proxmox token scoped to lab resources instead of broad root access.

Public docs describe roles and resource classes rather than exposing private addresses or token details.

## WARPi Field Platform

WARPi is the portable security field platform. It supports:

- Normal trusted-network mode
- Field Mode with hotspot and capture services
- Tailscale-backed management
- Mission control health checks
- GPS and display state collection
- Security actions through approved wrappers

Active security tooling belongs on WARPi or other approved security devices, not on the general AI operations node.

## AI Security Target

DERP is a deliberately vulnerable AI/security target used for prompt-injection, secret-handling, and defensive AI workflow experiments. DERP is isolated by design and must never hold real secrets or trusted production access.

