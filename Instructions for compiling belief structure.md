# Generating a First Belief File

Instructions for an agent compiling a `BELIEF.md` from a principal's corpus.

Read [`README.md`](./README.md) first — it defines the format. This file tells you how to
produce one. They answer different questions: the README says what a valid file looks like,
this says how to get there without producing a well-formed file that isn't the person.

**Compile the inventory first.** As of 2.1 this is a two-artifact process: see
[`Instructions for compiling an inventory.md`](./Instructions%20for%20compiling%20an%20inventory.md).
`INVENTORY.md` retains the corpus verbatim; `BELIEF.md` organizes it. Everything below assumes
you have an inventory in hand and are working from it rather than from the raw corpus. If you
compile straight from the corpus you will condense while you extract, and you will not be able
to say afterward what you dropped.

The first version's job is **to be argued with.** Not to be complete, not to be safe, not
to be installed. A draft with six wrong lines that the principal can correct in an hour is
worth more than a hedged document nobody can read.

Two ways to fail, and they pull in opposite directions:

- **Invention** — asserting something the principal never said, or holding a belief more
  tightly on the page than they hold it in life. Guarded by `provenance`, guessed-`grip`
  lists, thin-evidence marks, and the prohibition on resolving anomalies.
- **Loss** — a file that is true, well-organized, and contains none of the phrases the person
  is actually known for. Guarded by the inventory, `covers:`, attached records, and the
  unpromoted list.

Earlier versions of these instructions guarded hard against the first and not at all against
the second, which is why generated files came back smooth, short, and slightly generic. Do not
fix that by loosening the anti-invention rules. Keep them and carry the material.

---

## What you need before you start

**Required:** enough of the principal's own material to hear them think — books, talks,
essays, interviews, transcripts, correspondence. Aim for material where they argue, decide,
or explain themselves under pressure, not just material where they describe their positions.

**Note whether the principal is available.** It changes what you produce:

| Access | Set | Then |
|---|---|---|
| Working with them live | `provenance: authored` | Ask `grip` directly. Don't guess it. |
| Corpus only, review to come | `provenance: reconstructed` | Guess `grip`, mark every guess, list them for the review. |
| Corpus only, no review planned | Stop | Don't generate an unratified file that will get installed. Say so. |

If you have less than roughly a book's worth of first-person material, say what's thin
rather than filling the gap with the tradition, profession, or demographic the principal
belongs to. Inferring beliefs from category membership is the single fastest way to produce
something they won't recognize.

The inventory is where thinness becomes measurable rather than impressionistic: a corpus that
yields forty `claim` records and two `practice` records is telling you the person has been
recorded explaining themselves and not recorded acting, and the belief file should say so
instead of inventing the practices that would balance it.

---

## Order of work

Do these in order. The order matters more than anything else in this file, because working
schema-first produces a file organized around the format instead of around the person.

### 1. Read the inventory whole before you group anything

Every record, in one pass, without sorting. You are looking for what recurs and what the
person keeps reaching for — which is visible across the inventory and invisible record by
record.

Do not re-extract from the corpus at this stage. If something is missing, add it to the
inventory as a new record with a locator, then come back. The inventory stays the single
source of retained material; a belief that cites nothing is a belief you invented.

### 2. Cluster the records

Group inventory records by what they are *about*. Not by structure type, not by layer — by
subject. A cluster typically comes out as one `claim` or two, plus the `phrase` the principal
says it with, plus a `practice` or two, plus the `story` they always tell about it. That shape
is the tell that you have found a real belief rather than a topic.

Three things to watch:

- **Clusters of one are fine.** A single vivid claim with nothing attached is still a belief;
  it is just one you know less about. Do not merge it into a neighbor to make the file tidier.
- **A record can sit in two clusters.** Cite it in both. Records are cheap; the inventory is
  not a partition.
- **Leftovers are data.** Records that join no cluster go on the unpromoted list with a
  one-line reason. Do not force them into the nearest belief, and do not delete them. Step 7.

**Do not condense to hit a size.** There is no target count. A book-sized corpus usually
clusters into somewhere between twenty and forty beliefs, and if it comes out at fifty, the
file has fifty beliefs. See *Length* below for what to do about the loaded file.

### 3. Name each cluster as a belief, and attach its material

Write the belief as a title plus two or three sentences in the principal's voice. Then attach
the rest of the cluster rather than absorbing it into the prose:

```markdown
### [The belief, as they would say it]
`covers: i-014, i-022, i-031`

Two or three sentences in their voice.

**Says it as.** The formulation they actually use. `i-014`
**Practice.** What they do, not what they endorse. `i-031`
**Exemplar.** The story they tell to carry it. `i-022`
```

