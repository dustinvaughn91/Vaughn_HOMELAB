# Security Policy

## Scope

This repository documents VaughnLab architecture, governance, and public-safe operating patterns. It is intentionally sanitized and should not contain:

- Real secrets, tokens, keys, certificates, or credentials.
- Private IP addresses, private DNS names, or Tailscale hostnames.
- Raw security scan output for private systems.
- Customer, employer, or third-party confidential data.
- Rebuild-sensitive operational access details.

## Responsible Disclosure

If you find a security issue in the public documentation, such as exposed secrets or private infrastructure details, please open a private security advisory or contact the repository owner through GitHub.

Please do not publish suspected secrets, private network details, or exploit steps publicly.

## DERP Clarification

DERP is a deliberately vulnerable AI/security training target. Vulnerability in DERP is intentional only inside its controlled lab scope.

DERP must never contain real secrets, production credentials, customer data, or trusted access to protected systems.

## Public Documentation Safety

Before public changes are pushed:

- Run secret scanning.
- Search for private IPs and Tailscale hostnames.
- Remove exact service discovery and live operational state.
- Keep raw logs, packet captures, evidence folders, and scan reports private.
- Prefer architecture and governance summaries over operational dumps.

## Approval Boundary

This public repository does not grant permission to test, scan, access, or attack any VaughnLab system. Security testing is only authorized through explicitly approved lab workflows.
