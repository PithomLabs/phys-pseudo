# phys-pseudo — Language Specification

**Status:** canonical, v0.1. This is the only normative statement of the language.
`CONVENTIONS.md` is a compatibility pointer. `MRC_REVIEW_PROTOCOL.md` says how to
review documents written in this language.

## 1. Purpose and the one invariant

phys-pseudo is a notation for writing physics reasoning down so it can be inspected:
a hypothesis being explored, a derivation being examined, or a paper being summarised.
It has seven constructs and no others.

> **Representing a proposition or reasoning step does not endorse its truth,
> validity, physical applicability, or empirical correctness.**

Consequences:

- A false hypothesis, an incomplete derivation, or an unfamiliar mathematical
  construction can be written down. Nothing is rejected for being unproven.
- There is no construct for marking anything proven, verified, supported, or
  confirmed. Such words inside a statement are ordinary prose with no standing; a
  reviewer treats them as claims that need support.
- A document that follows this specification has been *written clearly*. Nothing
  more follows from that.

## 2. Document form

- Plain text. A statement starts with one of the keywords `given`, `define`,
  `assume`, `claim`, `derive`, `if`, `then`, `else`, or `?`. A line starting with
  none of these continues the statement above it.
- Indentation is 4 spaces per level. It matters only for `if/then/else` (§5) and
  `?` (§6).
- `#`, at line start or after whitespace, begins a **note** that runs to the end of
  the line. Notes have no meaning to the language. Use them for source remarks (§7)
  and ordinary comments.
- Text after `:`, `:=`, and `|` is free-form mathematics and prose.

## 3. Names

- A `NAME` is a plain identifier (letters, digits, underscores). No argument lists:
  write `expand`, not `expand(f)`; say "for every f" in the statement itself.
- A name is declared once, by `given`, `define`, `assume`, `claim`, or `derive`.
  It identifies that statement. It carries no scientific status.
- **Declaration before use.** Names appear only after their declaration. They are
  referenced in `from [...]` lists and, optionally, as an `if` condition.
- **Scope.** A name is visible from its declaration to the end of the document,
  except names declared inside a `then`/`else` branch, which are visible only inside
  that branch (§5).
- **No unnamed premises.** If a step relies on something specific to this problem —
  a physical law, a model assumption, a result from this document or from a source —
  it must be a named declaration listed in `from`. Standard mathematics (product
  rule, linearity, Cauchy–Schwarz, …) may be invoked by name in the reasoning; the
  reviewer checks that its conditions actually hold.
- **Symbols.** Standard constants and notation need no declaration. Any quantity
  whose meaning, type, or domain the reasoning depends on must be introduced by
  `given`, `define`, or `assume` before it is used. Free-form mathematics is not a
  license to introduce an essential quantity silently.

## 4. The seven constructs

```text
given NAME: <content>
define NAME := <meaning>
assume NAME: <premise>
claim NAME: <proposition>
derive NAME: <explicit result> from [NAMES] | <reasoning>
if <condition>:
    then <consequence>
    else <alternative>
? <what is unresolved and what would resolve it>
```

