# Project Status and Evidence Tracker

**Last updated:** 2026-10-18  
**Current phase:** Documentation baseline / pre-implementation  
**Rule:** A feature is not “done” because it is described in a document or appears in a screenshot. It is done only when code, automated tests, and acceptance evidence exist.

## Overall status

- [x] Project goal and scope documented
- [x] Proposed architecture documented
- [x] Threat model and safe demo boundary documented
- [x] Requirements and traceability plan documented
- [x] Test and benchmark protocols drafted
- [ ] Application source code implemented
- [ ] Baseline unit tests passing
- [ ] End-to-end poisoning scenario demonstrated
- [ ] Lineage graph verified against ground-truth test links
- [ ] Quarantine and recovery verified
- [ ] Dashboard connected to real event data
- [ ] Clean-environment installation verified
- [ ] Final benchmark run recorded

## Feature evidence table

| Feature | Status | Evidence required | Evidence link / commit |
|---|---|---|---|
| Memory policy core | Planned | Unit tests for allow/deny policy decisions | TBD |
| Stable memory IDs | Planned | Tests prove IDs are stable and unique | TBD |
| Event ledger | Planned | Persistence, ordering, redaction and integrity tests | TBD |
| Source/parent lineage | Planned | Synthetic ground-truth lineage test | TBD |
| Suspicion scoring | Planned | Documented rules and evaluated test cases | TBD |
| Quarantine | Planned | Tests prove quarantined data cannot be recalled through guarded APIs | TBD |
| Trusted checkpoint restore | Planned | Snapshot-integrity and rollback tests | TBD |
| Safe replay | Planned | Replay allowlist and idempotency tests | TBD |
| Mock action gate | Planned | Test proves prohibited sink action never executes | TBD |
| Benchmark runner | Planned | Reproducible report generated from versioned corpus | TBD |
| Dashboard | Planned | UI integration tests and demo runbook evidence | TBD |

## Evidence standards

For each milestone, attach at least one of:

- test output saved with commit SHA and command;
- benchmark report plus exact corpus version;
- screenshot or short recording with a repeatable run command;
- documented API request/response from the local application;
- dependency/security scan output where applicable.

Never write “100% accurate,” “production-ready,” “tamper-proof,” or “fully recovered” unless the claim is narrowly defined and substantiated by evidence. Prefer measurable wording such as “blocked 18 of 20 prohibited mock actions in benchmark v0.1.”