No `layer`, no `grip`, no YAML yet. Attributes come at step 5, and adding them here makes you
write beliefs that fit the schema neatly instead of beliefs the person holds.

**The attached records are the point of this step.** The instinct to compress *"Says it as"*
into the belief prose and drop the id is the exact instinct that produced the summary-shaped
files this process exists to stop. Their phrasing survives compression. Your paraphrase of
their phrasing does not.

Where the principal has a named framework of their own — their pillars, their mentor's
three-part model — the framework is one belief and its parts stay named:

```markdown
**Parts.** *Create* — real work that demands judgment. *Support* — attention, tools,
coaching, room. *Reward* — share the fruits fairly and durably.
```

### 4. Rank by evidence quality

Now, not earlier. In descending reliability:

1. **What they decided when it cost them something.** A refused deal, a role handed off, a
   plan reversed. This is the strongest evidence there is.
2. **What they do repeatedly.** Practices, not preferences.
3. **What they say when someone disagrees.** Argument reveals what's load-bearing.
4. **What they've published more than once.** Repetition across years and venues.
5. **What they said once, warmly, in an interview.**

The ladder ranks; it does not filter. A belief resting only on (5) is written and marked
`thin` — it is not dropped, because tier 5 is where a person's idiom lives and the warm remark
in an interview is frequently the sentence they are known for. What tier 5 does *not* license
is `clenched`, or a place at `core`.

This ordering matters: ranking before clustering makes you cull candidates before you can see
what they belong to, and the material that goes first is phrasing.

### 5. Sort into structures

Now place them. Consult the README registry. Practical guidance:

- **`worldview`** — only answers to the five questions. If it isn't an answer to one of the
  five, it goes in `web`. Most principals answer three or four of the five in public
  material; leave the others out rather than reasoning them in from the ones you have.
- **`web`** — everything else, plus the anchor and the anomalies. This will be the biggest
  section and that's correct.
- **`decision-surface`** — write last. It's the rendered output of everything above.
- Optional types: add one only when you have real material for it. An empty `narrative`
  section is worse than no `narrative` section, because `structures:` in the frontmatter is
  how a reader learns what's genuinely absent.

**Find the anchor.** What does the whole web hang from? If it hangs from a single human
authority or a single institution, say so — that's a documented failure mode and naming it
is part of the job.

**Write the connections belief-to-belief.** Every term you name in a connection must be the
title of a belief in this file or an attached record under one. This is the rule that gets
broken most often and costs the most, because breaking it is invisible: a connection written
in the principal's domain vocabulary — *"tightly coupled to hiring, development, and
compensation"* — reads as informative and compiles to nothing, since none of those three is a
belief. Before you write a coupling, check that both ends exist. When one doesn't, you have
found either a missing belief or a coupling that is looser than it sounded. Say which, in the
file.

Loose couplings are couplings. *"Only loosely coupled to product decisions"* is a stated
connection with a stated strength, not an absence — write it.

**Find the anomalies.** Every web has questions it doesn't settle. Prefer the ones the
principal raised themselves: those are `question` records in the inventory, already in their
words, and an anomaly you can cite is worth two you noticed. Beyond those, look for places
where two of their commitments pull against each other and the corpus never resolves it — and
name which two, by belief title, so the tension is checkable. Name three to six. This is a
strength signal, and an agent that fills them in from the nearest doctrine is performing
exactly the drift the format exists to catch.

### 6. Add attributes — layer, then warrant, then grip

That's the order from mechanical to impossible. **Beliefs only.** Attached records take no
attributes; they are governed by the belief they hang from, which is what makes them cheap
enough to keep.

**`layer`** is mechanical:
- Answers one of the five worldview questions → `core`
- A derived domain (work, money, authority, family, politics) → `second`
- An applied position or preference → `third`

**`warrant`** is usually inferable from *how they argue for it.* Do they cite scripture or
authority (`revealed`), reason from premises (`reasoned`), point to what happened to them
(`experiential`), appeal to inheritance (`traditional`), or locate it in a community
(`communal`)?

**`grip`** is not inferable, and pretending otherwise is the most common defect in a
generated file. Guess it, then mark the guess. Default to `cradled` where you have nothing.
Reserve `clenched` for beliefs the principal has defended at cost — not beliefs they repeat
often. Frequency is not conviction; a person can say something a hundred times and still be
genuinely open about it.

`struck` is never a value you assign. It's an anti-pattern.

Then put every guess in one list at the top of the file. Grip is where a generated file and
a self-described file diverge most, which makes it the highest-value thing you can spend
the principal's review time on.

### 7. Write the orientations

Ten or fewer. Each one cites its source structure. Each one must produce behavior that
differs from your defaults — if an orientation describes what you'd do anyway, delete it.

