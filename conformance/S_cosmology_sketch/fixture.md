# Fixture S — Cosmology backreaction sketch

- **Status:** **ILLUSTRATIVE (non-golden)** — physics content unaudited; carries no golden status and cannot be promoted without a completed D4 audit (source check + independent derivation)
- **Mode:** exploration
- **Constructs exercised:** all seven
- **Invariant tests:** I2 (non-golden status ≠ verdict on the physics), plus the standing marking discipline
- **Document conformance (`PSEUDO.md`):** non-conforming, preserved verbatim
  — `sgn(Q_D)`'s premises `Buchert identity` and `declared domain
  conditions` are never declared and therefore unresolvable (§2); the
  `assume` is unnamed (§2); the `else:` line sits at column 0, breaking the
  block layout (§5.1); and no source note appears anywhere, so nothing in
  the document is actually *cited* (§8).

## Why this fixture is not golden

It is retained to test the corpus's *marking discipline* — that an unaudited
physics sketch can live in the corpus without being mistaken for audited
content. Its equations have not been checked against a primary source
(the Buchert acceleration relation and the coefficient question around
`𝒬_D` remain unaudited), so per plan2 D4 it is shape-only. Promotion
requires: primary-source equation verification + independent derivation of
every displayed relation. *(Stage 3 C4 correction: the promotion gate named
content the document does not contain — the sketch displays no Buchert
relation and no coefficients; its right-hand sides are bracketed
placeholders. Promotion would first require spelling the relations out,
then auditing them.)*

## Document

```text
# ILLUSTRATIVE SKETCH — unaudited physics; no golden status (see header)
given question: "can structure alone account for the observed acceleration?"
define Q_D := [kinematical backreaction scalar averaged on domain D]
assume dust, irrotational motion, foliation {t} = const, compact domain D
claim H: the Q_D contribution can reproduce the observed acceleration magnitude
derive sgn(Q_D) from [Buchert identity, declared domain conditions] | [volume average]
    ? [no admissible solution (g, D) is supplied; magnitude of Q_D not computable; the cited identity itself is unaudited in this corpus]
if |Q_D| >= [required magnitude]:
    then H holds within this model
else:
    H fails within this model
? [observational adequacy is not addressed by this argument]
```

## Expected MRC findings (recognition-level)

1. The **ILLUSTRATIVE marking is part of the expected finding**: any report
   on this document must carry its non-golden status — "correctly formed"
   and "physically audited" are different facts, and only the first is
   available here (I2 applied to the fixture level itself: its existence in
   the corpus is not support for its physics).
2. "Structurally well-formed" is **withdrawn** (Stage 3 C1): the premise
   names `Buchert identity` and `declared domain conditions` are never
   declared and therefore unresolvable — under `PSEUDO.md` §2 that is
   non-conformance, not style. What remains true: all seven constructs are
   exercised, the derivation's `?` and the document-level `?` sit in the
   right forms, and both branches state conditional conclusions. A report
   must not upgrade exercise-of-syntax into well-formedness.
3. `sgn(Q_D)`'s premise list names "Buchert identity", but the document
   contains **no citation at all** — the earlier wording "unaudited cited
   identity" was annotation-only (Stage 3 C2): the name is an undeclared
   premise, not a cited source. The `?` half-covers this ("the cited
   identity itself is unaudited") while itself assuming a citation exists.
   A reviewer must not treat the premise name as an established theorem
   *or* as an actual citation (in-catalog ≠ cited ≠ audited-in-corpus).
4. The branches carry the same conditional reading as fixture 04: neither
   outcome is a verdict about nature; both are model-internal.
5. **I2 forbidden in the fixture direction:** "the sketch parses and every
   construct is exercised ⇒ the physics example is validated." Structural
   conformance of an unaudited sketch is exactly the inference this
   fixture exists to prohibit.
6. **(Stage 3 — added)** three further gaps: the `if` guard `|Q_D| >=
   [required magnitude]` names no threshold and rests on no premise; no
   observational datum appears anywhere in the document, so the "observed
   acceleration" in the `given` question is unreferenced content; and the
   `then` clause "H holds within this model" restates the guard's
   definition rather than deriving anything.

## Rationale

Two purposes: keeps cosmology present in the corpus as exploration-mode
material (coverage), while making the golden/non-golden boundary itself a
tested discipline rather than a header convention. Its historical role is
also recorded: it descends from the v1 example whose equation coefficients
failed review — a reminder in the corpus of why D4 exists.

## Negative cases

**N1 — promotion by repetition (ANTI-PATTERN):** reusing this sketch in
another fixture or citing it as "the corpus's cosmology example" without
the ILLUSTRATIVE marking. Must be flagged: non-golden status must travel
with the content.

**N2 — audit claim without audit (ANTI-PATTERN):** labeling the sketch
GOLDEN without adding a completed D4 audit record. Must be flagged: golden
requires the recorded independent check, not intent.

## Audit history — Stage 4 metadata corrections

Metadata only. The `Document` block was not intentionally edited in this
pass. Byte identity against Stage 2/3 was not verified by a repository-wide
diff; no VCS diff is available (spot checks of representative document lines
were performed).
Corrections per `plan/final_REPORT_LOCKED.md` §2 (Fixture S) and
`PSEUDO.md`:

- Header: added the document-conformance line (unresolvable premises;
  unnamed `assume`; `else:` at column 0 breaking the block layout; no
  source note anywhere).
- "Why this fixture is not golden" — extended (Stage 3 C4): the promotion
  gate named the Buchert relation and coefficients, which the document does
  not display (right-hand sides are placeholders).
- Expected finding 2 — original: "The document is structurally well-formed:
  all seven constructs, local `?` …". "Structurally well-formed" withdrawn
  (Stage 3 C1: contradicted by the unresolvable premises).
- Expected finding 3 — original: "`sgn(Q_D)`'s premise list includes an
  unaudited cited identity …". Corrected (Stage 3 C2): there is no
  citation in the document at all; the premise is undeclared, and the `?`
  itself assumes a citation exists.
- Expected finding 6 — added (Stage 3 MAJORs: premise-less magnitude guard;
  no observational datum; the `then` clause is a definition restatement).
- Verified unchanged: the no-audit marking discipline and both negative
  cases (Stage 3 agreed on both).
