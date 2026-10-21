# Fixture 07 — Cited result vs. independent derivation (symbolic toy)

- **Status:** TOY (golden by construction) + ANTI-PATTERN negative case
- **Mode:** paper
- **Constructs exercised:** `given`, `assume`, `claim`, `derive`, `?`
- **Invariant tests:** I2 (citation is not derivation), I3 (no status laundering of citations)
- **Document conformance (`PSEUDO.md`):** non-conforming, preserved verbatim
  — the premise token `[assume]` is a bare construct keyword and the
  `assume` is unnamed (§2); `derive step` states no explicit result (§4).
  `given … from cited @…` and `claim … from paper, conclusion` are read as
  prose source notes inside the content (§8), not as clauses.

## Document (the faithful form)

```text
# paper extraction: the paper invokes an averaging identity it does not prove
given theorem_A: ⟨uv⟩ = ⟨u⟩⟨v⟩ + Cov(u, v)   from cited @external-work
assume the averaging measure on the working domain is declared and linear
define fluct: δu := u − ⟨u⟩
claim closure: the averaged system closes on barred quantities alone   from paper, conclusion
derive step from [theorem_A, assume] | substitute u = δu, v = δu: ⟨(δu)²⟩ = ⟨δu⟩² + Var(u) = Var(u), since ⟨δu⟩ = 0
    ? [the paper cites theorem_A at this step; the step is reproduced here from the cited statement, not independently proven]
? [closure claim rests partly on cited material the paper does not reproduce]
```

## Expected MRC findings (recognition-level)

1. `theorem_A` is a `given ... from cited` — **imported**, and every `derive`
   using it inherits that: `step` is *reproduction under citation*, not an
   independent proof of the theorem. Its `?` says so in place.
2. The **anti-pattern** (negative case N1 below) must be distinguishable by
   **where the imported content sits**: in this faithful form the imported
   identity is a `given` *premise* and the `derive`'s result is a new local
   proposition (`step`); in N1 the imported identity itself is the `derive`'s
   *result*, under an unrelated placeholder premise — an assertion→
   derivation upgrade. Listing the imported result among the premises is
   normal in both and is **not** the criterion (Stage 3: the earlier
   criterion, "imported result as premise-and-content vs. `given` + step
   that uses it", was structurally wrong — faithful forms also list the
   imported result as a premise, and N1's premise is a placeholder).
3. `closure` is a `claim ... from paper` with a document-level `?`: source
   assertion, not derivation, and the citation dependency is visible.
4. The intermediate computation in `step` (⟨δu⟩ = 0 ⇒ variance reduction)
   is legitimately re-derived here — recognizing that *local computation
   from a cited premise* differs from *proving the cited premise* is part
   of the expected finding.
5. **I2:** an imported theorem in the ancestry is a fact about provenance;
   it must not be reported as making `step` stronger ("uses an established
   theorem ⇒ correct") nor weaker ("just a citation ⇒ uninformative"). The
   dependency `step → theorem_A@external` is the reportable content.
6. **I3:** citation must not launder into status: "cited in a published
   paper" is not `PROVEN`/`VERIFIED`, and no finding may upgrade
   `theorem_A` from imported to established within this document.
7. **(Stage 3 BLOCKING — added)** the variance reduction in `step` needs a
   normalization the document never states: `⟨δu⟩ = 0` holds only when
   ⟨1⟩ = 1 for the averaging measure. Counterexample: ⟨f⟩ = ∫₀² f dx with
   u ≡ 1 gives ⟨δu⟩ = 2 − 0 = 2 ≠ 0. "Declared and linear" does not entail
   normalized; a reviewer must require ⟨1⟩ = 1 explicitly.
8. **(Stage 3 — added)** `define fluct` is load-bearing — δu is defined
   nowhere else — yet appears in no premise list; the computation cites
   `δu` without declaring `fluct` into the ancestry (§2). The earlier
   attachment ambiguity of the indented `?` is now settled by rule (§6):
   it attaches to `step` (strictly deeper), and the trailing `?` at column
   0 is the document-level marker about `closure`.

## Rationale

Tests the corpus's core source-fidelity requirement at the smallest
possible scale: how a cited result enters (`given ... from cited`), how it
may be used (reproduction steps with local computation), and how an
author's conclusion over cited material is marked (`claim` + `?`).

## Negative cases

**N1 — citation laundering (ANTI-PATTERN):**

```text
derive theorem_A from [some other step] | ⟨uv⟩ = ⟨u⟩⟨v⟩ + Cov(u, v)
```

The cited theorem rewritten as an in-document derivation whose reasoning
just restates it. Must be flagged: an assertion→derivation upgrade —
precisely the upgrade fidelity rule (`PSEUDO.md` §8; formerly CONVENTIONS
§1) forbids. Note the
distinction from fixture 01's `expand`: re-deriving a *step from* a cited
rule is fine; "deriving" *the cited rule itself* by restating it is not.

**N2 — status laundering of the citation (ANTI-PATTERN, I3):**

```text
given theorem_A: …   from cited @external-work   # VERIFIED — cited in a published paper
```

An inline `# VERIFIED` on a citation. Must be flagged: publication is not
verification status, and no status word is construct-licensed.

## Audit history — Stage 4 metadata corrections

Metadata only. The `Document` block was not intentionally edited in this
pass. Byte identity against Stage 2/3 was not verified by a repository-wide
diff; no VCS diff is available (spot checks of representative document lines
were performed).
Corrections per `plan/final_REPORT_LOCKED.md` §2 (Fixture 07) and
`PSEUDO.md`:

- Header: added the document-conformance line (bare `[assume]` token and
  unnamed `assume`; result-less `derive step`; the `from cited` /
  `from paper` tails read as prose source notes).
- Expected finding 2 — original: distinguish the anti-pattern "purely by
  construct structure: `derive` with the imported result as premise-and-
  content vs. `given` + step that *uses* it." Rewritten (Stage 3: the
  criterion was structurally wrong — N1's premise is a placeholder, and
  the faithful form also lists the imported result as a premise); the
  discriminating axis is where the imported content sits (premise vs
  result).
- Expected findings 7–8 — added (Stage 3 BLOCKING: the ⟨δu⟩ = 0 step needs
  ⟨1⟩ = 1, absent; plus `define fluct` load-bearing but never a premise).
- N1 prose: repointed the fidelity-rule reference from CONVENTIONS §1
  (superseded) to `PSEUDO.md` §8.
- Noted, not changed: Stage 3's audit-absence item (no audit block; README
  anatomy item 4) — the fixture's content is symbolic and the missing-audit
  status is already carried by its TOY marking.
