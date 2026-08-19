# agentic-atlas

Consult the published agentic-atlas pattern corpus while designing
skills and agent systems. One skill (`consulting-patterns`) as the
door, one agent (`pattern-librarian`) as the engine, both riding the
current frozen surface of eight `atlas_*` tools on the hosted MCP
endpoint (`.mcp.json` → Streamable HTTP at
`https://agentic-atlas.dev/mcp/`) — nothing to install, nothing to
cache, no local corpus or local server needed.

Issue #136 moved the plugin onto that endpoint. There is no bundled
client, no downloaded artifact, no pinned release and no rollback path
left in it: the endpoint serves the one active Corpus Release, and a
promotion replaces it wholesale. The frozen grammar the prose is
allowed to name lives in
`contract/fixtures/publication/agent/tools.json`; `tests/plugins/`
checks the plugin against it mechanically rather than by eye.

## Layout

- `.claude-plugin/plugin.json` — plugin manifest.
- `.mcp.json` — registers the hosted endpoint (the public consultation
  surface; tests in `tests/plugins/`).
- `skills/consulting-patterns/` — the trigger discipline and
  inline-vs-dispatch rung routing.
- `agents/pattern-librarian.md` — the traversal method and the
  bounded, path-cited return contract.

Harnesses with no plugin system get the same contract as copyable
prose, served at
[agentic-atlas.dev/consult.md](https://agentic-atlas.dev/consult.md).

This directory contains only what ships publicly (issue #282): the
corpus traversal CLI that once lived under `scripts/` is private
pipeline tooling and lives at `interchange/corpus.py` now.

Design: `docs/plans/2026-07-05-pattern-corpus-plugin-design.md`.
