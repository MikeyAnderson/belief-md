# Belief.md Specification

> A standardized way to give AI agents a persistent philosophical and ethical operating context.

---

## Overview

`belief.md` is an open format for expressing a person's or organization's beliefs, values, and epistemological commitments so that AI agents can act as genuine extensions of their principal — not just task executors, but agents that reason and prioritize in alignment with a coherent worldview.

Where `SKILL.md` encodes *how to do things*, `belief.md` encodes *why things are done, what matters, and how to reason under uncertainty*. A skill is procedural knowledge; a belief file is philosophical context.

**The key distinction:**

| | `SKILL.md` | `belief.md` |
|---|---|---|
| Encodes | Capability | Character |
| Applies to | Specific tasks | All tasks |
| Contains | Instructions | Principles |
| Loaded | On-demand | Always |
| Scope | Narrow | Global |

---

## Directory Structure

A belief is a directory containing, at minimum, a `BELIEF.md` file:

```
belief-name/
├── BELIEF.md             # Required: metadata + principles
├── orientations/         # Optional: domain-specific guidance
├── references/           # Optional: supporting texts, thinkers, frameworks
└── ...                   # Any additional files or directories
```

Unlike skills, which are loaded on demand, `belief.md` files are loaded at session start and remain active throughout. They are the ambient context within which all skills operate.

---

## `BELIEF.md` Format

The `BELIEF.md` file must contain YAML frontmatter followed by Markdown content.

### Frontmatter

| Field | Required | Constraints |
|---|---|---|
| `name` | Yes | Max 64 characters. Lowercase letters, numbers, and hyphens only. Must not start or end with a hyphen. |
| `description` | Yes | Max 1024 characters. Describes whose beliefs these are, what domain they cover, and when they should govern agent behavior. |
| `version` | Recommended | Semantic version string (e.g. `"1.0"`, `"2.3.1"`). Beliefs evolve; versioning enables traceability. |
| `author` | Recommended | Name or identifier of the belief holder. |
| `scope` | No | Max 500 characters. Domains or task types where these beliefs apply. Omit to apply universally. |
| `conflict-resolution` | No | One of: `principles-over-rules` (default), `rules-over-principles`, `surface-and-pause`. Governs how to handle conflicts between beliefs and explicit instructions. |
| `license` | No | License name or reference to a bundled license file. |
| `metadata` | No | Arbitrary key-value mapping for additional metadata. |

**Minimal example:**

```markdown
---
name: principled-entrepreneurship
description: >
  The personal beliefs and epistemic commitments of [Author], grounded in
  market-based ethics and Popperian epistemology. Active in all contexts
  where this agent acts on my behalf.
version: "1.0"
author: your-name
---
```

**Full example:**

```markdown
---
name: principled-entrepreneurship
description: >
  Personal beliefs of [Author] covering ethics, epistemology, human nature,
  and value creation. Grounded in PBM (Principle-Based Management) philosophy.
  Governs all agent behavior across professional and analytical contexts.
version: "2.1"
author: your-name
scope: All professional, analytical, and creative tasks undertaken on my behalf.
conflict-resolution: principles-over-rules
license: Private
metadata:
  framework: PBM
  updated: "2026-05"
---
```

---

### Frontmatter Field Reference

#### `name` field

* Must be 1–64 characters
* May only contain lowercase alphanumeric characters (`a-z`, `0-9`) and hyphens (`-`)
* Must not start or end with a hyphen
* Must not contain consecutive hyphens (`--`)
* Must match the parent directory name

#### `description` field

* Must be 1–1024 characters
* Should describe: *whose* beliefs these are, *what philosophical territory* they cover, and *when* they should be active
* A good description helps agents understand when to surface beliefs during reasoning — not just to load them, but to weight them

#### `version` field

* Recommended for any belief file intended to persist across time
* Should follow semantic versioning: `MAJOR.MINOR` or `MAJOR.MINOR.PATCH`
* Increment `MAJOR` when a core principle changes
* Increment `MINOR` when a principle is added or refined
* Increment `PATCH` for clarifications and wording improvements

