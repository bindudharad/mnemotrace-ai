# 6. Threat Model

## Assets to protect

- persistent agent memories and their metadata;
- system/policy instructions and protected keys;
- agent identities and access permissions;
- action authorization decisions;
- event ledger and checkpoints;
- integrity of benchmark results and incident reports.

## Security objectives

- prevent unauthorized memory writes/reads where policy applies;
- detect and explain suspicious memory changes;
- keep prohibited simulated actions from executing;
- preserve enough evidence to investigate a delayed attack;
- restore a verified checkpoint without replaying unsafe records;
- prevent the UI or model from bypassing enforcement.

## Adversary capabilities

Assume an attacker can submit malicious documents, user messages, tool outputs, or memory candidates; may try paraphrases; may exploit an agent's over-trust of retrieved content; and may aim for delayed activation after a session reset. Do not assume the attacker can modify the policy engine or database file directly in the basic threat model. Direct host compromise is a separate, out-of-scope threat that still requires operational safeguards.

## Threat scenarios

| ID | Scenario | Expected defense | Residual risk |
|---|---|---|---|
| T-01 | Direct malicious memory write | Detector and policy deny/quarantine | Unknown payloads can evade detectors |
| T-02 | Poison survives a context reset | Persistent record remains tracked and tested at later recall | Context reset may not clear external caches |
| T-03 | Payload is paraphrased in a derived record | Explicit parent links preserve known lineage; optional semantic analysis flags candidates | Semantic relation detection may miss or over-link records |
| T-04 | One agent writes into another agent's protected namespace | Principal/key authorization denies operation | Identity propagation bugs can undermine policy |
| T-05 | Poisoned memory requests a prohibited tool action | Independent action gateway denies it | Any bypass path to the tool is a critical vulnerability |
| T-06 | Quarantined record is read through an alternate route | All supported reads use the memory service | Direct database access bypasses application policy |
| T-07 | Rollback removes source but leaves child records | Descendant review and recovery tests flag remaining records | Missing lineage means impact can be underestimated |
| T-08 | Ledger leaks sensitive memory contents | Metadata-first events, redaction and access control | hashes can still reveal equality and need protection |
| T-09 | Attacker floods memory with large/rapid writes | Limits, quotas, anomaly flags, backpressure | Resource-exhaustion protection is not complete in MVP |
| T-10 | AI-generated incident explanation invents causal links | Evidence labels and deterministic source data | Users may over-trust narrative text |
| T-11 | Recovery replays hostile operations | Allowlisted replay with per-event policy check | External side effects cannot always be undone |
| T-12 | Benchmark is overfit to known examples | Holdout corpus, benign controls, versioned tests | Small benchmark may not generalize |

## Trust labels

- `UNTRUSTED`: content from a source that has not been approved.
- `OBSERVED`: an event directly recorded by the application.
- `RECORDED_LINEAGE`: explicit source/parent relationship recorded at write time.
- `SUSPECTED_INFLUENCE`: inferred relationship that requires review.
- `QUARANTINED`: hidden from normal reads by policy.
- `VERIFIED_CHECKPOINT`: snapshot whose stored integrity checks passed; this does not mean all its content is semantically safe.

## Security invariants

1. No denied action reaches the mock sink.
2. Normal read APIs never return quarantined records unless the caller uses an authorized review interface.
3. A checkpoint restore cannot skip identity/policy validation.
4. A failed integrity check cannot result in `VERIFIED_CHECKPOINT`.
5. Inferred lineage cannot by itself trigger destructive deletion.
6. No LLM response can directly set an operation to `ALLOW`.
7. Errors must not expose raw secrets or memory values.

## MVP non-goals

The initial demo does not claim protection against compromised hosts, malicious maintainers, kernel-level attacks, arbitrary external tool side effects, every semantic paraphrase, or every type of vector-store poisoning. These should be documented before any broader deployment claim.
