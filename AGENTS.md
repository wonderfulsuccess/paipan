# Repository Guidelines

## Project Structure & Module Organization

Keep the repository centered on the Qi Men Dun Jia computation engine described in `PRD.md`. Place production code under `src/paipan/`, separating `core/` algorithms from `adapters/` (e.g., API or CLI surfaces). House integration glue such as FastAPI routers in `src/paipan/api/`. Store reusable fixtures in `tests/fixtures/` and planning docs in `docs/`. Add sample payloads in `samples/` to mirror the JSON shown in the product spec.

## Build, Test, and Development Commands

Create a virtual environment and install dependencies with `poetry install`. Run `poetry run pytest` for the test suite and `poetry run pytest tests/integration` when validating end-to-end flows. Launch the local API server with `poetry run uvicorn paipan.api.main:app --reload`. Use `poetry run ruff check src tests` and `poetry run ruff format` before opening a pull request.

## Coding Style & Naming Conventions

Target Python 3.11 and rely on type hints for all public functions. Use 4-space indentation, snake_case for functions and modules, PascalCase for classes, and UPPER_CASE for constants. Keep modules small (under ~300 lines) and expose shared contracts in `src/paipan/core/interfaces.py`. Prefer pure functions for calculations; add inline comments only to clarify traditional terminology from the spec. Defer to `ruff` and `black` for linting and formatting consistency.

## Testing Guidelines

Write tests with `pytest`. Match module paths to mirror structure: `tests/core/test_pan_solver.py` exercises `src/paipan/core/pan_solver.py`. Use parametrized tests for calendar edge cases and ensure fixtures cover both 转盘 and 飞盘 modes. Any new feature must include regression cases derived from the example JSON in `samples/`. Maintain ≥90% branch coverage to ensure the computational rules stay guard-railed.

## Commit & Pull Request Guidelines

Follow Conventional Commits (`feat:`, `fix:`, `chore:`, etc.) so release notes stay legible. Reference issue IDs in the subject when available (`feat: add xin dun router (#42)`). Pull requests should summarize scope, enumerate validation commands, and attach screenshots or sample payload diffs when API responses change. Request review from domain specialists before merging changes that modify divination logic or calendrical conversions.

## Security & Configuration Tips

Never hard-code API keys or paid ephemeris credentials; rely on `.env` entries prefixed with `PAIPAN_`. Document configuration defaults in `docs/config.md` and keep sensitive examples in `.env.example`. Regularly regenerate dependencies (`poetry lock --no-update`) when shipping security patches.