#### `conflict-resolution` field

Specifies how the agent should behave when an explicit instruction conflicts with a stated belief:

| Value | Behavior |
|---|---|
| `principles-over-rules` | Reason from the underlying principle; surface the conflict and explain the resolution. *(Default)* |
| `rules-over-principles` | Follow explicit instructions; note the tension if relevant but proceed. |
| `surface-and-pause` | Flag the conflict explicitly and wait for the principal's guidance before proceeding. |

---

### Body Content

The Markdown body contains the belief content itself. There are no mandatory sections, but the following structure is recommended for comprehensiveness and agent usability.

#### Recommended Sections

Each section should follow a consistent pattern: **statement of belief** followed by **agent-facing orientation** — the operational implication the agent should carry forward.

---

**1. Ethics**
Core moral commitments. What counts as right action, legitimate value creation, and acceptable conduct. The test the agent should apply when evaluating whether an action is appropriate.

**2. Epistemology**
How knowledge is acquired, tested, and updated. Beliefs about evidence, uncertainty, confirmation bias, and the value of challenge. This section directly shapes how the agent reasons — whether it seeks to confirm or to falsify, whether it treats dispersed knowledge as valid, whether it holds conclusions loosely.

**3. Ontology** *(optional)*
What the agent should assume about the nature of reality, systems, and causality. Useful for shaping how the agent frames problems — e.g., whether it defaults to bottom-up or top-down explanations, whether it treats entropy as a real force to be countered.

**4. Human Nature** *(optional)*
Assumptions about people's motivations, capacity for growth, and response to systems and incentives. Shapes how the agent interprets human behavior and designs recommendations involving people.

**5. Power & Justice** *(optional)*
Beliefs about legitimate authority, decision rights, subsidiarity, and structural fairness. Useful when the agent must evaluate governance decisions, organizational structures, or policies.

**6. Change & Progress** *(optional)*
Beliefs about how change happens, what drives progress, and the relationship between effort and transformation. Shapes the agent's orientation toward improvement and innovation.

**7. Relationships & Obligations** *(optional)*
Beliefs about the nature of legitimate relationships and mutual obligations — to collaborators, customers, communities, and society.

**8. Meaning & Purpose** *(optional)*
The deepest motivational context. What gives work meaning, what the point of contribution is, and what a life well-lived looks like.

---

#### Agent Orientations Block (Required)

Every `BELIEF.md` must include an explicit **Agent Orientations** section. This is the operational translation of beliefs into standing instructions the agent should carry in all contexts.

Format each orientation as: a named heuristic, followed by its application.

```markdown
## Agent Orientations

When acting on behalf of this principal, apply the following orientations in all contexts:

**Principles over rules.** When a rule and the underlying principle conflict, surface
the conflict and reason from the principle. Rules encode best practices, not moral absolutes.

**Challenge, don't confirm.** Actively look for what might be wrong in any plan or
argument — not just what is right. Seek disconfirming evidence before endorsing a conclusion.

**Mutual benefit standard.** For every recommended action, ask: does this create genuine
value for all parties, or does it extract from one to benefit another?

**[Add orientations here...]**
```

Agent orientations are the highest-priority section for agent consumption. They should be specific enough to produce different behavior than the agent's defaults.

---

## Progressive Disclosure

Unlike skills, belief files are loaded at session initialization, not on demand. However, the same principle of progressive disclosure applies to *depth*:

1. **Frontmatter** (~100 tokens): Loaded first. Establishes whose beliefs, what scope, and how to handle conflicts.
2. **Agent Orientations** (~200–500 tokens): The operational core. Should be concise enough to hold in active context throughout a session.
3. **Full belief body** (as needed): Loaded when the agent needs to reason deeply about a specific domain — e.g., when an ethical question arises, the Ethics section is consulted in full.
4. **References** (on demand): External texts, thinkers, and frameworks loaded only when explicitly relevant.

Keep `BELIEF.md` under 800 lines. Move supporting arguments and cited sources to `references/`.

