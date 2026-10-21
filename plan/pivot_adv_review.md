Provenance is there, and by the first-principles test it should leave the core language. Applying your own test to everything in the files shows the same thing for several other features.

**The test.** Which concrete reasoning failure becomes impossible to express correctly if the feature is omitted? A feature that fails the test is cut or deferred. A feature that is merely useful to a checker or reviewer is deferred.

## Where provenance lives now

- **The `from` clause.** It is optional syntax on `given`, and §4.3 also puts it on `assume` and `claim`. `derive` uses `from` for premises instead, so the word is overloaded.
- **`inputs(s)`.** plan2 A.3 computes the kinds of `given` in a statement's ancestry: measured, cited, paper, problem.
- **The B.1 fidelity check.** A statement marked `from paper` and written as `derive` must show its premises and reasoning.
- **The PhysTrace evidence-class mapping.**
- **Citation handles.** The fixtures use `@qm-postulates`, `@project-guidelines` and `@textbook`, and none of them resolves to anything.

Dropping it loses nothing expressible. "Imported result presented as derived" is already prevented by `given` vs. `derive`. "Authors' conclusion with no displayed derivation" is already `claim` + `?`. `from paper` is redundant with the construct choice. A source note in a comment covers the rest.

## Complexity inventory

| Item | Failure it prevents | Verdict |
|---|---|---|
| `from` clause, `inputs(s)`, PhysTrace mapping | None that construct choice doesn't already cover | **Cut** from the core; use source notes |
| Dependency-facts block and weakest-ancestor propagation | Nothing inexpressible. Fixture 02's four omitted premises show it is unsound over declared edges | **Cut**; optional reviewer practice |
| I1/I2/I3 plus the §3 tooling ceiling | I1 governs a guide that doesn't exist. I2 and §3 govern a checker that isn't built. I3 follows from having no status construct | **Collapse** to one sentence: representation is not endorsement |
| Six-step check ladder and Stage 4 checker | Nothing in the language | **Defer** |
| Fixture status taxonomy (GOLDEN, golden-by-construction, illustrative, deferred), audit records, modes | Mixes testing expressiveness with certifying math | **Reduce**: each fixture is a document, the distinctions it protects, and "checked or unchecked" per math claim |
| Stage 3 apparatus (3 phases, packets, 4 severities, D1–D6, 6 deliverables) | None; `plan3.1.md` (13 KB) is larger than `CONVENTIONS.md` (8 KB) | **Replace** with one blind pass plus a CAS check, then your decision rule |
| The Fixture 02 correction cycle | None. `plan2.1` and `plan2.2` spend about 7.7 KB rewording one operator-domain `?` | **Move** domain-condition lists to the higher-rigor layer (`DERIVATION_SPEC_GUIDELINES`) |
| `?` meaning ambiguity, missing premise, unjustified step, known-false and attribution | One marker can't carry all of those | **One meaning**: unresolved, plus what would resolve it |
| Five label-binding syntaxes | None; they make agents parse the same chain differently | **One form** |

## Where I'd push back on the recommendation

1. **Some of the "removals" are already removed.** There is no branch or operator registry in the files; plan2's non-goals ban them. Computed statuses were also replaced in plan2. What remains is the dependency-facts block, which is item 2 above.
2. **`derive` still needs its result.** The recommendation's `derive R from [A]` has no separable proposition. Without it a reader can't tell what is claimed to follow, and that is a real failure the test catches. I'd keep `derive R: <result> from [A] | <reasoning>`.
3. **`if/then/else` is the weakest construct.** `assume C as c; derive X from [c]` expresses "holds only under C". The case-split framing is the only extra, and branch scoping is undefined. Keep it for now, but it is the first one to cut if review finds the scoping rules unworkable.
4. **The math guardrail still has to live somewhere.** Leaving it out of the language is right, but nothing in the approved stages produces the MRC guide. It belongs with the guide and the derivation guidelines, not in the spec, but it needs a named owner.

## Retractions from my earlier review

Several of my amendments add structure that fails the same test: `from computed` (E2), the type/dimension annotation microsyntax (E3), the three lints including citation resolution (E4), and the machine-readable findings oracle (G4). Citation resolution only matters if `from` exists. Move all of these to the tooling or review layer, not the spec. The same goes for the lower-impact findings (C9, C10, F6, P4).

## What survives as the minimal spec

```text
given NAME: <content>
define NAME := <meaning>
assume NAME: <premise>
claim NAME: <proposition>
derive NAME: <result> from [NAMES] | <reasoning>
if <condition>: then <consequence> [else <alternative>]
? <what is unresolved, and what would resolve it>
```

Add three rules:

1. Any premise a step uses is listed in its `from`.
2. `?` means unresolved only. A known-false claim gets a counterexample or conflicting `derive`.
3. A `?` refers to the statement it is indented under. Unindented, it is a document-level question.

Add one principle: representation is not endorsement.

**What still must be fixed.** The mismatch between the §1 table and the §4 examples (C1), the verdict-in-`?` in §4.1 (C5), and unnamed assumptions that steps rely on (C6) all clear your decision rule, because they can mislead or cause divergent readings. Fixture 02's missing non-vanishing step (F2) and its under-declared premises (F1) must also be fixed or the fixture's golden label dropped. The remaining findings are deferred until a real example needs them.