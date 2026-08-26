# Compiling an Inventory

Instructions for an agent extracting an `INVENTORY.md` from a principal's corpus.

This is the first of two passes. The inventory **retains**; `BELIEF.md` **organizes**. Read
[`README.md`](./README.md) for the format the second pass targets, then come back — but do not
let it shape this one. Working belief-first at extraction time is what this pass exists to
prevent.

---

## The one rule that matters

**Retain, don't select.**

A belief file is a lossy projection of a person, necessarily and correctly. The inventory is
the thing that makes the loss visible, which it can only do if it is compiled before anyone
knows what the beliefs are going to be. The moment you start asking *is this a belief?* you
have begun condensing, and the material that goes first is always the same material: the
phrase they say it with, the story they always tell, the practice they never bothered to
justify. That is the material a person recognizes themselves in.

So: no length target, no candidate count, no merging of near-duplicates, no judgment about
whether something is important. Judgment happens in pass two, where it is recorded and can be
argued with. Here you are building the record that judgment gets exercised against.

The failure mode is an inventory that already looks like a belief file — thirty tidy
propositions, no idiom, no repetition. If your inventory could be pasted into `BELIEF.md` with
light editing, you compiled the wrong artifact.

---

## Output

One file, `INVENTORY.md`, in the belief directory. It is never loaded into agent context — not
at session start, not on demand — so it carries no size budget and needs no summarization.

---

## Record types

Eight. When something could be two types, file it twice rather than choosing.

| Type | What it captures | Example |
|---|---|---|
| `claim` | A proposition they assert. | "Every person is made in the image and likeness of the Creator." |
| `principle` | A rule they apply, stated as guidance. | "Make money a servant, not a master." |
| `practice` | Something they do repeatedly. Not an endorsement — a habit. | Still does customer interviews personally. |
| `framework` | A named multi-part model of theirs, with its parts. | Create / Support / Reward. |
| `phrase` | A coinage, an idiom, a formulation they repeat. | "Self-licking ice cream cone." |
| `story` | A concrete exemplar they use to carry a point. | Two employees nearly sank the company; he had them build the system that would prevent the next one. |
| `anti-pattern` | Something they name as wrong, and the name they give it. | "A values statement is not a culture." |
| `question` | Something they say they haven't settled. | Where enterprise stops being the answer. |

Four notes on the types that get under-collected:

**`phrase` is the one that decides whether the read-aloud test passes.** People are recognized
by their formulations before their propositions. Collect the phrase even when you have already
collected the claim it expresses — especially then. They are different records and the second
one is the one that sounds like them.

**`practice` is the strongest evidence in the corpus and the least often written down.** Look
in the places where the principal describes their week rather than their views: what they still
do themselves, what they refuse to delegate, what happens every morning. A practice that
contradicts a stated belief is not an error to reconcile — file both, and pass two will have a
`dissonance` record to build on.

**`question` records make anomalies citable.** An anomaly the principal raised in their own
words is worth two the compiler noticed. Any sentence of the form *I don't have a complete
account of…* or *I've never resolved…* is a record.

**`framework` keeps its parts.** Record the parts as part of the record. A framework whose
parts have been dissolved into a summary sentence cannot be recognized, cited, or coupled to
anything later.

---

## Record format

```markdown
### i-014 · phrase
> "How may I help you?"
`evidence: repeated-practice` · `where: Ciocca Center podcast ep. 41, 08:12`
The question he says he opens every customer conversation with. Recurs in at least four
places in the corpus.
```

| Field | Required | Notes |
|---|---|---|
| id | Yes | `i-` plus a sequential number. **Never renumber.** Beliefs cite these, and a renumber silently breaks every citation. Retired records keep their id and are marked `superseded`. |
| type | Yes | One of the eight. |
| text | Yes | **Verbatim, in a blockquote.** Their words, their punctuation, their emphasis. Trim to the sentence, don't rewrite it. |
| `evidence` | Where determinable | The ladder from `Instructions for compiling belief structure.md`: `cost-bearing-decision` · `repeated-practice` · `defended-under-disagreement` · `published-repeatedly` · `said-once`. A label, never a filter — nothing is dropped for scoring low. |
| `where` | Yes | Locator precise enough to return to: work, chapter, timestamp, page. "Somewhere in the book" is not a locator. |
| context | Optional | One line: what they were doing when they said it, what it was in answer to, how often it recurs. |
| `received-from` | Optional | Where they credit someone else for the formulation. |
| `parts` | `framework` only | The named components, each with its one-line gloss. |
| `see-also` | Optional | Other record ids. Cheap, and useful to the clustering pass. |

