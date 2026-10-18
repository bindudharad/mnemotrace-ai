# 7. Event and Memory Data Model

The model is intentionally small for the MVP. Field names may change before the first implementation; update API, migrations, and traceability documents together.

## Memory record

| Field | Type | Purpose |
|---|---|---|
| `memory_id` | string/UUID | Stable identity for a memory record |
| `key` | string | Namespaced logical key; apply size and character limits |
| `value` | application value | Stored content; synthetic data in MVP |
| `value_hash` | string | Optional content digest used for comparison/integrity, not proof of trust |
| `principal` | string | Agent/user identity responsible for operation |
| `trust_label` | enum | Untrusted, observed, quarantined, etc. |
| `source_ref` | string/null | ID of input event or external source record |
| `parent_memory_ids` | list[string] | Explicit records from which this one was derived |
| `created_at` | UTC timestamp | Creation time |
| `status` | enum | Active, quarantined, retired |
| `snapshot_id` | string/null | Checkpoint association when relevant |

## Event record

```json
{
  "event_id": "evt_01H...",
  "run_id": "run_demo_001",
  "trace_id": "trace_001",
  "occurred_at": "2026-10-18T10:00:00Z",
  "principal": "research_agent",
  "operation": "memory.write",
  "memory_id": "mem_017",
  "key": "research.notes",
  "source_ref": "source_supplier_pdf_01",
  "parent_memory_ids": [],
  "policy_decision": "QUARANTINE",
  "policy_rule_id": "POL-MEM-004",
  "reason_codes": ["UNTRUSTED_INSTRUCTION_PATTERN"],
  "detector_findings": [{"detector_id": "instruction-risk-v1", "severity": "high"}],
  "value_redacted": true,
  "snapshot_id": "snap_003"
}
```

This is an illustrative schema, not a real output. Use UTC timestamps. Do not log raw content in the ledger by default. The application may retain synthetic payloads in the test fixture separately.

## Lineage edge

Fields: `edge_id`, `from_id`, `to_id`, `edge_type`, `evidence_type`, `method`, `confidence` (optional), `reason`, `created_at`, `run_id`.

`evidence_type` must be either `RECORDED` or `INFERRED`. Confidence applies only to inferred edges; it is not a probability guarantee. Recorded source edges should cite the exact event/field that created them.

## Policy decision enum

- `ALLOW`
- `DENY`
- `REDACT`
- `QUARANTINE`
- `REVIEW_REQUIRED`

Do not overload detector severity with a policy decision. A detector reports findings; the policy engine decides the permitted operation.

## Storage considerations

- Use parameterized database operations.
- Use transactions where memory changes and event records must agree.
- Document retention/deletion behavior.
- If a hash chain is added, describe it as tamper-evident under stated assumptions—not tamper-proof. Protect signing keys separately if signatures are later introduced.
- Avoid using content hashes as public identifiers when they may enable guessing of low-entropy values.
- Apply schema migrations and test upgrades from an empty database.
