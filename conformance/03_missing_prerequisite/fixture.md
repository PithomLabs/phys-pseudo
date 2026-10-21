# Fixture 03 — Missing prerequisite (symbolic toy)

- **Status:** TOY (golden by construction — purely symbolic, no external mathematical claim)
- **Mode:** exploration
- **Constructs exercised:** `given`, `define`, `derive`, `?`
- **Invariant test:** I2 (dependency reported, conclusion status not inferred)
- **Document conformance (`PSEUDO.md`):** non-conforming, preserved verbatim
  — `K` and `c` are undeclared (§2; the defect under test, marked by `?`),
  `m` is declared twice (`define m`, `derive m`; §2.4), and `derive m` has
  no explicit result slot (§4). The `given NAME:` spelling that older
  reviews counted as a deviation is now the canonical form (§1).

## Document

```text
given data: y = g(x) on a declared domain
define m := slope of the best linear fit of y against x
derive m from [data, K] | least-squares normal equations
    ? [K — the weighting measure for the fit — is never defined; 'best' is undefined without it]
derive prediction: ŷ = m·x + c from [m]
    ? [depends on m, which is unresolved; also c is undeclared in this document]
```

## Expected MRC findings (recognition-level)

1. `m`'s derivation has a **local missing prerequisite**: `K` is referenced
   as a premise but was never declared (`given`/`define`/`assume`). The `?`
   sits exactly on the step that needs it.
2. `prediction` is structurally **unresolved-by-ancestry**: its premise `m`
   carries a `?`, and it separately references an undeclared `c`. Two
   distinct defects must be recognized: one inherited (`?` through `m`),
   one local (undeclared `c`). `c` also has **no producer node**: the
   least-squares normal equations co-determine (m, c), so its absence is
   structural, not merely lexical (Stage 3).
3. Reasoning may continue past both defects: `prediction` remains
   representable and usable *conditionally*; it must never be presented as
   established, and it must not be deleted either.
4. **I2 permitted:** report "`prediction` depends on undefined `K` (via
   `m`) and undeclared `c`."
5. **I2 forbidden:** infer "`prediction` is therefore false" — an unresolved
   prerequisite is not refutation; and conversely infer nothing positive:
   nothing here licenses "valid pending K."
6. The `?` list is **part** of this document's review agenda — define K;
   declare or remove c. It is not the whole agenda (Stage 3: the earlier
   "agenda output … is its `?` list" wording was contradicted): unmarked
   defects exist here too — `g` and the domain inside the `given` are
   undeclared, and the fit family plus Var_K(x) > 0 conditions are silent.
   The reviewer's agenda is the `?` list **plus** findings discovered
   without a marker.

## Rationale

The minimal missing-prerequisite shape: shows `?` local attachment,
inherited vs. local defects, and that unresolved ≠ halted ≠ refuted.

## Negative cases

**N1 — silent gap (ANTI-PATTERN, described-only):** the same document with
both `?` lines deleted. Must be flagged: `K` and `c` then enter a `derive`
with no marker — the exact failure the `?` construct exists to prevent (gap
invisible at point of use). *(No variant document is instantiated in this
fixture; Stage 3 recorded that gap — marked described-only rather than
instantiated.)*

## Audit history — Stage 4 metadata corrections

Metadata only. The `Document` block was not intentionally edited in this
pass. Byte identity against Stage 2/3 was not verified by a repository-wide
diff; no VCS diff is available (spot checks of representative document lines
were performed).
Corrections per `plan/final_REPORT_LOCKED.md` §2 (Fixture 03) and
`PSEUDO.md`:

- Header: added the document-conformance line (undeclared `K`/`c` — the
  subject defect; duplicate name `m`; result-less `derive m`; `given
  NAME:` now canonical rather than a deviation).
- Expected finding 2 — extended with the structural cause for `c` (the
  normal equations co-determine (m, c); no producer node — Stage 3 MAJOR).
- Expected finding 6 — original: "The agenda output of a document like this
  is its `?` list: define K; declare or remove c." Contradicted (Stage 3):
  the `?` list is not a complete agenda; unmarked defects now listed.
- Negative case N1 — marked described-only (Stage 3 disposition:
  "instantiate or mark").
