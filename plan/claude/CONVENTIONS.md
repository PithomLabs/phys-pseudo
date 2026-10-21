# Phys Pseudo — Conventions (compatibility note)

**This page is not a specification.** The language is defined only in
[`PSEUDO.md`](PSEUDO.md). Reviews follow
[`MRC_REVIEW_PROTOCOL.md`](MRC_REVIEW_PROTOCOL.md). Implementation-ready derivations
are governed by `DERIVATION_SPEC_GUIDELINES.md`. If this page and `PSEUDO.md` ever
disagree, `PSEUDO.md` wins.

The provisional Stage 1 conventions that used to live here are superseded. Their
three invariants survive as follows:

- **I1 (the advisory guide is advisory):** unchanged in effect. `reality_check.md` may
  motivate a finding or a `?`; it never auto-rejects anything
  (`MRC_REVIEW_PROTOCOL.md`).
- **I2 (facts, not verdicts) and I3 (no author-typed status):** folded into the
  single invariant in `PSEUDO.md` §1: representation is not endorsement, and the
  language has no status construct.

## Reading older documents and fixtures

Stage 1/2 documents predate `PSEUDO.md`. Read them as follows; edit a fixture only
when a concrete contradiction needs removing, and say why.

| Older form | Canonical reading |
|---|---|
| `given NAME = …` | `given NAME: …` |
| `given … from cited @x`, `from paper …`, `from measured …` | `given NAME: …` plus a note naming the source (`PSEUDO.md` §7). No `from` provenance clause. |
| `assume … as LABEL` | `assume LABEL: …` |
| `derive LABEL from […] \| chain` with no stated result | state the result: `derive LABEL: <result> from […] \| …` |
| Premises that are not names (`product rule`, `[assume]`) | invoke standard mathematics in the reasoning; name every problem-specific premise |
| Parameterised labels such as `expand(f)` | plain names (`expand`); put "for every f" in the statement |
| `? [W is false …]` | a `derive` that refutes W (`PSEUDO.md` §9); `?` is only for unresolved items |
| A `?` that follows an `if` block and is meant for the whole document | column-0 `?` (document-level), or an indented `?` under the intended statement |

## Superseded Stage 1 material

- The seven-construct table and usage notes: see `PSEUDO.md` §4.
- The §4 worked examples: replaced by `PSEUDO.md` §9. The old §4.1 placed a verdict
  (`W is false`) inside `?` and used non-name premises, so do not copy it.
- The "tooling assertion ceiling": reduced to one sentence in `PSEUDO.md` §8. No
  checker exists or is planned in this milestone.
