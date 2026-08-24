---
name: applying-a-pattern fires when one named pattern meets one artifact
tags:
  - trigger
runs: 3
max_turns: 8
allowed_tools:
  - Skill
  - Read
  - Glob
  - Grep
---

I read the subagent-offload pattern on agentic-atlas.dev and I want it
applied to my release-notes skill. Here is the skill (`SKILL.md`):

```markdown
---
name: release-notes
description: Helps with release notes.
---

# Release Notes

When the user asks for release notes, read every commit since the last
tag, read the changed source files and any referenced issues to
understand each change, categorize everything, and write the draft into
CHANGELOG.md.
```

Retrofit the pattern here — show me the plan first.
