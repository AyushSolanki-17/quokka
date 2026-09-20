# Development

## Environment

Use Python 3.12.13, pinned in `.python-version`, and [uv](https://docs.astral.sh/uv/getting-started/installation/) for the local environment and dependency lockfile. If using [pyenv](https://github.com/pyenv/pyenv#installation), install that interpreter first:

```sh
pyenv install -s 3.12.13
uv sync --locked --python "$(pyenv which python)"
uv run --locked pre-commit install
```

Run these commands from the repository root with pyenv and uv on `PATH`. The committed `.python-version` selects the interpreter for this project without changing your global Python. If pyenv is unavailable, `uv sync --locked --python 3.12.13` can provision Python itself.

`uv sync` creates `.venv/` and installs the locked development tools. Use `uv run --locked <command>` or optionally activate the environment with `source .venv/bin/activate`. The environment and caches stay out of Git.

There are no runtime dependencies or application entry points yet. Packaging is disabled until an importable implementation is needed; no model downloads are part of setup.

## Checks

```sh
uv lock --check
uv run --locked ruff check .
uv run --locked ruff format --check .
uv run --locked pre-commit validate-config
uv run --locked pre-commit run --all-files
git diff --check
```

Ruff has no Python source to inspect yet, and its hooks will skip until Python files exist. This is expected, not test coverage. Hooks call the same locked Ruff installation as the direct commands. Fix formatting with `uv run --locked ruff format .`; inspect any lint autofixes before committing.

Add pytest with the first meaningful behavior tests and mypy when typed Python modules exist. Document their actual commands here then. Unit tests should protect meaningful logic and regressions; integration tests should cover real component boundaries. Keep tests proportional to risk, with small deterministic fixtures and no model downloads or network calls in the default unit suite. Explicitly opt into resource-heavy integration runs.

## Changes and dependencies

- Use focused Conventional Commits, for example `docs: clarify local setup`, `feat: add baseline measurement`, or `fix: handle inference timeout`. No commit-message checker is required.
- Use `uv add <package>` for necessary runtime dependencies and `uv add --dev <package>` for development tools. Commit both `pyproject.toml` and `uv.lock`; upgrade dependencies deliberately, not as unrelated cleanup.
- Use Ruff for linting, formatting, and import sorting. Prefer tool configuration and direct commands over custom validation or formatting scripts.
- Small documentation/configuration changes need direct review and existing checks, not new test harnesses. Add tests for meaningful behavior, not line counts or coverage targets.
- Keep README focused on what users can do, honest project status, usage, and measured results. Put contributor setup here and agent-specific instructions in `AGENTS.md`.

## Local data and publishing

Keep private notes under ignored `docs/internal/` and downloads, datasets, and raw run output under ignored `artifacts/`. Public development must work without private notes. Never put real credentials in examples.

Before committing, review `git status --short`, the exact staged paths, and `git diff --cached`. `git ls-files -- docs/internal/ artifacts/ .venv/` must produce no output. Ignore rules do not remove already tracked files. Never force-add private notes or generated assets.
