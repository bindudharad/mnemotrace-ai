# 3. Solution and Novelty

## Product concept

MnemoTrace is an evidence-first memory security workbench. It connects memory policy enforcement to an incident lifecycle: inspect → link → contain → recover → prove.

## Core building blocks

### A. Guarded memory boundary
All supported writes, reads, deletes, promotions, snapshots, and restores pass through an explicit service boundary. Direct access to the underlying store is prohibited in the prototype architecture.

### B. Memory event ledger
Every operation creates an event with a unique event ID, time, principal, operation, memory ID, policy decision, detector findings, and safe source/parent references. The ledger should avoid raw memory content by default.

### C. Causal lineage view
The graph contains two relationship types:

- **Recorded lineage:** explicit source/parent IDs recorded when a memory was derived;
- **Suspected influence:** an inference based on retrieval sequence or similarity, shown with method, confidence, and explanation.

The UI must never present suspected influence as confirmed causal proof.

### D. Scoped containment
When a record is confirmed suspicious, it is quarantined. Directly linked descendants are flagged for review. A graph connection alone does not automatically prove that every descendant is malicious; containment rules should be conservative, reversible, and visible.

### E. Verified recovery
Recovery includes checkpoint integrity verification, quarantine review, policy-approved replay, and the same adversarial/benign regression suite. A successful rollback alone is not considered proof of recovery.

### F. Replay benchmark
An immutable scenario manifest records each scenario's ID, initial state, injected test record, reset behavior, expected policy result, mock-sink condition, and expected benign behavior.

## Novelty claim to use responsibly

**Proposed contribution:** integrate delayed poisoning scenarios, provenance-aware incident investigation, scoped containment, trusted-state restoration, and post-recovery regression testing into one reproducible workflow for long-lived AI-agent memory.

Do not claim that memory poisoning, provenance graphs, quarantine, rollback, or security benchmarks are individually new. The novelty claim is the integrated workflow and its evaluated implementation. A prior-art review and working prototype are required before making stronger originality claims.

## Comparison with common defensive patterns

| Common pattern | Useful contribution | Gap MnemoTrace targets |
|---|---|---|
| Prompt-only filtering | Flags suspicious current input | May not explain later use of already stored memory |
| Write-time detector | Stops some unsafe writes | May not trace derived records or delayed activation |
| Audit log | Records events | May not connect memory source to downstream use |
| Snapshot/rollback | Restores an earlier state | May not review descendants or verify future behavior |
| Model-generated incident summary | Speeds explanation | Can hallucinate causality if evidence is not linked |
| MnemoTrace proposed loop | Links events, containment, recovery and retesting | Must be validated; graph quality and recovery correctness remain open engineering questions |

## Example

A malicious note is written as `M-017`; the session ends; a later task retrieves it; a summary `M-024` references its parent ID; an action request is denied by the policy gate. The graph shows the recorded parent link between `M-017` and `M-024`. If semantic analysis merely suggests another record may be related, the edge is labelled `SUSPECTED_INFLUENCE`, not `RECORDED_LINEAGE`.

## What will make the contribution credible

- explicit threat model and non-goals;
- implementation evidence for each advertised capability;
- deterministic attack and benign scenario corpus;
- comparison with an unprotected baseline and a simple write-time detector;
- full reporting of false blocks, attack success, lineage coverage, latency, and limitations.
