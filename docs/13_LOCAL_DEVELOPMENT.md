# 13. Local Development and Proposed Repository Structure

This is a setup blueprint. The application files do not exist merely because their planned paths are listed here.

## Recommended layout

```text
mnemotrace-ai/
├── README.md
├── PROJECT_STATUS.md
├── CHANGELOG.md
├── CONTRIBUTING.md
├── SECURITY.md
├── pyproject.toml
├── .env.example
├── .gitignore
├── docs/
│   ├── INDEX.md
│   ├── 01_PROJECT_CHARTER.md
│   ├── ...
│   └── decisions/
├── src/mnemotrace/
│   ├── __init__.py
│   ├── api/
│   ├── core/
│   ├── detectors/
│   ├── storage/
│   ├── ledger/
│   ├── lineage/
│   ├── containment/
│   ├── recovery/
│   ├── actions/
│   └── evaluation/
├── tests/
│   ├── unit/
│   ├── integration/
│   ├── security/
│   └── e2e/
├── scenarios/
│   ├── attacks/
│   └── benign/
├── reports/
└── frontend/                 # optional in first milestone
```

## Environment policy

- Use a supported Python 3.11+ environment for the prototype; select exact versions in `pyproject.toml`.
- Use a dedicated virtual environment.
- Keep credentials in environment variables or a local ignored `.env`; do not commit secrets.
- The core demo should run without external API credentials.
- Use only synthetic fixture data.

## Initial PowerShell setup (after source skeleton exists)

```powershell
cd C:\Projects\mnemotrace-ai
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -e ".[dev]"
pytest -q
```

These commands become valid only after `pyproject.toml` and package/tests have been created. Do not expect them to work from this documentation-only archive by itself.

## Proposed developer dependencies

Select and pin current compatible versions when implementing: `fastapi`, `uvicorn`, `pydantic`, `pytest`, `httpx`, coverage, a linter/formatter, and optionally `networkx`. Keep the required runtime dependencies small.

## Local run commands to implement

Recommended interface (to be wired up in M1/M3):

```powershell
python -m mnemotrace.cli demo delayed-poisoning
python -m mnemotrace.cli test --suite smoke
python -m mnemotrace.cli benchmark --suite mvp --output reports/latest.json
```

## Clean-clone verification

Before pitching, delete any local database and generated output, follow the documented setup exactly in a clean environment, run tests and demo, and verify that the shown results are generated from the current code. Preserve only the harmless scenario fixtures and reports needed for reproducibility.
