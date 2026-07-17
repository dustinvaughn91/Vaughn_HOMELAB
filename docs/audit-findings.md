# Audit Findings

Snapshot date: 2026-07-17 UTC

This is a public-safe summary of the current environment audit.

## Healthy Signals

- Proxmox host is online.
- Lab storage is active with healthy free space.
- WARPi is online in Normal Mode.
- WARPi mission backend health check is passing.
- WARPi Tailscale, SSH, GPS service, and K.E.R.N.E.L. service are active.
- Kismet is intentionally disabled at boot and launched only when needed.
- DERP and the AI lab VM are stopped by default.
- Local memory embeddings for K.E.R.N.E.L. are running locally, avoiding API embedding costs.

## Current Gaps

- WARPi documentation audit reports old mode-script paths as missing.
- WARPi has only one project documentation file under its documentation directory so far.
- Some service warnings are present on WARPi and should be triaged over time.
- GitHub publishing path still needs authenticated repo access from the automation environment.
- Public documentation should remain sanitized before every push.

## WARPi Localhost Scan

The approved WARPi security wrapper was used to scan localhost.

Open services observed:

```text
22/tcp    SSH
5060/tcp  SIP
```

A prior scan also briefly observed an additional local service on `8081/tcp`; it was not present in the later scan. This should be rechecked if that service matters.

## Notes

This report avoids private network identifiers and raw operational logs. Full details remain local.

