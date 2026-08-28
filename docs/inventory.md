# Sanitized Inventory

This inventory is intentionally public-safe. It describes system roles, normal power posture, and major dependencies without credentials, private host-level addresses, Tailscale hostnames, token IDs, or rebuild-sensitive access details.

## Power Posture Summary

| System | Role | Normal State | Public-Safe Posture |
| --- | --- | --- | --- |
| Proxmox cluster | Virtualization platform | Always-on | Private two-node cluster virtualization layer |
| netcore01 | Infrastructure appliance | Always-on | Physical witness and DNS/Tailscale appliance |
| Proxmox host | Virtualization platform | Always-on | Private virtualization layer |
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

## Core / Always-On Systems

### Proxmox Host

The Proxmox host is the virtualization foundation for VaughnLab. It runs the private control-plane services, segmented lab systems, and on-demand security/AI workloads.

Routine automation uses least-privilege Proxmox access where possible. Root or broad host-level authority is treated as an emergency or explicitly approved maintenance path, not a default agent capability.

The public repository documents Proxmox as an architecture layer and avoids publishing exact host access paths, token IDs, or privileged command material.

### OpenClaw / K.E.R.N.E.L. Node

The OpenClaw/K.E.R.N.E.L. node is the AI operations workspace and coordination point. It maintains documentation, runs approved checks, coordinates lab workflows, and interacts with Proxmox through scoped automation.

This node is part of the control plane. It should remain available when experimental systems are stopped, and it should not be treated as the place to run arbitrary offensive tooling or untrusted malware workflows.

K.E.R.N.E.L. uses named administrative identities and key-based access where supported. Protected systems remain outside routine automation unless explicitly brought into scope by the human operator.

### Holocron

Holocron is the private web UI for K.E.R.N.E.L. and family-facing workflows. It provides a controlled interface for chat, tickets, household announcements, shared terminal use, household calendar workflows, and local app features while preserving role boundaries.

Holocron is always-on because it is a private service surface and a user entry point. It depends on the OpenClaw/K.E.R.N.E.L. side for agent responses and on the ticketing system for GLPI-backed ticket intake.

Holocron application users are separate from Linux machine-login accounts. A Family Terminal mode provides a shared/tablet-oriented station identity for household use without turning that station into a personal account. Per-account UI preferences now cover theme, accessibility, and notification intent while keeping settings isolated to the authenticated Holocron account.

Public docs describe the role model and preference surface without publishing live user records, private URLs, session keys, calendar identifiers, notification delivery internals, or credentials.

### AdGuard DNS

AdGuard Home provides controlled DNS for routed lab workloads. It is intentionally staged as a private resolver and DNS telemetry point rather than a public service.

OpenWrt advertises AdGuard to the routed lab segments. This keeps DNS behavior more consistent for lab workloads and allows direct DNS bypass attempts to be blocked and logged.

Household-wide router/client DNS cutover is not implied. The public documentation describes the DNS role without publishing credentials or operational admin paths.

### OpenWrt

OpenWrt is the routed lab boundary for VaughnLab segments. It routes private lab networks for pentest, security, services, AI/lab, and triage workloads using the documented `10.66.x.x` lab ranges.

OpenWrt is always-on because routed lab services and compatibility paths depend on it. It provides DHCP for lab segments, advertises AdGuard DNS, blocks direct DNS bypass from routed workloads, and preserves selected private service paths.

OpenWrt is not the household router. It must not become a default household gateway, NAT boundary, or public exposure point without a separate approved cutover and rollback plan.

### Tickets / GLPI

The ticketing system provides a lightweight private helpdesk and operational tracking service. It supports K.E.R.N.E.L. helper workflows and Holocron ticket intake.

Tickets is always-on because it is a shared internal workflow dependency. Holocron and K.E.R.N.E.L. automation rely on it for ticket creation, follow-up, and status tracking.

Public docs describe the ticketing role and integrations without publishing application credentials, API tokens, private allowlists, or direct service URLs.

### Guardian

Guardian is the defensive SIEM and monitoring host. It runs Wazuh, receives local host telemetry, receives OpenWrt firewall/DHCP/syslog events, and receives sanitized Proxmox telemetry from the K.E.R.N.E.L. side.

Guardian is always-on because it provides the defensive logging and alerting baseline. It helps correlate routed-lab DNS bypass logs, Proxmox task/resource events, and local security telemetry.

Guardian does **not** currently provide full packet visibility across all Proxmox bridges. That would require an approved mirror, TAP, or dedicated sensor design. Public docs should not imply broader visibility than the current architecture actually provides.

## On-Demand Systems

### Mission Control Backend

The mission backend supports WARPi and future field-operations workflows. It is an operations service rather than a public-facing system.

Mission is on-demand and protected outside routine automation scope. It should be started for approved development or field-ops work and stopped when idle.

Public docs describe the backend role only at a high level. Detailed access paths and operational internals remain private.

### DERP

DERP is a deliberately vulnerable AI/security target used for prompt-injection, secret-handling, and defensive AI workflow experiments.

DERP is on-demand and isolated. It should never contain real secrets, production credentials, customer data, or trusted access to protected systems.

DERP may be intentionally weak inside its controlled lab scope, but public docs must make clear that those weaknesses are part of a training target, not a pattern for trusted systems.

### AI Lab VM

The AI lab VM is a local experimentation host for AI and security work. It has historically hosted local model experiments and staging work before workloads moved to more specific systems.

It is on-demand and should normally remain stopped. Start it only for local AI/security experiments, migration work, or controlled testing.

The public docs describe its role as a sandbox and avoid publishing live configuration, model paths, or private runtime details.

### Workflow Automation VM

The workflow automation VM hosts private automation for specific business or personal workflows. It is not a public service and should not be treated as a general-purpose exposure point.

It is on-demand under the current power policy. Start it only when automation work is needed, then stop it when idle.

Public docs describe the automation role without publishing customer/employer data, live service URLs, credentials, browser automation targets, or workflow secrets.

### Malware Triage VM

The malware triage VM is an isolated defensive analysis workspace for static triage and investigation tooling.

It is on-demand and should remain stopped unless a defensive analysis workflow is active. Unknown samples and risky artifacts should stay away from the control plane and normal-use systems.

Public docs describe the role and isolation goal without publishing sample details, investigation artifacts, or live triage findings.

### Pentest VM

The pentest VM is a Kali-based security assessment workspace. It belongs behind the routed lab boundary and is intended for approved testing workflows.

It is on-demand and should remain stopped unless an assessment or lab exercise is active. Offensive tooling belongs here, WARPi, or other explicitly approved security platforms rather than on the general AI operations node.

Public docs describe the role and approval model without publishing targets, live scan output, credentials, or private assessment details.

## WARPi Public Description

WARPi is documented publicly by capability rather than by live operational telemetry:

- Field and lab operating modes
- Approved reporting wrapper
- Approved security command wrapper
- Hardware-aware status collection
- Explicit approval before modifications or non-approved security actions

## Proxmox Lab Pool Description

The lab virtualization layer is designed around:

- Purpose-built VMs and containers
- Least-privilege automation where available
- Recovery through snapshots and rebuildable configuration
- Public documentation that describes roles without publishing live state
- A deliberate always-on versus on-demand power policy

## Excluded From Public Inventory

The following are intentionally not published:

- Private host-level IP addresses
- Live Tailscale DNS names
- Token IDs or secret file paths
- Personal account identifiers
- Employer/customer workflow details
- Exact SSH keys, usernames, or credentials
- Raw service discovery or scan output
