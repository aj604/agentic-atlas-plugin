---
name: designing-agent-systems
description: 'Design a new agent system with the published Agentic Atlas patterns — interview the user, consult the corpus once with the consolidated problem, and propose a decomposition where every structural choice carries its citation. Use whenever the user is starting a skill, subagent, agent definition, plugin, hook set, or multi-agent workflow that does not exist yet, or is rethinking one''s shape from open questions — "help me design", "how should I decompose this", "what should my agent carry and return", choosing dispatch boundaries, context budgets, verification seams, or persistence shape. Also the home for quick atlas lookups: "what does a pattern prescribe", "what does the atlas mean by X", "where do I start with the atlas". Not for auditing an artifact that already exists (that is reviewing-agent-designs), not for retrofitting one named pattern (applying-a-pattern), and not for ordinary software design — a database schema, an API, application code — that merely mentions agents.'
---

# Designing Agent Systems

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
stop. Never answer from memory of the corpus.

A dispatch that later returns `surface-unavailable` while these tools are
present in the session is the child's tool scope failing to bind, not the
atlas — per the contract's rule 1, say what happened and fall through to
the rule-2 inline path below instead of stopping.

## Cheap path — no dispatch

One term ("what does the atlas mean by momentum") → `atlas_define`. One
pattern's gist → `atlas_cards` on its id (batch 1–4 ids for an explicit
comparison). "Does the atlas have anything about X" with no id in hand →
`atlas_orient`, one call, then cards on whichever candidates the user
wants opened. "Where do I start" → `atlas_navigate` with `view="tour"`,
the publisher's curated walk, one call. Answer directly from the payload,
cite as `[<id> § <section>](https://agentic-atlas.dev/nodes/<id>#<section>)`
— the contract's citation form: the visible address works with
`atlas_read`, the link opens the exact Section — and done. A trivial
lookup never pays child-boot cost. Everything below is for an actual
design problem.

## Interview inline

The dialogue is never offloaded — a dispatched agent cannot ask your user
anything. Establish, in the user's own terms:

- the goal — what the system should make happen
- the moments it serves — when it fires, who invokes it, what arrives
- constraints — harness, available tools, context budget, conventions
  already ruled
- what exists so far, if anything

Stop when a fresh reader could act on the problem statement without you.
Don't over-interview a user who arrived with the answers already stated.

## One consolidated dispatch

Consultation quality degrades when a problem accretes turn by turn, so
consolidate the entire problem into one fresh dispatch of the
`pattern-librarian` agent each time. There is no stateful consultation
session: when the design shifts materially after a proposal, compose a
fresh consolidated dispatch from scratch — the whole updated problem, not
a delta on the last one. A fresh dispatch may also land on a newer
Release than the last one did; the new proposal re-cites everything from
the new consultation rather than reusing the old proposal's citations, so
two Releases are never stitched into one recommendation.

The librarian holds only the `atlas_*` tools — no file access, by
charter. Everything it needs travels *as prose* in the dispatch: a file
path in "Current shape" is a dead reference it cannot follow, so describe
what exists rather than pointing at it. This is also why, unlike the
auditor dispatches, no contract path travels here — the shape sections
are pasted in full instead.

Dispatch prompt:

    Design problem: <goal>. Constraints: <constraints>. Current shape:
    <what exists or is proposed so far>. Decision being made: <the
    specific structural choices this consultation must inform>.

    Return shape — conform exactly:
    <paste the contract's "Shared forms", "Traversal rules", and
    "ConsultationReturn" sections, verbatim>

If the harness has no subagent support, contract degradation rule 2: read
`${CLAUDE_PLUGIN_ROOT}/agents/pattern-librarian.md` and run its method
inline yourself, producing and validating the same shape. In a standalone
skills-CLI install that file and the contract are absent too — read
https://agentic-atlas.dev/consult.md and run its consultation method
under its four governing rules (the contract's Traversal rules):
`atlas_orient` only when you hold no identity yet, `atlas_cards` on the
ids you hold, `atlas_read` on the `node#section` address a claim names,
carrying `expected_revision` throughout. The consultation is never
optional.

## Validate, then propose

Run the ConsultationReturn receiver checks from the contract. On a
violation, degradation rule 4: exactly one corrective re-dispatch carrying
the failure evidence; a second violation is surfaced to the user verbatim.

A `nothing-bears` return is a valid result, not a failure: present it
honestly — the nearest nodes and why they fall short — before proposing
anything. A proposal can still follow, but it rests on general design
judgment rather than the atlas, and it says so plainly instead of
carrying citations it does not have. Inventing a citation to dress up an
uncited choice is the defect that status exists to prevent.

From a `consulted` return, propose the decomposition and present it for
approval before scaffolding anything: skill and agent count, each trigger
contract, dispatch boundaries, what each child carries in and returns,
verification seams. Every structural choice carries its own citation in
the contract's form, so the user can challenge any single choice by
reading its source — and statuses travel honestly, so a choice resting on
`fleshed` guidance says so. Nothing is created until the user approves.

On approval, build the artifacts yourself, in the main context, through
the normal development workflow and approval flow — the librarian never
touches files — keeping each citation attached to the choice it grounds
as you scaffold. Follow-ups route to the siblings: "apply <pattern>" to
what now exists belongs to applying-a-pattern, and auditing the built
system against the full corpus belongs to reviewing-agent-designs.
