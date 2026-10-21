# Final Consistency Amendment — Stage 4 (`phys-pseudo`)

**Scope:** one bounded documentation pass. Source of the task: the
independent review [`plan/stage4_review.md`](stage4_review.md) (findings 1–3
plus the consolidated amendment task). No new review stage follows this
pass. The whole-milestone summary is
[`plan/PSEUDO_STAGE4_REPORT.md`](PSEUDO_STAGE4_REPORT.md); this file is only
the change log for the amendment itself.

**Constraint observed throughout:** fixture `Document` blocks were not
edited; no constructs, parser, checker, linter, or status engine were added;
no tooling was specified; `plan/claude/` and `plan/stage4_review.md` were
left untouched as the review record.

---

## 1. Files changed

| File | What changed |
|---|---|
| [`PSEUDO.md`](../PSEUDO.md) | §2 name form + `from []` rejection; §3 define-substitution test and claim-as-premise; §4 empty-list ban + claim-premise rule; §5 worked example replaced by a §9 pointer (layout rule extended); §6 tightened `?` rule; §8 no-automatic-`?` rule; **new §9 Examples**; renumbering §9→§10 (relationship), §10→§11 (Stage 3 appendix), internal refs updated; appendix amendment note |
| [`MRC_REVIEW_PROTOCOL.md`](../MRC_REVIEW_PROTOCOL.md) | Step 2 source-check clause; step 3 overreach patterns + counterexample-first + hand/tool statement; step 4 limits/degenerate cases + attributed oscillator illustration; step 8 closing evidential-boundary paragraph |
| [`CONVENTIONS.md`](../CONVENTIONS.md) | Migration-table rows updated (`?` attachment wording, paper-claim row, tooling row §9→§10 with no-ceiling note, examples row → §9); amendment-history bullet |
| [`conformance/README.md`](../conformance/README.md) | Status line "unchanged documents" replaced; reading-corpus paragraph distinguishes unedited `Document` blocks from edited metadata; matrix intro standard byte-identity wording + spot-check note; labels-are-audit-provenance note under the status vocabulary |
| `conformance/0{1,3,4,5,6,7,8}_*/fixture.md`, `conformance/S_*/fixture.md` (8 files) | `Audit history` opener only: "byte-identical to Stage 2/3" replaced with the standard wording (below). Fixture 02 untouched (never edited since Stage 2) |
| [`plan/PSEUDO_STAGE4_AMENDMENT.md`](PSEUDO_STAGE4_AMENDMENT.md) | this file |
| [`plan/PSEUDO_STAGE4_REPORT.md`](PSEUDO_STAGE4_REPORT.md) | milestone report, written after this one |

**Not changed:** every fixture `Document` block (including fixture 02),
`plan/claude/`, `plan/stage4_review.md`, `plan/final_REPORT_LOCKED.md`,
`conformance/DERIVATION_SPEC_GUIDELINES.md`, `plan/reality_check.md`.

### The standard byte-identity wording

> The `Document` block was not intentionally edited in this pass. Byte
> identity against Stage 2/3 was not verified by a repository-wide diff; no
> VCS diff is available (spot checks of representative document lines were
> performed).

Used identically in `conformance/README.md` and all eight `Audit history`
sections. No byte-identity claim remains anywhere outside the review record
(`plan/stage4_review.md`, untouched — it is the document that *raised* the
finding).

---

## 2. Adopted from the independent review (`plan/claude/` via `plan/stage4_review.md`)

- **Define-substitution test** (`PSEUDO.md` §3): a `define` must be
  replaceable by its right-hand side without changing any proposition;
  existence/uniqueness presuppositions must be stated as `assume`.
- **Counterexample-first tactics** (protocol step 3): try the simplest case
  where the premises hold; named overreach patterns (bound → equality,
  recurrence → complete spectrum, "for some" → "for all", existence →
  uniqueness, eigenvalue relation → nonzero eigenvector); state whether each
  check was done by hand or with a tool.
- **Source-check** (protocol step 2): check that the cited source says what
  the `given` says; if it cannot be checked, say so.
- **Limits and degenerate cases** added to step 4's relevance-judged list.
- **Attributed oscillator illustration** (step 4): the half-line oscillator
  with Dirichlet at 0 (reported ground energy 3ħω/2 vs ħω/2 on the full
  line) as an omission-class illustration — attributed to the independent
  review as symbolically checked by its author, explicitly **not**
  corpus-audited, not proven here, not experimental; checks stay
  proportional.
- **Evidential-boundary paragraph** (step 8): what was checked and how, what
  could not be checked, what remains unresolved; no global
  correct/incorrect verdict; no "verified" beyond checks actually performed.
- **Plain-identifier names** (`PSEUDO.md` §2): no argument lists —
  `expand`, not `expand(f)`.
- **Corrected worked examples** (`PSEUDO.md` §9): the old §5 example (with
  the `else:` spelling contradiction and the leading-pipe `|` annotation
  after `claim H`) was replaced. The examples now cover scope/`?` placement,
  refutation-instead-of-`?`, and paper-overview attribution.

## 3. Rejected (conflicts with settled decisions)

