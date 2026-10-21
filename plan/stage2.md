# Stage Report — Conformance Corpus (Stage 2 completion)

**Repository:** `/home/chaschel/Documents/go/phys-pseudo`
**Baseline:** `plan/plan2.md` (approved) + `CONVENTIONS.md` (Stage 1 output)
**Scope executed:** Stage 2 only — Markdown conformance corpus. No grammar, parser, checker, advisory-guide validator, `PSEUDO.md`, or Phys-library integration. `CONVENTIONS.md` and both plan files unmodified.

## 1. Files created

```text
conformance/
  README.md                        corpus conventions, status vocabulary (GOLDEN / TOY /
                                   ILLUSTRATIVE / ANTI-PATTERN), invariant summary,
                                   coverage matrix, acceptance gate, "proves nothing" scope note
  01_operator_composition/fixture.md      GOLDEN — anchor fixture, corrected values
  02_ladder_operators/fixture.md          GOLDEN — audited in-fixture this stage
  03_missing_prerequisite/fixture.md      TOY
  04_conditional/fixture.md               TOY — all seven constructs, both modes noted
  05_dimensional_mismatch/fixture.md      TOY — mechanical/reasoned boundary
  06_novel_structure/fixture.md           TOY — I1 / anti-registry direction
  07_cited_result/fixture.md              TOY + ANTI-PATTERN — citation fidelity
  08_competing_hypotheses/fixture.md      TOY — peer claims, comparison ≠ selection
  S_cosmology_sketch/fixture.md           ILLUSTRATIVE (non-golden) — marking discipline
```

Each fixture contains: pseudocode document, expected recognition-level MRC findings, rationale, audit provenance, at least one binding-invariant test (including the forbidden direction where applicable), and negative cases.

No other files touched: no `*.go`, no `go.mod`, no `PSEUDO.md`, no `MRC_GUIDE*` (scope check verified empty); plans and CONVENTIONS untouched.

## 2. Structural coverage (grep-verified, both modes)

| Construct | Present | Fixtures |
|---|---|---|
| `given` | ✓ | all 9 |
| `define` | ✓ | all 9 |
| `assume` | ✓ | 02, 04, 06, 07, 08, S |
| `claim` | ✓ | all except 03 |
| `derive` | ✓ | all 9 |
| `if/then/else` | ✓ | 04, 06, 08, S |
| `?` | ✓ | all 9 |

