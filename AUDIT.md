# Repository Audit

**Scope:** all tracked files (`.gitignore`, `docs/Azure-AI-Learning-Path-2026.md`, `docs/Phase-0-Python-Curriculum.md`). The repo is documentation only (about 6,850 lines of Markdown). It has no source code, manifests, CI config or Dockerfiles.

## 1. TODO / FIXME comments

None found. A case-sensitive search for `TODO` and `FIXME` across `docs/` and the root returned no matches.

## 2. Tests

No test suite exists. There is no `tests/` directory, no `pytest`/`tox`/`package.json`/`Makefile` and no CI workflow, so nothing was run. The Python code in the curriculum is only embedded in the Markdown and is not executed or validated anywhere.

## 3. Dependencies (outdated / unpinned)

There are no manifest or lock files. The docs tell the reader to install packages without version pins:

| Location | Command | Issue |
|---|---|---|
| `docs/Azure-AI-Learning-Path-2026.md:487` | `pip install azure-ai-projects azure-identity` | unpinned |
| `docs/Azure-AI-Learning-Path-2026.md:1117` | `pip install azure-ai-projects azure-identity azure-search-documents azure-ai-evaluation` | unpinned |
| `docs/Azure-AI-Learning-Path-2026.md:1207` | `pip install agent-framework` | unpinned |
| `docs/Azure-AI-Learning-Path-2026.md:1565` | devcontainer `postCreateCommand: pip install -U uv` | floating version |
| `docs/Phase-0-Python-Curriculum.md:2713` | `pip install httpx` | unpinned |
| `docs/Phase-0-Python-Curriculum.md:2714` | `pip install "openai>=1.0"` | lower bound only |
| `docs/Phase-0-Python-Curriculum.md:2755`, `:2845`, `:2985` | `uv pip install httpx openai python-dotenv` | unpinned |

- The curriculum does suggest `uv pip freeze > requirements.txt` (line 2852). That gives reproducibility, but only if the reader follows it.
- Several Azure SDK packages (e.g. `azure-ai-projects`) change their APIs quickly. Unpinned installs can break the lab code.
- I did not check whether the versions named in the docs are current, because there is nothing pinned to compare.

## 4. Security smells

**Secrets:** none found. There are no keys, tokens, private keys or connection strings in the files. The `ApiKey=<key>` entries are placeholders. `.gitignore` excludes `.env`, `.venv/`, `logs/` and `transcripts/`.

**Unpinned container images** (these are examples in the docs, but readers will copy them):
- `docs/Azure-AI-Learning-Path-2026.md:1725` uses `mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment:latest` in a Kubernetes manifest.
- `docs/Azure-AI-Learning-Path-2026.md:1763-1767` uses the same `:latest` image in a `docker run` example.
- `docs/Azure-AI-Learning-Path-2026.md:1803` uses `ollama/ollama:latest` in a Kubernetes manifest.
- Recommendation: pin a version tag or a digest.

**Secrets on the command line:**
- `docs/Azure-AI-Learning-Path-2026.md:1767` passes `ApiKey=<key>` as a `docker run` argument. That leaves the key in shell history and the process list.
- The Kubernetes example (around lines 1725-1730) should be checked to confirm the key comes from a `Secret` rather than inline env.
- Recommendation: use `--env-file` or a Kubernetes Secret.

**Broad permissions:** none found. There is no `chmod 777`, `sudo`, `curl | sh` or `--privileged`. The Ollama manifest uses `runtimeClassName: nvidia`, which is expected for GPU access. It does not show a `securityContext` or resource limits, so those are worth adding.

**Other:**
- `AUDIT.md` is tracked and is overwritten by this audit.
- There is no `LICENSE`, `SECURITY.md` or CI secret-scanning (e.g. gitleaks). The last one is cheap insurance, because the docs repeatedly tell the user to handle `.env` files.

## Summary

| Area | Result |
|---|---|
| TODO/FIXME | 0 |
| Tests | none exist |
| Unpinned deps | 9 doc install commands, no lockfile |
| Secrets | none |
| `:latest` images | 3 occurrences |
