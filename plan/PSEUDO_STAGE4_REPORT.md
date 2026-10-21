# Stage 4 Report — Phys Pseudo Canonical Language and Review Protocol

**Milestone:** Stage 4 of `phys-pseudo` — a canonical pseudocode language, an
adversarial review protocol, and a conventions pointer, consolidating Stages
1–3 after the Stage 3 adversarial review (`plan/final_REPORT_LOCKED.md`,
PASS-WITH-AMENDMENTS).

**Status:** complete, including the final bounded consistency amendment.
The amendment's change log, checks, and remaining uncertainty are in
[`PSEUDO_STAGE4_AMENDMENT.md`](PSEUDO_STAGE4_AMENDMENT.md) — this report
summarizes the milestone and does not duplicate it.

---

## 1. Deliverables

| Document | Role |
|---|---|
| [`PSEUDO.md`](../PSEUDO.md) | The sole authoritative specification of the language: seven constructs (`given`, `define`, `assume`, `claim`, `derive`, `if/then/else`, `?`), names and references, roles, `derive` slots, conditional scope, `?` semantics, the central invariant, source fidelity, examples, layer relationships, and the Stage 3 findings→resolutions map. Explicitly **not** a grammar, parser contract, or checker specification. |
| [`MRC_REVIEW_PROTOCOL.md`](../MRC_REVIEW_PROTOCOL.md) | The operational review method: eight proportional steps from scope reconstruction to evidential-boundary reporting, with `plan/reality_check.md` as consulted-not-embedded advisory knowledge and an explicit boundary to [`conformance/DERIVATION_SPEC_GUIDELINES.md`](../conformance/DERIVATION_SPEC_GUIDELINES.md) for implementation candidates. |
| [`CONVENTIONS.md`](../CONVENTIONS.md) | Pointer and migration note only — demoted from Stage 1 specification so there is no second competing spec. |
| [`conformance/README.md`](../conformance/README.md) | Corpus reading guide: status vocabulary, construct matrix, defect notes, byte-identity and label clarifications. |
| 8 fixture `Audit history` sections | Metadata-only correction records (fixtures 01, 03–08, S), each citing `plan/final_REPORT_LOCKED.md` §2 and the applicable `PSEUDO.md` sections. |

**Three-layer separation** (kept deliberately un-merged): language
(`PSEUDO.md`) / MRC review (`MRC_REVIEW_PROTOCOL.md`, advisory knowledge
`plan/reality_check.md`) / implementation-ready requirements
(`conformance/DERIVATION_SPEC_GUIDELINES.md`).

## 2. Canonical rules held throughout

- Seven constructs only; declaration-before-use; names are plain
  identifiers; named premises with **≥1 name per `from [NAMES]`** —
  `from []` is not part of the language.
- Explicit results mandatory on `derive`; no define-smuggling of independent
  assumptions (plus the substitution test).
- `?` = unresolved and only unresolved: statement-level = immediately
  follows the target at exactly one level deeper; document-level = column 0;
  conditional-as-a-whole → document-level; known-false → counterexample,
  contradiction, or conflicting derivation — never `?`.
- Source attribution is prose; `from` is premises-only; **no automatic `?`
  for paper claims** (`claim` + honest attribution unless a consequential
  inference is genuinely missing).
- Central invariant: **representation ≠ endorsement** — structure carries no
  verdicts; no author-typed statuses (`PROVEN`, `VERIFIED`, …).
- No tooling this milestone: no parser, checker, linter, status engine, or
  provenance registry exists or is implied, and **no universal capability
  ceiling for future tools is prescribed**; a future tool needs its own
  milestone and review.

## 3. Stage 3 findings → resolutions

The full map (14 findings → sections) is the `PSEUDO.md` §11 appendix table;
it was written in the original Stage 4 pass and preserved verbatim by the
amendment apart from aligning the `?` row's wording with the tightened §6
rule. Headline resolutions: one `given NAME:` spelling; name/reference
definition closing the `product rule` / `Buchert identity` citations;
`from` restricted to `derive`; unnamed `[assume]` premises banned when
referenced; mechanical `?` attachment; deliberate non-citability of branches
recorded as a design boundary; explicit `derive` results; verdict-in-`?`
banned; `?` lifecycle = deletion + prose resolution.

## 4. Regression evidence: failure patterns → rule → demonstrating fixture

Checked in this milestone against the corpus README matrix (read directly)
and the `PSEUDO.md` / protocol sections (read directly); fixtures were
spot-checked, not re-audited line-by-line (see §6):

| # | Failure pattern (Stage 3 review) | Rule / step | Demonstrating fixture |
|---|---|---|---|
| 1 | Result-less `derive` | `PSEUDO.md` §4; protocol step 3 | 05, 06, 08 (also 02, 04, 07 per matrix) |
| 2 | Unnamed / bare `[assume]` premises | §2.3; step 3 | 04, 07 (also 02, 06, 08, S) |
| 3 | Use before declaration | §2.1, §2.6; step 1 | 03 (undeclared `K`, `c`), 08 (`s`), 06 (σ) |
| 4 | Physical laws smuggled into `define` | §3 + substitution test; step 2 | 06 |
| 5 | Verdict-form `?` (known-false as question) | §6; step 8 | 01 |
| 6 | `?` misattachment at `else` | §6; step 1 | 04, 08, S |
| 7 | Citation laundering into status/`from` | §8; step 2 | 07, 01 |
| 8 | Missing premise in a consequential derivation | §4; step 3 (counterexample-first) | 03, 05 |
| 9 | Omitted domain/normalization conditions | §3/§5; step 4 (limits, degenerate cases, attributed oscillator illustration) | 02 (domain conditions `?` by design), 07 (normalization BLOCKING finding) |

## 5. Preserved fixture boundaries

- **No `Document` block was intentionally edited** in Stage 4 or the
  amendment — adversarial defects remain as inputs. Byte identity against
  Stage 2/3 was **not** verified by a repository-wide diff (no VCS is
  available); only representative-line spot checks were performed. The
  standard wording appears in `conformance/README.md` and all eight audit
  histories; no byte-identity claim remains elsewhere.
- Fixture metadata (headers, status lines, expected findings, audit
  histories) **was** corrected, each fixture recording its own edits;
  fixture 02 was never edited and has no audit-history section.
- Corpus labels (GOLDEN/TOY/ILLUSTRATIVE/ANTI-PATTERN) are documented as
  audit provenance / test purpose — never scientific truth or validity —
  while the §7 ban on author-typed statuses in pseudocode is preserved.
- `plan/claude/` (independent-review versions) and `plan/stage4_review.md`
  remain untouched as the review record.

## 6. Known limitations

- No VCS history in this directory: verification is content-grep and read
  based; the strongest claim about `Document` blocks is "not intentionally
  edited," with spot checks only.
- Expected findings were not re-audited line-by-line against
  `plan/final_REPORT_LOCKED.md` in this pass; the README matrix is
  descriptive of Stage 2/3 records, not certified exhaustive.
- Fixture 02's domain conditions remain `?` by design (open by record, not a
  defect of the spec).
- The oscillator illustration in protocol step 4 is attributed to the
  independent review as symbolically checked — not corpus-verified, not
  proven, not experimental.
- No automation exists; every conformance statement is recognition-level.

**Verification detail** (checks run, with verification level, and the
amendment's rejections — `from []`, tooling ceiling, automatic `?`): see
[`PSEUDO_STAGE4_AMENDMENT.md`](PSEUDO_STAGE4_AMENDMENT.md) §2–§5.
