# Review Response — Blocking Finding on Fixture 02 (Correction Specification)

**Type:** correction review of Stage 2 — supplements `plan/stage2.md`
(the Stage 2 report) under the `plan/plan2.md` baseline.
**Revised per `plan/plan2.2.md`** (supersedes this file as the execution
spec; the revisions below incorporate its domain-condition correction and
the full-spectrum clarification).
**Review source:** user review of two uploaded files —
`conformance/02_ladder_operators/fixture.md` and `plan/stage2.md`.
**Review coverage caveat (carried forward):** the reviewer's pass covered
those two files only, *not* the entire repository and not the other seven
fixture contents; their reported checks are not independently verified here.
**Execution status:** correction specified below, **not yet applied** —
awaiting go.

## 1. Blocking finding confirmed: the ground-state energy is not derived

**The mathematics was independently verified before acceptance:**

- From the fixture's own steps: the recurrence
  `H(a†|n⟩) = (Eₙ + ħω)·a†|n⟩` gives spacings, hence
  `Eₙ = E₀ + n·ħω` and nothing about `E₀`.
- The bound `⟨a†a⟩ = ‖a|ψ⟩‖² ≥ 0 ⇒ E ≥ ħω/2` gives `E₀ ≥ ħω/2`
  and nothing about attainment.
- Neither implies `E₀ = ħω/2`; the fixture's `spectrum` step claimed
  exactly the missing implication.
- The only valid route is the reviewer-specified lowering argument:
  `[H,a] = ħω[a†a, a] = −ħω·a` (since `[a†,a] = −1`), so
  `H(a|0⟩) = (E₀ − ħω)·a|0⟩`; if `a|0⟩ ≠ 0` that is a strictly lower
  eigenstate, contradicting `lowest_state`; therefore `a|0⟩ = 0` and
  `E₀ = ħω/2` follows directly from `H = ħω(a†a + ½)`.
  The argument needs `a|0⟩ ∈ dom(H)` for the commutator manipulation —
  the domain-condition `?` is required, not decoration.

**Annotation defect confirmed, and its severity:** the old `?` asserted
"existence … is assumed above" about a premise the `assume` line never
contained. A `?` is not an assumption — and here the annotation
*misdescribed the document's own structure*. That is a defect class the
corpus did not previously cover, and the author's self-audit repeated the
gap instead of catching it — empirically confirming unresolved item #1
(author-self-audit is not independent verification).

## 2. Accepted correction — precise scope, no expansion

### 2.1 Fixture 02 document repair (reviewer's step chain, current vocabulary)

- Name the assumption so premises are referenceable:
  `assume H has a discrete spectrum with a lowest state |0⟩ … as lowest_state`
  (the `as LABEL` form already exists in CONVENTIONS §1 — no vocabulary
  change).
- Add: `derive lower_H from [H_in_ladder, comm(a, a†)] | [H, a] = −ħω·a`
  — hand-check: `[a†a, a] = a†[a,a] + [a†,a]a = −a` ✓.
- Add: `derive ground_annihilated from [lower_H, lowest_state] |` the
  contradiction argument, with
  `? [requires a|0⟩ ∈ dom(H) and that 'lowest' excludes lower eigenstates — domain conditions stated, not independently verified here]`.
- Add: `derive E0 from [H_in_ladder, ground_annihilated] | H|0⟩ = ħω(a†a+½)|0⟩ = (ħω/2)|0⟩`.
- Fix `spectrum` to `from [ladder, E0]` with the induction written as
  `Eₙ = E₀ + n·ħω = ħω(n+½)`.
- Keep the old bound step but rename/re-annotate it as `bound` with the
  teaching-point annotation: *the bound alone does not determine E₀;
  saturation is established separately by ground_annihilated*. The
  historical defect stays in the fixture, corrected, as an explicit
  in-document lesson — rather than being deleted.
- Update the header to reflect the source-fidelity fix (§2.4).

### 2.2 Audit record and assumption audit rewritten

- Add independent re-derivations of `[H,a] = −ħωa` and the contradiction
  step to the audit record.
