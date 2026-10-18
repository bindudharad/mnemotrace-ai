# 10. Step-by-Step Implementation Plan

Build the smallest end-to-end loop first. Resist building a complex dashboard before the policy boundary, mock sink, and replay tests work.

## Milestone M0 — Repository and baseline

**Deliverables:** project package skeleton, pinned/declarative dependencies, `.gitignore`, formatting/lint configuration, empty test suite, CI workflow, and this documentation pack in the repository.

**Tasks:**
- create a clean repository and virtual environment;
- define Python and Node versions if frontend is used;
- add dependency lock strategy;
- confirm `pytest` works from a fresh clone;
- add a docs-link checker or manually verify relative links.

**Exit criteria:** clean setup and CI pass on a trivial baseline; no credentials or test data containing secrets are committed.

## Milestone M1 — Policy core and mock action gate

**Deliverables:** decision enum, policy rules, principal identity model, guarded memory service interface, mock action sink.

**Tasks:**
- implement allow/deny/quarantine decision logic;
- add explicit namespace access rules;
- route every memory operation through one service boundary;
- implement a mock action request and a final independent gate;
- test that denied action never reaches sink.

**Exit criteria:** deterministic unit/integration tests prove the security invariants in `docs/06_THREAT_MODEL.md`.

## Milestone M2 — Memory store and event ledger

**Deliverables:** SQLite schema/migrations, memory IDs, event IDs, event ordering, redaction rules.

**Tasks:**
- create repository interfaces;
- implement memory CRUD with policy decisions;
- persist operation events transactionally where possible;
- add run and trace IDs;
- define behavior for failures between state mutation and ledger append.

**Exit criteria:** tests cover persistence, malformed input, redaction, duplicate IDs, invalid parent IDs, and store/ledger failure behavior.

## Milestone M3 — Delayed attack simulator

**Deliverables:** deterministic attack and benign fixtures, a context-reset simulation, scenario runner.

**Tasks:**
- plant synthetic poison in memory;
- reset only the conversation context while keeping persistent storage;
- start a later task that retrieves the record;
- demonstrate unprotected baseline behavior using a mock sink;
- enable policy gate and demonstrate the action is denied.

**Exit criteria:** repeated runs produce the same expected classifications and no real external action.

## Milestone M4 — Lineage and impact candidates

**Deliverables:** recorded graph edges, event timeline, query API, initial graph view or CLI report.

**Tasks:**
- propagate `source_ref` and `parent_memory_ids` when records are derived;
- build graph from recorded edges;
- label inferred links separately;
- display edge evidence and missing provenance;
- test graph completeness against known fixture relationships.

**Exit criteria:** exact source links in the test fixture are reproduced; unknown edges are not silently invented.

## Milestone M5 — Containment and recovery

**Deliverables:** quarantine service, trusted checkpoint selection, restore, policy-approved replay, recovery record.

**Tasks:**
- block normal reads for quarantined entries;
- preserve forensic events during restore;
- review children/derived records;
- replay only allowlisted/idempotent simulated operations;
- repeat attack and benign tests after recovery.

**Exit criteria:** recovery invariants pass; failed validation never reports `RECOVERY_VERIFIED`.

## Milestone M6 — Benchmark and UI

**Deliverables:** versioned corpus, baseline comparisons, metrics report, incident UI, demo runbook.

**Tasks:**
- add scenarios and benign controls;
- compare no-protection, simple write-time filter, and MnemoTrace policy/lineage workflow;
- record corpus hash, code commit, dependencies, machine, commands, and results;
- build UI sections for timeline, graph, quarantine, recovery, and test metrics.

**Exit criteria:** a new team member can run the documented demo without hidden setup; benchmark claims can be reproduced.

## Milestone M7 — Final readiness

**Deliverables:** fresh-clone verification, security review, known-limitations list, final report and pitch.

**Exit criteria:** `docs/17_RELEASE_CHECKLIST.md` completed, all critical findings addressed or disclosed, and no unsupported claims in the pitch.

## Priority rule

If time runs short, preserve the complete safety loop: policy gate → event record → delayed attack replay → quarantine/restore → retest. Reduce UI complexity rather than removing proof or safety controls.
