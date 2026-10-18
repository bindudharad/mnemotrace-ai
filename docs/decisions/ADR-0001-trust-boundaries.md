# ADR-0001: Independent Policy Enforcement at Trust Boundaries

- **Status:** Accepted for MVP design
- **Date:** 2026-10-18

## Context

An LLM may misinterpret instructions, be manipulated by memory content, or generate an incorrect explanation. If the same model is allowed to authorize its own access or tool call, a malicious instruction can potentially bypass the intended guardrail.

## Decision

All supported memory operations pass through a deterministic policy engine. All simulated tool actions pass through a separate action gateway that independently verifies principal, action, data classification and destination. The model may supply a request or explanation but cannot set a policy decision directly.

## Consequences

- The protected store and mock sink must not have unguarded paths.
- Policy decisions are auditable and testable without an LLM.
- Integration adapters must preserve the same enforcement semantics.
- A policy gateway bug is critical and must block release.
- The architecture is more explicit than a prompt-only solution, but adds implementation and testing work.
