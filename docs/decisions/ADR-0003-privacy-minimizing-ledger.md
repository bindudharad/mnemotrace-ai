# ADR-0003: Privacy-Minimizing Evidence Ledger

- **Status:** Accepted for MVP design
- **Date:** 2026-10-18

## Context

The ledger is needed for incident reconstruction, but storing every memory value can create a second sensitive database and increase breach impact.

## Decision

Store operation metadata, stable IDs, source/parent references, policy decisions, detector finding metadata, and redacted explanations by default. Keep raw test payloads in the synthetic fixture store only where needed. Redaction is applied before general logs and exports.

## Consequences

- The incident graph may require a protected, authorized lookup to view a synthetic record's contents.
- Content hashes are not treated as anonymization or as proof that a value is trustworthy.
- The design needs tests for accidental raw-value leakage and retention/deletion behavior.
- If a future use case requires raw content retention, it needs a documented threat/retention review.
