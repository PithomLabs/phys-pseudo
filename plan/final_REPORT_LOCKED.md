# Stage 3 — FINAL REPORT (locked)

Adversarial review of the MRC conformance corpus (fixtures 01, 03, 04, 05, 06,
07, 08, S) and CONVENTIONS.md under plan/plan3.1.md. No fixes applied; no
Stage 4. Delivered in chat to the author; this copy is the locked record.

---

## 1. Procedure, disclosures

- Packets were redacted (document block only + conventions abstract §1–3;
  §4 examples verified absent). plan/ and the §7 author register were never
  shown to Phase A/B reviewers.
- Full chains run: 8 blind (A) + 8 guided (B) + 8 reconciliation (C) + D6.
- **Fixture 06 redo:** the original blind session never returned a completion
  notification; on author authorization a single foreground relaunch ran
  against the identical untouched packet. Original session superseded; if a
  late notification arrives it is discarded (declared here, not silently).
- **Protocol repairs:** fixtures 01 and 03 Phase C reruns with the verbatim
  locked A/B artifacts as explicit inputs; earlier runs superseded.
- **Phase C context caveats (disclosed):** 01, 03 original runs re-derived
  (superseded); 04/05/07/08/S fresh spawns read the lock files; 06 Phase C
  fresh spawn supplied locked inputs and verified packet/fixture byte-identity.
- Lock files are author-transcribed condensations; verbatim originals remain
  in session transcripts (author transcription role disclosed per plan3.1 §8).
- Incident: fixture S Phase C grep surfaced plan3.1 §7; its C2 row recorded
  corroborated-not-sourced.
- Limitations: procedural (not cryptographic) isolation; no VCS — all
  verification content-grep-based, no diff claims.

## 2. Per-fixture findings (all reviewer-verified unless noted)

### Fixture 01 (operator composition) — verdict: faithful-with-omissions
| Sev | Finding | Evidence | Proposed disposition |
|---|---|---|---|
| BLOCKING | `?` carries a settled verdict; refutation performed inside annotation; `derive` never asserts the refutation | `? [W is false: … requires a·f′ = 0]` | Amend fixture expected #4 (currently reads the same `?` positively); add expected finding |
| MAJOR | `product rule` premise undeclared; fixture claims "premises visible in-document" | `from [op, product rule]` | Amend expected #2 |
| MAJOR | counter references W's expression; LHS/RHS shorthand undefined | `counter(f) … RHS` | Record; conventions: claim-reference gap |
| MINOR×4/NOTE×3 | derive template, regularity smuggled into define, f double duty, "for general f" quantifier, schema-vs-object label semantics, notation drift | — | Feed conventions amendments (label/template) |
| Audit | ALL values AGREE (4a²/2a², inequality, a·f′=0 condition); attribution "from the cited guideline" DISAGREE (handle unverifiable) | — | Verified; amend audit wording |

### Fixture 03 (missing prerequisite) — faithful-with-omissions; no BLOCKING
| Sev | Finding | Evidence | Disposition |
|---|---|---|---|
| MAJOR | `c` has no producer node (normal equations co-determine (m,c)) | `from [m]` with c used | Amend expected #2/#4 with structural cause |
| MAJOR | undeclared `g`/domain inside the given; fit family and Var_K(x)>0 silent | "on a declared domain" | Amend expected #6 (contradicted: `?`-list not a complete agenda) |
| MINOR | gloss invented for K; `given NAME:` form; template deviation; two labels named `m`; annotation attachment straddle | — | Conventions amendments; fixture cleanup |
| Negative case | N1 described, not instantiated (no variant document) | — | Instantiate or mark described-only |

### Fixture 04 (conditional) — faithful-with-omissions
| Sev | Finding | Evidence | Disposition |
|---|---|---|---|
| BLOCKING | line-5 `derive step` not entailed — q<1 in no premise (q=1,2 counterexamples) | `derive step from [assume, contractive]` | **Add to expected findings** (absent entirely) |
| MAJOR | unlabeled `[assume]` reference; define-as-factual-premise; `?` unreachable from intended target; completeness absent from `[step]`; if-condition insufficient for then-consequence | — | Conventions: premise tokens + `?` attachment; fixture findings 3/4 corrected |
| Disputed | fixture findings 3/4 assert localization/ancestry as settled that §1 cannot deliver | — | Amend fixture |
| Negative | N1 exhibits condition-drop, but line-5's own condition-drop undesigned | — | Extend negative case |

### Fixture 05 (dimensional) — faithful-with-omissions
| Sev | Finding | Evidence | Disposition |
|---|---|---|---|
| BLOCKING | sole `derive` states no result (no `:`, no result slot) | `derive step from [K, constants] | dimensional check: …` | Add expected finding; conventions: template classification |
| MAJOR | E, p declarations missing from premises; provenance circular (K cited in check of K) | `from [K, constants]` | Amend fixture |
| Fixture | finding 3 gloss accurate of annotation not claim; finding 4 asserts behavior of unexercised variant | — | Amend wording; exercise variant or mark |

