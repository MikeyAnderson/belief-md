# Compiling a Belief Graph

Instructions for an agent compiling a `belief-graph.json` from a finished `BELIEF.md`.

This is a **projection**, not a third pass. `INVENTORY.md` retains, `BELIEF.md` organizes, the
graph *renders*. Nothing may enter the graph that is not already in the belief file, and the
graph is discarded and recompiled whenever the file changes. It is a view, and views are cheap.

`belief-graph.schema.json` is the authority on field names and enums. Where this document and
the schema disagree, the schema wins. Validate before delivering.

---

## The one rule that matters

**The graph asserts nothing the file does not.**

Every node is a belief that carries `layer`/`grip`/`warrant` in the file. Every edge is a
coupling the file states, belief-to-belief. Every anomaly stays open. The compiler's own
contribution is limited to three things, each of which must be visible in the output:
`primacy`, which is arithmetic; a supplied `strength` on a stated coupling, which goes in the
edge `note`; and the report at the end, which is prose to the principal and not part of the
file.

The failure mode is a graph that looks better connected than the file is. A sparse graph from a
file whose connections don't resolve is a **correct** graph — the sparseness is the finding, and
smoothing it over destroys the only diagnostic the projection offers.

---

## Output

One file, `<name>.belief-graph.json`, where `<name>` is the `name` from the file's frontmatter.
Drop it on `belief-graph.html` to render.

Top-level shape:

```json
{
  "format": "belief-graph",
  "formatVersion": "1.0",
  "protocol": "belief.md 2.1",
  "compiled": { "at": "", "from": [], "by": "", "notes": "" },
  "belief": {},
  "nodes": [],
  "edges": [],
  "anchor": {},
  "anomalies": [],
  "dissonances": [],
  "boundaries": [],
  "tripwires": [],
  "deepStructure": {},
  "plausibility": {},
  "formation": {},
  "narrative": {},
  "orientations": [],
  "review": {}
}
```

`compiled.notes` is where the compiler states its standing caveat: what provenance the source
carries, whether grips are guessed, and that only stated couplings are drawn.

---

## What becomes a node

**Beliefs only** — anything carrying a `layer: … · grip: … · warrant: …` line. That is the
whole test.

| In the file | In the graph |
| --- | --- |
| A belief under `## Worldview` | node, `structure: worldview`, `layer: core` |
| A belief under `## Web` | node, `structure: web`, layer as written |
| An attached record (2.1) | **not a node.** It carries no attributes and is governed by its belief. |
| A structure declared in frontmatter with no section | **nothing.** Report it. |
| A section whose entries carry no attribute line | **nothing.** Report it. |

`id` is the slugified title, lowercase, hyphens. **Titles are not rewritten to make better ids.**
Ids are what edges, anomalies, dissonances, tripwires, and orientations cite, so they are stable
across recompiles of the same file: if a title changes, the id changes and the reference breaks
loudly, which is the intended behavior.

`statement` is the belief's prose, verbatim. `agentImplication` is its **Agent implication**
paragraph, verbatim. Do not compress either; the graph is not a summary.

### Required and derived node fields

| Field | Rule |
| --- | --- |
| `worldviewQuestion` | Required on every `layer: core` node. `humanity` · `knowledge` · `ethics` · `ultimate-reality` · `god`. Take it from which of the five questions the belief answers. If the file's own accounting says a question is answered only obliquely, use that assignment and say so in `note`. |
| `evidence` | Only where the file supplies a marker: `cost-bearing-decision` · `repeated-practice` · `defended-under-disagreement` · `published-repeatedly` · `said-once`. Never inferred from tone. |
| `primacy` | Display weight, not a truth claim. Base `0.50`, plus `0.04` per inbound edge. An `evidence` marker overrides: `cost-bearing-decision` → `0.9`, `repeated-practice` → `0.7`. Clamp to `0`–`1`. Record the basis in `note`. |
| `grip` | Copied from the file. **`struck` is never a positive value** — a file asserting it is a compile error, not a node. |
| `gripGuessed` | `true` on every node whose grip the file did not get from the principal — which is *all of them* when `provenance: reconstructed`. |
| `note` | Where the compiler's own reasoning goes. Record which grips the file's guessed-grip table covers and which it doesn't; that distinction is the single most useful thing the graph surfaces for review. |
| `source` | Where the file credits someone else for the formulation (`received-from` in the inventory). |

---

## Edges

An edge is a coupling the `## Web` **Connections** block states, where **both ends are node
titles**. That is the 2.1 connections-must-resolve rule, enforced at compile time.

```json
{ "from": "", "to": "", "strength": "tight", "kind": "derives-from", "note": "" }
```

- `strength`: `tight` · `moderate` · `loose`. Loose couplings are couplings — draw them.
- `kind`: `derives-from` · `supports` · `tension`.
- Direction runs from the dependent belief to the one it hangs on. *"Move X and decision rights
  move"* is an edge **from** decision rights **to** X.
- If the file states a coupling but no strength, supply one and say so in `note`. That is the
  only value the compiler is permitted to invent, and it is never invisible.
- A coupling whose other end is a *domain* — hiring, compensation, product decisions — draws
  **nothing**. Do not substitute the nearest belief. List it in the report as a coupling that
  did not resolve, and name which case it is: a missing belief, or a coupling looser than it
  sounded.

Never create an edge from thematic similarity, shared vocabulary, or an obvious derivation the
file leaves unstated. The obvious ones are the most tempting and the most damaging, because they
are the ones a principal will not notice were added.

