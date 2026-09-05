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
  # The case begins after a dispatch, so the surface check has already
  # passed. Without the surface the contract's answer is rule 1 — say so
  # and stop — and the recovery these graders judge could never run.
  - mcp__plugin_agentic-atlas_agentic-atlas__*
  # Granted for the same reason, one rung up: rule 4's recovery *is* a
  # dispatch. Withheld, the run can only reach rule 2's inline path, and
  # the corrective re-dispatch could be described but never taken — which
  # is all a grader reading the message could ever have observed.
  - Agent
---

You are mid-way through the reviewing-agent-designs flow from the
agentic-atlas plugin: read that skill and its shared return-shapes
contract now if you have not already. The parent session's `atlas_*`
tools are working. You dispatched the design-auditor in audit mode over
my skill at `./my-skill/SKILL.md`, and this is the complete reply that
just came back from the agent:

```
Thanks for the interesting artifact! Here's my take.

The skill has some problems. The description is quite vague and the body
does a lot of work inline that a subagent should probably do. There's a
pattern about offloading work to subagents that seems relevant, and
another one about contracts between agents. Overall I'd call this a 6/10
design. Let me know if you want more detail!
```

Continue the flow from here and tell me what you are doing and why.