### Fixture 06 (novel structure) — faithful-with-omissions
| Sev | Finding | Evidence | Disposition |
|---|---|---|---|
| BLOCKING | empty result slot; `if` condition anaphoric to prose with no antecedent proposition | `derive check from … \| expand both sides…` | Add expected finding (same failure mode as 05/08) |
| MAJOR | circular under literal reading (assume ≡ claim P); else-branch vacuous/unreachable; no `?` on the ambiguity | `assume □ is associative` vs `claim P: … literally` | Add expected finding; amend EF4's "merely conditional + unresolved" |
| MAJOR | interchange/involution laws smuggled into `define` (assert propositions) — ratified by EF3 | `define □: … declared interchange law` | Amend EF3 "honest / recognizable as exactly that" |
| MAJOR | σ used before declaration (the fixture's one machine-checkable defect); stated route misdescribed | line 2 vs line 3 | Add expected finding |
| Fixture metadata | "golden by construction / checkable by inspection" survives only under no-external-claim reading; declared I1 but EF4 is an I2 test; no audit/"what is missing" note | — | Qualify status; fix metadata |
| Negative | N1 (ontology forcing) exhibits its defect verbatim, correctly fenced | — | Verified |

### Fixture 07 (cited result) — faithful-with-omissions
| Sev | Finding | Evidence | Disposition |
|---|---|---|---|
| BLOCKING | `⟨δu⟩=0` needs normalization ⟨1⟩=1; counterexample ⟨f⟩=∫₀²f dx, u≡1 | `assume … declared and linear` | Add expected finding |
| MAJOR | unlabeled `[assume]`; `define fluct` never in premises though load-bearing; `?` attachment ambiguous | `from [theorem_A, assume]` | Amend; conventions: premise tokens |
| Disputed | **EF2's headline anti-pattern criterion is structurally wrong** (N1's premise is a placeholder; faithful form also lists imported result as premise) | — | Rewrite EF2 criterion |
| Audit | no audit block (violates README anatomy item 4); Cov identity AGREE (definitional); line-16 AGREE conditional on ⟨1⟩=1 | — | Add audit/absence note |

### Fixture 08 (competing hypotheses) — faithful-with-omissions
| Sev | Finding | Evidence | Disposition |
|---|---|---|---|
| BLOCKING×2 | sign-difference in none of [H₁,H₂,data]; branch verdicts require undeclared "H₁ predicts s>0" | `derive discriminant …` | Add both expected findings (fixture under-anticipates) |
| MAJOR | `s` never declared; three-valued predicate split two ways (sign(s)=0 refutes); `data` a no-op input; derive result slot empty; `?` names insufficient resolver | — | Amend fixture; conventions: template/`?` |
| Fixture | finding 5 is a transfer rule about a hypothetical document, not a fixture property; finding 3 says "definitions" where the pinned item is an `assume` | — | Relabel; fix wording |

### Fixture S (cosmology, non-golden) — faithful (with overstated claims)
| Sev | Finding | Evidence | Disposition |
|---|---|---|---|
| BLOCKING | "Buchert identity" + "declared domain conditions" unresolvable premises; no `from cited` anywhere | `derive sgn(Q_D) from […]` | Add expected finding (finding 2 claims well-formed) |
| MAJOR | magnitude guard premise-less (no threshold given); no observational datum anywhere; reasoner clause is definition-restatement | — | Add expected findings |
| Disputed C1/C2/C4 | "structurally well-formed" contradicted by unresolvable premises; "cited identity" is annotation-only; promotion-gate names content the document lacks (no Buchert relation/coefficients) | — | Amend all three claims |
| Marking | no-audit discipline holds in four redundant places; negative cases exhibit defects | — | Verified |

## 3. Agreement matrix (compact)

| Fixture | Blind BLOCKING found | In expected findings? | Audit | Verdict |
|---|---|---|---|---|
| 01 | yes (`?` verdict) | **no** (opposite reading given) | all values AGREE | faithful-with-omissions |
| 03 | none | — | none | faithful-with-omissions |
| 04 | yes (line 5) | **no** | none | faithful-with-omissions |
| 05 | yes (result-less) | partial | none | faithful-with-omissions |
| 06 | yes (empty slot) | **no** | none | faithful-with-omissions |
| 07 | yes (normalization) | partial | none | faithful-with-omissions |
| 08 | yes (×2) | partial | none | faithful-with-omissions |
| S | yes (unresolvable) | partial | no-audit claim holds | faithful, overstated claims |

Pattern: **every fixture omits at least one reviewer-confirmed defect; four omit
a BLOCKING one; several affirmatively certify defective structure as clean.**

