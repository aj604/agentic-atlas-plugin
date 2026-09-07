# Installing Agentic Atlas for Cline

This is a remote, hosted Model Context Protocol server. There is nothing to
clone, build, or install locally, and nothing to configure with secrets.

- **Endpoint:** `https://agentic-atlas.dev/mcp/`
- **Transport:** Streamable HTTP
- **Access:** read-only, no authentication, no account, no payment

## Add the server

Add a remote server to Cline with this configuration:

```json
{
  "mcpServers": {
    "agentic-atlas": {
      "type": "streamableHttp",
      "url": "https://agentic-atlas.dev/mcp/"
    }
  }
}
```

No API key, environment variable, or other secret is required. Once added,
Cline should list the server's tools against the endpoint above with no
further setup.

## What it serves

This `0.6.0` source artifact is prepared for the target-v6 surface of five
`atlas_*` tools: orienting into the corpus, batching Cards with optional
provenance, reading Nodes, Decisions and terms at returned addresses,
following links, and navigating the Release. Its publication is gated on
promotion of the coordinated v6 server Release; this preparation does not
claim the hosted endpoint has changed. All calls are read-only.
