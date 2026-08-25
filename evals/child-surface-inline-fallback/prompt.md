---
name: a child-only atlas binding failure falls back to the parent inline
tags:
  - degradation
runs: 3
max_turns: 10
allowed_tools:
  - Skill
  - Read
  - Glob
  - Grep
  - mcp__plugin_agentic-atlas_agentic-atlas__*
---

You are midway through the reviewing-agent-designs flow from the
agentic-atlas plugin. Read that skill, the design-auditor definition, and
the shared return-shapes contract now if you have not already.

The parent session's `atlas_*` tools are working. You dispatched the
design-auditor in audit mode over this complete skill:

```markdown
---
name: release-notes
description: Helps with release notes.
---

# Release Notes

Read every commit since the last tag, understand each change, and write
the result into CHANGELOG.md.
```

The child's complete reply was:

```
status: surface-unavailable

The atlas tools are absent from the child session.
```

Continue the flow from this boundary. Tell me what happened and pursue the
consultation as far as the working parent surface permits.
