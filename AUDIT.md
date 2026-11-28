# Repository Audit

Scope: all tracked files (`.gitignore`, `docs/Azure-AI-Learning-Path-2026.md`, `docs/Phase-0-Python-Curriculum.md`).
The repo is documentation only (Markdown, ~6,850 lines). It has no source code, manifests, or CI.

## 1. TODO / FIXME comments

None found. A case-sensitive search for `TODO` and `FIXME` across the repo, excluding `.git` and this file, returned no matches.

## 2. Tests

There is no test suite: no test files, no `pytest`/`package.json`/`Makefile`, no CI config. Nothing was run, so there are no failures to report.
The Phase 0 curriculum teaches pytest, but the repo has no code to test.

## 3. Dependencies (outdated / unpinned)

There are no manifest or lock files. The only dependency references are install commands inside the docs, and these are unpinned:

| Location | Command | Issue |
|---|---|---|
| Azure-AI-Learning-Path-2026.md:487 | `pip install azure-ai-projects azure-identity` | unpinned |
| Azure-AI-Learning-Path-2026.md:1117 | `pip install azure-ai-projects azure-identity azure-search-documents azure-ai-evaluation` | unpinned |
| Azure-AI-Learning-Path-2026.md:1207 | `pip install agent-framework` | unpinned |
| Azure-AI-Learning-Path-2026.md:1565 | `pip install -U uv` (devcontainer `postCreateCommand`) | unpinned and auto-upgrading |
| Phase-0-Python-Curriculum.md:2713, 2755, 2845, 2985 | `pip`/`uv pip install httpx openai python-dotenv` | unpinned |
| Phase-0-Python-Curriculum.md:2714 | `pip install "openai>=1.0"` | open-ended lower bound |

Recommendation: if learner projects are committed here, add a `requirements.txt` or `pyproject.toml` with pins and a lock file (`uv lock`).
I did not check version currency against the registries.

## 4. Security smells

- **Secrets in files:** none found. A search for key, token and private-key patterns (`sk-…`, `AKIA…`, `BEGIN … PRIVATE KEY`) matched only prose. No `.env` file is tracked.
- **`.gitignore`:** it covers `.env`, `.venv/`, `logs/` and `transcripts/`. It does not cover `*.pem`, `*.key`, `.azure/`, or `*.tfstate`. Consider adding them, since the curriculum involves Azure credentials.
- **Unpinned container images** in example snippets:
  - Azure-AI-Learning-Path-2026.md:1725: `mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment:latest`
  - Azure-AI-Learning-Path-2026.md:1803: `ollama/ollama:latest`

  Pin to a version tag or a digest.
- **Broad permissions:** no `chmod 777`, `curl | sh`, or privileged-container patterns found.
- **Personal data:** the docs mention a specific employer tenant ("HYLIFE") by name, at Azure-AI-Learning-Path-2026.md:61. This is not a secret, but review it before making the repo public.

## Summary

| Area | Result |
|---|---|
| TODO/FIXME | 0 |
| Tests | none exist |
| Unpinned deps | 6 kinds of install command, in docs only |
| Secrets | none |
| Unpinned images | 2 (`:latest`) |
