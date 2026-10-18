# 4. Product and Engineering Requirements

Priority levels: **P0** = MVP critical; **P1** = valuable after core loop; **P2** = stretch.

## Functional requirements

| ID | Priority | Requirement | Acceptance criteria |
|---|---|---|---|
| FR-001 | P0 | Evaluate memory operations against explicit policies | Unit tests cover allow, deny, redact/quarantine, and unknown-policy outcomes |
| FR-002 | P0 | Assign stable IDs to memory records and events | IDs are unique; parent references resolve or are explicitly marked missing |
| FR-003 | P0 | Record an audit event for every guarded operation | Event includes actor, operation, decision, time, run ID, and memory ID where relevant |
| FR-004 | P0 | Preserve explicit provenance links | Test fixture links can be reconstructed exactly from the ledger |
| FR-005 | P0 | Gate simulated high-risk actions | A denied action cannot reach the mock sink, even if the model requests it |
| FR-006 | P0 | Quarantine a suspicious memory record | Quarantined record is not returned by guarded recall unless an authorized review path is used |
| FR-007 | P0 | Restore a trusted checkpoint | Restore validates snapshot ID/integrity and records an audit event |
| FR-008 | P0 | Run a delayed-poisoning demo | Payload persists across simulated context reset; expected action is blocked after protection |
| FR-009 | P0 | Run benign controls | Normal memory operations and a legitimate task succeed under the same test setup |
| FR-010 | P0 | Produce a benchmark report | Report states exact corpus version, counts, metrics, command, and environment |
| FR-011 | P1 | Show interactive memory lineage | UI distinguishes recorded source links and inferred influence |
| FR-012 | P1 | Review possible contaminated descendants | User can see why each record was flagged and approve/reject action |
| FR-013 | P1 | Replay approved events after recovery | Replay excludes quarantined and non-approved events; duplicate replay is handled safely |
| FR-014 | P1 | Export incident evidence | Export redacted JSON/Markdown with event IDs and policy reasons |
| FR-015 | P2 | Add optional semantic relationship analysis | It proposes edges but cannot authorize operations |
| FR-016 | P2 | Add optional framework adapters | Each adapter has its own integration tests and documented limitations |

## Non-functional requirements

- **NFR-001 Safety:** external actions are mocked by default.
- **NFR-002 Security:** no direct unguarded route to the memory store or mock tool executor.
- **NFR-003 Explainability:** every policy denial includes a stable rule ID and reason code.
- **NFR-004 Privacy:** raw values are not stored in the ledger by default; secrets are redacted.
- **NFR-005 Reproducibility:** tests use fixed seeds and versioned scenario manifests.
- **NFR-006 Reliability:** failures in authorization, snapshot integrity, or ledger persistence fail safely for protected operations.
- **NFR-007 Accessibility:** essential status and graph information is also represented in text/table form; color is not the only signal.
- **NFR-008 Maintainability:** core policy, storage, lineage, recovery, API, UI, and evaluation are separate modules.
- **NFR-009 Observability:** request/run IDs connect UI actions, API calls, security decisions, and benchmark outputs.
- **NFR-010 Performance:** measure overhead; do not set a performance target until baseline measurements exist.

## Requirements explicitly outside the MVP

- support for every agent framework or memory backend;
- automatic decisions on live enterprise data;
- guarantees that semantic provenance is perfectly accurate;
- cloud multi-tenancy or production identity management;
- proof that all possible poisoning attacks are detectable.

## Definition of done

A requirement is done only when: implementation exists, relevant automated tests pass, user documentation is updated, evidence is recorded in `PROJECT_STATUS.md`, and any limitation is added to the release notes.
