# 8. Recovery Protocol

## Purpose

Recover from a suspected memory-poisoning incident without assuming that a rollback alone makes the agent safe. The prototype uses synthetic state and simulated actions.

## Recovery states

`DETECTED` → `TRIAGE_REQUIRED` → `QUARANTINED` → `CHECKPOINT_SELECTED` → `RESTORED` → `SAFE_REPLAY` → `REGRESSION_TESTED` → `RECOVERY_VERIFIED`.

Any failed check transitions to `RECOVERY_BLOCKED` and requires investigation or authorized human action. Do not mark the recovery verified merely because the restore function returned successfully.

## Step-by-step protocol

1. **Freeze the test run.** Capture the run ID, last trusted checkpoint ID, current ledger head, and relevant policy version.
2. **Identify the suspected source.** Record why the source was flagged and whether this is a direct detector finding or analyst-provided evidence.
3. **Build impact candidates.** Follow recorded parent/child relationships first. Add inferred semantic links separately and label them as candidates, not facts.
4. **Quarantine.** Prevent normal reads of the confirmed suspicious records. Require authorization for quarantine/unquarantine changes. Keep a record of who performed the operation.
5. **Review descendants.** For each downstream record, show its source links, retrieval events, time, policy state, and reason for review. Do not auto-delete every connected record.
6. **Select a trusted checkpoint.** Verify checkpoint metadata/integrity. “Trusted” means it passed integrity and policy checks available to the system; it is not a claim that the snapshot is free from every unknown attack.
7. **Restore.** Restore into a controlled state. Record the checkpoint ID, operator/principal, policy version, and resulting ledger event.
8. **Replay safely.** Never blindly replay all events. Replay only an allowlisted subset after reapplying current policy and ensuring the operation is idempotent or safely simulated.
9. **Run the same attack again.** The prohibited action must remain blocked.
10. **Run benign controls.** A safe task must still succeed; otherwise the recovery may be too destructive.
11. **Create a recovery report.** Include before/after state IDs, quarantined records, unresolved candidates, tests run, results, and limitations.
12. **Close only with evidence.** If a test fails or a relevant lineage link is missing, recovery remains unverified.

## Recovery invariants

- No live external side effects in the demo.
- A policy denial cannot be bypassed by recovery/replay.
- A quarantined record cannot be recalled via the normal interface.
- Rollback must not erase the evidence needed to investigate the incident.
- Quarantine and restore operations are auditable.
- Inferred influence alone is insufficient for irreversible deletion.

## Manual approval gates

Require approval for selecting a checkpoint that changes active memory, unquarantining a record, deleting records, or replaying any event with potential external side effects. In MVP, external side effects are represented only by a mock sink.

## Recovery definition for evaluation

A scenario counts as recovered only if: (a) the chosen trusted state passes integrity checks, (b) relevant suspicious records are unavailable through normal reads, (c) prohibited mock actions remain blocked when the attack is replayed, and (d) specified benign controls succeed.
