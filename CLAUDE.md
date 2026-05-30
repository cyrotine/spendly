# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

**Spendly** — a personal expense tracker web app built with Flask and SQLite, targeted at Indian users (currency: ₹). This is a step-by-step student project; many routes in `app.py` are stubs with placeholder strings, and `database/db.py` is intentionally empty pending implementation.

## Running the app

```bash
source venv/bin/activate
python app.py          # runs on http://localhost:5001 with debug mode
```

## Running tests

```bash
source venv/bin/activate
pytest                 # all tests
pytest tests/test_foo.py::test_bar   # single test
```

## Architecture

- **`app.py`** — all Flask routes. Currently only `/`, `/register`, `/login`, `/terms`, and `/privacy` render real templates; the remaining routes (`/logout`, `/profile`, `/expenses/*`) return placeholder strings awaiting future steps.
- **`database/db.py`** — will hold `get_db()`, `init_db()`, and `seed_db()`. Not yet implemented; `get_db()` should return a SQLite connection with `row_factory = sqlite3.Row` and `PRAGMA foreign_keys = ON`.
- **`templates/base.html`** — shared layout with navbar (Sign in / Get started links) and footer (Terms · Privacy). All page templates extend this.
- **`static/css/style.css`** — single stylesheet with CSS custom properties defined in `:root`. Design tokens: `--ink`, `--paper`, `--accent` (#1a472a dark green), `--accent-2` (gold). Fonts: DM Serif Display (headings/brand) + DM Sans (body).
- **`static/js/main.js`** — currently empty; page-specific JS is inlined in `{% block scripts %}` within individual templates.

## Design conventions

- CSS uses a paper/ink metaphor: `--paper` (warm off-white background), `--ink` (near-black text), `--accent` (dark green) as the primary brand color.
- No JS framework — vanilla JS only. Page-specific scripts go in the `{% block scripts %}` block of the relevant template.
- Jinja2 `url_for()` is used for all internal links; never hardcode paths.