- **`from []`** — claude's version allows empty premise lists. Rejected: the
  ≥1-name rule is restored explicitly (`PSEUDO.md` §2.3, §4: "`from []` is
  not part of the language").
- **Universal tooling-capability ceiling** — claude's version caps all
  future tooling at document form. Rejected: no tooling is defined this
  milestone and no ceiling is prescribed (`PSEUDO.md` §8 invariant retained;
  `CONVENTIONS.md` §10 row records the no-ceiling decision).
- **Automatic `?` for paper claims** — claude's table attaches `?` whenever
  a paper asserts without a displayed derivation. Rejected: such claims are
  `claim` + honest prose attribution; `?` only for a genuinely unresolved
  consequential inference (`PSEUDO.md` §8, demonstrated in §9).
- **Rewriting the base document** — claude's `PSEUDO.md` was *not* adopted
  wholesale; the repository-root `PSEUDO.md` remains canonical and received
  only the selected additions above.

## 4. Review findings 1–3, specifically

1. **Syntax inconsistencies** — the `else:` example is gone; the only
   conditional example (§9) uses the §1 template spelling
   (`else` + consequence), and the leading-pipe annotation is deleted (the
   paper example uses `#` comments instead). *Verified by direct read of §1,
   §5, §9 and a repo-wide grep for `else:` and `^\| `.*
2. **README byte-identity overstatement** — replaced everywhere with the
   standard wording; the "unchanged documents" status line was also
   corrected. *Verified by grep (before the reports were written):*
   `byte-identical`/`unchanged documents` matched only the untouched review
   record; the phrases now also appear in this report and the milestone
   report only while describing that replacement.*
3. **Corpus labels vs scientific statuses** — `conformance/README.md` now
   states GOLDEN/TOY/ILLUSTRATIVE/ANTI-PATTERN record audit provenance or
   test purpose only, with the `PSEUDO.md` §7 author-typed-status ban
   preserved. *Verified by direct read.*

The sign-of-`s` example fix (consolidated finding): the branch-wide question
is a column-0 `?` asking about the *sign* of `s`, not about the inequality
`s ≤ a` that `s_below` establishes.

---

## 5. Checks actually performed

All checks below were run in this pass; no VCS diff exists, so nothing is
claimed beyond these.

**Direct (grep or read, result inspected):**

- `byte-identical` / `byte identical` / `unchanged documents` repo-wide,
  run before these two reports were written → only `plan/stage4_review.md`;
  after writing, the only additional matches are this report's and the
  milestone report's discussion of the replacement (no document *makes* the
  claim).
- `from []` → only rejection sentences in `PSEUDO.md` + the untouched
  review/claude records.
- `else:` → only fixture `Document` blocks (preserved adversarial inputs),
  plan records, and README defect descriptions; **not** in `PSEUDO.md`.
- `^\| ` (leading-pipe annotation) → only markdown table rows, none in
  `PSEUDO.md` code blocks.
- Section numbering §1–§11 and every `§9`/`§10`/`§11` reference → consistent
  (§9 Examples, §10 relationship, §11 Stage 3 appendix).
- Link targets exist on disk: `plan/reality_check.md`,
  `conformance/DERIVATION_SPEC_GUIDELINES.md`, `plan/final_REPORT_LOCKED.md`,
  `plan/stage4_review.md`, `plan/claude/*` (three files), and both reports
  after being written.
- `Audit history` present in 8 fixtures; fixture 02 has none (correct — it
  was never edited).
- Standard wording appears in README + all 8 audit histories (edit
  tool reported exactly one replacement per file).

**Direct (manual trace):**

- §9 examples: declaration-before-use holds in all three; every `from` list
  has ≥1 name; the scope example's `?` is column 0 and immediately after the
  conditional block; the paper example's `?` is 4 spaces under a column-0
  `claim` (exactly one level deeper, immediately following); no `?` carries a
  known-false content (refutation example uses `derive not_W`); the
  operator values (4a² ≠ 2a²) match fixture 01's audit record.
- `?` rule: statement-level = immediately follows + exactly one level
  deeper; document-level = column 0; conditional-as-a-whole → document
  level; known-false → refutation only — all four clauses present in §6.

**Spot-check only:**

- Byte identity of fixture `Document` blocks against Stage 2/3: representative
  lines only (not a repository-wide diff — none is available).
- Consistency between the README matrix's per-fixture defect lists and each
  fixture's expected findings: spot-checked for fixtures 01, 04, 07, S.

**Not verified (assumed from prior stages, stated as such):**

- The per-fixture expected findings against `plan/final_REPORT_LOCKED.md`
  in full (only the rows touched in earlier Stage 4 edits were consulted).
- Scientific correctness of any fixture document.

## 6. Remaining uncertainty

- The corpus README's matrix lists known per-fixture defects; it is
  descriptive of what was recorded at Stage 2/3, not certified exhaustive.
  Fixture `Document` blocks use some forms (e.g. `else:` inside documents)
  that the canonical template spells differently; these blocks are
  deliberately preserved adversarial inputs and were not cataloged for
  spelling-level defects in this pass.
- No VCS history exists in this directory, so "not intentionally edited" is
  the strongest available claim about `Document` blocks; byte identity is
  spot-checked, not proven.
- The oscillator illustration is attributed, not corpus-verified.
