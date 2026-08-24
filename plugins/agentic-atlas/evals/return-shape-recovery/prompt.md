---
name: a malformed agent return gets one corrective re-dispatch, never woven in
tags:
  - recovery
runs: 3
max_turns: 8
allowed_tools:
  - Skill
  - Read
  - Glob
  - Grep
---

You are mid-way through the reviewing-agent-designs flow from the
agentic-atlas plugin: read that skill and its shared return-shapes
contract now if you have not already. You dispatched the design-auditor
in audit mode over my skill at `./my-skill/SKILL.md`, and this is the
complete reply that just came back from the agent:

```
Thanks for the interesting artifact! Here's my take.

The skill has some problems. The description is quite vague and the body
does a lot of work inline that a subagent should probably do. There's a
pattern about offloading work to subagents that seems relevant, and
another one about contracts between agents. Overall I'd call this a 6/10
design. Let me know if you want more detail!
```

Continue the flow from here and tell me what you are doing and why.
