# Agentic Atlas — companion plugin for Claude Code

[Agentic Atlas](https://agentic-atlas.dev/) is a collection of field-tested
patterns for designing agent systems, readable by people and consultable by
agents over MCP. This companion plugin supplies three skills for the three
design moments — auditing an artifact you have, designing a system you don't
have yet, and applying one pattern you just read — over two strictly
read-only agents, all riding the current frozen surface of
eight `atlas_*` tools on the hosted MCP endpoint (`.mcp.json` → Streamable HTTP at
`https://agentic-atlas.dev/mcp/`). It installs no SDK, CLI, local server, or
content bundle.

There is no bundled client, downloaded artifact, pinned release, or rollback
path in the plugin. The endpoint serves one active Release, and a promotion
replaces it wholesale. Every response identifies that Release so a
consultation can refuse to cross a promotion silently.

## Layout

- `.claude-plugin/plugin.json` — plugin manifest.
- `.mcp.json` — registers the hosted public consultation endpoint.
- `contracts/return-shapes.md` — the one normative statement of every
  skill↔agent seam: the three return shapes, the shared status vocabulary,
  the citation form, and the uniform degradation rules. Skills paste the
  relevant shape into each dispatch and validate returns against its
  receiver checks; nothing restates a shape anywhere else.
- `skills/reviewing-agent-designs/` — audit an existing skill, agent,
  plugin, or workflow against the patterns; cited, checkable findings.
- `skills/designing-agent-systems/` — inline interview, one consolidated
  corpus consultation, a proposed decomposition with every structural
  choice cited. Also the home of cheap inline lookups.
- `skills/applying-a-pattern/` — verify one named pattern against the live
  Release, get a cited edit plan, execute it in the main context.
- `agents/pattern-librarian.md` — pure corpus traversal
  (ConsultationReturn); serves designing-agent-systems.
- `agents/design-auditor.md` — reads the user's artifact read-only and
  consults the corpus; audit mode (AuditReturn) serves
  reviewing-agent-designs, apply mode (EditPlanReturn) serves
  applying-a-pattern. It never edits.
- `evals/` — behavioral evals for the `claude plugin eval` harness:
  trigger accuracy (positive and negative) and return-shape recovery.
  See `evals/README.md` for the run line and the deliberate gaps.

Harnesses with no plugin system get the consultation contract as copyable
prose, served at
[agentic-atlas.dev/consult.md](https://agentic-atlas.dev/consult.md).

This directory contains only the public companion components. Corpus files,
publisher tooling, a local client, and a fallback server are not part of the
plugin.