---

## Optional Directories

### `orientations/`

Domain-specific belief orientations. Useful when beliefs have substantially different implications across contexts:

```
orientations/
├── hiring.md          # How beliefs apply to talent decisions
├── investment.md      # How beliefs apply to capital allocation
├── communication.md   # How beliefs shape messaging and framing
```

Each file should follow the same format as the Agent Orientations block: named heuristic + application.

### `references/`

Supporting intellectual material:

* `thinkers.md` — Key thinkers and their relevant ideas (Popper, Hayek, Frankl, etc.)
* `frameworks.md` — Named frameworks the beliefs draw on (PBM, Stoicism, etc.)
* Domain-specific files for deep context

### `changelog/`

A record of belief evolution over time. Recommended for any long-running use:

```
changelog/
├── CHANGELOG.md       # Human-readable record of what changed and why
```

---

## Relationship to `SKILL.md`

`belief.md` and `SKILL.md` are complementary, not competing:

* A skill tells an agent *how* to write a memo. A belief file tells it *what to stand for* in that memo.
* Skills are activated by task match. Beliefs are ambient throughout.
* Skills encode best practices. Beliefs encode non-negotiables.

When a skill's instructions conflict with a stated belief, the `conflict-resolution` field governs resolution. The default (`principles-over-rules`) means the agent should surface the tension and reason from the belief — not silently override the skill or silently suppress the belief.

---

## Validation Checklist

Before deploying a `belief.md` file, verify:

- [ ] Frontmatter contains `name` and `description` at minimum
- [ ] `name` matches the parent directory name
- [ ] An **Agent Orientations** section is present and non-empty
- [ ] Each orientation is specific enough to change agent behavior, not just restate a value
- [ ] `version` field is present if the file is intended to evolve
- [ ] `conflict-resolution` is explicitly set if the default (`principles-over-rules`) is not intended
- [ ] The file is under 800 lines; longer material is moved to `references/`
- [ ] The belief file has been read aloud or summarized — if it sounds generic, it needs more specificity

---

## Complete Example

```markdown
---
name: principled-entrepreneurship
description: >
  Personal beliefs of [Author] covering ethics, epistemology, human nature,
  and value creation. Grounded in PBM philosophy. Governs all professional
  and analytical tasks undertaken on my behalf.
version: "1.0"
author: your-name
scope: All professional, analytical, and creative work undertaken on my behalf.
conflict-resolution: principles-over-rules
metadata:
  framework: PBM
  updated: "2026-05"
---

## Ethics

I believe the only legitimate way to profit is to create genuine value for
others. Profit extracted through political favor, exploitation, or manipulation
— even when legal — is unethical. The test: does this create genuine mutual
benefit, or does it extract value from others to deliver it to me?

## Epistemology

I follow Popper's insight: the goal is to disprove a theory, not confirm it.
I believe knowledge is dispersed — no single person or hierarchy possesses
all the relevant knowledge needed to make optimal decisions.

## Agent Orientations

When acting on my behalf, apply the following in all contexts:

**Principles over rules.** When a rule and the underlying principle conflict,
surface the conflict and reason from the principle.

**Challenge, don't confirm.** Actively look for what might be wrong — not just
what is right. If my views are rarely challenged, treat that as a warning sign.

**Mutual benefit standard.** For every recommended action, ask: does this
create genuine value for all parties?

**Entropy is always operating.** When a process or assumption hasn't been
questioned recently, treat that as a signal to examine it — not evidence it's fine.

**Long-term focus.** When near-term and long-term considerations conflict,
surface both explicitly. Consistently prioritize long-term value creation.
```

---

## Open Standard

The `belief.md` format is proposed as an open standard, complementary to Agent Skills. Contributions and discussion are welcome.

The format is intentionally minimal in its requirements and flexible in its body structure — beliefs are personal, and no schema should constrain what a person considers important to express.

The one non-negotiable: every `belief.md` must contain an **Agent Orientations** section. Beliefs that cannot be translated into operational guidance are philosophical statements, not agent context.# belief
