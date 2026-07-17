# WARPi Remote Operations

WARPi remote operations use standard OpenSSH and approved K.E.R.N.E.L. wrappers.

## Rules

- Use standard OpenSSH.
- Do not use `tailscale ssh`.
- Do not request sudo for security scans.
- Do not invent raw `nmap`, `curl`, `openssl`, `bettercap`, `aircrack-ng`, `tcpdump`, or `tshark` commands when a `kernel-security` command exists.
- Do not modify WARPi without explicit approval.

## Status

```bash
kernel-report --json
```

## Documentation Audit

```bash
kernel-doc-audit --json
```

## Approved Security Activity

```bash
kernel-security <approved-command> <target>
```

If `kernel-security` rejects the target, stop and ask for target approval.

## Example

```bash
kernel-security scan 127.0.0.1
```

This scans WARPi's own localhost through the approved wrapper.
