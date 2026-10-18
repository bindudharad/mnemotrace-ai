# 9. API Contract (Draft)

This file describes a proposed local API contract. Endpoints are not implemented until code and tests exist. The MVP may expose equivalent CLI commands first, but their semantics should match this contract.

## General rules

- Bind to `127.0.0.1` by default.
- Use JSON request/response bodies and structured error codes.
- Include `request_id` or `run_id` where operations can be tied to an incident.
- Never expose secret raw values in generic error messages.
- Mutating operations require principal and policy validation.
- The API is not a substitute for enforcing policy inside the core service.

## Proposed endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| `GET` | `/health` | Liveness and version; no sensitive data |
| `POST` | `/api/v1/memory` | Create/write a memory through the guarded service |
| `GET` | `/api/v1/memory/{memory_id}` | Read memory subject to policy and quarantine status |
| `POST` | `/api/v1/memory/{memory_id}/quarantine` | Quarantine a record with a reason and principal |
| `POST` | `/api/v1/recovery/plan` | Build a recovery proposal; does not mutate state |
| `POST` | `/api/v1/recovery/execute` | Execute approved synthetic recovery plan |
| `GET` | `/api/v1/incidents/{incident_id}` | Return incident summary with evidence labels |
| `GET` | `/api/v1/incidents/{incident_id}/lineage` | Return graph nodes/edges, with recorded vs inferred labels |
| `POST` | `/api/v1/evaluations/runs` | Execute a named synthetic scenario set |
| `GET` | `/api/v1/evaluations/runs/{run_id}` | Retrieve metrics and test results |

## Example write request

```json
{
  "principal": "research_agent",
  "key": "supplier.notes",
  "value": "Synthetic benign test note",
  "source_ref": "fixture_supplier_001",
  "parent_memory_ids": [],
  "run_id": "demo_001"
}
```

## Example decision response

```json
{
  "decision": "ALLOW",
  "memory_id": "mem_example_001",
  "event_id": "evt_example_001",
  "policy_rule_id": "POL-MEM-ALLOW-001",
  "reason_codes": [],
  "value_returned": true
}
```

These examples are specifications only, not evidence of a running endpoint.

## Error model

Use stable codes such as `POLICY_DENIED`, `QUARANTINED_MEMORY`, `UNKNOWN_PRINCIPAL`, `CHECKPOINT_INTEGRITY_FAILED`, `RECOVERY_APPROVAL_REQUIRED`, `INVALID_PARENT_REFERENCE`, `EVENT_STORE_UNAVAILABLE`, `RATE_LIMITED`, and `VALIDATION_ERROR`.

## Security acceptance checks

- unauthenticated remote exposure is not enabled by default;
- no endpoint bypasses the core policy engine;
- invalid principal and malformed input tests fail safely;
- incident/lineage responses redact sensitive values;
- restore and quarantine operations produce audit events;
- the action gateway has no public endpoint that lets clients force an `ALLOW` decision.
