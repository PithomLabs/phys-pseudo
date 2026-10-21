# MRC Review Protocol

How an adversarial reviewer (an AI agent or a human) examines physics reasoning
written in phys-pseudo (`PSEUDO.md`). MRC means Math Reality Check.

**Stance.** Representing a statement is not endorsing it, so speculative hypotheses
and incomplete papers are legitimate inputs. Your job is to expose weaknesses and
state the current evidential boundary. It is not to approve, not to suppress a
hypothesis for being unproven, and not to manufacture certainty. "This cannot yet be
settled, and here is what would settle it" is a valid finding.

**Never trust the document's own assurances.** A `from [...]` list is a proposal.
Clean syntax, resolved names, and the absence of `?` show only that the document was
written clearly.

**Advisory knowledge.** `reality_check.md` records what a mathematical framework
establishes, where it is silent, and where it applies only partially. Consult it for
the framework in use. An entry may *motivate* a finding or a `?`. It never
auto-rejects anything, and you may challenge an entry with a counterexample. Do not
paste its checklist into your report.

## The eight steps

### 1. Reconstruct the target

Before judging anything, write a short paragraph: the question being asked, the
statement(s) that carry the stated result (by name), the regime in which the result
is claimed, and what is explicitly *not* claimed. If you cannot do this from the
document, that is your first finding.

### 2. Separate epistemic roles

Sort every statement into its role: definition, given, assumption, source assertion,
cited result, derivation, conjecture, unresolved issue. Then check:

- A source claim, a cited result, or an AI reconstruction must not be treated as
  proved. If a `given` quotes a source, check the source says that. If you cannot
  check it, say so; an unverifiable citation is not established.
- A `define` must not carry a physical law or an existence/uniqueness presupposition.
  Test: replace the name by its right-hand side everywhere. If any proposition
  changes, it is a hidden assumption.
- Notes about authorship (paper's derivation vs. reconstruction) should be honest. A
  reconstruction presented as the paper's own is a source-fidelity defect.
- A `claim` used as a premise means the result rests on something unestablished.

### 3. Check mathematical validity

For each *consequential* `derive` (one the stated result rests on), work it
yourself; do not just read the reasoning.

- Restate the result. Does it follow from the listed premises by the stated reasoning?
- Which premises does the reasoning actually use? Anything used but not listed is an
  omitted dependency. Anything listed but unused is noise.
- Is it circular: does a premise rest on the result, or on something equivalent?
- Is the result stronger than the premises support? Typical overreach: bound →
  equality, recurrence → complete spectrum, "for some" → "for all", existence →
  uniqueness, eigenvalue relation → nonzero eigenvector.
- Try the simplest case where the premises hold and test the result. A concrete
  counterexample beats a general objection.
- If you used a computation tool, say so. If you checked by hand, say so.

### 4. Check mathematical well-formedness

Ask which of these could actually change the result *here*, and examine only those:
quantities and types (scalar, vector, operator, function), dimensions and units,
domains and codomains, operator conditions (domains of unbounded operators,
self-adjointness, whether a composition exists), normalization, boundary and initial
conditions, convergence, the regime of any approximation, degenerate branches
(zero, sign changes).

Illustration (checked symbolically): the ladder-operator argument gives a ground
energy of ħω/2 for the oscillator. The same algebra, with the same formal
commutator, also fits the half-line oscillator with a Dirichlet condition at 0 — yet
that system's lowest energy is 3ħω/2. The lowered state is nonzero at the boundary,
so it is outside the Hamiltonian's domain. The algebra needed a domain or
self-adjointness premise the argument never stated. This is the kind of omission to
look for; it is not a reason to demand such checks everywhere.

### 5. Check physical applicability

Does the mathematical result apply under the stated physical assumptions and regime?

- Is identifying a mathematical object with a physical quantity itself an
  assumption? (It usually is.)
- Is the result used outside the regime in which its assumptions hold?
- Is a framework used where `reality_check.md` records it as silent or only partly
  applicable?

A valid derivation is not evidence that the model describes Nature.

### 6. Check empirical support separately

State what empirical evidence is actually present: measured inputs, comparisons made,
what the data constrain. Do not invent experimental confirmation. Do not treat a
theoretical derivation, or the presence of data among the inputs, as support. A
datum in the premises can contradict the claim it sits near. "No empirical content in
this document" is an acceptable finding.

### 7. Locate the decisive gaps

- **Unresolved** (unknown): record with `?`, saying what is missing and what would
  resolve it.
- **Known false:** refute it with a counterexample, a contradiction, or conflicting
  reasoning. Never relabel it as unresolved.
- A `?` that is really a known-false statement, or really an attribution note, should
  be reported and restated.

Rank gaps by *decisiveness*: resolving the gap would change whether a stated result
follows, applies, or is supported.

### 8. Report actionable findings

For each material issue:

| Field | Content |
|---|---|
| **Where** | The affected statement name, or the step within it. |
| **Defect** | One sentence: omitted premise; invalid or circular step; conclusion stronger than premises; undeclared quantity; missing domain condition; derivation with no explicit result; conditional result stated as unconditional; assumption inside a definition; source claim presented as established; theory conflated with empirical truth; known-false item marked `?`. |
| **Why** | The supporting reasoning or counterexample. |
| **Minimum fix** | The smallest correction, premise, calculation, or evidence that would address it. |

Separate **consequential** issues (they change whether a stated result follows,
applies, or is supported) from **cosmetic** ones (wording, naming, layout). List
cosmetic items briefly or omit them. Do not spend review effort on preferences that
do not affect meaning.

Close with an **evidential boundary** paragraph: what you actually verified and how,
what you could not check, and what remains unresolved. Do not give a global
"correct/incorrect" verdict, and do not write that anything is "verified" beyond the
checks you performed.

## Boundary with implementation

Passing this review does not make a derivation implementation-ready. When a
derivation is being specified for implementation, `DERIVATION_SPEC_GUIDELINES.md`
adds its own requirements: exact quantity definitions, domains, operation semantics,
independently checked expected results, verification, and provenance. Those are not
required of exploratory hypotheses or paper overviews, and this protocol does not
replace them.
