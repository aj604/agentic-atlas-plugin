---
name: consulting-patterns
description: Consult Agentic Atlas when designing, reviewing, or restructuring a skill, subagent, agent definition, plugin, or multi-agent workflow — especially while choosing decomposition, dispatch boundaries, context budgets, subagent carry/return shape, verification seams, or persistence/config shape. Use before settling those design decisions; not for executing an existing skill, ordinary application code, or tasks that merely mention agents.
---

# Consulting Patterns

The published atlas (agentic-atlas.dev) is the single source of truth; this
skill only routes into it. Restate nothing from it.

## The consultation surface (locate, don't call yet)

The Claude Code plugin registers the hosted transport itself (`.mcp.json` →
Streamable HTTP at `https://agentic-atlas.dev/mcp/`). A standalone skills CLI
install carries only this skill, so its operator must connect that same hosted
endpoint first (instructions: `https://agentic-atlas.dev/connect`). In either
installation, the `atlas_*` tools must already be in the session — nothing to
cache and no corpus on this machine. The surface is eight tools over one active
Release, and the disclosure tiers run `atlas_orient` → `atlas_cards` →
`atlas_read` (a named Section address) → `atlas_read` (the whole Node id);
`atlas_navigate` and `atlas_define` answer quick lookups in one call.
`atlas_navigate` with
`view="tour"` answers "where do I start" with the publisher's own curated
walk, in one call, before any of the above;
the rest are the deliberate floor. Statuses are honest at every tier — weight
`stable` above `fleshed`. A roadmap disclosure is unpublished: write only its
name and hook with "(roadmap — nothing published yet)" and leave it unlinked.

**Address directly.** The tiers are a cost order, not a walk: an identity
you already hold reaches the lowest sufficient payload in one call, so
never orient to earn a card you could have asked for. Every payload
declares what it left out and the one call that recovers it — follow that
address rather than guessing the next rung.

**Carry the revision.** Each payload names the Release it was read from;
pass it back as `expected_revision` on every later call in the same
consultation, and pass a cursor back unchanged. A promotion mid-traversal
comes back as `revision_changed` with no payload — restart the
consultation on the new Release rather than mixing two.

If the `atlas_*` tools are absent from the session, say so and stop — the
plugin's MCP server didn't register (needs network to the atlas domain).
A `catalog_unavailable` error means the deployment is serving no Release;
say that too. Never answer from memory of the corpus in their place.

## Route by question shape — load only what the rung uses

Decide the rung from the question alone, before calling any tool.

**"Where do I start"** — `atlas_navigate` with `view="tour"`, one call: the
publisher-curated first tour, an ordered walk of Nodes with narration. Answer
from it directly; do not assemble a walk from the `tree` view in its place.

**Inline rung** — the need is one term or one pattern's gist ("what does
the atlas mean by momentum", "what does heavy-agent prescribe"): for a
term, `atlas_define` (one admitted glossary entry; ambiguity comes back as
candidate terms, not an error); for a pattern, `atlas_cards` on its id,
which is one call for hook, status and the decision-bearing claims. Reach
for `atlas_orient` (identity, title, status and hook per candidate) or
`atlas_navigate` with `view="tree"` (canonical id, title and depth, in
canonical order) only when
you don't have the id yet, and for **at most one** `atlas_read` of a named
section if the card isn't enough. Do not dispatch.

For an explicit comparison between named patterns, batch their ids in one
`atlas_cards` call rather than assembling separate reads — 1–4 distinct
ids, one Card each, and no ranking at read time. For "why did the corpus
choose this?", use `atlas_decisions` and then `atlas_read` with the listed
`decision:<id>` address for the record itself; decision records explain
history but never override the live Release.

**Dispatch rung** — a design decision where multiple patterns plausibly
bear (decomposition, dispatch boundary, context budget, return shape,
verification seam, persistence): dispatch the `pattern-librarian` agent
directly — do not walk the ladder first; the librarian runs its own
traversal with the same `atlas_*` tools. State the design problem in full —
the librarian answers only what is stated:

    Design problem: <goal>. Constraints: <constraints>. Current shape:
    <what exists or is proposed so far>. Decision being made: <the specific
    choice this consultation must inform>.

    Return per your contract: pattern bullets first
    (`- **<name>** ([<id> § <section>](https://agentic-atlas.dev/nodes/<id>#<section>))`),
    every substantive published-pattern claim cited in that Markdown form,
    statuses flagged, under ~80 lines.

The librarian returns applicable patterns with per-design guidance,
tensions, and `[<id> § <section>](https://agentic-atlas.dev/nodes/<id>#<section>)`
citations: the visible address remains directly usable with `atlas_read`, and
the link opens the exact Human Section.

If the rung is ambiguous, call `atlas_navigate` with `view="tree"` and
re-decide.

**Degradation rule** — in a harness with no `pattern-librarian` agent (including
a standalone skills CLI install), the dispatch rung does not exist: run the
librarian method inline yourself —
`atlas_orient` (only if you hold no identity yet; match its candidates
against the task), `atlas_cards` (batch the candidates 1–4 at a time; a
bad id fails the whole call, so drop it and re-batch rather than retrying
one by one), `atlas_read` (a `node#section` address first, the bare Node id only
where the decision turns). The rule is absolute:
never fabricate a dispatch, and never skip the consultation because
dispatch is missing.

## Validate the return, then apply

Check the librarian's reply before using it: it begins with a
`- **<pattern name>**` bullet, every pattern bullet carries an
`[<id> § <section>](https://agentic-atlas.dev/nodes/<id>#<section>)` citation,
every substantive published-pattern claim is Section-cited, and the reply is
within ~80 lines. On violation, discard the reply and re-dispatch once with
the original task **plus the failed contract evidence and a targeted
correction**; do not merely roll the same prompt again, repair the reply in
place, continue the same agent, or fill in citations yourself. If the second
reply also violates, show the user the malformed return and say validation
failed, rather than weaving it in.

Weave a valid consultation into the design work at hand. Cite pattern
names with the same linked `id § section` Markdown form so the user can read
deeper through `atlas_read` or open the exact Section on agentic-atlas.dev.
Where a claim has to be auditable, pass
the Card's compact source addresses to `atlas_provenance` — publisher and
attestation date, charged only when you are actually auditing. Treat
`fleshed` guidance as claims-frozen but still gathering proofs — say so
when you rely on it.
