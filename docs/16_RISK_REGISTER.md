# 16. Risk Register

Likelihood/impact labels are initial qualitative estimates; revisit them after implementation and testing.

| ID | Risk | Likelihood | Impact | Mitigation | Owner / status |
|---|---|---|---|---|---|
| R-01 | Inferred graph edge is mistaken for proof | Medium | High | Explicit `RECORDED` vs `INFERRED` edge types, visual distinction, evidence panel | Project / Open |
| R-02 | Action sink can be called without policy gate | Medium | Critical | Single gateway, no direct route, negative security tests | Backend / Open |
| R-03 | Quarantine misses a copy or descendant | High | High | Recorded lineage propagation, descendant review, benchmark ground truth | Core / Open |
| R-04 | Recovery replays malicious operation | Medium | Critical | Allowlisted replay, recheck policy, mock-only execution, idempotency checks | Recovery / Open |
| R-05 | Detector false positives block normal work | Medium | High | Benign controls, review state, metric/reporting, policy tuning | Detection / Open |
| R-06 | Detector false negatives are overclaimed | Medium | High | Versioned corpus, holdout tests, explicit scope/limitations | Evaluation / Open |
| R-07 | Audit ledger leaks raw memory | Medium | High | Metadata-first schema, redaction tests, export review | Storage / Open |
| R-08 | UI leaks cross-principal memory | Low/Medium | High | API-side authorization, tenant-scope tests before multi-user work | API / Open |
| R-09 | Database and ledger disagree after partial failure | Medium | High | Transactions, failure injection tests, repair/reporting policy | Storage / Open |
| R-10 | Project scope exceeds hackathon time | High | Medium | Prioritize complete loop; defer cloud/framework breadth | Team / Open |
| R-11 | Benchmarks are too small or too easy | High | Medium/High | Holdout scenarios, varied benign controls, report raw counts | Evaluation / Open |
| R-12 | Dependency/model cannot be installed at venue | Medium | Medium | Core offline mode, lock dependencies, preflight test and recording backup | DevOps / Open |
| R-13 | Name conflicts with an existing mark/project | Unknown | Medium | Search repository/brand availability before public launch | Team / Open |
| R-14 | Documentation implies unimplemented capabilities | Medium | High | Status labels, project status table, release checklist | Documentation / Open |

## Escalation rule

Any confirmed bypass of the action gateway, policy identity confusion, exposure of secrets, or false recovery-verification result is a release blocker until fixed or explicitly removed from the supported scope.
