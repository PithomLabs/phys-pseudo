I'll start by checking which of the uploaded files are actually on disk, since only some of them came through in the context.

# Adversarial review of phys-pseudo: conventions, plans, and Fixture 02

**Bottom line.** The seven-construct vocabulary survives: none of my findings needs a new keyword. The weaknesses are in the conventions page, the fixture's audit claims, and a gap between the stated goal and what the plans actually deliver. As specified, phys-pseudo is a provenance and dependency language. It is not yet a math-reality-check language.

**Limits of this review.** I was given only Fixture 02 (`fixture.md`). Fixtures 01 and 03–08 and S were not uploaded, so I saw 01 only through CONVENTIONS §4.1, and I cannot confirm or contradict your §7 register for the others. This is not a blind Phase A pass in your plan3.1 sense, since I read everything including the register. I also share a model family with likely corpus authors, so correlated blind spots are possible. I treated the uploaded `plan2_2.md` and `plan3_1.md` as identical to the in-context copies and did not diff them.

## Checks I ran (sympy)

- **Identities.** `[a,a†]=1`, `H=ħω(a†a+½)`, `[H,a†]=ħωa†` and `[H,a]=−ħωa` all hold on a generic test function.
- **Ground state.** The Gaussian satisfies `a ψ₀=0` and `Hψ₀=(ħω/2)ψ₀`.
- **§4.1 values.** `(a∂ₐ)²a² = 4a²` and `a²∂ₐ²a² = 2a²`, as recorded.
- **Raised tower.** `a(a†ⁿψ₀) = n·a†ⁿ⁻¹ψ₀` for n ≤ 4.
- **Half-line oscillator.** With a Dirichlet condition at x=0, the lowest eigenvalue is `3ħω/2`. Applying `a` gives a nonzero Gaussian equal to 1 at the boundary, so it is outside `dom(H)`.

The record's algebra is right. The problems are in what the document declares and annotates.

## A. Goal-level findings

| # | Finding | Sev. |
|---|---|---|
| G1 | **The math-reality-check guardrail has no deliverable.** plan2's Stages 1–4 produce conventions, corpus, review, then spec and checker. `MRC_GUIDE` appears in none of them. The checker list (references, cycles, unknown keywords, definition-before-use) is hygiene. The dimension/type check from plan.md B.2.3 was dropped from the Stage 4 list and is absent from CONVENTIONS §3. Fixture 05 and plan2 B.1.3 still expect it. Category errors such as operator vs. function, dimension mismatch and domain violations therefore have no guard. | BLOCKING (vs. stated goal) |
| G2 | **"Facts" are author-declared edges, not actual dependencies.** Fixture 02 shows this four times: `H_in_ladder` uses `[x,p]` but lists `[a, a†, H]`; `ladder` uses `H\|0⟩=E₀\|0⟩` but lists `[commute_H]`; `ground_annihilated` needs `ħω>0` but omits the unnamed assume; `bound` needs `a†` to be the adjoint of `a`, which is never declared. Propagation runs over declared edges, so omitting an edge launders a `?`. I2 guards "clean ancestry ≠ valid" but not "declared ancestry ≠ true ancestry". | MAJOR |
| G3 | **Citations are unresolvable.** `@qm-postulates`, `@project-guidelines` and `@textbook` resolve to nothing. For LLM authors, a hallucinated citation becomes an "imported premise with provenance", and `inputs(s)=cited` reads as reassurance. | MAJOR |
| G4 | **Conformance has no oracle.** Expected findings are recognition-level prose, and the Stage 4 checker only checks structure, so the corpus cannot be run. Some findings (e.g. "ccr ∈ depends_on(spectrum)", "`?` in ancestry") are graph facts that a tool could assert. The mathematical ones need a human or a CAS. The corpus does not separate the two. | MAJOR |

## B. CONVENTIONS.md

