# Repository Guidelines

> Note: Active development happens in `egallis31/pwnagotchi`. Please open issues and pull requests against that repository, not upstream forks. We periodically sync from upstream; do not submit changes there.

## Project Structure & Module Organization
- Code lives in `pwnagotchi/` (core package). Notable modules: `cli.py` (entrypoint), `agent.py`, `plugins/`, `ui/`, `mesh/`, `google/`, `locale/`, `defaults.toml`.
- Scripts for development are in `scripts/` (e.g., `language.sh`).
- Packaging and metadata: `pyproject.toml` (Python 3.11, setuptools). Make targets in `Makefile`.
- Assets/translations: `pwnagotchi/locale/` (use Make targets below to update/compile).

## Build, Test, and Development Commands
- Create venv: `python -m venv .venv && source .venv/bin/activate`.
- Editable install: `pip install -e .` (exposes `pwnagotchi` CLI).
- CLI help/run: `pwnagotchi --help` and `pwnagotchi run` (see `pwnagotchi/cli.py`).
- Update locales: `make update_langs` (refresh `.po` from `voice.py`).
- Compile locales: `make compile_langs` (build `.mo` files).

Repository remotes
- Primary: `https://github.com/egallis31/pwnagotchi` (target for PRs).
- Optional upstream (read‑only): `git remote add upstream <UPSTREAM_URL>` then `git fetch upstream && git checkout main && git merge upstream/main` to sync.

## Coding Style & Naming Conventions
- Python 3.11; follow PEP 8 with 4‑space indentation and UTF‑8 source.
- Names: modules/files `lower_snake_case.py`; classes `CapWords`; functions/vars `lower_snake_case`.
- Docstrings: use brief module/class/function docstrings; prefer type hints for new/changed code.
- Keep PRs focused: avoid mixing refactors with features/fixes.

## Testing Guidelines
- Framework: pytest (recommended). Place tests in `tests/` with files like `test_cli.py`.
- Quick run: `pytest -q` (from repo root).
- Aim to cover CLI behaviors and key modules (`agent.py`, `plugins/`). Use fakes for hardware/bettercap interactions.

## Commit & Pull Request Guidelines
- Open an issue first for features/large changes; one topic per PR with a clear description and test plan.
- Sign your commits (DCO): `git commit -s` is required.
- Messages: concise, imperative mood (e.g., "Add plugin loader retry"). Reference issues (`Fixes #123`).
- PRs: include screenshots/logs when UI/CLI output changes; note config impacts (e.g., `defaults.toml`).

## Security & Configuration Tips
- Do not commit secrets, PCAPs, or personal data. Keep device‑specific configs out of VCS.
- Configuration lives in `defaults.toml`; document new keys and provide safe defaults.
- When touching locales, run `make update_langs && make compile_langs` and include updated `.po/.mo`.
