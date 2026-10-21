# Fixture 05 — Dimensional mismatch (symbolic toy)

- **Status:** TOY (golden by construction — for the annotated dimensional
  arithmetic only; the branch remark inside the `?` invokes external physics
  (the relativistic energy–momentum relation), unaudited here; qualified per
  Stage 3)
- **Mode:** exploration
- **Constructs exercised:** `given`, `define`, `claim`, `derive`, `?`
- **Invariant test:** I2 (annotated-type finding is a fact; the verdict "wrong physics" remains review's)
- **Document conformance (`PSEUDO.md`):** non-conforming, preserved verbatim
  — `derive step` states no explicit result (§4; the Stage 3 BLOCKING this
  fixture now records), and `E`, `p` enter the check without appearing among
  its premises (declared via `define energy` / `define momentum`; §2).

## Document

```text
given constants: c = speed of light, declared c : L·T⁻¹
define energy: E : M·L²·T⁻²
define momentum: p : M·L·T⁻¹
claim K: E equals p·c
derive step from [K, constants] | dimensional check: [p·c] = M·L·T⁻¹ · L·T⁻¹ = M·L²·T⁻² = [E]
    ? [equivalence checked dimensionally only; relativistic relation E² = (pc)² + (m₀c²)² has branches with E ≠ p·c]
```

## Expected MRC findings (recognition-level)

1. The annotated-type check **passes**: the declared dimensions on both
   sides match (`M·L²·T⁻²`). The document may report this — it is a fact
   about the annotations, and it is *all* the mechanical check can say.
2. **I2 forbidden (the direction this fixture exists for):** the matching
   dimensions must NOT be reported as evidence that `K` is *true* —
   dimensional consistency is necessary, never sufficient. The `?` makes the
   gap explicit: `E = p·c` holds only in the massless branch.
3. **I2 second direction:** the document must not be reported as *wrong*
   either — the **annotations** on `K` are dimensionally coherent, and the
   `?` records that the relation holds only on the massless branch. The
   document establishes nothing about `K`'s truth; the earlier gloss
   ("dimensionally coherent and conditionally true") described the
   annotation, not the claim, and has been corrected (Stage 3). The report
   must not convert an annotation match into "wrong" or into "true".
4. *Rule, described-only — the stripped-tags variant is not instantiated in
   this fixture (Stage 3):* in a document without the `: …` annotations, no
   dimensional finding at all may be issued — absent annotations make
   compatibility a review question, never a silent pass.
5. **(Stage 3 BLOCKING — added)** `derive step` states **no explicit
   result**: under `PSEUDO.md` §4 the result slot is mandatory, and its
   absence means the step asserts nothing checkable — a reader must not
   silently read "the dimensions match" off the reasoning text as if it
   were the step's conclusion. Separately, `E` and `p` enter the check but
   appear in no premise list (they are declared elsewhere via `define`).

## Rationale

Pins the mechanical/reasoned boundary from the plan: annotated consistency
is checkable and reportable *as a fact*; sufficiency, physical correctness,
and branch selection are not. Tests both forbidden directions of the same
fact.

## Negative cases

**N1 — unit violation with annotations (ANTI-PATTERN):**

```text
define force: F : M·L·T⁻²
derive bad from [F, energy] | "E = F·t ⇒ E : M·L²·T⁻²"
```

`[F·t] = M·L·T⁻¹ ≠ M·L²·T⁻²`: an annotated mismatch. Must be flagged at
the step — and flagged as *annotation inconsistency*, not as a proof that
the physics is wrong (a reviewer may find, e.g., a missing length factor in
the intended relation; the mechanical finding only names the mismatch).

## Audit history — Stage 4 metadata corrections

Metadata only. The `Document` block was not intentionally edited in this
pass. Byte identity against Stage 2/3 was not verified by a repository-wide
diff; no VCS diff is available (spot checks of representative document lines
were performed).
Corrections per `plan/final_REPORT_LOCKED.md` §2 (Fixture 05) and
`PSEUDO.md`:

- Status line — original: "TOY (golden by construction)". Qualified: the
  golden-by-construction claim covers the annotation arithmetic; the `?`'s
  branch remark invokes the external relativistic energy–momentum relation
  (Stage 3: qualify "golden by construction" lines).
- Header: added the document-conformance line (result-less `derive`; `E`,
  `p` absent from the premises).
- Expected finding 3 — original: "`K` is dimensionally coherent and
  conditionally true; the document says exactly that …" Corrected: that
  gloss described the annotation, not the claim (Stage 3).
- Expected finding 4 — marked described-only (Stage 3: the stripped-tags
  variant is asserted about but never exercised here).
- Expected finding 5 — added (Stage 3 BLOCKING: the sole `derive` states no
  result; was only "partial" in the fixture before).
