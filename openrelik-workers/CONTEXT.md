# Python Project Context & Standards (OpenRelik Workers Monorepo)

## Repository Layout
- This repository is a monorepo containing:
  - `lib/openrelik_worker_common`: Shared library package.
  - `workers/<worker-name>`: Individual worker packages (e.g. `workers/hasher`, `workers/exif`, `workers/yara`, etc.).
- Each package has its own `pyproject.toml`, `src/`, `tests/`, and `uv.lock`.

## Environment & Dependency Management
- **Toolchain:** `uv` (Fast Python packaging)
- **Execution:** Always prefix Python and tool commands with `uv run` inside the relevant worker or lib directory (e.g., `cd workers/<worker-name> && uv run pytest` or `uv run --project workers/<worker-name> ...`).
- **Dependencies:** To add new packages, run `uv add <package>` inside the relevant worker directory instead of modifying `pyproject.toml` manually.
- **Strict Rule:** Never install packages globally or use global python/pip.

## Quality & Testing
- **Test Framework:** `pytest`
- **Linting/Formatting:** `ruff` (`uv run ruff check` and `uv run ruff format`)
- **Strict Rules:**
  1. Every new or modified feature module under `workers/<worker-name>/src/` must have corresponding test coverage under `workers/<worker-name>/tests/` prefixed with `test_`.
  2. Background agents must verify that `uv run pytest` and `uv run ruff check` pass cleanly in the target worker directory before marking a task complete.

## Change review and fix
- Always review code against to the initial design or ask before comitting in git.
- Make sure to fix errors or ommisions.
- Make sure code is documented according to Google Python standards.
- Make sure Python code is using type hints using "from __future__ import annotations".

## Integration Testing
- **Toolchain:** `openrelik` (OpenRelik CLI)
- **Execution:** Always use `openrelik skill install --local --harness pi --yes` to generate a skill. Read and learn how you can use the tool from that generated skill file.



