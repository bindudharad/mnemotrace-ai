# MnemoTrace

> **Trace the poison. Contain the spread. Prove recovery.**

MnemoTrace is a proposed AI-memory security platform for investigating delayed memory-poisoning attacks in long-lived and multi-agent AI workflows. It is designed around an evidence-first security loop: inspect memory operations, preserve lineage, contain suspicious records, recover to a trusted state, and verify recovery with repeatable tests.

**Project status:** Documentation and implementation blueprint. Features listed as planned are not considered implemented until the corresponding code, tests, and evidence are committed.

## The problem

A malicious instruction can be written into persistent agent memory, remain after a conversation ends, and influence a later task. A detector that only checks the current prompt may not see the original instruction when it is retrieved, summarized, or passed to another agent. A simple rollback may also be incomplete if derived records remain.

## Proposed solution

MnemoTrace combines five capabilities:

1. **Memory policy enforcement** — inspect memory writes and reads using explicit rules and detector findings.
2. **Event ledger and provenance** — record stable memory/event IDs, actor identity, source references, policy decisions, and relationships between records.
3. **Causal lineage investigation** — visualize recorded links separately from inferred influence; do not present an inference as a fact.
4. **Containment and trusted recovery** — quarantine suspicious records, review possible descendants, restore a known-good checkpoint, and replay only events permitted by policy.
5. **Recovery verification lab** — rerun the same delayed attacks and benign controls to measure whether prohibited actions remain blocked and legitimate work still succeeds.

## What makes the approach distinct

The central contribution is not a claim that a single detector is unprecedented. It is the proposed end-to-end workflow that connects delayed attack investigation with scoped containment, recoverability, and reproducible post-recovery testing.

## Documentation map

Start with [`docs/INDEX.md`](docs/INDEX.md). Important documents:

- [Project charter](docs/01_PROJECT_CHARTER.md)
- [Problem and stakeholders](docs/02_PROBLEM_AND_STAKEHOLDERS.md)
- [Solution and novelty](docs/03_SOLUTION_AND_NOVELTY.md)
- [Requirements](docs/04_REQUIREMENTS.md)
- [Architecture](docs/05_SYSTEM_ARCHITECTURE.md)
- [Threat model](docs/06_THREAT_MODEL.md)
- [Data model](docs/07_EVENT_AND_MEMORY_DATA_MODEL.md)
- [Recovery protocol](docs/08_RECOVERY_PROTOCOL.md)
- [API contract](docs/09_API_CONTRACT.md)
- [Implementation plan](docs/10_IMPLEMENTATION_PLAN.md)
- [Test strategy](docs/11_TEST_STRATEGY.md)
- [Benchmark protocol](docs/12_BENCHMARK_PROTOCOL.md)
- [Development setup](docs/13_LOCAL_DEVELOPMENT.md)
- [Demo runbook](docs/14_DEMO_RUNBOOK.md)
- [Privacy and ethics](docs/15_PRIVACY_AND_ETHICS.md)
- [Risk register](docs/16_RISK_REGISTER.md)
- [Release checklist](docs/17_RELEASE_CHECKLIST.md)
- [Hackathon pitch](docs/18_HACKATHON_PITCH.md)
- [Requirements traceability](docs/19_TRACEABILITY_MATRIX.md)
- [Progress log](docs/20_PROGRESS_LOG.md)
- [Architecture decision records](docs/decisions/)

## Proposed technical baseline

- **Backend:** Python 3.11+ and FastAPI
- **Core policy and memory services:** Python modules with explicit typed contracts
- **Event storage:** SQLite for the first prototype; keep the repository layer replaceable
- **Lineage analysis:** directed graph representation; NetworkX can be used in the prototype
- **Frontend:** React/Next.js dashboard, or a small server-rendered UI if time is limited
- **Testing:** pytest plus deterministic simulated attack/benign scenarios
- **Evaluation:** local synthetic data and a mock action sink; no real corporate data or external actions

This stack is a proposed baseline, not a claim about an existing implementation. See [Architecture](docs/05_SYSTEM_ARCHITECTURE.md) and [Implementation Plan](docs/10_IMPLEMENTATION_PLAN.md).

## Quick start for contributors

The documentation pack does not contain the application runtime yet. To implement the project in a clean repository:

1. Read `docs/01_PROJECT_CHARTER.md` and `docs/04_REQUIREMENTS.md`.
2. Follow the milestones in `docs/10_IMPLEMENTATION_PLAN.md`.
3. Create the package skeleton described in `docs/13_LOCAL_DEVELOPMENT.md`.
4. Implement the policy core and mock tool boundary before adding the dashboard.
5. Use `docs/11_TEST_STRATEGY.md` and `docs/12_BENCHMARK_PROTOCOL.md` from the first commit.

## Project principles

- **Security decisions are enforced by deterministic policy controls.** An LLM may help explain or prioritize a finding, but it must not authorize its own memory access or recovery.
- **Evidence and inference are different.** Record direct links explicitly; label semantic influence as inferred and provide a confidence/justification field.
- **Fail closed at critical boundaries.** If authorization or recovery integrity cannot be established, reject the sensitive operation or require an authorized human decision.
- **No false claims.** Do not publish performance or detection numbers until the benchmark has been run and the exact test set is documented.
- **Safe by default.** Use synthetic payloads, isolated local storage, and mocked external actions.

## Current status

See [`PROJECT_STATUS.md`](PROJECT_STATUS.md). All feature checkboxes begin as not implemented/not verified. Update them only when evidence is available.