Write them as though they will be followed. Do not mark them provisional; the file's
unratified status lives in the frontmatter, once. An orientation set that's entirely
disclaimed changes nothing and makes the file a document about itself.

Test each one: *could a reader tell whether I complied?* "Be thoughtful about people" fails.
"Name the affected person and show one thing that changed after talking to them" passes.

### 8. Write the coverage report

Not in `BELIEF.md` — it goes in your reply and, if the project keeps one, at the foot of
`INVENTORY.md`. Four lists:

1. **Counts.** Records in the inventory, records covered by a belief, beliefs written.
2. **Unpromoted.** Every record no belief covers, with a one-line reason. *Duplicate of i-014.
   Too thin to stand alone. Topical, not a belief. Couldn't place it.* "Couldn't place it" is a
   perfectly good reason and the most useful entry on the list.
3. **Orphans.** Practices and phrases attached to a belief that does not really account for
   them, and beliefs citing no records at all. The first says a belief is missing; the second
   says a belief is yours rather than theirs.
4. **Unresolved couplings.** Any term you wanted to name in a connection that resolved to
   nothing.

This report is what the principal argues with second, right after `grip`. Producing a belief
file without one means nobody can tell what the compilation cost.

---

## Five prohibitions

1. **Don't infer `grip` silently.** Mark it. List it. Ask about it.
2. **Don't resolve anomalies.** Name them and stop.
3. **Don't promote content to schema — but don't flatten it either.** The principal's own
   frameworks are beliefs and go in `web`; custom `x-` types are for structural information
   the registry can't express, not for content you want to emphasize. That still holds. What
   does *not* follow, and what earlier versions of this file wrongly implied, is that a
   five-part framework should come out as one undifferentiated sentence. Keep the parts named
   under the belief. The vocabulary a person thinks in is not decoration, and a framework
   whose parts have been dissolved can no longer be cited, coupled, or recognized.
4. **Don't drop anything silently.** Material you chose not to promote goes on the unpromoted
   list. Not into the nearest belief's prose, not into a footnote, and not out of existence.
   A compiler that quietly discards is doing the same thing as a compiler that quietly
   invents, and it is harder to catch because the evidence is what's missing.
5. **Don't build a provenance apparatus.** You will feel the risk of misattributing
   something to a living person, and that risk is real. It is fully handled by
   `provenance: reconstructed` in the frontmatter, a per-belief `source:` where a belief was
   inherited from a named teacher, and one honest paragraph at the top. Status ledgers,
   approval matrices, and per-sentence disclaimers produce a document nobody can read —
   which serves the principal worse than a clearly-marked draft with a few wrong lines.
   `covers:` ids are not a provenance apparatus: they are one token per record, they carry no
   claim about ratification, and they are what makes the unpromoted list computable.

---

## Length

**There is no belief budget.** The file has as many beliefs as the inventory clusters into.
Earlier versions specified 3–5 worldview beliefs, 10–20 web beliefs, and about 300 lines
total, against 30–60 collected candidates — which mandated a cull of more than half before
anyone had seen the material, and the cull landed on whatever didn't fit a belief-shaped slot.
That is where the phrasing went. The budgets are withdrawn.

Two limits remain, and they are limits on different things:

| Limit | Applies to | Why |
|---|---|---|
| 800 lines | `BELIEF.md`, the file loaded into every session | Context economy. Real, and worth respecting. |
| None | `INVENTORY.md`, `structures/`, `references/` | Never loaded at session start. Nothing is saved by shrinking them. |

When `BELIEF.md` runs long, **move, don't cull.** Structures go to `structures/`, supporting
argument to `references/`. Material moved is one fetch away; material culled is gone, and the
context saving is identical.

Two things worth keeping short for their own sake, not for the budget: orientations, ten or
fewer, because an agent cannot hold thirty priorities; and apparatus. If the file's apparatus
outweighs its beliefs, you've built the wrong thing.

---

## Before you deliver

- [ ] Read the whole file aloud. Does it sound like one person talking, or like a
      well-organized summary of someone's public output? The second is the standard failure.
- [ ] Every orientation cites a structure and would produce non-default behavior.
- [ ] Every `core` belief answers one of the five worldview questions.
- [ ] `structures:` lists exactly what's present.
- [ ] Anomalies are named, not answered.
- [ ] Tripwires, if present, name an authority other than the principal.
- [ ] Guessed `grip` values are collected in one list.
- [ ] No YAML sits between sentences of prose. Machine metadata goes at the end of a record
      or in the frontmatter, so the read-aloud test is actually runnable.
- [ ] `provenance` is set honestly.

Recall:

- [ ] Every belief cites at least one inventory record.
- [ ] Every inventory record is covered or on the unpromoted list with a reason.
- [ ] Every term named in a connection resolves to a belief or an attached record.
- [ ] The phrases the principal is known for appear verbatim, not paraphrased.
- [ ] Named frameworks still have their parts.
- [ ] Read the unpromoted list. If nothing on it makes you want to argue, you culled by
      shape rather than by judgment.