**Modes:** paper-extraction shape — fixtures 01, 07 (plus 04's paper-mode note); constructed textbook-style (paper-extraction *shape*, no specific source) — fixture 02 after the Stage 2.1 correction; exploration — 03, 05, 06, 08, S. Every fixture carries the required sections (Expected findings / Rationale / Negative cases — grep: 9/9 each).

*Audit defect found and fixed:* the README coverage matrix disagreed with grep on three rows (01, 07, 08); the matrix was corrected to match the documents, not vice versa.

## 3. Audit results by status

- **GOLDEN (2):**
  - Fixture 01 — audit record embedded: product-rule expansion, f = a² ⇒ **LHS 4a², RHS 2a²**, equality condition `a·f′ = 0`. Grep confirms the corrected `2a²` appears 6× and the old `4a²/4a²` form appears exactly once, confined to negative case N1.
  - Fixture 02 — audit performed *during this stage*, then **repaired after
    independent review** (see "Defects found in review" below). Final form:
    nine steps independently re-derived (bilinear commutator → 1;
    `H = ħω(a†a+½)` reconstructed from the `a†a` expansion; `[H,a†] = ħωa†`;
    `[H,a] = −ħωa`; ladder recurrence from `|0⟩`; the lowering-operator
    contradiction forcing `a|0⟩ = 0`; `E₀ = ħω/2`; the independent bound as
    a consistency check; induction to `Eₙ = ħω(n+½)`). The assumption audit
    lists exactly the premises the document carries (`ω, m > 0`; named
    `lowest_state`) and records the lowering argument's domain conditions as
    an **open `?` item, not as satisfied assumptions**. Golden-on-steps:
    the encoded steps are independently checked; the full-spectrum claim's
    unresolved completeness dependency is stated in the findings.
- **TOY golden-by-construction (6):** 03–08 — symbolic; correctness checkable by document inspection; no external mathematical claim.
- **ILLUSTRATIVE non-golden (1):** S — marking present in header, expected findings, and both negative cases (promotion-by-repetition and audit-intent-without-audit flagged).

## 4. Invariant tests, both directions where applicable

- **I1:** fixture 06 — guide-silence must not reject the novel bracket (plus N1 flagging ontology forcing). Only one direction applies (no legitimate rejection exists to permit), as expected.
- **I2 (all 9 fixtures declare one; four test both directions):**
  - 01: may recognize dependency facts / must not infer "justified from clean ancestry."
  - 02: must not conclude `spectrum` is established (forbidden) nor broken (forbidden) — both error directions on one step.
  - 05: matching dimensions ≠ true (direction 1); matching dimensions ≠ license to call it wrong (direction 2) — same fact, both over-readings prohibited.
  - 08: taken branch ≠ establishment; untaken branch ≠ refutation; plus the ancestry-datum clause (sign datum ≠ support).
  - 03 (dependency ≠ verdict), 04 (conditional ≠ verdict), 07 (citation ≠ strength/weakness), S (structure ≠ physics validation).
- **I3:** four smuggling attacks in fixtures 01, 02 (including the `confirmed by experiment` empirical-support twist), 07 (`# VERIFIED` on a citation), 08 (N1 `PROVEN`-winner) — all designated must-flag.
- **Verdict-language sweep (semantic audit):** every occurrence of *justified / proven / verified / established / supported* across the corpus sits inside a forbidden-inference bullet, a negative case, or an innocent use (06's `no established branch … has been consulted`) — no finding asserts a verdict in its own voice.

## 5. Stage 2 acceptance checklist

| Gate | Result |
|---|---|
| Every golden has auditable derivation + independent check in-fixture | **Verified** — audit records present in 01 and 02 (grep + read); 01's values independently confirmed |
| Every non-golden visibly marked | **Verified** — 9/9 status headers; S marked in header, findings, negative cases, and README matrix |
| Source claims / assumptions / inferred material distinguishable | **Verified** — fixtures 01 (cited rule vs derived steps vs claim), 02 (CCR import vs named assumption vs derivation, with domain conditions kept as open `?`), 07 (cited theorem vs reproduction vs author claim), S |
| No implementation capability implied by a Markdown pass | **Verified** — README states pass = reviewer recognition only; no executable artifacts exist in the repo |
| Scope lock (no grammar/parser/checker/guide/PSEUDO.md/Stage 3-4) | **Verified** — `find` for `*.go`, `go.mod`, `PSEUDO.md`, `MRC_GUIDE*` returned empty; plans and CONVENTIONS untouched |

## Verified vs. unresolved

**Verified:**
- Corpus complete in proposed scope and order (01 → 02 → toys → S).
- Construct coverage across both modes (grep-verified per construct per fixture).
- Corrected operator values in place; wrong form quarantined as negative test only.
- Fixture 02 golden earned by an independent in-stage audit, then re-earned after the correction cycle below.
- Invariants I1/I2/I3 each tested, with forbidden directions where applicable.
- Scope lock held; verdict language confined to forbidden/negative contexts.

**Unresolved (deferred, by design):**
1. The corpus has been audited by its author **and, for `stage2.md` + fixture 02 only, by the independent reviewer** — the remaining seven fixture contents were *not* covered by that pass (reviewer's own caveat) and still await independent interpretation in Stage 3.
2. Induction / `?`-attachment conventions flagged in plan2 Deliverable E remain re-test cases; no dedicated fixture exercises them yet.
3. Raychaudhuri and stat-phys fixtures await verified sources (recorded in plan2 fixture-source decisions).
4. Promotion path for fixture S and any future physics fixtures awaits its first D4 audit by a second party.
5. ~~Fixture 02's mode relabel (constructed textbook-style) is not yet
   reflected in the README coverage matrix's mode column~~ — **resolved**:
   single-cell fix applied to the README matrix (Mode cell of row 02 →
   "constructed derivation / paper-extraction shape"); construct columns
   verified unchanged and grep-consistent with the fixture; no other
   README content touched. Authorized explicitly after the Stage 2.1
   acceptance review.

## 6. Defects found in independent review (Stage 2.1 correction cycle)

Recorded per the correction plans `plan/plan2.1.md` (superseded spec) and
`plan/plan2.2.md` (final spec, executed):

1. **Missing ground-state inference (blocking).** The original fixture
   derived only `E ≥ ħω/2` (from `⟨a†a⟩ ≥ 0`) and the recurrence spacing,
   then claimed the full spectrum `Eₙ = ħω(n+½)`. Neither implies
   `E₀ = ħω/2`; the missing step is the lowering-operator contradiction
   (`[H,a] = −ħωa` ⇒ `a|0⟩ = 0` ⇒ `E₀ = ħω/2`). Repaired: `lower_H`,
   `ground_annihilated`, `E0` steps added; `spectrum` retargeted to
   `[ladder, E0]`; old bound kept as the `bound` teaching-point step.
2. **Annotation inventing a premise (defect class ii).** The original `?`
   claimed the normalizable `a|0⟩ = 0` solution was "assumed above," but
   the `assume` line never contained it — a `?` is not an assumption, and
   the annotation misdescribed the document's own structure. Repaired:
   the assumption is now either derived (`ground_annihilated`) or listed
   as an unestablished domain `?`; nothing is recorded as satisfied that
   the fixture does not establish.
3. **Unverifiable citation designation.** The fixture was labeled
   paper-extraction mode with a non-specific reference (`@qm-postulates`).
   Repaired: relabeled constructed textbook-style (paper-extraction
   *shape*); mathematical golden status kept separate from source-fidelity
   claims; true paper-mode upgrade deferred to a D4-verified source.
4. **Domain-condition misstatement inside the first correction itself.**
   The `plan2.1.md` audit listed `a|0⟩ ∈ dom(a)` where the argument needs
   `|0⟩ ∈ dom(a)`, `a|0⟩ ∈ dom(H)`, commutator validity, and (per the
   final precision pass) `H|0⟩ ∈ dom(a)` — the last *derived* from
   `H|0⟩ = E₀|0⟩` + linearity, its premises unestablished. A further
   instance of class (ii), caught by the reviewer before execution and
   fixed in `plan2.2.md`.
5. **Full-spectrum scope made explicit.** Expected findings now state the
   two-part conclusion: tower sequence (derived) vs. entire spectrum
   (completeness argument + per-level domain conditions, unresolved);
   `GOLDEN` means checked steps, not unconditional conclusions.

**Meta-note:** defects 1–2 survived the author's self-audit — the audit
record that shipped with the original fixture repeated the gap instead of
catching it. This empirically confirms unresolved item 1: self-audit is
not independent verification. The reviewer's assessment — "a document can
have the right structure, clear provenance, and an audit record while
still containing a missing mathematical inference" — is now recorded in
the corpus itself (fixture 02's rationale and `bound` teaching point).

**Stage status:** Stage 2 **accepted as complete in scope** by final
review (report-based; not an independent repository inspection).
Acceptance record:

- Fixture 02 ground-state correction: accepted, subject to the reported
  checks.
- Operator-domain conditions: correctly remain unresolved.
- Full-spectrum completeness: explicitly unresolved.
- README Mode correction: reported complete, construct coverage preserved.
- Scope control: honored; no Stage 3 or Stage 4 work.
- Other seven fixtures: still need independent adversarial review (Stage 3
  input).

**Recorded limitation (reviewer's qualification):** the agent's claim
that only the intended README cell changed rests on content greps, not a
version-control diff — `phys-pseudo` has no VCS, so no independent diff
was available. This limitation remains on record with the acceptance.

Stage 3 (adversarial review of the remaining seven fixtures and the
conventions) is the next stage and begins **only upon explicit
authorization** — not started.
