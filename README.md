# Phys Pseudo

A minimal pseudocode language for making physics reasoning inspectable.

Humans and AI agents use it to communicate hypotheses, derivations, and
paper reasoning while keeping assumptions and unresolved gaps visible on
the page — so speculation is never mistaken for established fact.

## What it's for

- **Hypothesis exploration** — write down a conjecture, its premises, and
  what would have to hold, then examine the consequences adversarially.
- **Inspecting derivations** — a readable counterpart to the essential
  reasoning behind Phys Go derivations, for human review before
  implementation.
- **Paper overviews** — a compact map of a paper's assumptions, reasoning,
  and open questions, in a form that separates what the source shows from
  what remains missing.

## Illustrative example

```text
given x_positive: x is a positive real number
define y := x + 1
derive y_positive: y > 0 from [x_positive, y] | adding one to a positive real gives a positive real
? whether this premise describes a particular physical system is not established; that requires separate justification or evidence
```

The derivation follows mathematically from its premise — but writing it
down does not establish that the premise describes any physical system.

## The limitation worth knowing

Writing an equation or derivation in Phys Pseudo does **not** prove it
correct or establish that a model describes Nature. The language records
reasoning; it carries no verdicts. (Formally: representation is not
endorsement — `PSEUDO.md` §7.)

## Getting started

- [`PSEUDO.md`](PSEUDO.md) — the canonical language specification.
- [`MRC_REVIEW_PROTOCOL.md`](MRC_REVIEW_PROTOCOL.md) — how reasoning
  written in it is adversarially reviewed.
- [`conformance/README.md`](conformance/README.md) — example fixtures,
  including deliberately flawed ones, and how to read them.

**Implementation handoffs:** derivations intended for implementation must
additionally follow
[`conformance/DERIVATION_SPEC_GUIDELINES.md`](conformance/DERIVATION_SPEC_GUIDELINES.md).

Working in this repository as an agent? See [`AGENTS.md`](AGENTS.md).


## License

MIT