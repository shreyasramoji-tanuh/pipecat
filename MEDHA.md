# MeDHA fork

TANUH AI-CoE's fork of [pipecat-ai/pipecat](https://github.com/pipecat-ai/pipecat) for
MeDHA's voice layer. Design: medha-chatbot-dev,
`docs/superpowers/specs/2026-09-24-pipecat-voice-layer-design.md` §9.

- `main` tracks upstream; `medha` is `main` plus MeDHA's additions.
- Base: upstream `9d4c5087aaa1bd5193262136a59d677348bb950c`.
- Upstream files are never edited. A capability that cannot be built by subclassing
  Pipecat's public API from outside lands as a new file under `src/pipecat/medha/`.
  This file is itself the only addition so far.
- GitHub: `https://github.com/shreyasramoji-tanuh/pipecat` (`origin`); upstream is the `upstream` remote. medha-chatbot-dev
  installs this fork from that git URL, pinned to a `medha` commit in its `pyproject.toml`
  (`[tool.uv.sources]`), so every run records the exact commit.

## Re-syncing with upstream

```bash
git fetch upstream
git checkout main && git merge --ff-only upstream/main
git checkout medha && git rebase main
uv run pytest tests -q
```

Then update the Base line above, commit, `git push origin main medha --force-with-lease`,
and in medha-chatbot-dev re-pin with
`uv add --optional voice "pipecat-ai @ git+https://github.com/shreyasramoji-tanuh/pipecat@<new medha SHA>"` and run its suite.
