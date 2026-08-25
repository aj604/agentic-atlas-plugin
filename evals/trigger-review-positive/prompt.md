---
name: reviewing-agent-designs fires on an audit ask (and its siblings stay quiet)
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

I just finished writing a Claude Code skill for my team and I'd like it
checked against the agentic-atlas patterns before I ship it. I'm worried
the description is too vague to trigger reliably. Here is the whole file
(`SKILL.md`):

```markdown
---
name: standup-notes
description: Helps with standup notes.
---

# Standup Notes

When the user asks for standup notes, read the last day of git commits,
read every changed file to understand what happened, summarize each
teammate's work in 2-3 sentences, and post the summary to Slack with the
slack MCP tool. If anything is unclear, make your best guess rather than
asking.
```

Can you audit it?
