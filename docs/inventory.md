# Sanitized Inventory

This inventory is intentionally public-safe. It describes system roles and current observed state without live private addresses, credentials, or sensitive business details.

## Systems

| System | Role | Platform | Public-Safe State |
| --- | --- | --- | --- |
| Proxmox host | Virtualization platform | Proxmox VE 8.x | Online and healthy |
| OpenClaw/K.E.R.N.E.L. node | AI operations workspace | Linux container/host | Active control-plane environment |
| Mission control backend | WARPi service backend | Linux VM | Protected operations service |
| WARPi | Portable security field platform | Raspberry Pi / Debian | Normal mode, connected, healthy |
| AI lab VM | Local AI and security experimentation | Ubuntu VM | Stopped by default |
| DERP | Deliberately vulnerable AI/security target | Ubuntu container or VM | Stopped by default |
| Automation VM | Private workflow automation host | Ubuntu VM | Running, private access only |

## Proxmox Lab Pool Snapshot

Recent read-only inventory showed:

- Lab pool available
- Proxmox host online
- DERP target stopped
- AI lab VM stopped
- Automation VM running
- Local storage active with healthy free space
- Routine automation access limited to approved lab resources

## WARPi Snapshot

Recent WARPi report showed:

- Mode: Normal
- State: Connected
- Trusted Wi-Fi: available
- Tailscale: active
- Mission backend: healthy
- GPS service: running, searching for fix
- Kismet: disabled at boot by design
- SSH: active
- Root disk: low utilization
- Temperature: normal operating range

## Excluded From Public Inventory

The following are intentionally not published:

- Private IP addresses
- Live Tailscale DNS names
- Token IDs or secret file paths
- Personal account identifiers
- Employer/customer workflow details
- Exact SSH keys, usernames, or credentials

