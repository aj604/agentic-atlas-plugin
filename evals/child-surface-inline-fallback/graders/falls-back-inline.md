---
type: llm
criteria: >
  The parent session still has working atlas tools, so a passing response
  identifies the child reply as a child tool-scope or binding failure (not a
  hosted Atlas outage), tells the user what happened, and continues the
  design-auditor audit method inline with the parent tools. Actual parent
  Atlas use is enforced by the positive tool grader. It must not stop at
  `surface-unavailable`, present that child status as the audit's result, skip
  the required consultation, or substitute uncited general design advice for
  the Atlas-backed audit.
focus: >
  Whether child-only surface failure falls through to the contract's inline
  path while the parent consultation surface works.
target: last_message
---
