# Stage 3 Plan (Revised) — Adversarial Review of the Conformance Corpus and Conventions

**Status:** revised plan for approval, superseding `plan/plan3.md`.
**Stage 3 is not authorized until explicitly approved; no review work has
begun.** This file records the plan revisions accepted from the
preliminary review (plan3 review returned two blocking plan issues and
nine fixture-level observations).

**Authority:** `plan/plan2.md` (baseline, D1–D4), `CONVENTIONS.md`
(7 constructs, I1–I3, tooling assertion ceiling), `plan/stage2.md`
(accepted Stage 2 status + recorded limitations).

**Objective:** test whether the conventions and corpus survive scrutiny
that is genuinely independent of the corpus author — not to add
features, formalize grammar, or fix anything in place.

## 1. Scope — corrected

**In scope for review — eight fixtures:** **01, 03, 04, 05, 06, 07, 08,
S** (the earlier plan's "seven" was a miscount inherited from a
reviewer-caveat figure; the independent pass covered fixture 02 only, so
eight remain unreviewed — fixture 08 was wrongly omitted and is now
included), plus `CONVENTIONS.md` itself — vocabulary, three invariants,
annotation semantics, tooling assertion ceiling.

**Known discrepancy outside Stage 3 scope:** `plan/stage2.md`
unresolved item 1 carries the same "seven" miscount; its correction is a
queued one-word Stage 2 record fix, awaiting separate authorization.

**Explicitly out of scope:** grammar, parser, Go checker, advisory-guide
validator, `PSEUDO.md`, library integration, any change to
fixtures/conventions/plans. **Any defect found is reported, never fixed
in place** — dispositions are executed only under separate approval,
same discipline as the Fixture 02 cycle.

**Preserved by instruction:** Fixture 02's lowering-argument domain
conditions remain unresolved `?` by design; Stage 3 does not revisit or
"close" them. Fixture 02 is reviewed only where other findings touch it.

## 2. Independence model (restructured — three phases)

