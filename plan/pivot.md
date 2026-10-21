## prompt

while waiting for the agent, what are the unnecessary complexities that we adopted in our approach (e.g. is provenance there and if so, that is not needed), we should aim to derive from first principles and the specs should do just that, no more no less

## answer

I think we have adopted some unnecessary complexity. The root cause is that we started mixing the language for expressing reasoning, the process for reviewing reasoning, and the requirements for implementing verified derivations. Those are related, but they do not need the same amount of structure.

My recommendation is to derive `phys-pseudo` from first principles and aggressively minimize it.

## 1. Start from the irreducible problem

What must an AI agent express to reason about an arbitrary physics idea?

It needs to say:

1. What it starts with.
2. What its mathematical objects mean.
3. What it provisionally assumes.
4. What proposition it is investigating.
5. What it thinks follows from which premises.
6. Under which conditions a conclusion holds.
7. What remains unresolved.

That is the justification for our seven constructs. Anything else must demonstrate that it adds essential meaning rather than just more bookkeeping.

The language should let an agent express a false hypothesis, an incomplete derivation, or an unfamiliar mathematical construction without being rejected merely because it is unproven. MRC examines the reasoning and exposes its weaknesses; representation is not endorsement.

## 2. Complexity audit: what stays, what goes

Keep: the seven constructs

`given`, `define`, `assume`, `claim`, `derive`, `if / then / else`, and `?`.

Each captures a meaningful distinction in the reasoning process. In particular, `claim` must not be confused with `derive`, and `assume` must not silently become an established fact.

Simplify: labels and references

A label should be optional and used only when a later step needs to refer to something. Do not require every statement to have an ID, nor introduce a separate registry of premises.

Resolve the current `[assume]` inconsistency with a simple naming convention—for example, `assume A: ...` and `derive R from [A]`.

Remove from the core language: mandatory provenance syntax

This is an important simplification, but it needs a distinction. Detailed provenance metadata is unnecessary for exploratory hypotheses. For paper summaries, knowing whether a step is the author's derivation, a cited result, or an agent's reconstruction can be essential to source fidelity.

That information should be conveyed through ordinary source notes or comments when needed—not a mandatory `from` clause with separate syntax rules. Full source mapping belongs in the implementation-ready derivation specification, not the minimal pseudocode language.

Remove: computed scientific statuses

No `PROVEN`, `VERIFIED`, `SUPPORTED`, or automatically inferred truth status. Resolving every reference does not make a derivation correct. A source datum can contradict a claim.

The reviewer can report concrete structural facts and reasoning defects without inventing a universal status engine.

Remove from the language: branch and operator registries

Keep the `reality_check.md` shines/silent/partial knowledge as advisory guidance. Do not make the language depend on a predefined catalogue of physics branches, operations, or accepted mathematical objects.

Defer: grammar, parser, and checker

Our existing decision to test loose conventions against real examples first is correct. A parser is a future convenience, not a prerequisite for useful pseudocode.

## 3. The biggest semantic simplification: define exactly what each construct claims

Some current conventions use `?` for ambiguity, missing premises, unjustified steps, and even statements that are already known to be false. That is too much semantic work for one marker.

I would establish these minimal meanings:

| Construct          | What it means—and no more                                                                          |
| ------------------ | -------------------------------------------------------------------------------------------------- |
| `given`            | Material supplied to the present reasoning. It does not guarantee that the material is true.       |
| `define`           | Establish the intended meaning of a mathematical object or symbol.                                 |
| `assume`           | Provisionally adopt a premise or restrict the current model.                                       |
| `claim`            | State a proposition being considered.                                                              |
| `derive`           | Present a proposed inference and its premises. The syntax does not certify the inference.          |
| `if / then / else` | State what follows under a condition, and what follows under its alternative.                      |
| `?`                | Mark something genuinely unresolved or under-specified, and indicate what is needed to resolve it. |

This leads to one important rule: do not use `?` to mean both “unknown” and “known false.” If a claim is contradicted, express the counterexample or conflicting derivation. If it is still unresolved, use `?`.

These meanings are sufficiently small to cover the three purposes we have locked in.

## 4. Keep three levels of rigor separate

Our three use cases do not need three languages. They need the same language, with additional detail only when the task requires it.

### Exploration

A human or AI agent formulates a conjecture, records assumptions, and follows conditional reasoning. Missing definitions or unjustified steps are annotated. No full source registry or implementation contract is required.

### Paper overview or Go counterpart

The pseudocode preserves the important reasoning chain and the distinctions between statements, derivations, and unresolved steps. Source notes or implementation references are added only where useful to preserve fidelity.

### Implementation-ready derivation specification

The separate `DERIVATION_SPEC_GUIDELINES.md` applies its additional requirements: exact quantity definitions, domains, operation semantics, independent expected results, verification, and provenance. These details are required by the higher-rigor task—not by the core language.

The attached derivation guidelines already make this distinction possible: they demand a complete source-to-result chain and independently checked mathematical operations for implementation work. We do not need to encode all those obligations into the pseudocode syntax itself.

## 5. What about our own review process?

There is complexity in the review procedure too. Stage 3's blind/guided/reconciliation process has a legitimate purpose: prevent authors from treating their own audit as independent evidence. We should finish the authorized review, identify the actual defects, and make a single evidence-based disposition.

But afterwards, we should avoid perpetuating a review cycle for every tiny wording choice. The decision rule should be:

- A contradiction that can mislead reasoning must be fixed.
- An ambiguity that causes agents to interpret the same chain differently must be resolved.
- A stylistic preference that does not affect meaning does not justify a new rule.
- A potential future feature is deferred until an actual example needs it.

That keeps rigorous review from becoming an end in itself.

## My final recommendation

Our current seven-construct language is the core; nearly everything else is optional guidance, review practice, or a higher-rigor specification layer.

Provenance is the clearest example: it matters for some paper and implementation tasks, but it is not an irreducible ingredient in the language. Likewise, explicit dependency facts are useful; a global dependency registry and computed scientific statuses are not necessary for humans or adversarial agents to inspect the reasoning chain.

The remaining Stage 3 report should tell us which conventions actually cause errors. After that, make the smallest amendments needed to remove those ambiguities, freeze the minimal specification, and move forward.

Our guiding test for every proposed addition should be:

What concrete reasoning failure becomes impossible to express correctly if we omit this feature?

If there is no convincing answer, it does not belong in the core specification.