# Day 3 — Modern Python tooling: uv and Ruff

My study summary of the [uv docs](https://docs.astral.sh/uv/) and [Ruff docs](https://docs.astral.sh/ruff/) (getting started).

## 1. The problem these tools solve

A Python project needs three things to be repeatable on any machine:

1. **A known Python version** (3.12, not "whatever is installed").
2. **Its own isolated packages** — a *virtual environment* (`.venv/`), so project A's libraries don't clash with project B's.
3. **A record of exact package versions** — a *lock file*, so your laptop, CI and the server all install the same thing.

The old way used several tools (`pyenv` + `venv` + `pip` + `pip-tools`). **uv** does all of it, and is 10–100× faster.

Code quality used `flake8` (lint) + `black` (format) + `isort` (imports). **Ruff** does all of it, also very fast.

## 2. uv — the commands you'll use

| Command | Does |
| --- | --- |
| `uv init --package` | Create a new project with a `src/` layout and `pyproject.toml` |
| `uv python install 3.12` | Download a Python version (no admin rights needed) |
| `uv add requests` | Add a dependency (updates `pyproject.toml` + `uv.lock`, installs it) |
| `uv add --dev ruff` | Add a **development-only** tool (not needed to run the app) |
| `uv remove requests` | Remove a dependency |
| `uv sync` | Make `.venv` match the lock file exactly (use after `git pull`) |
| `uv run <command>` | Run a command **inside** the project's environment, e.g. `uv run python`, `uv run ruff check` |
| `uv lock` | Re-resolve and update `uv.lock` |
| `uv tree` | Show the dependency tree |

With `uv run`, you never need to "activate" the virtual environment.

## 3. The files uv creates

```
daleel/
├── pyproject.toml      ← project description + tool settings (commit it)
├── uv.lock             ← exact versions of every package (commit it)
├── .python-version     ← which Python this project uses (commit it)
├── .venv/              ← the installed packages (NEVER commit — .gitignore)
└── src/
    └── daleel/
        └── __init__.py ← your package starts here
```

### `pyproject.toml` explained

```toml
[project]
name = "daleel"
version = "0.1.0"
description = "Bilingual Arabic/English assistant over public documents"
readme = "README.md"
requires-python = ">=3.12"
dependencies = []            # runtime packages: uv add puts them here

[project.scripts]
daleel = "daleel:main"       # `uv run daleel` calls main() in src/daleel/__init__.py

[build-system]               # how to turn src/daleel into an installable package
requires = ["uv_build>=0.9,<0.10"]
build-backend = "uv_build"

[dependency-groups]
dev = ["ruff>=0.14"]         # dev tools: uv add --dev puts them here
```

(Exact version numbers will differ — uv writes the current ones.)

## 4. Why a `src/` layout?

Without `src/`, Python can import your code straight from the project folder, even if packaging is broken. Tests then pass on your machine and fail everywhere else. With `src/`, code is only importable after it's properly **installed** into `.venv` — so if it works for you, it works for CI and the server too.

## 5. Ruff — lint and format

| Command | Does |
| --- | --- |
| `uv run ruff check` | Find problems: unused imports, undefined names, bad patterns |
| `uv run ruff check --fix` | Fix the ones that are safe to fix automatically |
| `uv run ruff format` | Reformat code to a consistent style (like `black`) |
| `uv run ruff format --check` | Only report — used in CI (Day 18) |

- **Linting** = finding likely bugs and bad practice.
- **Formatting** = layout only (spaces, quotes, line breaks). It never changes what code does.

### Ruff settings in `pyproject.toml`

```toml
[tool.ruff]
line-length = 88
target-version = "py312"

[tool.ruff.lint]
select = [
  "E", "W",  # pycodestyle: style errors and warnings
  "F",       # pyflakes: unused imports, undefined names
  "I",       # isort: import order
  "UP",      # pyupgrade: use modern Python syntax
  "B",       # bugbear: likely bugs
]
```

Each letter is a *rule family*. Ruff's default is only `E` and `F`; adding a few more catches real bugs without being noisy.

## 6. `.gitignore` for a Python project

```
.venv/
__pycache__/
*.pyc
.ruff_cache/
.env
```

`.env` is where API keys will live from Phase 3 — it must never reach GitHub.

## 7. WSL note: project on the Windows drive

`~/daleel` in Ubuntu points to the Windows folder (`/mnt/c/...`), while uv's download cache lives in Ubuntu (`~/.cache/uv`). uv normally *hard-links* files from its cache, which can't work across the two file systems, so it warns and copies instead. Setting `UV_LINK_MODE=copy` tells uv to copy from the start and silences the warning.

## Test yourself

1. What's the difference between `pyproject.toml` and `uv.lock`? Which do you edit by hand?
2. Why should `.venv/` never be committed, but `uv.lock` should?
3. What's the difference between `uv add` and `uv add --dev`?
4. What's the difference between `ruff check` and `ruff format`?
5. Why use a `src/` layout?