| # | Finding | Sev. |
|---|---|---|
| C1 | **Table and examples disagree on syntax.** The table gives `derive LABEL: <result> from …`. Every example writes `derive LABEL from …` with no colon and no separate result, so the result is whatever ends the prose chain. The table gives `given NAME = …`, but every example uses `given NAME:`. The table says only `given` takes `from`, yet §4.3 puts it on `assume` and `claim`. There are five different label-binding forms. | MAJOR |
| C2 | **`from` is overloaded**: premises on `derive`, provenance elsewhere. A `derive` has no provenance slot. The paper-derive vs. agent-reconstruction distinction (EXPLICIT_SOURCE vs. SPEC_INFERENCE) is therefore pushed into `?` text. That is the wrong channel, because a `?` in ancestry poisons propagation. | MAJOR |
| C3 | **The golden candidate fails §3's ceiling.** Premises `product rule`, `Buchert identity`, `declared domain conditions` and `[assume]` are not labels, so "references resolve" would fail on §4.1 and §4.2. Parameterized labels like `expand(f)` and `comm(a,a†)` are undefined. | MAJOR |
| C4 | **`?` attachment contradicts itself.** The rule is "nearest preceding statement", yet a standalone `?` is a document-level question. §4.2's closing `?` follows the `else` branch, so by the rule it attaches there. Indentation is the de facto disambiguator, and the page never mentions whitespace. | MAJOR |
| C5 | **§4.1 puts a verdict in `?`.** `? [W is false …]` contradicts I2 and the definition of `?` (undetermined things). Refutation is expressible properly as `derive notW from [counter(f)]`. The example labeled golden teaches the misuse. | MAJOR |
| C6 | **Unnamed `assume` has no scope rule.** The page says to name an assume only if later steps reference it, but Fixture 02's steps depend on `ω>0` and cannot cite it. "Assume upstream" is undefined: by document order, or by graph? | MAJOR |
| C7 | **Promised items are missing.** plan2 said supersession and opaque-`define` conventions fold into Stages 1–3, and Stage 1 acceptance requires the A.5 justifications. None is in CONVENTIONS.md. | MAJOR |
| C8 | **Undefined policies.** Three of these are cheap mechanical checks.<br>• May a `derive` cite a `claim` as a premise (a silent claim→assume promotion)?<br>• May a `derive` have an empty premise list? plan.md's mutation test for this was dropped in plan2.<br>• May labels defined inside a branch be referenced outside it?<br>• When is a conditional an `if`, and when is it prose inside `\|`? Fixture 02 uses contradiction and induction inside `\|`, so plan2's induction re-test flag is still open. | MAJOR |
| C9 | **I2's scope is unclear.** Does it bind tooling only, or reviewers too? Fixture finding 7 says "only dependency facts are reportable". A competent reviewer with a counterexample (see F4) should be able to say "does not follow from the declared premises". | MINOR |
| C10 | **The `define`/`given` boundary is fuzzy.** `given op` is the definition of an operator power. `given ccr` is a model postulate, so by the page's own test (falsification delimits rather than invalidates) it is assume-like. | MINOR |

## C. Fixture 02

