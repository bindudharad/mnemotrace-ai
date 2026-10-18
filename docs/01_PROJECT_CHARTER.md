# 1. Project Charter

## Working name

**MnemoTrace — AI Memory Poisoning Defense and Verified Recovery**

## Vision

Make delayed memory-poisoning incidents in AI-agent systems easier to detect, investigate, contain, and recover from—with evidence that can be reproduced.

## Mission

Build a focused runtime-security prototype that monitors memory operations, records memory provenance, reconstructs possible contamination paths, applies policy-controlled containment, and retests the system after recovery.

## Problem statement

AI agents may persist information across turns and sessions. A malicious or untrusted record can survive a conversation reset and later influence retrieval, planning, or tool usage. Once records are summarized, copied, or used by another agent, it may be difficult to determine which records are related to the original source. Restoring one snapshot does not automatically prove that derived records or future behavior are safe.

## Primary users

- AI application developers integrating persistent memory;
- security engineers validating agent memory controls;
- incident responders investigating suspected memory poisoning;
- evaluators who need reproducible security evidence.

## Product promise

MnemoTrace aims to answer five questions for a controlled incident:

1. Where did the suspicious record enter?
2. Which later records have direct lineage links to it?
3. Which downstream events may have been influenced, and which links are only inferred?
4. Which policy blocked, quarantined, or restored the memory?
5. Did the same attack remain blocked after recovery while benign tasks still succeeded?

## MVP boundaries

The first demonstrator will use local synthetic records, a deterministic policy engine, SQLite-backed event history, a graph view, and a simulated action sink. It will not send real emails, access corporate systems, or automatically alter production agent memory.

## Success criteria

The MVP is successful when a fresh environment can run the documented demo and tests proving all of the following:

- a synthetic poisoned record survives a simulated context reset;
- the event ledger retains IDs and provenance relationships for the tested path;
- the policy gate prevents a prohibited simulated action from reaching the mock sink;
- quarantine and trusted-checkpoint restore have testable semantics;
- the original attack and benign controls can be replayed;
- results include corpus version, command, environment, and test summary.

## Non-goals for the first build

- guaranteeing detection of every attack;
- proving true semantic causality from embeddings alone;
- autonomous remediation on live enterprise systems;
- production-grade multi-tenant SaaS;
- formal verification of all policies;
- claims of production readiness before security review.

## Constraints and assumptions

- Development time is limited and priorities must protect the end-to-end demo loop.
- External model APIs are optional, not required for the deterministic core.
- Semantic influence analysis can be probabilistic; enforcement must remain rule-based.
- Any claim about detection or recovery must be supported by an explicit test.