- Assumption audit premise list changes: "normalizable `a|0⟩ = 0`
  solution assumed" is **removed** (now derived), replaced by exactly:
  `ω, m > 0`; discrete spectrum with a lowest state (the named
  `lowest_state`). Separately and **not** as satisfied assumptions, the
  lowering argument's conditions are recorded as an open item:
  `|0⟩ ∈ dom(a)` (so `a|0⟩` exists); `a|0⟩ ∈ dom(H)` (so the lowered state
  can be acted on by `H`); `H|0⟩ ∈ dom(a)` (so `a·H|0⟩` exists) — this
  last derived from `H|0⟩ = E₀|0⟩` + `|0⟩ ∈ dom(a)` + linearity of
  `dom(a)`, the derivation recorded but its premises unestablished;
  commutator identity valid on the state with all required compositions
  defined. All remain marked `?` — unestablished, never entered as
  premises.
- Step count changes from six to nine; every step re-checked in-record.

### 2.3 Expected findings rechecked

Findings 2, 3, 5, 6 change with the dependency chain:

- `spectrum`'s ancestry now runs through `ground_annihilated`, so its `?`
  (domain conditions) *is* in `spectrum`'s ancestry; the correct
  structural reading becomes "derived under stated assumptions with one
  unresolved domain gap in its ancestry."
- The I2-forbidden pair (established / broken) is re-tested on that new
  chain.
- Finding 3 (the old localization claim) is replaced by the two real
  annotations.
- **`spectrum`'s conclusion is two-part** (per plan2.2 clarification):
  the sequence `Eₙ = ħω(n+½)` for the generated tower (derived from
  `ladder` + `E0`), and the claim that this is the **entire** spectrum
  (rests additionally on the completeness argument — lowering on the
  relevant eigenstates — and its domain conditions, unresolved). The
  findings state this retained dependency explicitly.
- The `GOLDEN` header means: encoded mathematical steps independently
  checked. It does not assert unconditional establishment of every
  conclusion.

### 2.4 Source-fidelity designation — option (b) recommended

Relabel fixture 02 as **"constructed textbook-style derivation
(paper-extraction *shape*)"** and state that its mathematical golden
status is independent of any source-fidelity claim.

Rationale: option (a) — identifying and verifying a precise primary
source — is exactly the sourcing work already deferred by the
fixture-source decisions (Raychaudhuri, stat-phys). `@qm-postulates` is
honest as a postulate-level reference but not a paper citation, so the
fixture stops claiming extraction. Corpus paper-mode coverage is
unaffected: fixture 01 cites a real identifiable document
(`@project-guidelines`); fixture 07 covers citation shape symbolically.
Upgrade path for fixture 02 to true paper-mode stays under D4 when a
source is verified.

### 2.5 Stage report (`plan/stage2.md`) updated

- Fixture-02 audit numbers, assumption audit, source designation,
  affected findings, acceptance-gate row rechecked.
- New short "defects found in review" record:
  1. missing ground-state inference;
  2. annotation asserting a premise the document lacked;
  3. unverifiable citation designation.
  With the meta-note that the author's self-audit missed (i).

### 2.6 Explicitly out of scope

- No new fixtures; no changes to the other seven fixture contents
  (the review did not cover them — that stays an unresolved item).
- No grammar, parser, checker, guide validator, `PSEUDO.md`.
- Stage 3 not started; scope of plan2 and CONVENTIONS unchanged.
- Defect-class (ii) is **not** added as a negative case inside fixture 02
  unless explicitly approved — the repair stays strictly to the listed
  corrections (default per prior exchange).

## 3. Disposition (per reviewer)

| Category | Items |
|---|---|
| **Retain** | 7-construct vocabulary, Markdown-first strategy, recognition-level findings, invariant tests, scope lock; stage report records no parser/checker/grammar/library added. |
| **Correct before acceptance** | Fixture 02 ground-state derivation repair; audit record + assumption audit update; source-fidelity designation; recheck of affected expected findings. |
| **Keep deferred** | Independent adversarial review (Stage 3), induction and annotation-attachment tests, later verification of proposed Raychaudhuri and statistical-physics sources. |

**Meta-note:** this defect — right structure, clear provenance, audit
record present, missing mathematical inference — is exactly the class the
corpus exists to expose; that it survived a self-audit validates the plan2
concern recorded as unresolved item #1.

## 4. Verification obligations on execution

On go, after applying §2:

1. Re-run the fixture-02 audits (structure + math) and report
   verified-vs-unresolved results without claiming any check that was not
   actually run.
2. Re-run corpus-wide structural greps only insofar as fixture 02's edits
   affect coverage/status rows (README matrix row 02, stage report
   numbers).
3. Confirm the revised audit lists no unestablished condition as
   satisfied, and confirm the spectrum finding text carries the retained
   dependency.
4. Stop — no Stage 3.