## 4. D6 CONVENTIONS review (independent, plan/ quarantined)
- BLOCKING ×4: F2 label undefined + "references to earlier labels" vs the
  page's own non-label premises; F3 `given NAME =` vs every example and all
  nine fixtures using `given NAME:`; F4 `from` defined only on `given` but
  used on `assume`/`claim` in §4.3 itself and fixture 07; F5 invariant scope
  (§2 preamble's artifacts vs I3's document-scope; §3 "Nothing else" vs I1/I3
  enforcement vocabulary).
- MAJOR ×8 (attachment, layouts, "only inference construct", template
  deviations unclassified, if-citability, declare-before-use undecidable, I3
  unfalsifiable, ceiling subject ambiguity), MINOR/NOTE ×14, gaps G1–G8
  (no `?` lifecycle; no referenceable conditional; provenance beyond given).
- Ceiling cross-check: **none of the six permitted assertions needs
  mathematical knowledge** — every flagged non-decidability is a definitional
  hole, repairable by clarificatory amendment.
- Five adjudications: 2a labels-only (insufficient text); 2b genuinely
  unsettled; 2c indeterminable intent; 2d inseparable table-vs-example split;
  2e undefined by silence.

## 5. Consolidated assessment (recommended; author disposes)

**PASS-WITH-AMENDMENTS** — argued from: (i) all eight documents are
expressible in the seven constructs (fixture 06's blind reviewer stated none
of its defects is a vocabulary failure); (ii) no reviewer found an invariant
violation presented as valid, and every deliberate anti-pattern was fenced;
(iii) all independently re-derived audit values agree; (iv) against that, D6
found four internal contradictions blocking a spec, and the corpus's
expected-findings sections systematically under-record defects.

**Minimal amendments indicated (described, not applied):**
1. Define "label" and the premise-token classes; state the forward-reference
   rule and token-matches-no-label status.
2. Define `?` attachment operationally ("statement", "standalone", branch
   scoping).
3. Settle `from`'s scope (which constructs carry provenance) — reconcile §1
   with §4.3.
4. Classify derive-template deviations (required vs descriptive).
5. Reconcile invariant scope and the §2/§3 enforcement-vocabulary conflict.
6. State declare-before-use's operational scope; state if-condition
   citability as recorded intent (either way).
7. Corpus-side: expected-findings completeness discipline; fixture metadata
   consistency (construct lists, invariant declarations); instantiate or mark
   described-only negative cases; qualify "golden by construction" lines.

## 6. §7 preliminary-observations comparison

**CONFIRMED** (independent review agrees): 01-a product rule/differentiability;
03 good-test shape; 04 `?`-attachment ambiguity; 07 normalization + unlabeled
assume; 08 sign-difference + sign(s)=0 gap; S "cited identity" miscategoried;
06 circularity — *refined*: confirmed under the literal reading, root cause is
the undischarged ambiguity (blind reviewer rated the ambiguity MAJOR, the
collision Blocking-tier under reading A); cross `[assume]` — confirmed and
**extended** to five fixtures (04, 06, 07, 08, S) and adjudicated by D6.

**DISPUTED**: 04's `0≤q<1` sub-claim — blind re-derivation shows the Cauchy
conclusion true for all real q<1 (q<0 forces a constant sequence); the
"decreasing geometric majorant" phrase fails for q<0 but the truth-condition
does not. Register's math note is contradicted; its attachment note stands.

**UNRESOLVED**: 01-b README-mode question (README outside packet scope — not
tested); 05's I2-forbidden-direction half (no reviewer adjudicated it).
Register was conservative overall: independent review produced major findings
absent from it (04 line-5, 05 result-less derive, 01 `?`-verdict, 07 EF2,
all of D6).

## 7. Verified vs unresolved

**Verified (checks actually run):** blind re-derivation of every `derive` in
all eight documents (each by an independent reviewer; fixture 01 by two
pass-runs with matching values); value-by-value audit comparison for 01;
no-audit claims for 03/04/05/06/07/08/S verified as absent; negative-case
exhibition checked case by case (exceptions noted: 03 N1 described-only, S N1
shallow, 04 N1 partial); packet/fixture byte-identity for 06; §4 redaction of
Phase A packets; D6 clause-by-clause read of CONVENTIONS.md.

**Unresolved (carried forward, not established):**
1. Fixture 02's lowering-domain conditions (intentionally open).
2. 01 README-mode vs header-shape question (out of scope this pass).
3. 05 I2-direction question (not adjudicated by any reviewer).
4. Fixture 06 original session fate (never notified; output never seen).
5. Late superseded notification may still arrive (will be discarded).
6. Lock files are author-condensed; verbatim only in transcripts.
7. No VCS — no diff-based verification possible.
8. stage2.md "seven vs eight" miscount — queued one-word fix, needs separate
   author authorization.
9. I1 guide-dependent tests vacuous until MRC_GUIDE exists.
10. D6's four BLOCKINGs await the author's adjudication (independent, not
    yet confirmed-by-adjudication).
11. Procedural-only isolation (not cryptographic).

**Boundary:** Stage 3 ends here. No fixture, convention, plan, or code file was
modified. Disposition decisions and any Stage 4 preparation require separate
authorization.
