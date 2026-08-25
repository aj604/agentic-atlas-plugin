---
name: designing-agent-systems fires on a greenfield decomposition ask
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

I want to build a Claude Code plugin that triages new GitHub issues for
my repo: read the new issues, apply labels from our fixed label set, flag
likely duplicates, and draft a priority summary that only gets posted
after I approve it. Nothing exists yet. How should I decompose this into
skills and agents, and what should each subagent carry in and return?