The corpus author's self-review is not independent — Stage 2's own
defect history proved this (Fixture 02's missing inference survived the
author's self-audit and its shipped audit record). Therefore:

### Phase A — blind, generic

- **Redacted packet:** the CONVENTIONS abstract clauses (§1–3 +
  tooling-assertion ceiling); **§4 worked examples withheld** —
  CONVENTIONS §4.1 contains fixture 01's exact answer (`4a²` vs `2a²`),
  so the full document would replace derivation with recognition. The
  fixture's **Document block only** — not expected findings, not audit
  record, not rationale. Access to cited primary sources where needed,
  for independent source checking.
- **Generic instructions only:** verify every derivation independently;
  check each annotation against actual document content; assess construct
  usage against the abstract rules; attempt expressiveness and
  counterexample challenges. **No defect-class catalogue, no
  fixture-specific hints, no project history.**
- Phase A output: the reviewer's own findings and own mathematical
  checks, locked before any further context is given.

### Phase B — guided adversarial

- Same locked Phase A findings, plus a **sanitized, generic defect-class
  catalogue**: missing inference with correct structure; annotation–
  document mismatch; premise overreach (conclusion exceeding its
  premises); label/reference inconsistency; branch-coverage gaps;
  undeclared named dependencies.
- **What Phase B must NOT receive:** the raw Stage 2 review history, the
  preliminary observations register (§7), or any fixture-specific hints.
  The catalogue is sanitized — class descriptions only, no instances, no
  references to which fixture exhibits which class.

### Phase C — reconciliation

- Expected findings, audit record, and rationale revealed. The reviewer
  reports discrepancies: findings the document supports that the fixture
  omits; findings the fixture claims the document does not support; audit
  steps that fail re-derivation.
- Phase C output is locked **before** the author compares independent
  findings against the preliminary observations in §7 — disagreements
  included, both directions.

### Reviewer isolation (operational rule)

> **Reviewer isolation:** Assemble phase-specific review packets
> containing only the materials authorized for that phase. Do not give
> Phase A or Phase B reviewers access to the full fixture files, the
> unredacted `CONVENTIONS.md`, `plan3.1.md`, the Stage 2 review history,
> or the preliminary observations register. Supply redacted content
> directly or through isolated temporary packets. Reveal additional
> material only at the designated phase transition. Preserve the locked
> outputs from each phase before revealing the next packet.

**Packet mechanics:**

- Redacted extracts are staged under `/tmp/opencode/scratch/` (the
  approved external scratch area) — one packet directory per phase per
  fixture. Phase A packets contain **only** the fixture's Document block
  and the abstract convention clauses §1–3 (plus the tooling-assertion
  ceiling); the §4 worked examples are withheld.
- Reviewer subagents receive **packet paths only** — never the
  `conformance/` or `plan/` directory paths, never full file paths of
  fixtures or plans.
- Subsequent material is revealed only after the previous phase's
  findings have been written down and locked; the author performs the
  packet assembly and transition, opening full files only at the
  designated transition.

**Recorded limitation (procedural, not cryptographic):** isolation rests
on packet discipline plus the fresh-context guarantee (each reviewer
subagent starts without prior-session knowledge) — there is no technical
barrier against a determined read. Any packet-assembly error (e.g., an
accidentally included section) is itself a reportable limitation to be
stated in the verified-vs-unresolved report, never silently overlooked
or silently retaken.

### Standing independence rules

1. **Audit records are not evidence.** Every audit claim (fixture 01's
   `4a²/2a²`, fixture 07's variance reduction, all toy steps) is
   re-derived from scratch; agreement with the author's record is a
   *result*, not a premise.
2. **Fresh-context reviewers.** Phases A–C are executed by subagents
   that receive only file paths and the phase-appropriate packet — no
   summaries, no author commentary, no prior-session context. The author
   transcribes results without editing them.
3. **Cross-fixture contamination control:** findings are formed
   per-fixture before any corpus-wide generalization.
4. **Independence-failure clause:** if a fresh-context independent
   reviewer cannot actually be obtained, the limitation is recorded and
   Stage 3 halts; a self-review is never reported as independent.

## 3. Review procedure (per fixture, per dimension)

Dimensions D1–D6 as in `plan3.md`, with these clarifications:

**D1 — Mathematical correctness.** Re-derive every `derive` step;
annotations checked against document content; conclusions tested against
premise sufficiency.

**D2 — Source fidelity.** For every `given … from cited` /
`claim … from paper`: is the provenance designation honest (real citation
vs. constructed vs. postulate-level reference vs. undeclared named
dependency)? Do source claims, assumptions, and derived material stay
distinguishable? Do fixture-header mode labels and the README matrix
agree with the documents?

**D3 — Construct semantics.** Each of the seven constructs used per the
abstract CONVENTIONS §1 rules. Does any fixture silently require
vocabulary or behavior the conventions don't define? (Anti-registry test:
fixture 06 must need no new keyword.)

**D4 — Binding invariants I1/I2/I3.** Both directions, per fixture:
every *forbidden* inference genuinely absent from the expected findings;
every *permitted* finding actually supportable; verdict language confined
to forbidden/negative contexts (fresh sweep, not inherited); I1's
advisory ceiling vs. fixture 06; I3 smuggling attacks in 01/02/07/08
under independent reading.

**D5 — Counterexample attempt.** For each expected finding, attempt to
construct a reading/document that satisfies its letter while violating
its intent. Report any success.

**D6 — CONVENTIONS.md adversarial pass** (after all fixtures). Are
I1–I3 testable as stated or vague anywhere? Do annotation semantics cover
everything the fixtures rely on? Is the tooling assertion ceiling
internally consistent? Any construct with fuzzy boundaries? (Includes,
blindly adjudicated: whether `[assume]`-as-premise-reference is fixture
inconsistency or a missing conventions rule — no new keyword may be
introduced to work around it.)

## 4. Severity taxonomy and deliverables

**Severity:** `BLOCKING` (math error, invariant violation, or conventions
defect that would mislead a user) / `MAJOR` (misleading annotation,
wrong coverage or mode claim, untestable convention clause) / `MINOR`
(wording, presentation) / `NOTE` (observation, no defect).

**Deliverables** (returned in-chat first; written to a report file only
upon instruction):

1. **Per-fixture findings tables:** fixture → finding → severity →
   evidence (exact text/step) → counterexample if any → proposed
   disposition (fix / relabel / defer / no action).
2. **Phase A vs. expected-findings agreement matrix** per fixture:
   independent findings vs. declared findings, gaps named both ways.
3. **CONVENTIONS.md assessment:** per-clause findings + consolidated
   verdict.
4. **Consolidated assessment:** does the vocabulary survive? Verdict
   `PASS` / `PASS-WITH-AMENDMENTS` (amendments listed, none applied) /
   `FAIL` (minimal change set) — per plan2's anti-registry principle,
   any proposed vocabulary change must be argued as necessary, not
   convenient.
5. **Preliminary-observations comparison:** after Phase C lock, §7
   observations compared against independent findings — confirmed /
   contradicted / not reproduced, each with the independent evidence.
6. **Verified-vs-unresolved report:** every claim tied to a check
   actually run; standing limitations carried forward verbatim
   (fixture-02 domain conditions by design; no VCS diffs; subagent
   results transcription-faithful).

## 5. Acceptance criteria for the stage itself

- All **eight** fixtures Phase A + Phase B + Phase C completed;
  CONVENTIONS.md D6 completed; no dimension skipped on any fixture.
- Every finding carries severity + evidence + proposed disposition; no
  disposition applied to any file.
- Every audit-record claim in the reviewed fixtures re-derived at least
  once independently (agreement/disagreement recorded either way).
- The consolidated verdict is argued from the findings, not asserted.
- Report contains only performed checks; anything not run is listed as
  unresolved.

## 6. File-immutability rule (retained)

Findings, severity, evidence, and proposed dispositions are reported
only. No fixture corrections, no convention changes, no plan edits
during Stage 3. Execution of any disposition — including the queued
`plan/stage2.md` "seven→eight" record fix and any fixture repairs
suggested by the §7 observations — requires separate approval after the
verdict.

## 7. Author-held preliminary observations register

Recorded from the plan3 preliminary review (verified against fixture
files by the author at registration time). **Contamination control: this
table is not shown to Phase A/B reviewers;** it is used only in the
post-Phase-C comparison (deliverable 5).

| Fixture | Observation | Severity (preliminary) |
|---|---|---|
| 01 | `expand` uses undeclared "product rule" premise; differentiability definition not in the dependency chain despite findings claiming premises visible | Major |
| 01 | README mode `paper` vs header `paper-extraction shape`; cited source is an internal guideline | Major |
| 03 | Review question: expected findings must treat the intentional defects as defects, not as successful validation | Good-test shape |
| 04 | Geometric-majorant argument needs `0≤q<1`, fixture declares only `q<1`; `?` indentation makes attachment ambiguous | Major |
| 05 | Expected finding over-reaches: I2 must not forbid judging the unqualified `E=pc` false on separate mathematical grounds; dimensional consistency establishes neither truth nor falsity | Major |
| 06 | Circular: `assume □ is associative` while claim P asks whether □ is associative | Blocking |
| 07 | `⟨δu⟩=0` requires normalization `⟨1⟩=1`, not linearity alone; unnamed `assume` referenced as `[assume]` | Major |
| 08 | `discriminant`'s sign-difference prediction undeclared; `sign(s)=0` branch missing — discriminator does not distinguish | Major |
| S | Expected finding 3 says "cited identity" but `Buchert identity` is named, never declared `given … from cited` | Major |
| cross | `[assume]` as premise reference without labels in 04, 06, 07 — fixture inconsistency or missing conventions rule? Blindly adjudicated in D6 | open question |

## 8. Execution order and reporting

Order: 01 → 03 → 04 → 05 → 06 → 07 → 08 → S → CONVENTIONS (D6) →
consolidated verdict → §7 comparison → verified-vs-unresolved report →
**stop**. No fixes, no Stage 4, awaiting disposition decisions.
Subagent results are reported as the reviewer's findings; the author's
transcription role is disclosed in the report.