---

## The remaining structures

| Structure | Field | Notes |
| --- | --- | --- |
| `web` anchor | `anchor` | `text` verbatim, `hangsFrom` one line. Set `singleHumanAuthority: true` when the web hangs on one person's judgment — including when the file diagnoses this about itself. It wants it said. |
| `web` anomalies | `anomalies[]` | `question` verbatim. `status` is **always `open`**. `between[]` holds only node ids the file itself names as being in tension. Resolving one end and not the other is correct and common — record the one. |
| `dissonance` | `dissonances[]` | `stated`, `actual`, `cause`, `onGap` (`name-it` · `hold-it` · `work-it`). `nodeId` only when the stated belief is a node title. |
| `boundary` | `boundaries[]` | `authority`, `boundedClaims[]`, `atTheEdge` (`refuse` · `flag` · `defer`). A boundary section naming two authorities with different edge behavior compiles to two entries. |
| `tripwire` | `tripwires[]` | `trigger`, `response`, `authority` verbatim. `nodeId` where the tripwire guards a specific belief. |
| `deep-structure` | `deepStructure` | `resisted[]` for the long-cycle forces; `ambientDefault` with `name`, `description`, `tell` for the default the agent must not drift toward. The `tell` is the operative part — keep the file's concrete contrast intact. |
| `plausibility` | `plausibility` | `assumed[]`, `contested[]`. One entry per line as written; do not merge. |
| `formation` | `formation` | `loves[]`, `practices[]`, `competingLiturgies[]`. |
| `narrative` | `narrative` | The seven beats: `onceUponATime`, `andEveryDay`, `untilOneDay`, `andBecauseOfThat[]`, `untilFinally`, `andEverSince`. |
| `decision-surface` | `orientations[]` | `imperative`, `body`, and `sourceRef` — the `←` pointer verbatim. Add `sourceNodeId` only when the pointer resolves to a node. An orientation citing `deep-structure`, `boundary`, `tripwire`, or a frontmatter key has a `sourceRef` and no `sourceNodeId`. |
| — | `review` | `guessedGrip[]` — every id whose grip was inferred. `leastConfident[]` — placements the file itself flags as shaky. |

---

## Prohibitions

1. **Don't resolve an anomaly.** Not in `question`, not in `note`, not by drawing an edge that
   implies the resolution. `on-anomaly` in the frontmatter binds the compiler too.
2. **Don't promote or demote.** `layer` is copied, never adjusted for graph balance.
3. **Don't merge near-duplicate beliefs.** Two beliefs at different abstraction levels are two
   nodes. Merging here undoes what the inventory pass exists to protect.
4. **Don't rewrite statements.** No tightening, no fixing the em-dashes, no dropping the hedge.
5. **Don't fill a declared-but-absent structure.** A `structures:` entry with no section is a
   finding about the file, and it belongs in the report, not in the JSON.
6. **Don't invent an id.** Every id in `edges`, `between`, `nodeId`, `sourceNodeId`, and
   `review` resolves to a node in the same file, or the compile fails.

---

## Before you deliver

- [ ] Validates against `belief-graph.schema.json`.
- [ ] Every `from`, `to`, `between`, `nodeId`, `sourceNodeId`, and `guessedGrip` id resolves.
- [ ] Every `layer: core` node has a `worldviewQuestion`.
- [ ] No node has `grip: struck`.
- [ ] `review.guessedGrip` equals the set of nodes with `gripGuessed: true`.
- [ ] Every anomaly is `status: open`.
- [ ] Every edge is traceable to a sentence in the Connections block.
- [ ] Node count equals the count of attribute-carrying beliefs in the file. If it doesn't, you
      either promoted an attached record or dropped a belief.

---

## The report

The graph is delivered with prose, and the prose is where the compile earns its keep. Four
things, every time:

**1. Grips defaulted.** How many, and — separately — how many of those the file's own
guessed-grip table gives a basis for. The uncovered ones are weaker than the ones the file
apologizes for, and nothing in the JSON makes that visible.

**2. Couplings that didn't draw.** Every connection whose other end is a domain rather than a
belief, and which case it is. Name the node that ends up isolated on screen when the text says
it is central. That contradiction is the most valuable output of the whole projection.

**3. Where the source fails its own checklist.** Declared structures with no section. Worldview
questions unanswered. A split or single-human anchor. Tripwire authorities nominated but never
asked.

**4. What the graph can't carry.** Agent implications attached to structures rather than
beliefs — Formation, Narrative, Plausibility — have nowhere to land, and one of them is usually
the most operative instruction in the file. Say which one was lost.

---

## Kickoff prompt

Paste this with `BELIEF.md`, `belief-graph.schema.json`, and this document attached:

> Read `Instructions for compiling a belief graph.md`, then compile `BELIEF.md` into a
> `belief-graph.json` and validate it against `belief-graph.schema.json`.
>
> Nodes are beliefs carrying `layer`/`grip`/`warrant`, statements and agent implications
> verbatim. Edges only where the Connections block states a coupling and both ends are belief
> titles — never from resemblance. All anomalies stay `open`. `gripGuessed` on every inferred
> grip, and every such id in `review.guessedGrip`.
>
> Then report: grips defaulted and how many the guessed-grip table actually covers, couplings
> that didn't resolve and why, where the file fails its own checklist, and what the projection
> had to drop.
