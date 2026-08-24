---
name: ordinary coding tasks leave all three skills quiet
tags:
  - trigger
runs: 3
max_turns: 6
allowed_tools:
  - Skill
  - Read
  - Glob
  - Grep
---

Two quick things. First, review this function for bugs:

```python
def dedupe(items):
    seen = []
    for i in items:
        if i not in seen:
            seen.append(i)
    return seen
```

Second, I'm designing the database schema for the agent-run history in
our app — runs, steps, and tool calls. Suggest tables and indexes.
