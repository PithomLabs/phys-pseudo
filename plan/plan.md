# Implementation Plan — Minimal Phys MRC Pseudocode

**Repository:** `/home/chaschel/Documents/go/phys-pseudo`
**Module path:** `github.com/PithomLabs/phys-pseudo`
**Status:** approved design; implementation not yet started. `phys-pseudo/` currently contains only `plan/`.

## Preamble: what governs this plan

Authority, as established by `phys-system/AGENTS.md` §21 and respected throughout:

- `phys/AGENTS.md` is frozen and untouched; `phys` and `phys-gr` are evidence only.
- `phys-math`, `phys-lib`, `phys-artifact`, `phys-trace` contracts are read-only inputs here. Their relevant invariants: no physical meaning in theory-neutral layers; no silent promotion of assertions to derivations; formal validity ≠ empirical truth; evidence levels (represented → structurally validated → executed → replayed → interpreted → empirically supported) are not interchangeable.
- `phys-trace/DERIVATION_SPEC_GUIDELINES.md` §3 already defines evidence classes (EXPLICIT_SOURCE, SOURCE_CITES_EXTERNAL_RESULT, SOURCE_ASSERTS_OR_SKETCHES, SPEC_INFERENCE, UNRESOLVED). The pseudocode vocabulary must map onto these without duplicating them — the mapping table is in Deliverable B.
- Anything uncertain about the repository is recorded in Deliverable D rather than invented.

## Architectural decisions (confirmed)

1. **Silence knowledge lives in an advisory layer, not the language.** The 7-construct language stays domain-free. The `reality_check.md` shines/silent/partial knowledge becomes a separate, explicit, inspectable MRC reasoning guide (`MRC_GUIDE.md`) that agents consult when annotating steps. Nothing in the syntax depends on it. The guide is challengeable: an agent may record a counterexample to a documented silence and continue exploring. Annotations must remain conditional on the actual framework and declared assumptions — never universal claims about what mathematics can never establish.
2. **Loose convention first, strict grammar later.** The seven constructs are conventions, not mandatory grammar productions, in the first milestone. Free-form mathematical notation and prose on every right-hand side. Validation stays deliberately shallow. Grammar formalizes only after a diverse corpus of real extractions reveals stable patterns.
3. **Conformance suite = markdown fixtures + expected MRC findings.** Go tests follow only after real examples demonstrate which conventions are stable. Expected findings are recognition-level obligations ("the conclusion depends on an unstated initial condition"), never prescribed annotation wording.

---

## Deliverable A — Canonical minimal pseudocode

### A.1 The language, smallest useful form

Seven constructs. No mode flag, no status labels, no operator catalogue, no metadata records.

```text
statement  ::= [ label ":" ] construct " " content
construct  ::= "given" | "define" | "assume" | "claim" | "derive"
             | "if" ... ":" ("then" ... | "else" ...) | "?"
```

| Construct | Exact semantics |
|---|---|
| `given NAME = <content> [from <source>]` | Declares an input the reasoning starts from: measured data, a cited result, established mathematics, or the problem statement itself. Provenance is an inline `from` clause — `from measured @Planck2018`, `from cited @Buchert1997`, `from paper §3 eq. (12)` — never a metadata object. A `given` asserts nothing about how the content was obtained; the `from` clause records it. |
| `define NAME := <meaning>` | Establishes the mathematical meaning of a symbol, object, or operation. Domain, type, dimension, and convention information belongs in the right-hand side *when the reasoning needs it* (`define a_D := (V_D/V_0)^(1/3), a_D : ℝ⁺`). `define` creates meaning; it asserts no proposition. |
| `assume <premise> [as LABEL]` | States a premise accepted provisionally or within a declared model/regime. Named only if later steps must reference it. An `assume` is a declaration whose falsity would invalidate, not falsify, everything downstream. |
| `claim LABEL: <proposition>` | States a proposition without presuming it is true and without attaching premises. A claim is the *object under investigation*: the paper's conclusion, the explorer's conjecture, a competitor hypothesis. |
| `derive LABEL: <result> from <premises> [| <reasoning>]` | The only inference construct. Asserts the result follows from the named premises by the stated reasoning. Premises are references to previously declared or derived labels. The right-hand side after `|` carries the reasoning in free form. |
| `if <condition>: then <consequence> [else <alternative>]` | Conditional reasoning. A statement inside a branch is established *only under the branch condition*. Conditions may reference claims, defines, or derived quantities. `else` is optional. |
| `? <annotation>` | Marks a meaningful ambiguity, missing premise, unjustified step, or unresolved prerequisite. Attaches to the nearest preceding statement; a standalone `?` (no preceding statement it modifies) is a document-level open question. The annotation states *what is undetermined and what would resolve it*, at the point where it matters. |