| # | Finding | Sev. |
|---|---|---|
| F1 | **Under-declared premises**: the four omissions in G2. | MAJOR |
| F2 | **Missing inference with correct structure**, the same class the repair targeted. `ladder` and `spectrum` assert that `a†ⁿ\|0⟩` is an eigenstate with energy `E₀+nħω`. That is vacuous unless it is nonzero. A one-line fix exists: `a(a†ⁿ\|0⟩)=n·a†ⁿ⁻¹\|0⟩≠0`, by induction from `[a,a†]=1`, `a\|0⟩=0` and `\|0⟩≠0` (checked n ≤ 4). Neither the steps, the `?`, nor audit steps 5 and 9 mention it. | MAJOR |
| F3 | **The domain `?` listing is incomplete and non-uniform.** The same condition class is silently assumed in `H_in_ladder` (operator equality, including domains), `commute_H`, `ladder` (per level), `E0` (`\|0⟩∈dom(a†a)`, `a\|0⟩∈dom(a†)`) and `bound`. It is annotated only at `ground_annihilated` and `spectrum`. I am not asking to resolve these, which is preserved by design. I am asking that the list be complete, or labeled non-exhaustive. The audit's "all remain marked `?`" overstates. | MAJOR |
| F4 | **The `?` carries real weight (witness).** On the half-line oscillator (Dirichlet at 0), every declared premise holds formally: CCR, ω,m>0, and a discrete spectrum with a lowest state. Yet `E₀=3ħω/2`, not `ħω/2`. This does not refute the textbook result. It shows that `derive E0 from [H_in_ladder, ground_annihilated]` does not follow from the premises as listed. The missing premise is, roughly, self-adjointness of x and p. | NOTE (strengthens F1/F3) |
| F5 | **"Independently checked" is unsupported.** The audit record is self-authored ("this derivation IS the audit") and names no checker or method. D4 requires an external authority. | MAJOR |
| F6 | **Smaller issues.**<br>• `x, p, ħ, i` are used before any declaration, and `ω, m` before `assume ω>0`. The fixture fails §3's own "symbols declared before use", which shows that check cannot be implemented on free-form math without a symbol convention.<br>• `define a := …, a† := …` binds two names in one statement.<br>• The `?` says the eigen-relation is "unestablished", but `lowest_state` assumes it. "Assumed, not established" is accurate. | MINOR |

## D. Plans and process

| # | Finding | Sev. |
|---|---|---|
| P1 | **The Fixture 02 exclusion from Stage 3 is unjustified.** It has failed review twice, and F1–F3 survived the correction cycle. The carve-out should cover only "domain conditions stay `?`", not the whole fixture. | MAJOR |
| P2 | **Reviewer independence is partial.** The independence-failure clause covers having no reviewer, not correlated errors from the same model family. Mathematical checks should be committed CAS or Lean artifacts, and source checks should be done by a human. | MAJOR |
| P3 | **Corpus-level gap.** The "≥2 pure paper" coverage requirement lacks genuine sources: 01 cites an internal guideline, 02 is constructed, and 07 is deferred. The paper-mode fidelity rule (B.1.2) has never met a real paper. | MAJOR |
| P4 | **Packet leaks.** Phase A's instruction "check each annotation against document content" hints at a Phase B defect class, and I2's text says a `derive` "can still be simply wrong". D2's mode-label and README checks cannot run in Phase A, because the header and README are excluded. Assign them to Phase C. | MINOR |

## E. Minimal amendments (no new keywords)

1. **Fix syntax.** Make the `derive` form uniform, with an explicit result: `derive L: <result> from [labels] | <reasoning>`. Use one `given NAME:` form, define label parameters, and write out whitespace and attachment rules for `?`.
2. **Add a tool-result channel.** Let tool-run math checks enter as `given check: <output> from computed @script#hash`. That is a new provenance value, not a status, so I3 holds. It also supplies the missing math-reality-check hook.
3. **Restore annotated type and dimension consistency.** Put it back in §3 and the Stage 4 checker, using a small machine-readable annotation inside `define`.
4. **Add three mechanical lints.** Flag label names mentioned in reasoning but absent from `from`. Flag a `derive` with an empty premise list. Flag citation handles that do not resolve to a bibliography entry. None of them asserts truth.
5. **Specify the open policies.** Cover unnamed-assume scope, claim-as-premise, branch-label scoping, and I2's scope (tooling vs. reviewers).
6. **Treat refutation as a `derive`, not a `?`.** Then amend §4.1, and relabel Fixture 02 as "GOLDEN on algebra only" until F1 and F2 are fixed and the check is reproducible by script.

**Verdict (your taxonomy).** The vocabulary gets PASS-WITH-AMENDMENTS: every issue above is a convention, provenance-value, or tooling-scope matter under your adjudication rule. CONVENTIONS.md as written is not ready, because C1–C6 would mislead anyone writing or parsing a document. Fixture 02's GOLDEN label should not stand as worded.

Would you like me to draft the convention amendments (E1–E6) as a diff against CONVENTIONS.md, or write the CAS verification script for Fixture 02 so the audit becomes reproducible?