# Contributing to MnemoTrace

Thank you for contributing. MnemoTrace is a security-sensitive prototype; correctness, explainability, and reproducibility are more important than adding features quickly.

## Before coding

1. Read `README.md`, `docs/04_REQUIREMENTS.md`, `docs/05_SYSTEM_ARCHITECTURE.md`, and `docs/06_THREAT_MODEL.md`.
2. Check `docs/10_IMPLEMENTATION_PLAN.md` and `docs/19_TRACEABILITY_MATRIX.md` for the relevant milestone and acceptance test.
3. For architecture changes, create or update an ADR under `docs/decisions/`.
4. Keep all demonstrations confined to synthetic memory and a mock tool sink unless an explicit, reviewed extension authorizes otherwise.

## Change workflow

1. Open an issue with the problem, affected component, expected behavior, security impact, and acceptance criteria.
2. Make the smallest change that satisfies the criteria.
3. Add tests for expected and denied behavior, including benign controls and error paths.
4. Run formatting, static checks, unit tests, integration tests, and relevant benchmark scenarios.
5. Update documentation, `PROJECT_STATUS.md`, and `CHANGELOG.md`.
6. Submit a pull request describing what changed, why, how it was tested, and any limitations.

## Engineering rules

- Never use real secrets, personal data, or production records in tests or screenshots.
- Do not log raw memory values by default; prefer IDs, hashes, redacted excerpts, and policy decisions.
- Do not rely on an LLM as the only enforcement mechanism.
- Do not silently convert unknown provenance into trusted provenance.
- Preserve existing policy behavior unless a change is explicit and tested.
- Use deterministic fixtures for security regression tests.
- Mark AI-generated explanations as explanations, not authoritative evidence.

## Commit style

Recommended prefixes: `docs:`, `feat:`, `fix:`, `test:`, `security:`, `refactor:`, `bench:`.

Example: `feat: add parent links to memory event ledger`