Optional `label:` prefixes exist solely so premises can be referenced. Free-form mathematical notation and prose are allowed on every right-hand side. Nothing requires a document to use every construct.

### A.2 What counts as what

- **Declaration:** `given`, `define`, `assume`. Introduces content; asserts no inference.
- **Mathematical inference:** `derive`. The single construct that says "this follows from that."
- **Conditional result:** any statement inside a `then`/`else` branch. Its justification is permanently visibly conditional on the branch condition.
- **Unresolved step:** any statement carrying (or transitively depending on) a `?`.

### A.3 Epistemic status is computed, never typed

No author ever writes a status label. Status is recovered from document structure:

```text
status(s) =
  asserted(s)            if s is a claim, or a derive whose own step carries ?
  unresolved(s)          if ? occurs in s's ancestry (premise chain)
  conditional(s, C)      if s sits inside an if-branch, or rests on assumes
  derived-from(P)        otherwise, with P = the declared premises in its ancestry
```

Derived from structure, not declared — this is the design's load-bearing decision. A statement's epistemic state is what the document's dependency graph says it is; there is no way to write "PROVEN" onto a claim, and no way for an assertion to masquerade as a derivation, because there is no construct that blurs the `claim`/`derive` boundary. Empirical support is not a status at all: it is simply whether measured `given`s appear in the ancestry.

### A.4 Smallest complete examples

**Exploratory hypothesis** (schematic; establishes nothing):

```text
given question: "can structure alone account for the observed acceleration?"
define Q_D := [kinematical backreaction scalar averaged on domain D]
assume dust, irrotational motion, foliation {t} = const, compact domain D
claim H: the Q_D contribution can reproduce the observed acceleration magnitude
derive sgn(Q_D) from [Buchert identity, declared domain conditions] | [volume average of Raychaudhuri]
    ? [no admissible solution (g, D) is supplied; magnitude of Q_D not computable]
if |Q_D| >= [required magnitude]:
    then H holds within this model
else:
    H fails within this model
? [observational adequacy is not addressed by this argument]
```

**Published-paper derivation** (schematic; source-faithful; establishes nothing):

```text
# source: averaged GR, §2 (schematic stand-in for a real extraction)
given field_eq = R_ij = 8πG(S_ij − ½ S g_ij)  from paper eq. (1)   # the paper states GR
given vars: S = T_αβ u^α u^β, S_ij = T_αβ e^α_i e^β_j  from paper §2
define a_D := (V_D/V_0)^(1/3)   with V_D = ∫_D √h d³x
assume D compact, irrotational dust (T_ij = 0), u_α = −∂_α t  from paper §2
derive ray_D: ä_D/a_D = −4πG⟨S⟩_D + 2𝒬_D/3  from [field_eq, vars, Raychaudhuri] | [average over D]
    ? [paper cites the Raychaudhuri equation; not derived here — from cited @Ellis-van-Elst]
claim closure: the averaged system closes on {a_D, V_D, 𝒬_D}  from paper, conclusion
    ? [asserted by the authors; displayed derivation stops at ray_D]
```

Note the fidelity mechanics in the second example: the authors' *derived* step is a `derive`; the imported theorem is a `given ... from cited`; the authors' *conclusion without displayed derivation* is a `claim` with `?`. Nothing is silently upgraded and nothing is silently dropped. An independently reconstructed derivation, if the agent later produces one, is a separate `derive` with its own premises — distinguishable from the paper's own reasoning by its `from` references and by an attribution note in the annotation.

Both documents are the same language. Exploration differs from extraction only in what fills the `given`s and how many `?`s survive.

### A.5 Construct-by-construct justification (what breaks without it)

