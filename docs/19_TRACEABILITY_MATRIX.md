# 19. Requirements Traceability Matrix

Use this table to connect what the team promises to what has been implemented and tested.

| Requirement | Component | Planned test | Evidence path | Status |
|---|---|---|---|---|
| FR-001 Policy decisions | `core/policy.py` | `test_policy_decisions.py` | TBD | Planned |
| FR-002 Stable IDs | `core/memory_service.py` | `test_memory_ids.py` | TBD | Planned |
| FR-003 Audit events | `ledger/event_store.py` | `test_event_ledger.py` | TBD | Planned |
| FR-004 Explicit lineage | `lineage/graph.py` | `test_ground_truth_lineage.py` | TBD | Planned |
| FR-005 Protected action gate | `actions/gateway.py` | `test_action_gate_bypass.py` | TBD | Planned |
| FR-006 Quarantine | `containment/quarantine.py` | `test_quarantine_reads.py` | TBD | Planned |
| FR-007 Trusted restore | `recovery/service.py` | `test_snapshot_restore.py` | TBD | Planned |
| FR-008 Delayed attack scenario | `evaluation/scenarios.py` | `test_delayed_poisoning_e2e.py` | TBD | Planned |
| FR-009 Benign controls | `evaluation/runner.py` | `test_benign_workflow.py` | TBD | Planned |
| FR-010 Benchmark report | `evaluation/runner.py` | `test_report_reproducibility.py` | TBD | Planned |
| FR-011 Lineage UI | `frontend/` | UI test / demo check | TBD | Planned |
| FR-012 Descendant review | `containment/` | `test_descendant_review.py` | TBD | Planned |
| FR-013 Safe replay | `recovery/service.py` | `test_replay_allowlist.py` | TBD | Planned |
| FR-014 Evidence export | `api/` | `test_export_redaction.py` | TBD | Planned |
| NFR-001 Mock-only actions | `actions/gateway.py` | configuration/integration test | TBD | Planned |
| NFR-004 Privacy/redaction | `ledger/` | `test_no_raw_value_leak.py` | TBD | Planned |
| NFR-006 Fail-safe critical path | Core services | failure injection tests | TBD | Planned |

## Updating this matrix

When a requirement changes, update the requirements document, this matrix, tests, and project status in the same pull request. A passing unit test is not enough for a user-visible capability if the end-to-end workflow is not tested.
