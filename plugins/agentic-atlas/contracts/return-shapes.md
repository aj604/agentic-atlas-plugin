# Return shapes — the skill↔agent contract

This is the one normative statement of every seam between this plugin's
skills and agents. A skill pastes the relevant shape section (plus the
Shared forms section) verbatim into each dispatch prompt, and validates the
return against that shape's receiver checks. An agent conforms to the shape
its dispatch carries. Nothing restates a shape anywhere else — a second
prose copy is how two seams drift into coincidentally-similar contracts,
and this document exists so that cannot happen.

Every receiver check below is deterministic on purpose: the receiving
skill must be able to judge a return without judgment calls, so a
malformed return is discarded and re-dispatched (degradation rule 4)
rather than argued with or repaired in place.

## Shared forms

**Status line.** Every return's first line is exactly
`status: <value>` — nothing before it, not even a greeting. The values:

| value | meaning |
|---|---|
| `consulted` | patterns were found and distilled for the stated problem |
| `findings` | the audit found pattern-backed findings, or the plan has edits |
| `clean` | the artifact was examined and no published pattern is violated |
| `nothing-bears` | no published pattern bears; the nearest nodes are named with why they fall short |
| `surface-unavailable` | the atlas tools are absent or serving no Release; nothing was answered from memory |

`clean` and `nothing-bears` are honest results, not failures. Inventing a
finding to avoid a quiet answer is the defect these statuses exist to
prevent — a user can only trust "clean" if "clean" is a real outcome.

**Citation form.** Every substantive published-pattern claim carries:

```
[<id> § <section>](https://agentic-atlas.dev/nodes/<id>#<section>)
```

The visible `id § section` address is directly usable with `atlas_read`;
the link opens that exact Section on the Human site.

**Statuses are honest — carry them.** `stable` is settled doctrine.
`fleshed` is claims-frozen and still gathering proofs — flag it inline as
"(fleshed — claims frozen, proofs pending)" and never present it as
settled. A roadmap disclosure is unpublished: write only its name and hook
with "(roadmap — nothing published yet)", leave it unlinked, and never
invent its content.

**No prose dumps.** Never quote more than two consecutive sentences from a
node. The value of a return is distillation against the stated problem.

## ConsultationReturn

Produced by `pattern-librarian`; consumed by `designing-agent-systems`.

```
status: consulted

- **<pattern name>** ([<id> § <section>](https://agentic-atlas.dev/nodes/<id>#<section>))
  — what it prescribes or warns *for this specific design*, in 2–5
  sentences grounded in the stated goal and constraints. Not a node summary.
  (One bullet per applicable pattern, ordered by how much it constrains
  the design.)

**Tensions** — only if any exist: where applicable patterns pull the
design in different directions, and what tradeoff the corpus says governs
the choice.
```

With `status: nothing-bears`, the content is one opening bullet
`- **No pattern bears** — ` stating that plainly, then two or three
nearest nodes, one line each on why they fall short.

Receiver checks:

1. Line 1 is exactly `status: ` followed by one of
   `consulted` / `nothing-bears` / `surface-unavailable`.
2. If `consulted` or `nothing-bears`, the first non-blank line after the
   status line begins `- **`.
3. Every pattern bullet carries the citation form.
4. The whole return is ≤80 lines.

## AuditReturn

Produced by `design-auditor` in audit mode; consumed by
`reviewing-agent-designs`.

```
status: findings

- **<finding, one line>** [stable|fleshed] ([<id> § <section>](https://agentic-atlas.dev/nodes/<id>#<section>))
  - where: <file:line, file, or the structural choice named precisely>
  - prescription: <what the cited pattern prescribes for this artifact, concretely>
  (One bullet per finding, all [stable] findings before all [fleshed] ones.)
```

With `status: clean`, the content is a short paragraph naming what was
examined — the files read and the structural choices checked — so a quiet
result is itself checkable. With `status: nothing-bears`, the same form as
ConsultationReturn's.

Receiver checks:

1. Line 1 is exactly `status: ` followed by one of
   `findings` / `clean` / `nothing-bears` / `surface-unavailable`.
2. If `findings`, every finding bullet begins `- **`, carries a
   `[stable]` or `[fleshed]` tag, and carries the citation form.
3. Every finding has a `where:` line and a `prescription:` line.
4. The whole return is ≤100 lines.

## EditPlanReturn

Produced by `design-auditor` in apply mode; consumed by
`applying-a-pattern`.

```
status: findings

1. **<edit, one line>** ([<id> § <section>](https://agentic-atlas.dev/nodes/<id>#<section>))
   — <file>: <the concrete change, precise enough to execute without
   re-reading the pattern>
   (Numbered, in the order the edits should land.)

**Deliberately skipped** — each prescription the cited pattern makes that
this plan does not apply, with the reason (conflicts with a stated
constraint, out of the artifact's scope, …). Write "none" if the plan
applies everything the pattern prescribes.
```

With `status: clean`, the artifact already conforms to the pattern: say
what was checked and against which sections. `nothing-bears` means the
pattern is published but genuinely does not bear on this artifact — say
why, briefly.

Receiver checks:

1. Line 1 is exactly `status: ` followed by one of
   `findings` / `clean` / `nothing-bears` / `surface-unavailable`.
2. If `findings`, the edits are a numbered list starting at `1.`, and
   every item carries the citation form and names a file.
3. If `findings`, a `**Deliberately skipped**` section is present (its
   content may be "none").
4. The whole return is ≤100 lines.

## Degradation rules — uniform across all skills and agents

1. **Atlas tools absent.** If no `atlas_*` tools are in the session, say
   so and stop. Never answer from memory of the corpus in their place —
   uncited guidance impersonating the Release is worse than no answer. In
   an agent, return `status: surface-unavailable` plus one line naming
   what failed. In a skill, tell the user the consultation surface didn't
   register (the plugin's MCP server needs network to agentic-atlas.dev;
   a standalone skills-CLI install must connect the hosted endpoint per
   https://agentic-atlas.dev/connect) and stop. A `catalog_unavailable`
   error means the deployment is serving no Release; report that the same
   way.
2. **No subagent support.** The dispatch rung does not exist in this
   harness: read the would-be agent's definition file and run its method
   inline yourself, producing the same shape and validating it the same
   way. The consultation is never optional, and a missing dispatch rung is
   never a reason to skip it.
3. **Revision change mid-traversal.** Every payload names the Release it
   was read from; carry it back as `expected_revision` on every later call
   in the same consultation, and pass any cursor back unchanged. A
   promotion mid-traversal comes back as `revision_changed` with no
   payload: restart the traversal on the new Release. Never stitch two
   Releases together.
4. **Malformed return.** Discard it. Re-dispatch exactly once with the
   original prompt plus the failure evidence — which receiver checks
   failed, quoting the offending lines — and a targeted correction. Do not
   merely roll the same prompt again, repair the return in place, continue
   the same agent, or fill in citations yourself. If the second return
   also fails a check, show the user the malformed return verbatim and say
   which checks failed, rather than weaving it into advice. This recovery
   is safe because both agents are strictly read-only: a discarded return
   has no side effects to undo.
