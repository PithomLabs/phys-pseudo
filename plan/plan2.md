# Implementation Plan v2 — Minimal Phys MRC Pseudocode (Revised after review)

**Repository:** `/home/chaschel/Documents/go/phys-pseudo`
**Module path:** `github.com/PithomLabs/phys-pseudo`
**Status:** approved baseline after architect review (v2 + correction delta of this revision). Sequence Stage 1 → Stage 2 → Stage 3 → Stage 4 approved. Implementation not started.

## Review disposition

Three blockers from review, all accepted:

1. **Sequencing formalized too early** — accepted. The v1 plan contradicted the confirmed "loose convention first" decision by putting a normative spec (grammar, exact semantics, status engine) in Stage 0 before any corpus existed. Fixed by reversing: conventions → corpus → adversarial stabilization → spec + checker.
2. **Computed-status rules made unjustified scientific claims** — accepted and sharpened. Not just "defer three labels"; the implication direction was wrong in principle, in any milestone. Fixed by replacing computed *status* with inspectable *dependency provenance*: facts, never verdicts.
3. **Cosmology examples fail their own audit role** — accepted. The canonical "source-fidelity" example used a Buchert acceleration equation with wrong coefficients (`−4πG⟨S⟩_D + 2𝒬_D/3` vs. the standard irrotational-dust Λ=0 form `3 ä_D/a_D = −4πG⟨ρ⟩_D + 𝒬_D`, equivalently `ä_D/a_D = −(4πG/3)⟨ρ⟩_D + 𝒬_D/3`), an undefined `𝒬_D`, and ambiguous `S, S_ij` tensor notation. Fixed by a binding fixture audit rule: golden status requires primary-source equation check + independent derivation; otherwise symbolic toys or explicitly marked sketches.

Plus a final simplification from review, adopted with one strengthening: the advisory guide stays strictly advisory this milestone; no guide-derived validator until the corpus demonstrates real need.

**Correction delta (second review round), all accepted:**

