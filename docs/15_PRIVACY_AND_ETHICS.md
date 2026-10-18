# 15. Privacy and Responsible Use

## Data minimization

The default ledger should store event metadata, IDs, hashes where appropriate, policy decisions, detector IDs, and redacted explanations. It should not copy full memory values into audit events by default. The synthetic demo may store harmless fixture content in the test database so scenarios can be reproduced.

## Redaction and retention

- Define redaction before implementing exports.
- Do not assume a hash anonymizes data; it may reveal repeated values or be guessable.
- Document how to clear the local database and generated reports.
- Avoid retaining input documents after extraction unless required for the synthetic test.
- Exports must remove secrets, access tokens, personal data, and private source content.

## Human control

- Quarantine should be reversible and auditable.
- Irreversible deletion and broad descendant quarantine require human review.
- The system must not make consequential business decisions based only on an inferred graph edge.
- AI explanations must cite event IDs or detector findings and state uncertainty.

## Safe demo boundaries

- All poisoning payloads are synthetic and only target the local mock environment.
- Never send real data to a real external address.
- Do not test unauthorized systems, credentials, or third-party agents.
- Do not execute submitted documents or tools as code.

## Explainability policy

Every alert should show: observed event(s), detection rule or method, policy outcome, known provenance, inferred relations (if any), uncertainty, and the next safe operator action. If the system lacks evidence, it must say “unknown” or “needs review.”

## Future deployment requirements

A production deployment would need a privacy review, access control, audit-retention policy, secret-management plan, secure update mechanism, incident-response process, and assessment of applicable legal/compliance obligations. This prototype does not claim to satisfy any particular compliance certification.