- **`given` vs `assume` — why not merge?** Merging loses the single distinction the whole design protects: an input the reasoning *starts from* (data, cited theorem, problem statement) versus a premise the reasoning *borrows provisionally*. Downstream consequences differ: falsified data invalidate; falsified assumptions only delimit. Claude's `measured|postulated` label pair is dissolved into the inline `from` clause plus the `given`/`assume` choice.
- **`define` vs `given`:** meaning-creation versus input-import. PhysTrace Lesson 1 (the `rho_Q`/`Q` identity loss) is exactly the failure this pair prevents: definitions carry their defining relations visibly.
- **`claim`:** without it there is no way to state a paper's assertion or a conjecture *without* presuming it, so assertions would either be smuggled in as `given` (overstating) or omitted (unfaithful).
- **`derive`:** the only inference. Removing it removes the ability to distinguish derivation from assertion — the core fidelity requirement.
- **`if/then/else`:** without it, conditional reasoning degenerates into prose qualifiers that do not bind consequents. Branch membership is what makes "established under condition C" a structural fact.
- **`?`:** the entire MRC surfacing mechanism. Without a first-class unresolved marker, gaps are either silent or escalate into global status fields.
- **What was considered and rejected:** `want ... vs N` (Claude) — a target-versus-null-model pair; every worked example in the corpus shows it is expressible as two `claim`s plus one `if`, and derivations do not need it. `hypothesis` (ChatGPT) — identical semantics to `claim`; merging avoids a distinction with no observable consequence. `input` — subsumed by `given`. `cite` — subsumed by the `from` clause. No additional keyword survives.

---

## Deliverable B — Math Reality Check semantics

### B.1 The two-layer architecture

```text
Layer 1 — the language        PSEUDO.md: the 7 constructs, theory-neutral
Layer 2 — the advisory guide  MRC_GUIDE.md: shines / silent / partial, inspectable
Layer 3 — local annotation    ? at the step where a gap bites
```

The language describes reasoning. The guide describes what each mathematical framework can establish, under which assumptions, and where it is silent — extracted from the `reality_check.md` corpus. The agent consults the guide to *recognize* a gap; it writes `?` to *expose* it. The guide never appears in the syntax.

The guide is challengeable: a conformance fixture (and later, a workflow note) allows an agent to record a counterexample to a documented silence and continue exploring. The annotation must remain conditional on the actual framework and declared assumptions — "this formulation does not supply initial data" is a legitimate annotation; "mathematics can never supply X" is not, unless the map entry says so explicitly.

### B.2 How MRC examines one reasoning step

Ordered checks, cheapest first. Only the first two are mechanical in milestone 1.

1. **Reference checks (mechanical):** every premise named in a `derive` exists; every symbol used was declared (`given`/`define`/`assume`) or locally bound; dependency graph has no cycles.
2. **Fidelity checks (mechanical-lite, paper mode):** a statement with a `from paper` provenance that is written as `derive` must have its premises and reasoning visible in the document; otherwise it must be `claim` or `given ... from cited`. This is what mechanically prevents assertion→derivation upgrades.
3. **Compatibility checks (mechanical where annotated):** when `define`s carry type/dimension annotations, a step combining incompatible ones is flagged. Where annotations are absent, compatibility is an explicit review question — never silently assumed, never pretended-checked.
4. **Entailment check (reasoned, not mechanical):** does the conclusion follow from the cited premises by the stated reasoning? The agent asserts this in the `derive`; MRC review tests it; when the agent cannot justify the step, the honest representation is a `?` on that step, not omission.
5. **Applicability check (advisory):** consult the guide. If the step's operation falls in a documented silence for the declared framework — e.g., a `derive` claiming to produce initial conditions, a vacuum selection, coupling values, or Born-rule probabilities from pure mathematics — the guide's entry triggers a required annotation at that step. This is where Claude's operator guards live now: not as built-in syntax, as guide entries.
6. **Propagation (mechanical, structural):** weakest-ancestor rule. A result's status is the minimum over its ancestry: any `?` upstream marks everything downstream unresolved; any `assume` upstream makes everything downstream conditional on it; claims stay asserted until given premises or a `derive`. Unresolved does **not** halt: an unresolved-dependent statement remains representable and usable *conditionally* — it simply can never be presented as established. The `?` list is the agenda.

### B.3 The four distinctions without a taxonomy

The brief requires distinguishing four things without building a status taxonomy. They fall out of structure:

| Distinction | Where it lives in the document |
|---|---|
| Syntactically representable | It parses under the conventions. No claim beyond that. |
| Mathematically justified | It is a `derive` with no `?` in its ancestry and non-asserted premises. |
| Physically applicable | Its ancestry includes the framework assumptions under whose regime the guide says the operation shines (not merely is silent-adjacent). |
| Empirically supported | Its ancestry reaches a `given ... from measured`. |

