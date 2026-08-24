# Agentic Atlas — companion plugin for Claude Code

[Agentic Atlas](https://agentic-atlas.dev/) is a collection of field-tested
patterns for designing agent systems, readable by people and consultable by
agents over MCP. This companion plugin supplies one skill
(`consulting-patterns`) as the door and one agent (`pattern-librarian`) as the
engine, both riding the current frozen surface of eight `atlas_*` tools on the
hosted MCP endpoint (`.mcp.json` → Streamable HTTP at
`https://agentic-atlas.dev/mcp/`). It installs no SDK, CLI, local server, or
content bundle.

There is no bundled client, downloaded artifact, pinned release, or rollback
path in the plugin. The endpoint serves one active Release, and a promotion
replaces it wholesale. Every response identifies that Release so a
consultation can refuse to cross a promotion silently.

## Layout

- `.claude-plugin/plugin.json` — plugin manifest.
- `.mcp.json` — registers the hosted public consultation endpoint.
- `skills/consulting-patterns/` — the trigger discipline and
  inline-vs-dispatch rung routing.
- `agents/pattern-librarian.md` — the traversal method and the
  bounded, path-cited return contract.

Harnesses with no plugin system get the same contract as copyable
prose, served at
[agentic-atlas.dev/consult.md](https://agentic-atlas.dev/consult.md).

This directory contains only the public companion components. Corpus files,
publisher tooling, a local client, and a fallback server are not part of the
plugin.
