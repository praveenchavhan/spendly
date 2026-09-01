# Project

Flask expense tracker app (Python + HTML/JS frontend). Layout: `app.py` (entry point), `database/`, `templates/`, `static/`.

## Environment

- OS: Windows. `python3` and `python` resolve to the Windows Store stub and fail with "Python was not found" — always use the venv's interpreter directly.
- Venv already exists at `venv/`. Do not recreate it; just call its binaries:
  - Run app: `venv/Scripts/python.exe app.py`
  - Install deps: `venv/Scripts/pip.exe install -r requirements.txt`
- Each Bash call runs in a fresh shell, so `venv\Scripts\activate` does not persist. Never rely on activation.
- Dev server runs on **http://127.0.0.1:5001** (not the Flask default 5000 — see `app.run(port=5001)` in `app.py`).

## Git

- Do not run `git push` — it hangs on a non-interactive credential prompt. Stage and commit, then hand back the exact push command to run manually.
