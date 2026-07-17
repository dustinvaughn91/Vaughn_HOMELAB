# Sanitized Inventory

This inventory is intentionally public-safe. It describes system roles and intended operating posture without live private addresses, credentials, or sensitive business details.

## Systems

| System | Role | Platform | Public-Safe Posture |
| --- | --- | --- | --- |
| Proxmox host | Virtualization platform | Proxmox VE | Private virtualization layer |
| OpenClaw/K.E.R.N.E.L. node | AI operations workspace | Linux container/host | Protected control-plane environment |
| Mission control backend | WARPi service backend | Linux VM | Protected operations service |
| WARPi | Portable security field platform | Raspberry Pi / Debian | Approved field and lab security platform |
| AI lab VM | Local AI and security experimentation | Ubuntu VM | Isolated experimentation environment |
| DERP | Deliberately vulnerable AI/security target | Ubuntu container or VM | Isolated training target |
| Automation VM | Private workflow automation host | Ubuntu VM | Private automation environment |

## Proxmox Lab Pool Description

The lab virtualization layer is designed around:

- Purpose-built VMs and containers.
- Least-privilege automation where available.
- Recovery through snapshots and rebuildable configuration.
- Public documentation that describes roles without publishing live state.

## WARPi Public Description

WARPi is documented publicly by capability rather than by live operational telemetry:

- Field and lab operating modes.
- Approved reporting wrapper.
- Approved security command wrapper.
- Hardware-aware status collection.
- Explicit approval before modifications or non-approved security actions.

## Excluded From Public Inventory

The following are intentionally not published:

- Private IP addresses
- Live Tailscale DNS names
- Token IDs or secret file paths
- Personal account identifiers
- Employer/customer workflow details
- Exact SSH keys, usernames, or credentials
