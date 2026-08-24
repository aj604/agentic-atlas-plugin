---
name: applying-a-pattern
description: Turn one named Agentic Atlas pattern into concrete, cited edits to one existing artifact. Use whenever the user names a specific atlas pattern — by id, by title, or by pointing at a page on agentic-atlas.dev — and wants it applied, adopted, retrofitted, or implemented in their skill, agent definition, plugin, or workflow: "apply <pattern> to my skill", "make my plugin follow <pattern>", "I read <pattern> on the atlas, retrofit it here". Not for a full audit against all the patterns (that is reviewing-agent-designs), not for open-ended design (designing-agent-systems), and not for refactors that don't trace to an atlas pattern — those stay with the normal development workflow.
---

# Applying a Pattern

The published atlas (agentic-atlas.dev) is the single source of truth;
this skill only routes into it — restate nothing from it. Every seam this
skill uses — return shapes, status vocabulary, citation form, degradation
rules — is defined once in the shared contract at
`${CLAUDE_PLUGIN_ROOT}/contracts/return-shapes.md` (the plugin root, two
directories above this skill). Read it before dispatching or validating;
this skill names its rules rather than restating them.

## Surface check first

The `atlas_*` tools must already be in the session — the plugin registers
the hosted transport itself (`.mcp.json` → Streamable HTTP at
`https://agentic-atlas.dev/mcp/`); a standalone skills-CLI install must
connect that same endpoint first (`https://agentic-atlas.dev/connect`).
If the tools are absent, follow contract degradation rule 1: say so and
stop. Never plan edits from memory of the corpus.

## Verify the pattern inline, before anything else

One `atlas_cards` call on the pattern id — this is the cheap check that
stops a misremembered id before any dispatch cost, and before a
fabricated plan can exist. If the user gave a loose title rather than an
id, `atlas_orient` first and confirm the match if more than one candidate
is plausible.

- **Unknown id** → stop with the honest answer: the id is not in the live
  Release, here are the nearest candidates from `atlas_orient`.
- **Roadmap-only** → stop: write the name and hook with
  "(roadmap — nothing published yet)", and leave it unlinked. An edit
  plan cannot be grounded in unpublished content.
- **Published** → note the Release revision the card came from; it travels
  into the dispatch so the plan is built on the same Release the
  verification saw (contract degradation rule 3).

## Dispatch apply mode

Locate the target artifact's files inline (ask if ambiguous), then
dispatch the `design-auditor` agent once, in apply mode:

    Mode: apply. Pattern id: <verified id>, read at revision <revision>.
    Artifact: <kind>. Files: <every path>.
    Constraints the user stated, verbatim: <quote, or "none stated">.
    Contract: <path to ${CLAUDE_PLUGIN_ROOT}/contracts/return-shapes.md>.

    Return shape — conform exactly:
    <paste the contract's "Shared forms" section and its "EditPlanReturn"
    section, verbatim>

If the harness has no subagent support, contract degradation rule 2: read
`${CLAUDE_PLUGIN_ROOT}/agents/design-auditor.md` and run its apply-mode
method inline yourself, producing and validating the same shape. In a
standalone skills-CLI install that file is absent too — read the pattern's
own sections (`atlas_read` on each `node#section` address the verified
card's claims name, carrying `expected_revision`), read the artifact
files, and derive the plan the same way. The consultation is never
optional, and every edit still cites as
`[<id> § <section>](https://agentic-atlas.dev/nodes/<id>#<section>)`,
the contract's citation form.

## Validate, present, then execute in the main context

Run the EditPlanReturn receiver checks from the contract. On a violation,
degradation rule 4: exactly one corrective re-dispatch carrying the
failure evidence; a second violation is surfaced to the user verbatim.

Present a valid plan whole: the ordered edits with their citations, and
the **Deliberately skipped** section with its reasons — partial
application is a visible decision the user gets to see, never a silent
gap. A `clean` return means the artifact already conforms; say so and
stop.

On approval, execute the edits yourself, in the main context, through the
normal development workflow and approval flow. The auditor never edits —
no subagent mutates the user's files out of sight — and the plan's
citations stay attached to the edits as you land them, so the user can
read the pattern's own words at any step.
