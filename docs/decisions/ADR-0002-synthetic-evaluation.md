# ADR-0002: Synthetic, Reproducible Security Evaluation

- **Status:** Accepted for MVP design
- **Date:** 2026-10-18

## Context

Live agent tools, corporate records, and real external destinations would introduce privacy and safety risks. Non-deterministic model responses also make a hackathon demo hard to reproduce.

## Decision

The MVP benchmark uses versioned synthetic scenario manifests, deterministic expected outcomes, and a local mock action sink. An LLM may be added as an optional transformation component, but the core security invariants must be testable without any external API.

## Consequences

- The demo is safe to run offline and on stage.
- Results are easier to reproduce and compare across code versions.
- The benchmark does not fully represent production traffic; this limitation must be stated.
- The project must report scenario counts, corpus version/hash, raw metrics, and holdout behavior.
