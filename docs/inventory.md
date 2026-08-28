# Sanitized Inventory

This inventory is intentionally public-safe. It describes system roles, normal power posture, and major dependencies without credentials, private host-level addresses, Tailscale hostnames, token IDs, or rebuild-sensitive access details.

## Power Posture Summary

| System | Role | Normal State | Public-Safe Posture |
| --- | --- | --- | --- |
| pve01 | Primary Proxmox workload node | Always-on | Cluster node / established virtualization host |
| pve02 | Secondary Proxmox compute node | Always-on | Cluster node / added compute capacity |
| OpenClaw/K.E.R.N.E.L. node | AI operations workspace | Always-on | Protected control-plane environment |
| Holocron | Private web UI | Always-on | Private UI for family/root workflows |
| AdGuard DNS | DNS sinkhole/staging resolver | Always-on | Controlled DNS for routed lab workloads |
| OpenWrt | Routed lab boundary | Always-on | Private lab router, not household router |
| Tickets/GLPI | Helpdesk and ticketing | Always-on | Private ticketing and automation target |
| Guardian | Defensive SIEM/logging | Always-on | Private monitoring and telemetry host |
| Mission backend | WARPi service backend | On-demand | Protected operations service |
| DERP | AI security target | On-demand | Isolated deliberately vulnerable target |
| AI lab VM | Local AI/security experiments | On-demand | Isolated experimentation environment |
| Automation VM | Workflow automation | On-demand | Private automation environment |
| Malware triage VM | Defensive malware analysis | On-demand | Isolated defensive triage workspace |
| Pentest VM | Kali/security assessment VM | On-demand | Approved security assessment workspace |
| WARPi | Portable security field platform | Device/workflow dependent | Approved field and lab security platform |
| netcore01 | Planned Raspberry Pi 5 network services appliance | Planned | External DNS/Tailscale services concept |

## Core / Always-On Systems

### Proxmox Cluster

VaughnLab uses a two-node Proxmox VE cluster. `pve01` is the established workload node and retains the existing segmented virtual-network design and current service placement. `pve02` is the newer cluster member and adds independent CPU, memory, storage, and future workload-placement capacity.

The nodes participate in Corosync quorum over the trusted private management network and are also reachable through approved private Tailscale management paths. The cluster is currently healthy as a two-vote design, which means loss of either voting node removes normal quorum. A separate third-vote/qdevice design is planned; duplicate qdevices hosted inside pve01 and pve02 are intentionally not treated as a resilience solution because they would share the same failure domains as the nodes they arbitrate.

Cluster membership centralizes administration but does not pool the two machines into one giant CPU/RAM resource. Workloads still execute on an individual node unless explicitly migrated or otherwise orchestrated.

The Proxmox host firewall is enabled with a default-deny inbound posture and explicit trusted-management allowances. K.E.R.N.E.L. has validated key-based administrative connectivity to both hypervisors. Public documentation intentionally omits exact management addresses, keys, host fingerprints, and other access material.

Routine automation uses least-privilege Proxmox access where possible. Root or broad host-level authority is treated as an emergency or explicitly approved maintenance path, not a default agent capability.

### OpenClaw / K.E.R.N.E.L. Node

The OpenClaw/K.E.R.N.E.L. node is the AI operations workspace and coordination point. It maintains documentation, runs approved checks, coordinates lab workflows, and interacts with Proxmox through scoped automation.

This node is part of the control plane. It should remain available when experimental systems are stopped, and it should not be treated as the place to run arbitrary offensive tooling or untrusted malware workflows.

K.E.R.N.E.L. uses named administrative identities and key-based access where supported. Protected systems remain outside routine automation unless explicitly brought into scope by the human operator.

### Holocron

Holocron is the private web UI for K.E.R.N.E.L. and family-facing workflows. It provides a controlled interface for chat, tickets, household announcements, shared terminal use, household calendar workflows, and local app features while preserving role boundaries.

Holocron is always-on because it is a private service surface and a user entry point. It depends on the OpenClaw/K.E.R.N.E.L. side for agent responses and on the ticketing system for GLPI-backed ticket intake.