A result can be mathematically justified and physically inapplicable (the guide's "partial applicability" region); derived from declared premises and empirically empty (most of theoretical physics); syntactically fine and unjustified (a `claim`). No author-typed label can conflate these, because no such label exists.

**Mapping to PhysTrace evidence classes** (integration contract, no duplication): `given ... from cited` ↔ SOURCE_CITES_EXTERNAL_RESULT; paper assertion as `claim` ↔ SOURCE_ASSERTS_OR_SKETCHES; agent-reconstructed `derive` marked in annotation ↔ SPEC_INFERENCE; `?` on ambiguity ↔ UNRESOLVED; `derive` with paper-visible steps ↔ EXPLICIT_SOURCE. The pseudocode layer is the front end; PhysTrace's spec remains the normative ingestion standard. Neither registry is duplicated in the other.

### B.4 What MRC explicitly does not do

It does not prove entailments, does not run mathematics, does not grade confidence, does not aggregate. There is no score that could conceal a failed dependency, because there is no score. A derivation replayable by PhysMath would later be *stronger* evidence than a pseudocode `derive` — and the language marks that difference honestly by never claiming more than "the agent reasons this follows."

---

## Deliverable C — Expressiveness tests (conformance suite)

Physical form: a markdown corpus, `conformance/`, each fixture pairing a pseudocode document with **expected MRC findings stated as recognition-level obligations** ("the conclusion must be recognized as depending on an unstated initial condition"), never as required annotation wording.

| # | Fixture | Domain | Mode | What it tests |
|---|---|---|---|---|
| 1 | Exploratory hypothesis | GR/cosmology | exploration | A conjecture is explored under provisional assumptions; `H` never becomes established; `?` marks the missing solution. |
| 2 | Published derivation | QM (ladder operators → spectrum) | paper | Assumptions, imported CCR postulate, derived steps, and the authors' asserted conclusion remain distinguishable. |
| 3 | Missing prerequisite | GR | paper | An omitted intermediate step is marked `?` at the step needing it; downstream stays usable conditionally. |
| 4 | Conditional reasoning | statistical physics (ensemble equivalence under a stated condition) | both | `if/then` binds the consequent to its condition; competing branch remains open. |
| 5 | Dimensional mismatch | dimensional analysis in a mechanics/field-theory step | exploration | An incompatible combination is surfaced; the fixture documents which part is mechanical (annotated types) and which is review. |
| 6 | Novel structure | proposed bracket with no established branch | exploration | Unfamiliar mathematics is expressible with zero new keywords; no branch classification required. |
| 7 | Cited result | Raychaudhuri imported | paper | `given ... from cited` is not misrepresented as independently derived; the fixture includes the anti-pattern (rewriting it as `derive`) as a negative case. |
| 8 | Competing hypotheses | dark energy vs. backreaction | exploration | Two claims, shared premises, one `if` comparing them; neither is treated as a failed proof of the other. |

Cross-cutting coverage requirements: at least one fixture exercises each of `given/define/assume/claim/derive/if/?`; at least two are pure exploration and two pure paper; the math-physics slot is filled by a fixture transcribing the `(a∂ₐ)²f ≠ a²∂ₐ²f` operator-composition case from the PhysTrace guidelines — chosen because it is a real historical error class with a known correct answer.

**Failure adjudication rule** (applied in the adversarial round): a failure is a *language* change only if no arrangement of the seven constructs can express the distinction the fixture protects. Everything else — inability to *execute* a step, verify an equivalence, or look up a theorem — is a library gap (PhysMath/PhysLib) or a guide gap (MRC guide), recorded as such. Deliverable E shows this rule already deciding four contested cases.

---

## Deliverable D — Implementation roadmap

### Repository shape (module `github.com/PithomLabs/phys-pseudo`, to be created in Stage 0+; nothing now)

```text
phys-pseudo/
  go.mod             # module github.com/PithomLabs/phys-pseudo (Stage 3)
  PSEUDO.md          # the normative language spec (Stage 0)
  MRC_GUIDE.md       # advisory shines/silent/partial, derived from reality_check.md (Stage 1)
  conformance/       # fixtures + expected findings (Stage 1)
  AGENTS.md          # package-local rules, pointing at phys-system/AGENTS.md
  cmd/pseudocc/      # shallow validator (Stage 3)
```

### Stage 0 — Language specification
- **Work:** write `PSEUDO.md`: the seven constructs with exact semantics (A.1–A.3), both worked examples (A.4), the construct-justification ledger (A.5), the computed-status rules (A.3), and the explicit non-goals (below).
- **Depends on:** nothing.
- **Acceptance:** every construct has a non-redundancy justification; both example documents are faithful to the fidelity rules; the spec contains no physics-branch list and no reference to any Phys library's current capability.

### Stage 1 — Conformance corpus + advisory guide
- **Work:** the eight fixtures of Deliverable C, each with document, expected findings, rationale, and adjudication notes. In parallel, `MRC_GUIDE.md`: one entry per mathematical area from `reality_check.md`, structured as *shines / silent / partial*, each entry conditional on framework and regime, plus the challenge mechanism (how an agent records a counterexample to a silence).
- **Depends on:** Stage 0 (fixtures cite spec sections).
- **Acceptance:** the corpus covers all seven constructs, both modes, and four physics areas plus mathematical physics; expected findings are recognition-level; the guide's every entry is traceable to a `reality_check.md` map, with the corpus's own maps cited as the source — the guide is derived evidence, not new doctrine.

### Stage 2 — Adversarial review round
- **Work:** run Deliverable E's counterexample method against the corpus and spec, by an independent reviewer/agent pass. Revise vocabulary only on demonstrated expressive deficiency; record every rejected revision and why.
- **Depends on:** Stage 1.
- **Acceptance:** each counterexample has a written verdict (representable / convention needed / genuine revision); any spec change includes the failing example that motivated it; the seven-keyword count either holds or is justified by a demonstrated failure.

### Stage 3 — Shallow structural validator
- **Work:** a small Go checker in `phys-pseudo` validating only: statement kinds against the vocabulary, label definition-before-reference, premise reference resolution, dependency acyclicity, `?` attachment well-formedness, and (where annotations exist) dimension-consistency of `define`s. It validates documents; it never validates mathematics. Module path: `github.com/PithomLabs/phys-pseudo`.
- **Depends on:** Stage 2 (frozen-enough conventions).
- **Acceptance:** the full conformance corpus passes; a mutated corpus (broken references, cyclic premises, `derive` with no premises, paper-`derive` with invisible reasoning) fails at the intended boundary; the validator's documentation states in its first paragraph that passing it proves nothing mathematical.

### Stage 4 — Guide-derived advisory checks (optional, opportunistic)
- **Work:** compile *only demonstrably helpful* guide entries into advisory validator warnings (e.g., "this `derive` produces a quantity the guide records as a selection/genesis silence for the declared framework; annotation required"). The registry derives from the guide, never defines the language; unrepresented structures can never be rejected, only questioned.
- **Depends on:** Stage 3, mature guide.
- **Acceptance:** no construct or document can be *rejected* by this layer; false-positive challenges feed back into the guide's challenge ledger.

### Stage 5 — Integration with the Phys stack (deferred, bounded)
- **Work, when real derivations demand it:** pseudocode documents as front matter for PhysTrace derivation specifications (using the B.3 evidence-class mapping); conformance anti-goldens (e.g., the `rho_Q`/`Q` case) reusable as pseudocode fixtures; MRC guide entries cross-referencing, not duplicating, PhysLib framework assumption registries.
- **Depends on:** a real paper-extraction workflow choosing to use the pseudocode layer.
- **Acceptance:** no reverse dependency (`phys-*` packages do not import `phys-pseudo`); no ontology merge; the pseudocode remains expressive when PhysMath cannot execute a step.

### Mechanical vs. reasoned — the honest split

| Mechanically enforceable | Requires proof, tool, or expert |
|---|---|
| Statement grammar, label/reference resolution, acyclicity | Whether a `derive`'s inference is valid |
| `derive`-fidelity in paper mode (premises/reasoning visible) | Whether a `define`'s meaning matches the source's meaning |
| Dimension/type consistency *where annotated* | Compatibility where annotations are absent |
| Weakest-ancestor propagation, `?` completeness of attachment | Whether an assumption is physically appropriate |
| Absence of status labels (spec invariant, greppable) | Whether the guide's silence entries are correct — challengeable by design |

### Explicit non-goals (roadmap law)

No Claravine-style API, no transactions or two-phase commit, no exploration/paper mode flag, no universal operator registry, no proof engine or solver, no ontology duplicating PhysMath/PhysLib, no prescribed research-stage sequence, no confidence scores.

### Recorded uncertainties (not invented)

1. `phys-pseudo` has no module, license, or `AGENTS.md` yet; creation is Stage 0/3 work.
2. Whether `phys-system/AGENTS.md`'s component map should list `phys-pseudo` is a collective-authority change — flagged, not assumed.
3. The MRC guide's provenance discipline: `reality_check.md` is internal research material; its distilled entries should carry attribution, and whether the guide is published alongside the spec is a licensing decision.
4. Validator host language is Go for ecosystem consistency; Stage 3 records the decision explicitly.

---

## Deliverable E — Adversarial review of the proposal

Simplest counterexamples, each with verdict. The adjudication rule from Deliverable C applied honestly:

1. **Circular derivation** (`derive A from B; derive B from A`). Representable syntactically; caught mechanically by the acyclicity check. No language change — this is exactly a reference-level defect.
2. **Undeclared symbol** in a `derive`. Representable; caught mechanically by definition-before-use. No change. (Claude's "only hard error" survives — as a validator check, not a language feature.)
3. **Paper asserts result with zero displayed derivation.** Representable as `claim` + `?` (A.4 does it). No change; this is the fidelity test the design exists to pass.
4. **Mid-document retraction of an assumption** (agent discovers `assume` is wrong and revises). Genuine gap in the *conventions*, not the vocabulary: the spec's answer is supersession — a new statement that supersedes the old assumption, with downstream steps re-derived or `?`-marked. Convention, recorded in Stage 2; no keyword. Re-tested in the corpus.
5. **Inductive / n-th order reasoning** ("repeat for k = 1…n"). Expressible in the right-hand side as free prose ("for each order k..."), but genuinely ambiguous about what the premises of the generic step are. Verdict: corpus test case (math-physics slot); if ambiguity persists on real inputs, the fix is a referencing convention, not a loop construct. Flagged, not pre-solved.
6. **Dimensionally inconsistent step presented as derived.** Representable and *misrepresentable* — which is the point: the document can lie, and MRC's job is the annotation. Partially mechanical (annotated types), partially review. No language change; the fixture exists to prove the checker does not overclaim.
7. **Two agents disagree about an inference's validity.** Representable as a counter-`claim` plus `?` on the disputed `derive`. No change; disagreement is data, and no status field is needed to record it.
8. **An object with no mathematical definition available** (opaque function from a cited theorem). Representable: `given` with the citation and a `define` marked opaque, per the PhysTrace rule "represent opaque functions explicitly; state the limit rather than pretending evaluation occurred." No change.
9. **Attempt to smuggle status:** `claim H: PROVEN that ...`. No grammar forbids the text, but no construct *licenses* it, and the computed-status rule ignores it — the spec invariant "no author-typed status" makes it a spec violation, greppable mechanically. Verdict: handled without grammar.
10. **A genuinely new mathematical structure** (fixture 6). Expressible by design; if it fails, that is the one failure class that would justify a language revision. None found in this round.

**Result of the adversarial round:** zero new keywords survive; two convention-level amendments (supersession; opaque definitions) and two flagged re-test cases (induction; annotation-wording level) are folded into Stages 0–2. The proposal stands as seven constructs.

---

## Acceptance-criteria mapping

1. *One language for both modes* — A.4's two examples; corpus fixtures 1–8 mix both.
2. *Every construct non-redundant* — A.5 ledger, with rejected candidates named.
3. *MRC visible at point of use* — B.2 checks 3–5 surface at the step; `?` is local.
4. *Conjectures explorable, never promoted* — computed status (A.3); fixture 1.
5. *Assertions / derivations / agent inferences distinguishable* — `claim` vs `derive` vs annotated reconstruction; B.3 mapping; fixtures 2, 7.
6. *Conditional continuation without silent promotion* — weakest-ancestor propagation (B.2 step 6); fixture 4.
7. *Not tied to any theory, branch, or library* — no branch list anywhere; guide is advisory and challengeable; fixture 6.
8. *Testable without proving math* — validator scope (Stage 3 acceptance) and the mechanical/reasoned table.
9. *No scope expansion into infrastructure* — non-goals restated as roadmap law; Stage 5 bounded and deferred.

---

## Next steps (awaiting instruction)

The success criterion is met by construction: the language is seven constructs whose entire expressive budget goes into declaring ingredients, binding premises, marking conditionals, and exposing gaps — and every status is computed from the dependency graph, so the document can describe an investigation more honestly than any metadata layer could rate it.

Two sequencing options for implementation kickoff:

- **Stage 0 first:** write `PSEUDO.md` (the spec draft itself), then corpus, then adversarial round.
- **Adversarial corpus first:** run a second independent reviewer pass against the vocabulary before the spec hardens; recommended only if an independent reviewer is available.

Default: Stage 0 first. Await instruction.
