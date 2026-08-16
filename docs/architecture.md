# Architecture

VaughnLab is organized as a private operations platform with clear separation between the control plane, always-on services, routed lab workloads, and on-demand security or AI experiments.

## Logical Layers

```text
Human Operator
      |
      v
K.E.R.N.E.L. / OpenClaw
      |
      +-- Documentation and runbook maintenance
      +-- Proxmox cluster inventory and VM lifecycle operations
      +-- Approved SSH/key-based administrative workflows
      +-- WARPi read-only reporting and approved security wrappers

VaughnLab Proxmox Cluster
      |
      +-- pve01: primary workload host / segmented virtual networking
      +-- pve02: second compute node / cluster capacity and resilience
      |
      +-- Always-on core services
      |     +-- Holocron private UI
      |     +-- AdGuard DNS staging resolver
      |     +-- OpenWrt routed lab boundary
      |     +-- GLPI ticketing
      |     +-- Guardian/Wazuh monitoring
      |
      +-- On-demand lab systems
            +-- Mission control backend
            +-- DERP AI security target
            +-- AI lab VM
            +-- Workflow automation VM
            +-- Malware triage VM
            +-- Kali/pentest VM
```

Mermaid source:

- [High-level architecture](diagrams/architecture.mmd)
- [AI decision workflow](diagrams/ai-decision.mmd)
- [Trust boundaries](diagrams/trust-boundary.mmd)
- [Public release pipeline](diagrams/release-pipeline.mmd)
- [Disaster recovery workflow](diagrams/disaster-recovery.mmd)
- [WARPi operation flow](diagrams/warpi-operation.mmd)

## Control Plane

K.E.R.N.E.L. runs from the OpenClaw operations environment and acts as the documentation and automation coordinator. It uses least-privilege access where possible and avoids direct control of protected systems unless explicitly approved.

K.E.R.N.E.L. is allowed to inspect approved lab resources, maintain documentation, and run specific approved operational commands. It does not make public exposure, billing, router, firewall, DNS, or destructive changes without explicit human approval.

The control plane is intentionally separated from on-demand lab workloads. This keeps routine operations available even when experimental systems are powered off or being rebuilt.

## Virtualization Layer

VaughnLab now uses a two-node Proxmox VE cluster named `VaughnLab`. Both nodes run the same Proxmox VE 8.4 release family and participate in Corosync quorum. Cluster communication uses the private management LAN, while Tailscale provides an additional approved private management path.

`pve01` remains the established workload host and carries the existing segmented virtual bridges and core services. `pve02` adds independent compute capacity and a second administrative/cluster node. Joining the nodes provides centralized cluster management and workload placement options; it does not by itself aggregate CPU/RAM into a single machine or provide automatic workload high availability.

The two-node cluster currently requires both node votes for normal quorum. A separate third-vote/qdevice design is planned rather than placing duplicate quorum voters inside the two failure domains they are intended to arbitrate.

Host firewall policy is enabled with default-deny inbound behavior and explicit allowances for trusted management traffic. Management access is limited to approved private LAN/Tailscale paths, while cluster communication remains restricted to the participating nodes. K.E.R.N.E.L. has validated key-based administrative reachability to both hypervisors. Exact host IP addresses, Tailscale addresses, keys, and other rebuild-sensitive details remain outside this public repository.

Routine automation should continue to use constrained identities and scoped access wherever practical. Broad host-level root authority remains an explicitly approved maintenance path rather than an assumed agent capability.

## Routed Lab Networking

OpenWrt provides the routed lab boundary for segmented workloads. Current documented routed segments use private RFC1918 `10.66.x.x` ranges at a public-safe abstraction level:

- Pentest segment
- Security segment
- Services segment
- AI/lab segment
- Malware triage segment

The management and recovery plane remains separate on the normal private LAN. Selected core systems intentionally stay there for recovery, DNS staging, SIEM access, and agent control.

OpenWrt is not the household router. It routes VaughnLab lab segments, provides DHCP to those routed segments, preserves selected service compatibility VIPs, and enforces DNS policy for lab workloads.

## DNS

AdGuard Home provides controlled DNS for routed lab workloads. OpenWrt DHCP advertises the AdGuard resolver to lab segments, and OpenWrt rejects direct DNS bypass attempts from routed workloads to other resolvers.

A separate Raspberry Pi 5 network-core concept (`netcore01`) is being planned as a future external DNS/Tailscale services module and possible foundation for broader portable/private-network functions. It is not yet documented as a production dependency, router replacement, or quorum voter.

## Defensive Monitoring

Guardian is the defensive monitoring and SIEM VM. It runs Wazuh, receives local host telemetry, receives OpenWrt firewall/DHCP/syslog events, and receives sanitized Proxmox telemetry from the K.E.R.N.E.L. side.

Guardian also runs IDS tooling locally, but it does **not** have full packet visibility across all Proxmox bridges. Full bridge-wide visibility would require an approved mirror, TAP, or dedicated sensor design that is not currently claimed here.

## Remote Access

Some private services use Tailscale for approved remote management or private service access. This repository documents Tailscale usage only at the architecture level and does not publish Tailscale DNS names, auth keys, session details, or device identifiers.

Public Internet exposure is not part of the default VaughnLab model. Any public exposure would require explicit approval and separate documentation.

## Holocron Family Interface

Holocron is the private family-facing UI layer for K.E.R.N.E.L. It supports normal personal Holocron accounts and a shared Family Terminal mode intended for tablet/station use. The shared terminal follows the normal Holocron visual language and role boundaries rather than becoming a separate product.

Household calendar workflows are routed through Holocron while keeping OAuth material, calendar identifiers, and event details outside public documentation. Holocron is fronted by a private reverse proxy for a cleaner internal URL, but that proxy does not represent public Internet exposure.

## Administrative Identity

Supported Linux guests use a named `kernel` administrative identity with SSH key-based access. `kernel` passwords are disabled where standardized, and routine administrative work uses key-based SSH plus approved sudo rights.

Linux root remains a local/console break-glass identity. Root SSH is not a routine access path. Hypervisor maintenance and appliance systems are documented as explicitly approved/platform-specific exceptions rather than forced into the normal guest sudo model.

## WARPi Field Platform

WARPi is the portable security field platform. It supports trusted-network operation, controlled field workflows, Tailscale-backed management when approved, health/state reporting, and security actions through approved wrappers.

Active security tooling belongs on WARPi, the dedicated pentest VM, or other approved security devices, not on the general AI operations node by default.

## AI Security Target

DERP is a deliberately vulnerable AI/security target used for prompt-injection, secret-handling, and defensive AI workflow experiments. DERP is isolated by design and must never hold real secrets or trusted production access.

DERP is on-demand. It should be powered on only for controlled lab use, then stopped again when idle.

## Public Release Workflow

```text
Engineering Change
      |
      v
Documentation Update
      |
      v
Sanitization Review
      |
      v
Automated Release Gate
      |
      v
Manual Approval
      |
      v
GitHub Push
```

The public release path favors architecture, governance, and sanitized workflows over operational dumps. Exact service discovery, host-level private addresses, private DNS, secrets, and sensitive access details stay out of the public repository.
