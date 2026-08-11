<div align="center">

<img src="../../assets/warpi-logo.png" alt="WARPi — Wireless Assessment & Reconnaissance Platform" width="420">

# WARPi Remote Operations

**Controlled remote operations for VaughnLab's portable field-security platform.**

[WARPi Overview](../warpi.md) • [Security Model](../security-model.md) • [Architecture](../architecture.md)

</div>

---

## Purpose

WARPi remote operations use **standard OpenSSH** and approved K.E.R.N.E.L. wrappers. The goal is to give the AI operations layer enough visibility and execution capability to coordinate authorized field workflows without turning the general control plane into an unrestricted security-tool host.

This runbook is intentionally public-safe. It documents command patterns and safety boundaries without publishing live credentials, private addresses, field targets, interface configuration, or rebuild-sensitive access details.

---

## Operating Rules

- Use standard OpenSSH.
- Do not use `tailscale ssh` as the WARPi administration model.
- Do not request sudo merely to run security scans.
- Do not invent raw `nmap`, `curl`, `openssl`, `bettercap`, `aircrack-ng`, `tcpdump`, or `tshark` commands when an approved `kernel-security` command exists.
- If `kernel-security` rejects a target, **stop and request target approval**.
- Do not modify WARPi itself without explicit approval.
- Prefer dry-run/planner behavior before network-mode or field-state changes.
- Treat unexpected state, malformed configuration, or lost assumptions as a safe-stop condition rather than guessing.

---

## Quick Reference

| Task | Approved command |
|---|---|
| Platform health/state | `kernel-report --json` |
| Documentation drift check | `kernel-doc-audit --json` |
| Approved assessment action | `kernel-security <approved-command> <target>` |

---

## Platform Status

```bash
kernel-report --json
```

Use the structured report as the preferred remote health/state source before making assumptions about WARPi's current operating condition.

---

## Documentation Audit

```bash
kernel-doc-audit --json
```

Use this to identify drift between documented WARPi behavior and the current implementation before starting broader maintenance or development work.

---

## Approved Security Activity

```bash
kernel-security <approved-command> <target>
```

Example against WARPi itself:

```bash
kernel-security scan 127.0.0.1
```

If the wrapper rejects the requested target or action, the rejection is the policy boundary working correctly. Do not replace the wrapper with an unrestricted raw-tool invocation to bypass that decision.

---

## Mode Operations

WARPi's dispatcher work separates planning from disruptive state transitions. The current validated public-safe command model includes:

```text
warpi mode enter-field
warpi mode return-normal
```

These paths are developed and tested as dry-run planners before real state changes are trusted. Mode logic should validate the expected runtime state and stop safely when that state is unavailable.

> [!IMPORTANT]
> A successful dry-run validates command structure and planner behavior. It does not by itself prove a real field-network transition has occurred.

---

## K.E.R.N.E.L. Workflow

```text
Read existing WARPi docs/source
        ↓
Check current health/state
        ↓
Use approved wrapper or dispatcher
        ↓
Validate the targeted behavior
        ↓
Review for unintended changes
        ↓
Document the durable result
        ↓
Stop at a clean checkpoint
```

For development work, repeated failed edits, uncertain file structure, unexpected corruption, or provider/model instability are reasons to stop and recover rather than continue blindly.

---

## Public Repository Boundary

Do not publish:

- API keys, passwords, private keys, tokens, or session secrets
- Live field targets or customer/employer information
- Private Tailscale names or authentication material
- Exact rebuild-sensitive remote-access configuration
- Raw private assessment output that exposes unnecessary operational detail

The public documentation should explain **how WARPi is engineered and controlled**, not disclose the material needed to impersonate or rebuild its trusted access paths.

---

<div align="center">

**FIELD OPERATIONS • APPROVED TARGETS • CONTROLLED EXECUTION**

See the full [WARPi project overview](../warpi.md).

</div>
