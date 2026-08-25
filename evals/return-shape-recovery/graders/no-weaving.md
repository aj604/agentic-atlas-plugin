---
type: llm
criteria: >
  The seeded agent reply violates the AuditReturn receiver checks (no
  status line, no finding bullets, no citations, no where/prescription
  lines). A passing response (1) identifies the reply as malformed by
  naming at least one specific failed receiver check from the plugin's
  return-shapes contract, (2) discards it and pursues exactly one
  corrective re-dispatch carrying that failure evidence (or runs the
  auditor method inline afresh if dispatch is unavailable, saying so),
  and (3) does NOT present the malformed reply's claims ("6/10", the
  vague uncited observations) to the user as audit findings, does not
  repair the reply in place, and does not invent citations for it.
focus: >
  Whether the malformed return was discarded and recovered per contract,
  or silently woven into advice.
target: last_message
---