| Construct | Says | Does not say |
|---|---|---|
| `given` | This material is supplied to the present reasoning: data, a result taken from a source, established mathematics, or the problem statement. | That the material is true, correctly quoted, or applicable. |
| `define` | This is the meaning or convention of a symbol, object, or operation. | Anything about Nature. It adds no physical content. |
| `assume` | This premise is adopted provisionally, or restricts the model or regime. | That the premise holds in Nature. If it fails, what rests on it is out of scope, not refuted. |
| `claim` | This proposition is being asserted or examined (a paper's conclusion, a conjecture, a competing hypothesis). | That it is derived, or true. |
| `derive` | This explicit result is proposed to follow from the listed premises by the stated reasoning. | That the inference is valid or that the listed premises are complete. |
| `if` | What follows under a condition (`then`) and under its alternative (`else`). | That the condition holds. |
| `?` | Something is unresolved or underspecified, and what would settle it. | That anything is false. |

### `define` is not a back door

A `define` may be replaced by its right-hand side everywhere without changing any
proposition in the document. If removing it would change which physical situations
the reasoning describes, it is not a definition. Write it as `assume` or `given`.
Definitions that presuppose existence or uniqueness ("the lowest state", "the
solution of …") smuggle that presupposition in: assume it explicitly.

### `derive` is a proposal

- The **result** is a complete statement, not just a name.
- `from [NAMES]` lists the premises the author proposes the reasoning uses,
  including assumptions. It is *not* source attribution (§7), and it is *not* proof
  that nothing was left out. A reviewer must look for omitted premises, hidden
  assumptions, circularity, invalid steps, and results stronger than the premises
  support.
- `| <reasoning>` is the concise path from premises to result, short enough to check.
- `from []` asserts that the result needs no problem-specific premise. Treat it as
  suspicious.
- A `claim` may be listed as a premise. The result then rests on a proposition the
  document does not establish.
- To record that a proposition is **false**, derive the refutation: a counterexample
  or a contradiction (example in §9). Do not use `?`.

## 5. Conditional scope

```text
if <condition>:
    then <consequence>
    else <alternative>
```

- `then` and `else` are indented one level under `if`. `else` is optional.
- A consequence is either inline after the keyword, or statements on the following
  lines indented one more level.
- **Governing condition.** Every statement inside `then` holds only under the `if`
  condition; every statement inside `else` holds only under its negation. The
  condition need not be repeated in `from` lists inside the branch.
- **End of scope.** The conditional ends at the first line indented at or below
  the `if` line. A statement at that level is unconditional.
- **Condition form.** The condition is the name of an earlier `assume` or `claim`,
  or an explicit self-contained proposition on the `if` line. Never a vague
  reference to surrounding prose.
- Names declared inside a branch are visible only inside it. To reason further under
  the condition, continue inside the branch.
- A branch is not evidence that its condition holds. If both branches matter, say
  what is known about the condition in a `?` or a separate statement.

## 6. `?` — unresolved, never "false"

- **Attached `?`.** A `?` indented one level deeper than a statement, directly below
  it, is an unresolved question about that statement. Formally: its subject is the
  nearest preceding line whose indentation is exactly one level less than its own.
  A `?` directly under `if`, before `then`, is about the condition; one indented
  under `then`/`else` is about that branch.
- **Document-level `?`.** A `?` at column 0 is an unresolved question about the
  document as a whole, wherever it appears.
- **Content.** State what is missing and, where possible, what would resolve it: a
  premise, a calculation, a derivation, a source, a measurement.
- A `?` is an agenda item, not a verdict. It does not make anything false or
  invalid, and its absence does not mean a statement is sound.

## 7. Source fidelity without syntax

There is no provenance syntax. For paper overviews, say in notes or prose who is
responsible for each statement: stated by the paper, derived by the paper, cited by
the paper from elsewhere, reconstructed by the pseudocode author or an AI, or
unresolved. Plain words; there is no fixed vocabulary.

| Situation | Write |
|---|---|
| Authors derive a step, showing the work | `derive` with the displayed reasoning |
| Authors import a theorem | `given`, with a note naming the source |
| Authors assert a conclusion without displayed derivation | `claim` plus an attached `?` |
| You reconstruct a step the paper skips | a separate `derive`, with a note that it is a reconstruction, not the paper's |

Do not use `?` for attribution, and do not label a reconstruction as the paper's.

## 8. Boundaries

phys-pseudo is **not** a checker, a status system, or a proof format. It has no
parser requirement, provenance fields, computed statuses, dependency propagation,
operator catalogue, or required types. If a tool is ever written, it may assert only
document form (names resolve, declaration-before-use, indentation well-formed). It
cannot assert mathematical or physical content.

Three documents, three roles:

| Document | Role |
|---|---|
| `PSEUDO.md` (this file) | Minimal language for communicating reasoning. |
| `MRC_REVIEW_PROTOCOL.md` | Adversarial method for examining that reasoning. Uses `reality_check.md` as advisory knowledge. |
| `DERIVATION_SPEC_GUIDELINES.md` | Higher-rigor standard for specifying derivations for implementation and verification. |

Clear pseudocode is not implementation-ready. Exploratory documents and paper
overviews need not carry implementation-ready fields.

## 9. Examples

Illustrative only. They show form, not established physics.

**Scope and references** (toy):

```text
given ab: a and b are real numbers
define s := a + b
assume a_pos: a > 0
if b > 0:
    then
        derive s_pos: s > 0 from [s, a_pos] | positive plus positive is positive
    else
        derive s_below: s ≤ a from [s] | b ≤ 0 gives s = a + b ≤ a
        ? the sign of s for b ≤ 0 is undetermined; it needs a relation between |b| and a
derive s_real: s is a real number from [ab, s] | the reals are closed under addition
```

`s_pos` and `s_below` hold only under their branch condition and are visible only
inside it. `s_real` is unconditional. The `?` is about the `else` branch. A
top-level `derive … from [s_pos]` would be invalid: `s_pos` is out of scope.

**Refutation instead of `?`** (the operator-composition case; the values below were
checked symbolically):

```text
given fn: f is any twice-differentiable function of a
define sq := (a·∂ₐ)² f ≡ a·∂ₐ(a·∂ₐ f)
claim W: (a·∂ₐ)² f = a²·∂ₐ² f for every such f
derive expand: (a·∂ₐ)² f = a·f′ + a²·f″ from [sq, fn] | product rule: a·∂ₐ(a·f′) = a·(f′ + a·f″)
derive counter: for f(a) = a², (a·∂ₐ)² f = 4a² while a²·∂ₐ² f = 2a² from [expand] | f′ = 2a, f″ = 2: a·2a + a²·2 = 4a²; a²·2 = 2a²
derive not_W: W is false from [counter] | one f with unequal sides refutes the universal claim
```

**Paper overview shape** (schematic):

```text
# source: <paper>, §N — schematic, structure only
given law: [the paper's field equation]            # stated in the paper, eq. (N); cited there from elsewhere
define q := [the paper's defining relation]
derive step_1: [intermediate result] from [law, q] | [the paper's displayed reasoning]    # the paper's own derivation
derive step_2: [next result] from [step_1] | [reasoning]    # reconstruction by the pseudocode author; not in the paper
claim result: [the paper's conclusion]             # asserted by the paper; its displayed derivation stops at step_1
    ? no derivation from step_2 to the conclusion is given; a derivation or a cited result would resolve this
```
