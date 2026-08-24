# Plugin evals — `claude plugin eval`

Behavioral evals for the companion plugin, judged entirely by external
behavior per issue #441's testing decisions: what fires, what gets
dispatched, what a return is checked against, what the user is told. No
prompt wording or internal call ordering is asserted.

Run from this plugin's directory (the harness is early-access; a plain
`claude plugin eval` in an empty directory tells you whether your session
is enabled):

```bash
claude plugin eval . --allow-tools Skill --allow-tools Read --allow-tools Glob --allow-tools Grep
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

Not covered here, deliberately:

- **Degradation honesty for an absent surface** (no `atlas_*` tools →
  honest stop) needs the hosted MCP endpoint to be unreachable, and the
  eval sandbox does not block network. Exercise it manually by running a
  case with the plugin's `.mcp.json` endpoint unreachable.
- **Seeding a real subagent's return** is not supported by the harness;
  `return-shape-recovery/` seeds the return through the prompt instead,
  which tests the same receiver behavior.
- **The child-surface fallback** (a dispatch returning
  `surface-unavailable` while the session's own `atlas_*` tools work →
  fall through to the inline path, per the contract's rule 1) has the
  same seeding limitation; exercise it manually by registering the
  hosted endpoint under a server name the agents' `tools:` glob does not
  match.
