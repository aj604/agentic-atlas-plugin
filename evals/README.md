# Plugin evals — `claude plugin eval`

Behavioral evals for the companion plugin, judged entirely by external
behavior per issue #441's testing decisions: what fires, what gets
dispatched, what a return is checked against, what the user is told. No
prompt wording or internal call ordering is asserted.

Run from this plugin's directory (the harness is early-access; a plain
`claude plugin eval` in an empty directory tells you whether your session
is enabled):

```bash
claude plugin eval . --allow-tools Skill --allow-tools Read --allow-tools Glob --allow-tools Grep --allow-tools 'mcp__plugin_agentic-atlas_agentic-atlas__*'
```

Coverage:

- `trigger-review-positive/`, `trigger-design-positive/`,
  `trigger-apply-positive/` — each skill fires on its own sentences and
  the siblings stay quiet (the main risk of the three-description
  decomposition).
- `trigger-negative-ordinary-code/` — ordinary coding tasks ("review this
  function", "design a database schema") leave all three skills quiet.
- `return-shape-recovery/` — a seeded malformed AuditReturn is discarded
  and recovered per the contract (one corrective re-dispatch carrying the
  failure evidence), never woven into advice.
- `surface-unavailable-stop/` — a parent session with no Atlas tools stops
  honestly before dispatch and never substitutes guidance from memory.
- `child-surface-inline-fallback/` — a seeded child-only tool-binding failure
  is disclosed and falls through to the working parent's inline audit method,
  making at least one parent Atlas call without retrying the broken child.

Not covered here, deliberately:

- **Seeding a real subagent's return** is not supported by the harness;
  `return-shape-recovery/` and `child-surface-inline-fallback/` seed the
  returned boundary through the prompt, then judge the same receiver
  behavior. The child-fallback case uses the real hosted parent surface.
- **Transport outage mechanics** are not simulated: the absent-surface case
  starts after failed MCP registration and judges the skill's public response.
  Transport connection and addressing are exercised by the publisher's MCP
  integration suite.
