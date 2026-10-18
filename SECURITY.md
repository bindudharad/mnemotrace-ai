# Security Policy

## Scope

MnemoTrace is intended to protect AI-agent memory operations and investigate memory-poisoning scenarios. During the prototype phase, the supported environment is local synthetic data with a mock tool sink.

## Reporting a vulnerability

Do not publish exploitable details in a public issue. Contact the maintainers through a private reporting channel once one is configured. Until then, do not include credentials, real user data, or live target details in issues; contact the repository owner privately.

## Security design expectations

- Sensitive actions must pass through a deterministic policy enforcement point.
- The UI and API must not offer an alternate path that bypasses the gate.
- API endpoints must not be exposed to untrusted networks without authentication and authorization.
- Raw memory contents should not be copied into the audit ledger unless explicitly needed and reviewed.
- Recovery must verify the checkpoint and must not replay arbitrary writes automatically.
- Unknown or incomplete provenance must be displayed as unknown, not trusted.
- Quarantine and rollback actions must themselves be authorized, audited, and tested.

## Supported status

No production release is declared by this documentation pack. Version support, response targets, and security advisories will be defined after an initial release and maintainer process exist.