---

## The handoff

A reconstructed file is a draft for a conversation. Structure that conversation.

Read each passage aloud and take one disposition:

**recognizable** · **wrong** · **missing** · **too strong** · **not mine**

*Too strong*, *not mine* and *missing* are the ones you're fishing for. *Too strong* usually
means grip was overstated. *Not mine* usually means a public statement got mistaken for a
conviction, or an inheritance got presented as an invention. *Missing* is the one the read-
aloud test cannot produce on its own, because a person hearing a coherent document rarely
notices an absence — which is why you read them the unpromoted list rather than waiting for it
to occur to them.

Work in this order, because attention runs out: worldview first, then the anomalies, then
anything with a guessed `grip`, then the unpromoted list, then the dissonances, then the
orientations. Third-layer positions last — they're the least consequential and the most fun to
argue about, which is a trap.

**On the unpromoted list, don't read all of it.** For a large inventory this is the item most
likely to eat the hour, and the return falls off fast. Read the entries you marked *couldn't
place it*, then any phrase that recurred three or more times and still didn't make the file.
Twenty entries is plenty. The rest keeps, and the list is there for the next pass.

When they correct a line, write what they said, not a tidied version of it.

---

## Skeleton

A complete, valid, useful file. Start here and grow only where you have material.

```markdown
---
name: principal-name
description: >
  Whose beliefs, what domain, and when they govern.
version: "0.1.0-draft"
author: principal-name
provenance: reconstructed
structures: [worldview, web, decision-surface]
conflict-resolution: named-judgment-owner
on-anomaly: surface
layer-policy: strict
---

> Draft reconstructed from published work. Nothing here is confirmed by the principal.
> `grip` values are guesses — those are the thing to argue about first.

## Worldview

### [One sentence they would actually say]
`layer: core` · `grip: cradled` · `warrant: reasoned`
`covers: i-003, i-011`

Two or three sentences in their voice.

**Says it as.** [Their formulation, verbatim] `i-003`
**Exemplar.** [The story they tell to carry it] `i-011`

**Agent implication.** One thing to do differently, stated so compliance is checkable.

## Web

**Anchor.** What the whole thing hangs from.

**Connections.** Which beliefs are tightly coupled to which — by title, both ends
resolving to something in this file — and which are explicitly loose.

**Anomalies.** Three to six questions this web does not settle, naming the two
commitments in tension where there are two. Do not resolve them.

### [A derived position]
`layer: second` · `grip: cradled` · `warrant: experiential`
`source: received — [name]`   ← only when inherited
`covers: i-024, i-037`

Their words.

**Practice.** [What they do, not what they endorse] `i-037`

**Agent implication.** Observable behavior.

## Agent Orientations

**[Imperative].** `← worldview: [belief title]`
What to do that differs from the default.

**Surface, don't patch.** `← on-anomaly: surface`
On [the named anomalies], say the web doesn't settle it. Answer provisionally and mark it.
```

---

## Kickoff prompt

Two prompts, because it is two passes. Paste the first with the corpus attached.

**Pass one — the inventory:**

> Read `README.md` and `Instructions for compiling an inventory.md` in this repo, then compile
> `INVENTORY.md` from the attached corpus.
>
> Retain, don't select. One record per thing the principal said — claims, principles,
> practices, named frameworks, phrases, exemplars, anti-patterns, open questions — verbatim,
> with a locator. No `layer`, no `grip`, no `warrant`, no length target, no merging of
> near-duplicates.
>
> Then tell me the record count by type, what the corpus is thin on, and any place you weren't
> sure whether something was one record or two.

**Pass two — the belief file:**

> Read `Instructions for compiling belief structure.md`, then compile a first-version
> `BELIEF.md` from `INVENTORY.md`.
>
> Work in the order the file specifies: read the inventory whole, cluster by subject, name each
> cluster as a belief and attach its phrasing, practices and exemplars with their ids, then
> rank by evidence, then sort into structures, then add layer → warrant → grip.
>
> Set `provenance: reconstructed`. Guess `grip` and collect every guess in one list at the top.
> Name the anomalies and leave them open — prefer the questions the principal raised
> themselves. Keep their frameworks in `web` with their parts named. Write connections
> belief-to-belief, both ends resolving. No length target; move to `structures/` if it runs
> long.
>
> Then give me the coverage report: counts, the unpromoted records with reasons, the orphans,
> the unresolved couplings, and the three lines you're least confident are actually theirs.

That last question is still the useful one. It's where the errors are. The unpromoted list is
where the omissions are, and those are the ones the principal can't find on their own.
