# Generating a First Belief File

Instructions for an agent compiling a `BELIEF.md` from a principal's corpus.

Read [`README.md`](./README.md) first — it defines the format. This file tells you how to
produce one. They answer different questions: the README says what a valid file looks like,
this says how to get there without producing a well-formed file that isn't the person.

The first version's job is **to be argued with.** Not to be complete, not to be safe, not
to be installed. A draft with six wrong lines that the principal can correct in an hour is
worth more than a hedged document nobody can read.

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

---

## Order of work

Do these in order. The order matters more than anything else in this file, because working
schema-first produces a file organized around the format instead of around the person.

### 1. Collect claims, in their words

Go through the corpus and pull out sentences where the principal states something they
believe. Keep their phrasing. Note where each one came from.

You want 30–60 candidates. Most will be duplicates of each other at different levels of
abstraction — that's useful, because the abstraction levels become your layers.

### 2. Rank by evidence quality

Not all statements are convictions. In descending reliability:

1. **What they decided when it cost them something.** A refused deal, a role handed off, a
   plan reversed. This is the strongest evidence there is.
2. **What they do repeatedly.** Practices, not preferences.
3. **What they say when someone disagrees.** Argument reveals what's load-bearing.
4. **What they've published more than once.** Repetition across years and venues.
5. **What they said once, warmly, in an interview.**

The last one is where reconstructions go wrong. A sentence someone liked out loud is not a
conviction. If a claim rests only on (5), either drop it or write it and mark it as thin.

### 3. Draft beliefs as plain prose — no attributes yet

Write each belief as a title plus two or three sentences in the principal's voice. Nothing
else. No `layer`, no `grip`, no YAML.

Do this for the whole file before you add a single attribute. If you add attributes as you
go, you will start writing beliefs that fit the schema neatly rather than beliefs the
person holds.

Use their concrete anchors. If they explain a principle with a particular story, keep the
story — a belief attached to a person doing something under pressure survives compression,
and an abstraction doesn't.

### 4. Sort into structures

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

**Find the anomalies.** Every web has questions it doesn't settle. Look for places where
two of the principal's commitments pull against each other and the corpus never resolves
it. Name three to six. This is a strength signal, and an agent that fills them in from the
nearest doctrine is performing exactly the drift the format exists to catch.

### 5. Add attributes — layer, then warrant, then grip

That's the order from mechanical to impossible.

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

### 6. Write the orientations

Ten or fewer. Each one cites its source structure. Each one must produce behavior that
differs from your defaults — if an orientation describes what you'd do anyway, delete it.

Write them as though they will be followed. Do not mark them provisional; the file's
unratified status lives in the frontmatter, once. An orientation set that's entirely
disclaimed changes nothing and makes the file a document about itself.

Test each one: *could a reader tell whether I complied?* "Be thoughtful about people" fails.
"Name the affected person and show one thing that changed after talking to them" passes.

---

## Four prohibitions

1. **Don't infer `grip` silently.** Mark it. List it. Ask about it.
2. **Don't resolve anomalies.** Name them and stop.
3. **Don't promote content to schema.** The principal's own frameworks — their pillars,
   their mentor's model, their favorite three-part test — are beliefs. They go in `web`.
   Custom `x-` types are for structural information the registry can't express, not for
   content you want to emphasize. Content promoted to schema is how a 300-line file becomes
   a 700-line one.
4. **Don't build a provenance apparatus.** You will feel the risk of misattributing
   something to a living person, and that risk is real. It is fully handled by
   `provenance: reconstructed` in the frontmatter, a per-belief `source:` where a belief was
   inherited from a named teacher, and one honest paragraph at the top. Status ledgers,
   approval matrices, and per-sentence disclaimers produce a document nobody can read —
   which serves the principal worse than a clearly-marked draft with a few wrong lines.

---

## Length

| Section | Budget |
|---|---|
| Frontmatter | ~15 lines |
| Orientations | 10 or fewer, 3 lines each |
| Worldview | 3–5 beliefs |
| Web | 10–20 beliefs |
| Everything else | as much as you have real material for |
| **Total, first version** | **~300 lines** |

The 800-line cap in the README is a ceiling, not a target. If the file's apparatus outweighs
its beliefs, you've built the wrong thing.

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

---

## The handoff

A reconstructed file is a draft for a conversation. Structure that conversation.

Read each passage aloud and take one disposition:

**recognizable** · **wrong** · **missing** · **too strong** · **not mine**

*Too strong* and *not mine* are the ones you're fishing for. *Too strong* usually means grip
was overstated. *Not mine* usually means a public statement got mistaken for a conviction,
or an inheritance got presented as an invention.

Work in this order, because attention runs out: worldview first, then the anomalies, then
the dissonances, then anything with a guessed `grip`, then the orientations. Third-layer
positions last — they're the least consequential and the most fun to argue about, which is
a trap.

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

Two or three sentences in their voice. Keep the story if there is one.

**Agent implication.** One thing to do differently, stated so compliance is checkable.

## Web

**Anchor.** What the whole thing hangs from.

**Connections.** Which second-layer positions are tightly coupled to which core
commitments — and which aren't.

**Anomalies.** Three to six questions this web does not settle. Do not resolve them.

### [A derived position]
`layer: second` · `grip: cradled` · `warrant: experiential`
`source: received — [name]`   ← only when inherited

Their words.

**Agent implication.** Observable behavior.

## Agent Orientations

**[Imperative].** `← worldview: [belief title]`
What to do that differs from the default.

**Surface, don't patch.** `← on-anomaly: surface`
On [the named anomalies], say the web doesn't settle it. Answer provisionally and mark it.
```

---

## Kickoff prompt

Paste this, with the corpus attached:

> Read `README.md` and `GENERATING.md` in this repo, then compile a first-version
> `BELIEF.md` for the attached principal.
>
> Work in the order `GENERATING.md` specifies: pull claims in their words, rank by evidence
> quality, draft every belief as plain prose before adding any attributes, then sort into
> structures, then add layer → warrant → grip.
>
> Set `provenance: reconstructed`. Guess `grip` and collect every guess in one list at the
> top. Name the anomalies and leave them open. Keep their frameworks in `web` — do not
> create custom `x-` types for them. Target about 300 lines.
>
> Then tell me: the guessed grip values, the anomalies you left open, and the three lines
> you're least confident are actually theirs.

That last question is the useful one. It's where the errors are.
