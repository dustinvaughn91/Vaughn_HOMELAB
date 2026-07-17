# Security Model

VaughnLab is designed around least privilege, explicit approval, and recoverable operations.

## Core Rules

- Default exposure is private/LAN-only.
- Remote access uses private overlay networking only when approved.
- Public Internet exposure requires explicit approval.
- Router, NAT, firewall, DNS, and billing changes require explicit approval.
- Destructive actions require explicit approval.
- Real secrets are never committed, pasted into chat, or placed in public docs.

## Role Separation

Human operator:

- Final authority
- Approves risky changes
- Owns secrets and external accounts

K.E.R.N.E.L.:

- Documents infrastructure
- Performs approved read-only checks
- Uses least-privilege tokens where available
- Recommends changes before risky operations

WARPi:

- Runs approved security and field tooling
- Provides structured status through `kernel-report`
- Provides security scans through `kernel-security`

DERP:

- Is an intentionally vulnerable test target
- Must never have real secrets
- Must remain isolated from trusted systems

## Public Repository Policy

Before publishing:

- Run secret scanning
- Remove private addresses and DNS names
- Remove customer or employer details
- Avoid raw logs unless sanitized
- Prefer architecture summaries over operational dumps

## Approved Security Activity Pattern

Security activity should be routed through approved wrappers when available. For WARPi, use:

```text
kernel-security <approved-command> <target>
```

Do not bypass an approved wrapper with raw tooling unless explicitly approved.

