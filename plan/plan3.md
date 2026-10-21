# Stage 3 Plan — Adversarial Review of the Conformance Corpus and Conventions

**Status:** plan for approval. **Stage 3 is not authorized until
explicitly approved; no review work has begun.** Output of the turn that
produced this plan: the plan only, per instruction.

**Authority:** `plan/plan2.md` (baseline, D1–D4), `CONVENTIONS.md`
(7 constructs, I1–I3, tooling assertion ceiling), `plan/stage2.md`
(accepted Stage 2 status + recorded limitations).

**Objective:** test whether the conventions and corpus survive scrutiny
that is genuinely independent of the corpus author — not to add
features, formalize grammar, or fix anything in place.

## 1. Scope

**In scope for review:**
- The seven fixtures not yet independently reviewed: **01, 03, 04, 05,
  06, 07, S** (fixture 02 was covered by the earlier partial review; it
  is re-checked only where other findings touch it).
- `CONVENTIONS.md` itself — the vocabulary, the three invariants, the
  annotation semantics, and the tooling assertion ceiling.

**Explicitly out of scope:** grammar, parser, Go checker, advisory-guide
validator, `PSEUDO.md`, library integration, any change to
fixtures/conventions/plans. **Any defect found is reported, never fixed
in place** — dispositions are executed only under separate approval,
same discipline as the Fixture 02 cycle.

**Preserved by instruction:** Fixture 02's lowering-argument domain
conditions remain unresolved `?` by design; Stage 3 does not revisit or
"close" them.

## 2. Independence model (the core requirement)

The corpus author's self-review is not independent — Stage 2's own
defect history proved this (Fixture 02's missing inference survived the
author's self-audit and its shipped audit record). Therefore:

1. **Two-phase blind procedure.** Each fixture is reviewed in two passes:
   - **Phase A (blind):** the reviewer sees only `CONVENTIONS.md` and
     the fixture's **Document** block — not the expected findings, not
     the audit record, not the rationale. Phase A produces the
     reviewer's *own* findings and *own* mathematical checks.
   - **Phase B (reconciliation):** the reviewer then sees the expected
     findings, audit record, and rationale, and reports discrepancies:
     findings the document supports that the fixture omits; findings the
     fixture claims that the document does not support; audit steps that
     fail re-derivation.
2. **Audit records are not evidence.** Every audit claim (fixture 01's
   `4a²/2a²`, fixture 07's variance reduction, all toy steps) is
   re-derived from scratch; agreement with the author's record is a
   *result*, not a premise.
3. **Fresh-context reviewers.** Phase A/B are executed by subagents that
   receive only file paths and this procedure — no summaries, no author
   commentary, no prior-session context. The author transcribes results
   without editing them.
4. **Cross-fixture contamination check:** findings are formed per-fixture
   before any corpus-wide generalization, so a defect in one fixture
   cannot seed expected defects in another.

## 3. Review procedure (per fixture, per dimension)

**D1 — Mathematical correctness.** Re-derive every `derive` step. Search
specifically for the defect classes already seen: missing inference with
correct structure (Fixture 02's original gap); annotations that
misdescribe or invent document content; conclusions exceeding their
premises (bound ⇒ saturation; recurrence ⇒ spectrum; consistency ⇒
truth). For TOY fixtures, symbolic consistency; for fixture 01, fresh
hand-check of both operator values and the equality condition.

**D2 — Source fidelity.** For every `given … from cited` /
`claim … from paper`: is the provenance designation honest (real citation
vs. constructed vs. postulate-level reference)? Do source claims,
assumptions, and derived material stay distinguishable? Do the mode
labels in each fixture header and the README matrix agree with the
documents?

**D3 — Construct semantics.** Each of the seven constructs used per
CONVENTIONS §1 (e.g., `?` attaches locally and never acts as an
assumption; `assume … as LABEL` premise referencing is consistent;
`if/then/else` branch binding unambiguous). Plus: does any fixture
silently require vocabulary or behavior the conventions don't define?
(The anti-registry test: novel-structure fixture 06 must need no new
keyword.)

**D4 — Binding invariants I1/I2/I3.** Both directions, per fixture: is
every *forbidden* inference genuinely absent from the expected findings;
is every *permitted* finding actually supportable; is verdict language
confined to forbidden/negative contexts (fresh sweep, not inherited from
the author's grep); does I1's advisory ceiling hold against fixture 06;
do the I3 smuggling attacks in 01/02/07/08 still read as must-flag under
independent reading?

**D5 — Counterexample attempt.** For each expected finding, attempt to
construct a reading/document that satisfies the letter of the finding
while violating its intent (the Fixture 02 lesson: right structure,
hidden gap). Report any success.

**D6 — CONVENTIONS.md adversarial pass.** Are I1–I3 testable as stated or
vague anywhere? Do the annotation semantics cover everything the fixtures
rely on? Is the tooling assertion ceiling internally consistent? Any
construct with fuzzy boundaries under independent reading?

## 4. Severity taxonomy and deliverables

**Severity:** `BLOCKING` (math error, invariant violation, or conventions
defect that would mislead a user) / `MAJOR` (misleading annotation,
wrong coverage or mode claim, untestable convention clause) / `MINOR`
(wording, presentation) / `NOTE` (observation, no defect).

**Deliverables** (returned in-chat first; written to `plan/stage3.md`
only upon instruction, consistent with the file-naming convention):

1. **Per-fixture findings tables:** fixture → finding → severity →
   evidence (the exact text/step) → counterexample if any → proposed
   disposition (fix / relabel / defer / no action).
2. **Phase A vs. expected-findings agreement matrix** for each fixture:
   independent findings vs. declared findings, with gaps named both ways.
3. **CONVENTIONS.md assessment:** per-clause findings + the consolidated
   verdict.
4. **Consolidated assessment:** does the vocabulary survive? Verdict
   `PASS` / `PASS-WITH-AMENDMENTS` (amendments listed, none applied) /
   `FAIL` (with the minimal change set that would fix it) — per plan2's
   anti-registry principle, any proposed vocabulary change must be argued
   as necessary, not convenient.
5. **Verified-vs-unresolved report:** every claim tied to a check
   actually run; the fixture-02 domain-condition limitation and the
   no-VCS limitation carried forward verbatim.

## 5. Acceptance criteria for the stage itself

- All seven fixtures Phase A + Phase B completed; CONVENTIONS.md D6
  completed; no dimension skipped on any fixture.
- Every finding carries severity + evidence + proposed disposition; no
  disposition applied to any file.
- Every audit-record claim in the reviewed fixtures re-derived at least
  once independently (agreement/disagreement recorded either way).
- The consolidated verdict is argued from the findings, not asserted.
- Report contains only performed checks; anything not run is listed as
  unresolved, including the standing items (fixture 02 domain conditions
  by design; no VCS diffs; subagent results are transcription-faithful).

## 6. Execution order and reporting

Order: 01 → 03 → 04 → 05 → 06 → 07 → S → CONVENTIONS.md (conventions
last, so clause-level findings can draw on all fixture experience without
pre-seeding fixture reviews). Subagent results are reported as the
reviewer's findings; the author's transcription role is disclosed. On
completion: findings + verdict + verified-vs-unresolved, then **stop** —
no fixes, no Stage 4, awaiting disposition decisions.
