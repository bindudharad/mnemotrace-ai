# 12. Benchmark Protocol

## Purpose

Measure the complete memory-poisoning defense and recovery loop. The benchmark is intended to compare configurations on the same test scenarios; it is not proof of universal protection.

## Configurations to compare

- **Baseline A — unprotected:** the synthetic workflow has no guard at memory operations or action execution. Use only the mock sink.
- **Baseline B — write-time detector:** use a simple detector at write time without lineage/recovery workflow.
- **Candidate C — MnemoTrace MVP:** policy-controlled memory operations, event ledger, lineage links, action gate, quarantine, restore, and regression retest.

Document precisely which controls each configuration enables. Do not compare materially different datasets or model settings and call the result a fair comparison.

## Scenario groups

1. direct memory poisoning;
2. delayed activation after a simulated context reset;
3. paraphrased or summarized payload;
4. cross-agent derived-memory influence;
5. protected-key or principal violation;
6. benign persistent notes;
7. normal follow-up retrieval;
8. recovery with a mixed benign/malicious history;
9. missing/partial lineage data;
10. malformed event or checkpoint integrity data.

## Metrics

- **Attack success rate (ASR):** prohibited mock actions executed / prohibited action attempts. Target is zero in the tested protected scenarios; report counts, not just percentages.
- **Block rate:** prohibited action attempts denied / prohibited action attempts.
- **False-block rate:** benign operations blocked / benign operations attempted.
- **Lineage coverage:** ground-truth source/parent relationships correctly recovered / ground-truth relationships in the fixture.
- **Lineage precision:** asserted recorded relationships that are supported by fixture source fields / all asserted recorded relationships.
- **Recovery time:** time from recovery start to completion of all required integrity and regression tests.
- **Recovery success rate:** recovery scenarios meeting every defined recovery invariant / recovery scenarios attempted.
- **Latency overhead:** guard-enabled operation latency compared with unguarded operation under the same environment.

## Corpus protocol

- store scenario manifests as versioned JSON/YAML;
- include unique scenario ID, category, seed, initial memory state, source IDs, parent IDs, expected decision, expected sink state, and benign/attack label;
- separate development and holdout scenarios;
- compute and publish a corpus hash;
- avoid tuning solely on the holdout set;
- keep benign controls varied enough to detect overblocking.

## Reproducibility report must include

- git commit SHA and package version;
- Python/OS/runtime versions;
- dependency lock or exact dependency versions;
- corpus version and hash;
- scenario counts and exclusions;
- command used;
- baseline definitions;
- raw counts and formulas;
- failures and known limitations;
- whether an LLM or external API was used.

## Result publication template

| Metric | Baseline A | Baseline B | MnemoTrace | Notes |
|---|---:|---:|---:|---|
| Prohibited actions executed | TBD | TBD | TBD | Raw counts required |
| Prohibited actions blocked | TBD | TBD | TBD | Raw counts required |
| Benign tasks blocked | TBD | TBD | TBD | Raw counts required |
| Lineage coverage | TBD | TBD | TBD | Ground truth from fixtures |
| Recovery tests passed | TBD | TBD | TBD | Must pass all required invariants |
| Median guard latency | TBD | TBD | TBD | Record environment |

Do not fill these values until the benchmark has actually run. Do not claim the benchmark generalizes to all agents, models, or memory backends.
