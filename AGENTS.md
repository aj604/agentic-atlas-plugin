# AGENTS.md — working on the Agentic Atlas companion plugin

Instructions for AI coding agents (and people) working in this repository.

## What this repository is

A Claude Code companion plugin for [Agentic Atlas](https://agentic-atlas.dev/),
a collection of field-tested patterns for designing agent systems. The plugin
is entirely prose and configuration: three skills, two read-only subagents, one
shared contract, and four manifests. There is no source code, no build step, no
test suite, and no dependency to install.

**This repository is a publication target.** Each release replaces its contents
wholesale, so an edit committed here does not survive the next one. Propose
changes through the
[issue tracker](https://github.com/aj604/agentic-atlas-plugin/issues) rather
than by patching files in place.

## The patterns are not in this tree

The atlas itself is served, not vendored. Every skill and agent here reaches it
over the hosted Model Context Protocol endpoint,
<https://agentic-atlas.dev/mcp/> — Streamable HTTP, unauthenticated, nothing to
install or cache. The endpoint serves one active Release and a promotion
replaces it wholesale, so every response names the Release it came from and a
consultation can refuse to cross a promotion silently.

Do not copy pattern text into this repository, and do not add a local cache,
bundled client, or fallback server. A restated pattern is a second source of
truth that ages the moment the atlas is promoted.

## Layout

    plugin.json                      portable manifest (agent-plugins.org 1.0.0)
    mcp.json                         portable MCP config (Streamable HTTP)
    .claude-plugin/plugin.json       Claude Code's manifest, same facts
    .mcp.json                        Claude Code's MCP config, same endpoint
    skills/<name>/SKILL.md           the three skills
    agents/*.md                      the two read-only subagents
    contracts/return-shapes.md       the one normative skill-to-agent seam
    evals/                           behavioral evals for `claude plugin eval`
    .claude-plugin/marketplace.json  the marketplace entry (repository root)

The two manifest dialects state one product. `plugin.json` and `mcp.json` are
the portable Agent Plugins format any conformant client reads; the dotted pair
is what Claude Code reads. Claude Code spells the transport `http` and Agent
Plugins spells it `streamable-http` — one endpoint, two vocabularies. Change one
dialect and you must change the other.

## Conventions to keep

- **Skills route, they do not restate.** A skill names when to consult the
  atlas and how to dispatch; the answer comes back from the endpoint.
- **Every seam is defined once**, in `contracts/return-shapes.md`: the three
  return shapes, the shared status vocabulary, the citation form, the traversal
  rules, and the degradation rules. Skills paste the relevant shape into a
  dispatch and validate what comes back. Nothing restates a shape elsewhere.
- **The agents are strictly read-only.** `pattern-librarian` has the atlas
  tools and nothing else; `design-auditor` adds read-only file tools. Neither
  edits, and neither self-initiates — a skill dispatches them.
- **Trigger descriptions must separate the siblings.** Each skill's
  `description` says which design moment it owns and names the two it does not,
  so three resident descriptions do not compete for one situation.
- **Claim nothing the endpoint cannot back.** Citations are fetchable
  addresses on agentic-atlas.dev; an unpublished pattern is named as
  unpublished rather than linked.

## Trying it

Connect the endpoint for your client first — instructions per client are at
<https://agentic-atlas.dev/connect>. Then either install the plugin
(`/plugin marketplace add aj604/agentic-atlas-plugin`) or install one skill
with the commands in [README.md](README.md).

For a harness with no plugin system, the same consultation contract is
published as copyable prose at <https://agentic-atlas.dev/consult.md>, and
<https://agentic-atlas.dev/llms.txt> lists every machine-readable surface this
publisher offers.
