# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Spendly is a Flask expense tracker built as a step-by-step teaching scaffold (see comments in `database/db.py` like "Students will write this file in Step 1 — Database Setup"). There is no README — this file is the primary onboarding doc.

- Framework: Flask 3.1.3 (Werkzeug), Jinja2 templates, plain CSS/JS (no build tooling, no frontend framework).
- Database: raw `sqlite3` — **no ORM**. Do not introduce SQLAlchemy or similar.
- Package manager: pip, via `requirements.txt` (no `pyproject.toml`/Poetry/Pipenv).

## Setup and running

```bash
pip install -r requirements.txt
python app.py
```

Runs the Flask dev server on port 5001 with `debug=True` (see bottom of `app.py`).

## Database conventions

- `database/db.py` is the single place for DB logic. It's expected to expose:
  - `get_db()` — returns a SQLite connection with `row_factory` and foreign keys enabled
  - `init_db()` — creates tables using `CREATE TABLE IF NOT EXISTS`
  - `seed_db()` — inserts sample data for development
- The database file is `expense_tracker.db` at the project root (already gitignored — never commit it).
- No migrations framework is used; schema changes go directly into `init_db()`'s `CREATE TABLE` statements.

## Routes

`app.py` holds all routes. Several are intentional placeholders returning plain strings (`/logout`, `/profile`, `/expenses/add`, `/expenses/<id>/edit`, `/expenses/<id>/delete`) with comments noting which future step implements them — don't "fix" these without being asked, they're scaffold markers for the course progression.

## Testing

`pytest` and `pytest-flask` are installed but no tests exist yet. When adding tests, put them under a `tests/` directory and run with `pytest`.

## Code style

No linter or formatter is configured (no flake8/black/ruff/pyproject settings). Match the existing style in `app.py`: PEP8-ish formatting with `# --- Section Name ---#` comment banners dividing route groups.

## Git conventions

Commit messages follow `Area: short imperative description` (e.g., `Landing: add privacy policy page`), sentence case, no conventional-commits prefixes. Branches use `type/kebab-case-description` (e.g., `feature/database-setup`).
