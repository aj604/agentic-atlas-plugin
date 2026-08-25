---
name: reviewing-agent-designs
description: Audit an existing skill, subagent or agent definition, plugin, hook configuration, or multi-agent workflow against the published Agentic Atlas patterns, returning cited, checkable findings. Use whenever the user asks to review, audit, critique, sanity-check, or grade an agent artifact they have already written — "review my skill", "audit my plugin", "is this agent definition right", "does my trigger description work", "check my subagent's carry and return shape" — even when they don't name the atlas. Not for greenfield design with no artifact yet (that is designing-agent-systems), not for retrofitting one named pattern (applying-a-pattern), and not for reviewing ordinary application code — a function, an endpoint, a schema — that merely lives near agents.
---

# Reviewing Agent Designs

The published atlas (agentic-atlas.dev) is the single source of truth;
this skill only routes into it — restate nothing from it. Every seam this
skill uses — return shapes, status vocabulary, citation form, degradation
rules — is defined once in the shared contract at
`${CLAUDE_PLUGIN_ROOT}/contracts/return-shapes.md` (the plugin root, two
directories above this skill). Read it before dispatching or validating;
this skill names its rules rather than restating them. In a standalone
skills-CLI install that file is absent — the hosted copy at
https://agentic-atlas.dev/consult.md stands in.

## Surface check first

The `atlas_*` tools must already be in the session — the plugin registers
the hosted transport itself (`.mcp.json` → Streamable HTTP at
`https://agentic-atlas.dev/mcp/`); a standalone skills-CLI install must
connect that same endpoint first (`https://agentic-atlas.dev/connect`).
If the tools are absent, follow contract degradation rule 1: say so and
stop. Never audit from memory of the corpus.

A dispatch that later returns `surface-unavailable` while these tools are
present in the session is the child's tool scope failing to bind, not the
atlas — per the contract's rule 1, say what happened and fall through to
the rule-2 inline path below instead of stopping.

## Cheap path — no dispatch

When the ask is really one lookup ("does the atlas have a pattern about
trigger descriptions?"), answer it inline — `atlas_cards` on an id you
hold, `atlas_define` for a term, `atlas_orient` when you hold no identity
— in one or two calls, cited as
`[<id> § <section>](https://agentic-atlas.dev/nodes/<id>#<section>)`,
the contract's citation form. The audit below is for an actual artifact.

## Locate the artifact inline

Find the files yourself before dispatching — the auditor should spend its
window auditing, not hunting. A skill is its SKILL.md plus bundled
resources; an agent is its definition file; a plugin is its manifest,
`.mcp.json`, hooks, and every skill and agent — audited as one
decomposition, including whether each skill earns its resident description
slot. A hook configuration is its hook entries plus every script they
invoke — the scripts are where the behavior lives, and an audit of the
entries alone misses it. A workflow is its orchestrating skill, prompt,
or script plus every agent definition it dispatches. If it's ambiguous
which artifact the user means, ask; a wrong guess audits the wrong thing
at full cost.

## One consolidated dispatch

Dispatch the `design-auditor` agent once, in audit mode, with everything
it needs — it cannot ask back. The user's stated concerns travel
**verbatim**: a paraphrase loses the constraint they actually care about,
and the concerns focus the audit without blinkering it.

    Mode: audit. Artifact: <kind — skill / agent / plugin / hooks / workflow>.
    Files: <every path located above>.
    The user's stated concerns, verbatim: <quote, or "none stated">.
    Contract: <path to ${CLAUDE_PLUGIN_ROOT}/contracts/return-shapes.md>.

    Return shape — conform exactly:
    <paste the contract's "Shared forms", "Traversal rules", and
    "AuditReturn" sections, verbatim>

If the harness has no subagent support, contract degradation rule 2: read
`${CLAUDE_PLUGIN_ROOT}/agents/design-auditor.md` and run its audit-mode
method inline yourself, producing and validating the same shape. In a
standalone skills-CLI install that file and the contract are absent too —
read https://agentic-atlas.dev/consult.md, then read the artifact files
yourself and run its consultation method under its four governing rules
(the contract's Traversal rules): `atlas_orient` only when you hold no
identity yet, `atlas_cards` on the ids you hold, `atlas_read` on the
`node#section` address a claim names, carrying `expected_revision`
throughout. The consultation is never optional.

## Validate, then present

Run the AuditReturn receiver checks from the contract. On a violation,
degradation rule 4: exactly one corrective re-dispatch carrying the
failure evidence; a second violation is surfaced to the user verbatim.

Present a valid return faithfully: findings in the auditor's order
(`[stable]` before `[fleshed]` — settled doctrine outranks claims still
gathering proofs), each tied to its file location or structural choice
with its citation and prescription intact, so the user can act on a
finding without re-deriving where it applies, and read the pattern's own
words before accepting it. A `clean` return is presented as clean, naming
what was examined; `nothing-bears` is presented honestly with the nearest
nodes. Offer to fix what the findings name — but start nothing until the
user asks; the fixes run in the main context under their normal approval
flow, and "apply <pattern>" follow-ups belong to applying-a-pattern.