Group records by type under `##` headings, ids ascending within each. That ordering is for the
compiler; nobody reads this file end to end.

---

## Order of work

**1. Pass through the corpus once without extracting.** Note where the person argues, decides,
or explains themselves under pressure — those passages are worth more per line than the
passages where they describe their positions.

**2. Extract linearly.** Work through the corpus in order and file records as you meet them.
Do not deduplicate, do not group, do not skip something because it resembles a record you
already have. Repetition across the corpus is signal you are collecting, not noise you are
filtering: a phrase appearing six times in four venues is the single most useful thing the
inventory can tell pass two.

**3. Take the whole sentence.** The instinct to trim to the proposition is the instinct that
loses the voice. If the sentence carries a hedge, a joke, or a piece of throat-clearing, keep
it — pass two can drop it and cite the record, but only if the record still has it.

**4. File the near-duplicates separately.** Two statements of the same idea at different
abstraction levels are two records. In pass two they usually become a belief and its
`Says it as`, which cannot happen if you merged them here.

**5. Mark what you are unsure about, don't resolve it.** `note: might be quoting someone else`
is a good record. Ambiguity resolved silently at extraction is invisible for the rest of the
project's life.

**6. Report.** Counts by type; what the corpus is thin on; anything you were unsure was one
record or two; anything you found in secondhand sources rather than the principal's own words.

---

## Prohibitions

1. **Don't paraphrase.** If you cannot get the verbatim text, record what you have and mark it
   `paraphrase: true`. A marked paraphrase is usable; an unmarked one is contamination that
   nobody can find later.
2. **Don't infer from category membership.** Nothing enters the inventory because the principal
   belongs to a tradition, profession, or demographic that typically believes it. This is the
   fastest route to a file they won't recognize, and at extraction time it is undetectable
   downstream.
3. **Don't assign `layer`, `grip`, or `warrant`.** Not even provisionally, not even in a
   comment. Attributes at this stage change what you collect.
4. **Don't drop for redundancy, thinness, or unimportance.** Those are pass-two judgments and
   pass two has a place to record them.
5. **Don't include secondhand attributions unmarked.** What a colleague says the principal
   believes is a record about the colleague. File it with `secondhand: [source]` or leave it
   out.

---

## Before you deliver

- [ ] Every record has an id, a type, verbatim text, and a locator.
- [ ] No record carries `layer`, `grip`, or `warrant`.
- [ ] Paraphrases and secondhand material are marked as such.
- [ ] Near-duplicates are separate records, not merged.
- [ ] `framework` records list their parts.
- [ ] `phrase` records exist. If there are none, you extracted propositions and skipped the
      voice — go back.
- [ ] `practice` and `question` records exist, or the report says why the corpus has none.
- [ ] The count is larger than a belief file's worth. An inventory the size of the file it
      feeds has done no retaining.

---

## Maintenance

The inventory is append-only in practice. New corpus material adds records with new ids.
Corrections from the principal add a record and mark the old one `superseded: i-###` rather
than editing it in place — what they corrected, and what they corrected it *from*, are both
worth having when the file is next recompiled.

When a belief file is recompiled at a different grain, it is recompiled **from the inventory,
not from the corpus.** That is the point of keeping one: the expensive, lossy read of the
source happens once.

---

## Kickoff prompt

Paste this with the corpus attached:

> Read `README.md` and `Instructions for compiling an inventory.md` in this repo, then compile
> `INVENTORY.md` from the attached corpus.
>
> Retain, don't select. One record per thing the principal said — claims, principles,
> practices, named frameworks, phrases, exemplars, anti-patterns, open questions — verbatim, in
> a blockquote, with a locator. Keep near-duplicates separate. Keep frameworks' parts named.
> No `layer`, no `grip`, no `warrant`, no length target.
>
> Then report: counts by type, what the corpus is thin on, anything you weren't sure was one
> record or two, and anything you had to paraphrase.