1. **Wrong counterexample in the golden operator-composition fixture** — accepted. Independently re-derived from the operator definition: (a∂ₐ)²f = a f′ + a² f″; for f = a² this is 4a², while a²∂ₐ²f = 2a² (v2's scratch value `4a²·... check a³` was wrong). Fixed in A.4 before corpus entry — this is exactly why expected results must be derived independently of any implementation or sketch.
2. **Audit rule refinement** — accepted. One principle, two variants: published-paper equations are audited against the original source plus independent derivation; elementary mathematical identities are audited against the operator/axiom definition plus independent working. Not every mathematical fixture needs a physics paper as its primary source.
3. **Sequencing and fixture sources (architect answers)** — recorded under "Fixture-source decisions" below; Raychaudhuri fixture deferred pending verification; first cut uses auditable examples + symbolic toys; ladder-operator conditional on independent check.

## What the review confirmed as correct (retained unchanged)

- Seven-construct vocabulary: `given`, `define`, `assume`, `claim`, `derive`, `if/then/else`, `?`.
- `reality_check.md` knowledge lives in a separate, inspectable advisory guide — never in the syntax.
- Markdown conformance corpus is the primary test of the language; expected findings are recognition-level, not prescribed wording.
- Paper extraction and independently reconstructed reasoning stay distinguishable (`claim` vs. annotated `derive`).
- Existing Phys library boundaries respected; no reverse dependencies, no ontology duplication.

---

## Revised architecture decisions

### D1 — Advisory guide, strictly advisory

```text
Layer 1 — the language        7 constructs, theory-neutral, no branch list
Layer 2 — the advisory guide  MRC_GUIDE: shines / silent / partial, inspectable,
                              conditional on framework and regime, challengeable
Layer 3 — local annotation    ? at the step where a gap bites
```

Normative constraint on the guide (to appear in the conventions page):

> The guide may only ever motivate an annotation. It may never appear in a rejection, a status, or a required field.

This sentence is the ratchet-stop: without it, advisory knowledge tends to reintroduce itself as a registry. The guide cannot reject unfamiliar mathematical structures, cannot supply an ontology, and entries claiming universal limits ("mathematics can never…") are out of bounds — entries state what a *framework under stated assumptions* does not establish. Agents may record counterexamples to any entry and continue exploring.

### D2 — Loose convention first, spec last

The seven constructs are usage conventions in milestones 1–3, not grammar productions. Free-form math notation and prose on every right-hand side. `PSEUDO.md` is written only after real fixtures demonstrate which rules are necessary — it records conventions that survived adversarial use, not rules designed in advance.

### D3 — Facts, not verdicts (replaces v1's "computed status")

**The language makes epistemic structure inspectable; it makes no epistemic verdicts.**

What document structure provides (facts about the document):

- a conclusion's dependency set — which premises, assumptions, and cited inputs it rests on;
- where `?` occurs in that dependency set;
- whether a step is written as `derive` or `claim`;
- whether measured or cited `given`s appear in the ancestry.

What structure never provides, in any milestone:

- that an inference is *valid* — a `derive` with clean ancestry can simply be wrong;
- that a framework use is *appropriate here* — a guide match does not prove applicability in this model;
- that a measurement *supports* the claim — a relevant datum in the ancestry may contradict it.

Permitted recognition statement (model for all tooling and fixtures): *the conclusion depends on assumption A and unresolved step B.*
Forbidden inference: *therefore the conclusion is true* — or false.

The no-smuggling invariant survives in its honest, purely syntactic form: `claim` vs `derive` is a syntactic distinction with no truth import, and no author-typed status exists (an attempt like `claim H: PROVEN that…` is a greppable spec violation, never licensed by any construct). This aligns with `phys-trace/AGENTS.md` §8: even replayed execution does not upgrade a claim, so a parseable document certainly will not.

### D4 — Fixture audit rule (golden status discipline), two variants of one principle

> **Fixture audit rule.** *Published-paper equation:* verify the original source and independently check the derivation. *Elementary mathematical identity:* verify the operator/axiom definition and independently work through the mathematics. Same principle — independent verification against an authority external to the fixture; different authority, so not every mathematical fixture needs a physics paper as its primary source. The independent check must never be generated from the implementation or sketch under test. Fixtures failing their applicable variant are allowed only as explicitly marked illustrative sketches with no golden status, or replaced by symbolic toy examples.

---

## Deliverable A — Canonical minimal pseudocode (revised)

### A.1 The language

```text
statement  ::= [ label ":" ] construct " " content
construct  ::= "given" | "define" | "assume" | "claim" | "derive"
             | "if" ... ":" ("then" ... | "else" ...) | "?"
```

(Shown as shape only; it becomes grammar when Stage 4 freezes it.)

| Construct | Exact semantics |
|---|---|
| `given NAME = <content> [from <source>]` | Declares an input: measured data, a cited result, established mathematics, or the problem statement. Provenance is an inline `from` clause — `from measured @Planck2018`, `from cited @Buchert1997`, `from paper §3 eq. (12)` — never a metadata object. |
| `define NAME := <meaning>` | Establishes the mathematical meaning of a symbol or operation. Domain/type/dimension annotations go in the right-hand side when the reasoning needs them. Creates meaning; asserts no proposition. |
| `assume <premise> [as LABEL]` | A premise accepted provisionally or within a declared model/regime. Named only if later steps must reference it. Falsity of an `assume` delimits, not refutes, downstream reasoning. |
| `claim LABEL: <proposition>` | States a proposition without presuming it is true and without attaching premises. The object under investigation: paper conclusion, conjecture, competitor hypothesis. |
| `derive LABEL: <result> from <premises> [\| <reasoning>]` | The only inference construct. Asserts the result follows from the named premises by the stated reasoning. Free-form reasoning after `\|`. |
| `if <condition>: then <consequence> [else <alternative>]` | Conditional reasoning. Branch statements hold only under the branch condition. `else` optional. |
| `? <annotation>` | Marks an ambiguity, missing premise, unjustified step, or unresolved prerequisite. Attaches to the nearest preceding statement; a standalone `?` is a document-level open question. States what is undetermined and what would resolve it. |

Optional `label:` prefixes exist solely for premise referencing. No document must use every construct.

### A.2 What counts as what

- **Declaration:** `given`, `define`, `assume` — introduces content, asserts no inference.
- **Mathematical inference:** `derive` — "this follows from that."
- **Conditional result:** any statement inside `then`/`else` — visibly conditional.
- **Unresolved step:** any statement carrying (or depending on) a `?`.

### A.3 Dependency provenance (replaces v1's computed-status rules)

No author writes a status label. Tooling may compute and report only *structural facts*:

```text
depends_on(s)  = labels in s's premise references (transitive)
unresolved(s)  = ? occurs in depends_on(s)
mode(s)        = s is a claim | s is a derive | s is inside an if-branch
inputs(s)      = kinds of given's in depends_on(s): measured | cited | paper | problem
```

These are inputs to review, never outputs of it. Nothing in this block licenses the words justified, applicable, proven, supported, or true. The complete set of system-level assertions is: *the document parses; references resolve; the graph is acyclic; these dependencies exist.* Everything else is a human/agent/proof-tool judgment.

### A.4 Smallest complete examples

**Exploratory hypothesis** (schematic, marked illustrative; establishes nothing):

```text
given question: "can structure alone account for the observed acceleration?"
define Q_D := [kinematical backreaction scalar averaged on domain D]
assume dust, irrotational motion, foliation {t} = const, compact domain D
claim H: the Q_D contribution can reproduce the observed acceleration magnitude
derive sgn(Q_D) from [Buchert identity, declared domain conditions] | [volume average]
    ? [no admissible solution (g, D) is supplied; magnitude of Q_D not computable]
if |Q_D| >= [required magnitude]:
    then H holds within this model
else:
    H fails within this model
? [observational adequacy is not addressed by this argument]
```

Marked as an illustrative sketch: its physics content is unaudited and it carries no golden status (D4). It demonstrates *shape*, not Buchert equations.

**Audited mathematical example** (golden candidate, no cosmology; elementary-identity audit — operator definition + independent derivation, values verified below):

```text
# operator composition — audited in phys-trace DERIVATION_SPEC_GUIDELINES.md §6
given op: (a·∂ₐ)² f = a·∂ₐ(a·∂ₐ f)   from cited @project-guidelines
claim W: (a·∂ₐ)² f equals a²·∂ₐ²f for general f
derive expand(f) from [op, product rule] | (a∂ₐ)²f = a∂ₐ(a·f′) = a·(f′ + a·f″) = a f′ + a² f″
derive counter(f) from [expand(f)] | f(a) = a² ⇒ LHS = 4a², RHS = 2a²
    ? [W is false: af′ + a²f″ = a²f″ requires a·f′ = 0]
```

Independently derived audit values (this derivation *is* the audit record; it must never be regenerated from any implementation): with f(a) = a², f′ = 2a, f″ = 2, so (a∂ₐ)²f = a·2a + a²·2 = 4a², while a²∂ₐ²f = a²·2 = 2a². The equality fails for any f with a·f′ ≠ 0.

**Published-paper shape** (structure only until audited):

```text
# source: <paper>, §N — ILLUSTRATIVE SKETCH, no golden status until audited
given law: [the paper's stated field equation]        from paper eq. (N)
define q := [the paper's defining relation]
assume [the paper's stated assumptions]                from paper §N
derive step_1 from [law, q] | [the displayed reasoning]
    ? [paper omits this intermediate step]
claim result: [the paper's conclusion]                 from paper, conclusion
    ? [asserted; displayed derivation stops at step_1]
```

Fidelity mechanics: authors' derived step = `derive` with visible premises; imported theorem = `given ... from cited`; conclusion without displayed derivation = `claim` + `?`. Agent reconstructions are separate `derive`s with their own premises and attribution in the annotation. Exploration and extraction remain the same language.

### A.5 Construct-by-construct justification (unchanged from v1, retained)

- **`given` vs `assume`:** input-the-reasoning-starts-from vs premise-borrowed-provisionally. Falsified data invalidate; falsified assumptions delimit. Claude's `measured|postulated` pair dissolves into the `from` clause + construct choice.
- **`define` vs `given`:** meaning-creation vs input-import. Guards against PhysTrace Lesson 1's `rho_Q`/`Q` identity loss: definitions carry defining relations visibly.
- **`claim`:** without it, assertions are either smuggled in as `given` (overstating) or dropped (unfaithful).
- **`derive`:** the only inference; removing it erases the derivation/assertion distinction.
- **`if/then/else`:** binds consequents to conditions structurally instead of prose qualifiers.
- **`?`:** the MRC surfacing mechanism; gaps stay local instead of escalating into status fields.
- **Rejected:** `want ... vs N` (two `claim`s + one `if` suffice); `hypothesis` (identical to `claim`); `input` (⊂ `given`); `cite` (⊂ `from` clause).

---

## Deliverable B — MRC semantics (revised)

### B.1 The check ladder

Ordered, cheapest first. In milestones 1–3 these are reasoning obligations documented in fixtures; only the first two become mechanical at Stage 4.

1. **Reference checks (mechanical):** premises exist; symbols declared before use; dependency graph acyclic.
2. **Fidelity checks (mechanical-lite, paper mode):** a `from paper` statement written as `derive` must show premises and reasoning in-document; otherwise it must be `claim` or `given ... from cited`. This is the mechanical anti-upgrade rule.
3. **Compatibility checks (mechanical where annotated):** dimension/type annotations on `define`s flag incompatible combinations in a step; absent annotations → explicit review question, never silently assumed, never pretended-checked.
4. **Entailment check (reasoned, never mechanical):** does the conclusion follow from the cited premises? The agent asserts it in the `derive`; review tests it; when unjustifiable, the honest encoding is `?` on that step — the system does not and will not certify it.
5. **Applicability check (advisory):** consult the guide. A documented silence for the declared framework (initial conditions, vacuum/coupling/Born-rule selection from pure math, …) motivates an annotation at that step. It cannot reject the step (D1).
6. **Propagation (mechanical, structural):** weakest-ancestor rule over *facts*: any `?` upstream marks the ancestry unresolved; any `assume` upstream makes resting conclusions structurally conditional; unresolved does not halt — downstream reasoning continues as conditional and can never be presented as established, because "established" was never a thing the system grants. The `?` list is the agenda.

### B.2 The four distinctions, restated under D3

| Distinction | Inspectable in the document | Verdict obtainable from structure? |
|---|---|---|
| Syntactically representable | it parses under the conventions | yes (and it is the *only* verdict) |
| Mathematically justified | step is `derive`, no `?` in ancestry | **no** — validity requires proof/review |
| Physically applicable | framework assumptions in ancestry; guide match | **no** — requires expert judgment |
| Empirically supported | measured `given`s in ancestry | **no** — a datum may contradict the claim |

The left column is what tooling reports. The right column is permanent: these verdicts belong to proof tools, external math systems, and expert review — never to the pseudocode layer.

**Mapping to PhysTrace evidence classes** (no duplication): `given ... from cited` ↔ SOURCE_CITES_EXTERNAL_RESULT; paper assertion as `claim` ↔ SOURCE_ASSERTS_OR_SKETCHES; annotated reconstruction ↔ SPEC_INFERENCE; `?` ↔ UNRESOLVED; `derive` with visible source steps ↔ EXPLICIT_SOURCE. Pseudocode is the front end; PhysTrace remains the normative ingestion standard.

### B.3 What MRC does not do

No proof of entailment, no execution, no scoring, no aggregation. No score exists that could conceal a failed dependency. Passing structural checks means: parses, references resolve, graph acyclic, provenance clauses present. Nothing more.

---

## Deliverable C — Conformance corpus (revised)

Markdown corpus, `conformance/`. Each fixture pairs a pseudocode document with recognition-level expected findings (never prescribed wording), a rationale, and a failure-adjudication note.

| # | Fixture | Domain | Mode | Golden? | What it tests |
|---|---|---|---|---|---|
| 1 | Audited operator composition | math-physics (`(a∂ₐ)²f` case) | paper | **golden** (audit values independently derived, see A.4) | Derived step vs imported rule vs false claim; anti-golden for the known wrong form; expected values 4a² vs 2a² for f = a². |
| 2 | Ladder-operator spectrum | QM (textbook algebra) | paper | **golden only after** its assumptions and expected derivation are independently checked | Assumptions, imported CCR postulate, derived steps, asserted conclusion — distinguishable. |
| 3 | Symbolic missing prerequisite | toy symbolic chain | exploration | golden (by construction) | Omitted step marked `?` where it matters; downstream usable conditionally. |
| 4 | Conditional reasoning | symbolic toy (stat-phys ensemble equivalence demoted to later, source-dependent replacement) | both | golden (by construction) | `if/then` binds consequent to condition; competing branch open. |
| 5 | Dimensional mismatch | toy annotated units | exploration | golden (by construction) | Incompatible combination surfaced; fixture documents mechanical vs. review split. |
| 6 | Novel structure | proposed bracket, no branch | exploration | n/a | Expressible with zero new keywords; no branch classification required. |
| 7 | Cited result + anti-pattern | Raychaudhuri imported — **deferred from first cut** | paper | not yet — enters only when exact equation, conventions, and source mapping are verified (Ellis–van Elst is a candidate to evaluate, not an approval) | `given ... from cited` not rewritten as `derive`; anti-pattern included as negative case. First cut uses a symbolic cited theorem with the same structure. |
| 8 | Competing hypotheses | two toy claims, shared premises | exploration | golden (by construction) | Two claims, one `if`; neither treated as failed proof of the other. |
| S | Cosmology backreaction sketch (A.4) | GR | exploration | **illustrative only** | Shape demo; explicitly un-audited; cannot be promoted without D4 audit. |

Coverage requirements: each construct exercised by ≥1 golden fixture; ≥2 pure exploration, ≥2 pure paper; cosmology content present only as marked sketches until audited.

**Failure adjudication rule:** a failure is a *language* change only if no arrangement of the seven constructs can express the distinction the fixture protects. Otherwise classify as: usage convention | advisory-guide update | future library capability (PhysMath/PhysLib).

**Audit rule for promotion:** any fixture promoted to golden or physics-authoritative status must pass D4 (primary-source equation check + independent derivation, never generated from any implementation).

---

## Deliverable D — Revised roadmap (the approved sequence)

```text
Stage 1  Provisional conventions
Stage 2  Conformance corpus
Stage 3  Adversarial review + language stabilization
Stage 4  Minimal specification (PSEUDO.md) + optional shallow checker
```

### Stage 1 — Provisional conventions
- **Work:** one page defining the 7 constructs, usage notes, and 2–3 minimal examples (the A.1/A.4 material). Includes verbatim: the D1 guide constraint, the D3 facts-not-verdicts invariant, and the no-status-label rule. Explicitly non-normative. No grammar, no parser, no status engine, no library integration.
- **Depends on:** nothing.
- **Acceptance:** a reader can produce a document and a reader can parse one; every construct has its A.5 justification; zero scientific verdicts claimed anywhere.

### Stage 2 — Conformance corpus
- **Work:** the fixtures of Deliverable C, each with document, expected recognition-level findings, rationale, and adjudication note. Auditable fixtures first (1, 2); symbolic toys for the rest; cosmology only as marked sketches.
- **Depends on:** Stage 1.
- **Acceptance:** all seven constructs covered by golden fixtures; both modes represented; every golden physics equation passes D4 audit or is replaced by a toy; expected findings state recognition obligations, never wording.

### Stage 3 — Adversarial review + stabilization
- **Work:** run counterexample attacks (v1 Deliverable E's ten cases, revised under D3) against corpus and conventions. Classify every failure: syntax change / usage convention / guide update / future library capability. Revise vocabulary only on demonstrated representational failure; record every rejected revision with its reason.
- **Depends on:** Stage 2.
- **Acceptance:** each counterexample has a written verdict; any convention change cites the failing example that motivated it; the seven-keyword count holds or is justified by demonstrated failure.

### Stage 4 — Minimal specification + optional shallow checker
- **Work:** (a) `PSEUDO.md` — versioned, recording conventions that survived Stage 3, not rules designed in advance. (b) Shallow Go checker (module `github.com/PithomLabs/phys-pseudo`) validating only demonstrated structural needs: unresolved references, circular dependencies, unknown construct words, definition-before-use. Docs state in the first paragraph: passing proves nothing mathematical.
- **Depends on:** Stage 3.
- **Acceptance:** corpus passes; mutated corpus (broken refs, cycles, undeclared symbols, unknown keywords) fails at the intended boundary; no fixture, construct, or document is rejected on guide grounds (D1); spec contains no physics-branch list and no dependency on any Phys library's current capabilities.

### Explicitly deferred (trigger-gated, not scheduled)
- **Guide-derived advisory warnings:** re-enter only when the corpus demonstrates a concrete need; even then advisory-only, never a rejection path.
- **Stage 5-type integration with Phys stack** (PhysTrace front-matter mapping, anti-golden reuse): when a real paper-extraction workflow chooses to use the layer.
- **Host language/layout decisions for anything beyond the Stage 4 checker:** recorded with rationale when reached.

### Mechanical vs. reasoned (unchanged from v1, binding)

| Mechanically enforceable | Requires proof, tool, or expert |
|---|---|
| Statement vocabulary, label/reference resolution, acyclicity | Whether a `derive`'s inference is valid |
| `derive`-fidelity in paper mode (premises/reasoning visible) | Whether a `define` matches the source's meaning |
| Dimension/type consistency where annotated | Compatibility where annotations are absent |
| `?` attachment completeness | Whether an assumption is physically appropriate |
| Absence of author-typed status labels (greppable) | Whether guide entries are correct — challengeable by design |

### Explicit non-goals (roadmap law)

No Claravine-style API, no transactions or two-phase commit, no exploration/paper mode flag, no universal operator registry, no proof engine or solver, no ontology duplicating PhysMath/PhysLib, no prescribed research-stage sequence, no confidence scores, **no computed scientific statuses of any kind, in any milestone.**

### Recorded uncertainties (not invented)

1. `phys-pseudo` has no module, license, or `AGENTS.md` yet; created at Stage 4 (module) and Stage 1 (conventions page can live without them).
2. Whether `phys-system/AGENTS.md`'s component map should list `phys-pseudo` is a collective-authority change — flagged, not assumed.
3. MRC guide provenance: `reality_check.md` is internal research material; distilled entries need attribution; publication status is a licensing decision.
4. Stat-phys fixture source: resolved for first cut — symbolic toy; a physics source may replace it later under D4 (see Fixture-source decisions below).

---

## Deliverable E — Adversarial counterexamples (revised under D3)

1. **Circular derivation** — representable; caught mechanically (acyclicity). No language change.
2. **Undeclared symbol** — representable; caught mechanically (definition-before-use). No change.
3. **Paper asserts with zero derivation** — representable as `claim` + `?`. No change; core fidelity test.
4. **Mid-document assumption retraction** — convention gap, not vocabulary: supersession statement + re-derived or `?`-marked downstream. No keyword.
5. **Inductive / n-th order reasoning** — free-prose right-hand side; premise ambiguity flagged as corpus re-test case; fix if needed is a referencing convention, not a loop construct.
6. **Dimensionally inconsistent step presented as derived** — representable and misrepresentable *by design*; structure records the lie's shape; review catches it. Under D3 the checker's role is exactly: report annotated-type inconsistency where annotations exist — and make no claim beyond that. No language change.
7. **Disagreeing reviewers on one inference** — counter-`claim` + `?` on the disputed `derive`. Disagreement is data; no status field needed.
8. **Opaque undefined object from a cited theorem** — `given ... from cited` + `define` marked opaque; per PhysTrace rule "state the limit rather than pretending evaluation." No change.
9. **Status smuggling** (`claim H: PROVEN that…`) — no construct licenses it; greppable spec violation; computed-provenance ignores it. Handled without grammar.
10. **Genuinely new mathematical structure** — expressible by design (fixture 6); the one failure class that would justify revision; none found.

**Result:** zero new keywords. Two convention amendments (supersession; opaque definitions) and two re-test flags (induction; annotation-wording level) fold into Stages 1–3. Vocabulary stands at seven.

---

## Acceptance-criteria mapping (task §8, re-checked against revision)

1. *One language for both modes* — A.4 examples + fixtures 1–8 mix both. ✔
2. *Every construct non-redundant* — A.5 ledger with rejected candidates named. ✔
3. *MRC visible at point of use* — B.1 checks 3–5 surface at the step; `?` is local. ✔
4. *Conjectures explorable, never promoted* — D3: promotion was never structurally possible; fixture 1/S. ✔
5. *Assertions / derivations / agent inferences distinguishable* — `claim` vs `derive` vs annotated reconstruction; B.2 mapping. ✔
6. *Conditional continuation without silent promotion* — B.1 propagation over facts only. ✔
7. *Not tied to theory, branch, or library* — no branch list; guide advisory + challengeable; fixture 6. ✔
8. *Testable without proving math* — Stage 4 scope + mechanical/reasoned table + D3 verdict column. ✔
9. *No scope expansion into infrastructure* — non-goals + deferred list with triggers. ✔
10. *(new) No unjustified scientific claims by the tooling itself* — D3 invariant in Stage 1 and Stage 4 acceptance. ✔

---

## Fixture-source decisions (architect answers — resolved)

**Sequencing (was Question 1):** APPROVED as baseline — Stage 1 → Stage 2 → Stage 3 → Stage 4. Begin with provisional conventions, build the Markdown corpus, challenge it with counterexamples, then freeze the surviving conventions into `PSEUDO.md`. The checker remains optional and shallow and must never certify mathematical truth.

**Fixture sources (was Question 2):** the two auditable examples plus symbolic/toy fixtures for the first corpus cut.

- Operator-composition fixture: corrected before entering the golden corpus — expected values independently derived (LHS 4a², RHS 2a² for f = a²; see A.4).
- Ladder-operator fixture: retained only after its assumptions and expected derivation are independently checked.
- Conditional reasoning and missing prerequisites: symbolic examples for the first cut; no milestone delayed while selecting additional physics references.
- Raychaudhuri fixture: added only when its exact cited equation, conventions, and source mapping are verified. Ellis–van Elst is a possible reference to evaluate, not an automatic approval.

**Standing constraint, binding throughout implementation:** the system may report which assumptions, citations, and unresolved annotations a conclusion depends upon. It must not infer that the conclusion is true merely because its references resolve or because no `?` appears in its ancestry (D3). Any checker output, fixture expectation, or spec sentence crossing this boundary is a defect regardless of stage.

**Architect verdict:** proceed with Stage 1; correct the operator-composition fixture before it enters the golden corpus (done, A.4); use the first conformance round to discover whether the seven constructs genuinely suffice across exploratory reasoning and source-faithful derivations. No further architecture expansion.
