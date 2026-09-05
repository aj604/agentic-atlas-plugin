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

The endpoint exposes eight `atlas_*` tools for consulting a published
collection of field-tested patterns for designing agent systems: orienting
into the corpus, reading cited pattern sections, and following decisions and
provenance. All calls are read-only.
