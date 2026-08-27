# Agentic Atlas — companion plugin for Claude Code

[Agentic Atlas](https://agentic-atlas.dev/) is a collection of field-tested
patterns for designing agent systems, readable by people and consultable by
agents over MCP. This repository distributes its public Claude Code companion
plugin.

## Install individual skills

    npx skills add aj604/agentic-atlas-plugin --skill reviewing-agent-designs
    npx skills add aj604/agentic-atlas-plugin --skill designing-agent-systems
    npx skills add aj604/agentic-atlas-plugin --skill applying-a-pattern

Each standard skills CLI command explicitly selects one skill —
`reviewing-agent-designs` audits an existing agent artifact against the
patterns, `designing-agent-systems` designs a new agent system, and
`applying-a-pattern` turns one named pattern into a cited edit plan. A
command installs that skill alone, not the repository's Claude Code plugin
manifest, MCP configuration, `pattern-librarian` agent, `design-auditor`
agent, or shared return-shapes contract; the skill then runs its
consultation method inline. Connect the hosted MCP endpoint for your
client first: <https://agentic-atlas.dev/connect>.

Browse the repository and its three capability areas on
[skills.sh](https://www.skills.sh/aj604/agentic-atlas-plugin):

- [reviewing-agent-designs](https://www.skills.sh/aj604/agentic-atlas-plugin/reviewing-agent-designs)
- [designing-agent-systems](https://www.skills.sh/aj604/agentic-atlas-plugin/designing-agent-systems)
- [applying-a-pattern](https://www.skills.sh/aj604/agentic-atlas-plugin/applying-a-pattern)

## Install the Claude Code companion plugin

    /plugin marketplace add aj604/agentic-atlas-plugin

Then install `agentic-atlas`. The plugin connects to the hosted, read-only MCP
endpoint at <https://agentic-atlas.dev/mcp/>. It installs no SDK, CLI, local
server, or content bundle.

Connection instructions are at <https://agentic-atlas.dev/connect>, and the
copyable consultation contract is at
<https://agentic-atlas.dev/consult.md>. Report plugin or transport problems in
this repository's [issue tracker](https://github.com/aj604/agentic-atlas-plugin/issues).

## Developer resources

The Atlas is a hosted publication, and its developer surfaces are served from
the domain rather than from this repository. All of them are read-only and
unauthenticated, and all are indexed at
<https://agentic-atlas.dev/developers>:

- [Agentic Atlas MCP server](https://agentic-atlas.dev/developers#developers-mcp-title)
- [Agentic Atlas HTTP API](https://agentic-atlas.dev/developers#developers-api-title)
- [Agentic Atlas authentication](https://agentic-atlas.dev/developers#developers-auth-title)
- [Agentic Atlas availability](https://agentic-atlas.dev/developers#developers-availability-title)
- [Agentic Atlas manifests and policy documents](https://agentic-atlas.dev/developers#developers-manifests-title)

Working on the plugin with an AI coding agent? Start with
[AGENTS.md](AGENTS.md).
