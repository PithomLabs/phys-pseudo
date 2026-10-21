# Fixture 06 — Novel mathematical structure (no branch classification)

- **Status:** TOY (golden by construction under the no-external-claim
  reading — the pentadentate content is constructed symbolism, with no
  external mathematical claim; qualified per Stage 3)
- **Mode:** exploration
- **Constructs exercised:** all seven
- **Invariant test:** I1 (advisory guide cannot reject; unfamiliar structure
  fully expressible); EF4's branch reading additionally exercises I2
  (metadata correction, Stage 3)
- **Audit provenance:** none (Stage 3 addition) — no D4 audit is claimed or
  possible here; what is missing: any independently checkable content — □
  and σ exist only inside this document, so there is nothing external to
  verify.
- **Document conformance (`PSEUDO.md`):** non-conforming, preserved verbatim
  — premise tokens `[define □, assume, σ]` mix construct keywords with a
  name, and the `assume` is unnamed (§2); `σ` is used (inside `define □`)
  before its declaration on the next line (§2.1); `define □` and `define σ`
  assert propositions — an interchange law and an involution (§3);
  `derive check` states no explicit result (§4); the `if` condition ("σ
  absorbs the rearrangement") is not an identifiable proposition (§5.3).

## Document

```text
given question: "does a bracket-like operation □ on a declared set S satisfy a pentadentate identity?"
define □: S × S → S, written a □ b, with declared interchange law a □ b = σ(b □ a) for a fixed involution σ
define σ: S → S with σ∘σ = id
assume □ is associative on S
claim P: every triple (a, b, c) satisfies (a □ b) □ c = a □ (b □ c) literally, not merely up to σ
derive check from [define □, assume, σ] | expand both sides for a generic triple; the interchange law rewrites LHS into σ of a rearrangement of RHS
    ? [the claim depends on which rearrangements σ can absorb — a property of σ not yet constrained; no established branch of mathematics has been consulted, and none is required to state the problem]
if σ absorbs the rearrangement:
    then P holds within these declarations
    else: P fails within these declarations
```

## Expected MRC findings (recognition-level)

1. The document is **fully representable** with the seven constructs: novel
   bracket, invented notation, self-declared laws — no new keyword needed,
   no branch name anywhere.
2. **I1 (the direction this fixture exists for):** no finding may reject,
   warn, or downgrade the document because the advisory guide has no entry
   for □-brackets. The guide's silence about an unfamiliar structure is not
   a silence *about* the structure — a missing entry cannot motivate even
   an annotation, let alone a rejection. The document's `?` (self-declared,
   not guide-supplied) demonstrates that gap-marking works without the
   guide.
3. The self-declared laws are recognizable as self-declared — `check`'s
   ancestry is visible; novel does not mean untraceable. But the role
   assignment is wrong: `define □` asserts an interchange law (with σ) and
   `define σ` an involution law — propositions inside `define`, which under
   `PSEUDO.md` §3 may carry meaning only. "Visible and honest" overstated
   this (Stage 3); the corrected reading is *visible but mis-typed*
   self-declared law.
4. **I2:** no branch is a verdict — that direction stands. But "conditional
   + unresolved" overstates the cleanliness: under the literal reading the
   `assume` ("□ is associative") collides with `claim P` (every triple
   satisfies associativity *literally*), so `check`'s ancestry is circular
   with `P`; the `?` marks neither that ambiguity nor the anaphoric
   condition below (Stage 3).
5. **(Stage 3 — added)** The `if` condition "σ absorbs the rearrangement" is
   not an identifiable proposition: "the rearrangement" has no antecedent
   statement (`PSEUDO.md` §5.3), leaving the `else` branch unreachable by
   reference and the ambiguity unmarked — no `?` records it. Separately,
   σ's use-before-declaration is the fixture's one purely mechanical defect
   (§2.1).

## Rationale

Proves the anti-registry property from the opposite side of fixture 01:
where 01 tests a well-known identity, this tests mathematics nothing in
the corpus has heard of. If either requires a language change, the
vocabulary is not minimal-general. Expected outcome per plan: no change.

## Negative cases

**N1 — ontology forcing (ANTI-PATTERN, I1):** a hypothetical reviewer note
"cannot classify □ into a known mathematical branch; reject/defer." Must be
flagged as a protocol violation — the corpus has no branch taxonomy and
none may be introduced (plan2 non-goal: no universal physics operator
registry / ontology).

## Audit history — Stage 4 metadata corrections

Metadata only. The `Document` block was not intentionally edited in this
pass. Byte identity against Stage 2/3 was not verified by a repository-wide
diff; no VCS diff is available (spot checks of representative document lines
were performed).
Corrections per `plan/final_REPORT_LOCKED.md` §2 (Fixture 06) and
`PSEUDO.md`:

- Status line — original: "TOY (golden by construction)". Qualified: the
  golden-by-construction claim survives only under the no-external-claim
  reading (Stage 3).
- Invariant test — original declared only I1; EF4's branch reading is an I2
  exercise as well (Stage 3: "declared I1 but EF4 is an I2 test").
- Audit provenance note — added (Stage 3: no audit / "what is missing"
  note; README anatomy item 4).
- Header: added the document-conformance line (bare premise tokens; σ use-
  before-declaration; laws inside `define`; result-less `derive`; anaphoric
  `if` condition).
- Expected finding 3 — original: "… `check`'s ancestry is visible and
  honest — novel does not mean untraceable." Corrected: the ancestry is
  visible but the laws are propositions smuggled into `define` (Stage 3
  MAJOR; the earlier wording ratified them).
- Expected finding 4 — original: "the conditional conclusion is again
  conditional + unresolved; no branch is a verdict." Corrected: the
  literal reading makes the ancestry circular and the `?` marks neither
  ambiguity (Stage 3 MAJOR).
- Expected finding 5 — added (Stage 3: anaphoric condition / vacuous else /
  unmarked ambiguity; σ use-before-declaration).
