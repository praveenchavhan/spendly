# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

"Spendly" — a Flask expense tracker built incrementally as a learning project. Backend is Flask with server-rendered Jinja2 templates; frontend is vanilla HTML/CSS/JS (no framework, no build step). Many routes and the database layer are intentionally unimplemented placeholders, filled in step by step (see Architecture below).

## Commands

- Run dev server: `venv/Scripts/python.exe app.py` — serves at http://127.0.0.1:5001 with `debug=True` (auto-reloads on file changes).
- Install/update deps: `venv/Scripts/pip.exe install -r requirements.txt`
- Run tests: `venv/Scripts/python.exe -m pytest` — `pytest` / `pytest-flask` are installed but no test files exist yet, so this currently collects zero tests. Run a single test once tests exist with `venv/Scripts/python.exe -m pytest path/to/test_file.py::test_name`.

## Environment

- OS: Windows. `python3` and `python` resolve to the Windows Store stub and fail with "Python was not found" — always invoke the venv's interpreter directly (see Commands), never bare `python`/`python3`.
- Venv already exists at `venv/`. Do not recreate it; just call its binaries directly.
- Each Bash call runs in a fresh shell, so `venv\Scripts\activate` does not persist. Never rely on activation.
- Dev server port is 5001, not Flask's default 5000 — see `app.run(port=5001)` in `app.py`.

## Git

- Do not run `git push` — it hangs on a non-interactive credential prompt. Stage and commit, then hand back the exact push command to run manually.
- Commit messages follow the pattern `<area>: <imperative summary>` (e.g. `landing: add privacy policy page and route`), area being the page/feature touched, not the file.

## Architecture

- `app.py` — single-file Flask app; all routes live here (no blueprints). Implemented routes just `render_template(...)` a matching file in `templates/`. Several routes (`/logout`, `/profile`, `/expenses/add`, `/expenses/<id>/edit`, `/expenses/<id>/delete`) are placeholders returning a plain string like `"Add expense — coming in Step 7"` — these are staged for future steps (auth, then expense CRUD) and not yet backed by real logic or templates.
- `database/db.py` — placeholder for the SQLite data layer. Intended shape (per its header comment, not yet written): `get_db()` returns a SQLite connection with `row_factory` and foreign keys enabled, `init_db()` creates tables with `CREATE TABLE IF NOT EXISTS`, `seed_db()` inserts dev sample data. `expense_tracker.db` (gitignored) is the expected SQLite file once this exists.
- `templates/` — Jinja2 templates. `base.html` defines the shared shell (nav, footer, font/CSS links, `{% block content %}` / `{% block scripts %}`); page templates (`landing.html`, `login.html`, `register.html`, `terms.html`, `privacy.html`) extend it. Route names are referenced via `url_for('<view_func>')`, not hardcoded paths.
- `static/css/style.css` — single global stylesheet (no per-page split, no preprocessor). `static/js/main.js` — single global vanilla-JS file for interactive bits (e.g. the landing page's "how it works" video modal); no page-specific JS files or bundler.
- `file.txt` — a running log of the prompts used to build recent features (footer links, terms/privacy pages, hero redesign, video modal). It's a working scratch note, not app code or documentation of current behavior — treat its contents as historical context, not a spec to re-apply.