### AdGuard DNS

AdGuard Home provides controlled DNS for routed lab workloads. It is intentionally staged as a private resolver and DNS telemetry point rather than a public service.

OpenWrt advertises AdGuard to the routed lab segments. This keeps DNS behavior more consistent for lab workloads and allows direct DNS bypass attempts to be blocked and logged.

### OpenWrt

OpenWrt is the routed lab boundary for VaughnLab segments. It routes private lab networks for pentest, security, services, AI/lab, and triage workloads using the documented `10.66.x.x` lab ranges.

OpenWrt is always-on because routed lab services and compatibility paths depend on it. It provides DHCP for lab segments, advertises AdGuard DNS, blocks direct DNS bypass from routed workloads, and preserves selected private service paths.

OpenWrt is not the household router. It must not become a default household gateway, NAT boundary, or public exposure point without a separate approved cutover and rollback plan.

### Tickets / GLPI

The ticketing system provides a lightweight private helpdesk and operational tracking service. It supports K.E.R.N.E.L. helper workflows and Holocron ticket intake.

### Guardian

Guardian is the defensive SIEM and monitoring host. It runs Wazuh, receives local host telemetry, receives OpenWrt firewall/DHCP/syslog events, and receives sanitized Proxmox telemetry from the K.E.R.N.E.L. side.

Guardian does **not** currently provide full packet visibility across all Proxmox bridges. That would require an approved mirror, TAP, or dedicated sensor design.

## Planned Network Core

### netcore01

`netcore01` is a planned Raspberry Pi 5 appliance intended to evolve the DEFPI-style private-network concept into a small independent network-services module. The initial design goal is deliberately incremental: external DNS services and Tailscale connectivity first, with routing, wireless/captive-portal, or broader edge-network functions considered only after the base platform is stable.

The Pi 5's built-in networking is sufficient for initial Ethernet-connected DNS/Tailscale work. More advanced wireless gateway or captive-portal designs may require additional network hardware so upstream and downstream/wireless roles can be separated cleanly.

`netcore01` is also the preferred future location to evaluate an independent Proxmox qdevice vote because it would exist outside the two Proxmox-node failure domains. That role is planned, not currently asserted as deployed.

## On-Demand Systems

### Mission Control Backend

The mission backend supports WARPi and future field-operations workflows. It is an operations service rather than a public-facing system.

### DERP

DERP is a deliberately vulnerable AI/security target used for prompt-injection, secret-handling, and defensive AI workflow experiments. DERP is on-demand and isolated and should never contain real secrets, production credentials, customer data, or trusted access to protected systems.

### AI Lab VM

The AI lab VM is a local experimentation host for AI and security work and normally remains stopped outside controlled testing.

### Workflow Automation VM

The workflow automation VM hosts private automation for specific business or personal workflows and remains on-demand under the current power policy.

### Malware Triage VM

The malware triage VM is an isolated defensive analysis workspace for static triage and investigation tooling and remains stopped unless an analysis workflow is active.

### Pentest VM

The pentest VM is a Kali-based security assessment workspace intended for approved testing workflows behind the routed lab boundary.

## WARPi Public Description

WARPi is documented publicly by capability rather than by live operational telemetry:

- Field and lab operating modes
- Approved reporting wrapper
- Approved security command wrapper
- Hardware-aware status collection
- Explicit approval before modifications or non-approved security actions

## Proxmox Lab Pool Description

The lab virtualization layer is designed around:

- Multiple independent cluster nodes rather than a single-host-only control model
- Purpose-built VMs and containers
- Least-privilege automation where available
- Recovery through snapshots and rebuildable configuration
- Public documentation that describes roles without publishing live state
- A deliberate always-on versus on-demand power policy
- An independent future quorum-vote design for the two-node cluster

## Excluded From Public Inventory

The following are intentionally not published:

- Private host-level IP addresses
- Live Tailscale DNS names
- Token IDs or secret file paths
- Personal account identifiers
- Employer/customer workflow details
- Exact SSH keys, usernames, host fingerprints, or credentials
- Raw service discovery or scan output
