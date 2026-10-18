# 11. Test Strategy

## Testing philosophy

Security controls need tests for both the behavior they should block and legitimate behavior they should preserve. Test the critical action boundary with deterministic fixtures before integrating an LLM.

## Test layers

### Unit tests

- policy allow/deny decisions;
- principal and namespace access;
- detector interface and finding normalization;
- memory ID and event schema validation;
- lineage edge labeling;
- quarantine state transitions;
- checkpoint checksum/integrity checks;
- replay allowlist and idempotency.

### Integration tests

- memory mutation and event ledger consistency;
- detector plus policy plus storage flow;
- context reset with persistent memory;
- a denied action never reaches mock sink;
- quarantine affects reads;
- restore preserves forensic evidence;
- API authentication/authorization assumptions for any non-local mode.

### End-to-end tests

1. clean benign task completes;
2. direct poison is detected/denied or isolated according to policy;
3. delayed poison remains present after simulated context reset;
4. later action request is stopped by the final gate;
5. the lineage graph matches expected recorded links;
6. recovery is executed and integrity rechecked;
7. the same attack is replayed and remains blocked;
8. benign task still succeeds after recovery.

### Security regression tests

- paraphrased attack payload;
- untrusted source transformed into summary;
- unknown principal;
- cross-agent write to protected key;
- quarantined record requested through each supported read path;
- malformed parent IDs and cyclic graph references;
- oversized and rapid repeated memory writes;
- ledger/storage failure during a sensitive operation;
- error messages and exports checked for leaked raw values;
- attempt to call action sink without gateway authorization;
- recovery replay attempts to repeat a prohibited action.

## Testing tools

Proposed baseline: `pytest`, coverage, a static linter, a dependency vulnerability scanner, and optional API tests using a FastAPI test client. Pin versions in the actual dependency file after implementation.

## Test data policy

Use synthetic names, email addresses under example domains, fake secrets such as `CANARY-DO-NOT-EXFILTRATE-001`, and simulated finance records. Never put real user credentials, real confidential documents, or malware in the test corpus.

## CI gates

- format/lint checks;
- unit tests;
- integration tests;
- security regression suite;
- docs/link consistency where practical;
- benchmark smoke run with a small deterministic subset.

A full benchmark can run separately if it is too slow for every commit, but the required fast regression cases should always run in CI.

## Reporting failures

A failed test report must include command, commit SHA, runtime versions, scenario ID, expected and observed outcomes, and safe logs. A failed security invariant blocks release regardless of the overall test pass percentage.
