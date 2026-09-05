---
name: a missing parent atlas surface stops without invented guidance
tags:
  - degradation
runs: 3
max_turns: 6
allowed_tools:
  - Skill
  - Read
  - Glob
  - Grep
  # Granted so that not dispatching is the plugin's choice rather than the
  # harness's: `no-child-dispatch.md` asserts the child is never started,
  # and an absence claim over a tool the run could not reach passes itself.
  - Agent
---

Audit this existing Claude Code skill against the Agentic Atlas patterns:

```markdown
---
name: release-notes
description: Helps with release notes.
---

# Release Notes

Read every commit since the last tag, understand each change, and write
the result into CHANGELOG.md.
```

For this case, the companion plugin loaded but its hosted MCP registration
failed before this turn: no `atlas_*` tools are present in the parent
session. Exercise the plugin's public failure behavior. Do not answer the
audit itself from general design knowledge or memory of the patterns.
