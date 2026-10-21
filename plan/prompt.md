# Task: Canonicalize `phys-pseudo` and Establish the MRC Review Protocol

## Objective

Implement the next high-impact milestone for `phys-pseudo`: consolidate the completed Stage 3 findings into **one minimal, canonical language specification and one concise, practical Math Reality Check (MRC) review protocol**.

The purpose is to make `phys-pseudo` useful for three workflows through one shared language:

1. AI agents express physics hypotheses, explore mathematical consequences, and conduct adversarial reviews without having to present speculative ideas as established facts.
2. Humans inspect the essential reasoning behind relevant Phys Go derivations before examining their implementations.
3. Humans quickly understand physics papers, including their assumptions, central reasoning, results, source claims, derivation gaps, and unresolved questions.

The milestone is documentation and workflow design, not implementation of a parser, checker, or automated scientific-verification system.

**Work in:** `/home/chaschel/Documents/go/phys-pseudo`

Follow all applicable workspace and repository `AGENTS.md` instructions before making changes.

## 1. Read and reconcile the existing evidence

Inspect the actual repository and available workspace documents before editing. Locate and read:

- The final Stage 3 report.
- `pivot_review.md` and `plans_review.md`, or their actual equivalent filenames.
- The existing `CONVENTIONS.md`.
- The current `reality_check.md` or equivalent MRC advisory material.
- `DERIVATION_SPEC_GUIDELINES.md`.
- The existing Stage 2 fixtures, their README, and any other documents that define the current examples and intended workflows.

Use actual files and paths. Do not pretend a document was inspected if it is unavailable.

Treat the completed Stage 3 report as the primary audit record. Consolidate the other reviews by accepting their valid findings, rejecting unnecessary complexity, and resolving contradictions explicitly. Stage 3 recommended **PASS-WITH-AMENDMENTS**: the seven-construct vocabulary survived review. The principal defects concern unclear or contradictory conventions and inadequate examples, not a need for more language constructs.

Do not restart the prior review process or create another planning-only milestone. Implement the changes below.

## 2. Create the canonical `PSEUDO.md`

Create `PSEUDO.md` as the sole authoritative specification of the core language.

Retain exactly these seven core constructs:

```text
given NAME: <content>
define NAME := <meaning>
assume NAME: <premise>
claim NAME: <proposition>
derive NAME: <explicit result> from [NAMES] | <reasoning>
if <condition>:
    then <consequence>
    else <alternative>
? <what is unresolved and what would resolve it>
```

This is the baseline syntax. Refine its presentation only where necessary to remove ambiguity; do not expand the language with new constructs.

The specification must explicitly settle the following issues found during Stage 3:

### A. Consistent syntax and names

- Use one spelling and delimiter convention consistently: for example, `given NAME:` rather than switching between `=` and `:`.
- Define what a `NAME` identifies and how later statements refer to it.
- Decide and document whether references must point to earlier declarations. Prefer simple declaration-before-use rules unless the existing evidence gives a concrete reason not to.
- Keep labels as ordinary reference identifiers, not an ontology or a registry of scientific statuses.
- Do not allow unnamed premises when the format otherwise requires named references.
- Treat mathematical symbols and quantities used in reasoning as something the author or reviewer must account for. Free-form mathematics must not become an excuse for silently introducing essential undefined quantities.

### B. Distinguish definitions, premises, claims, and derivations

Specify the intended role of each construct.

In particular:

- A `define` introduces the meaning or convention of an expression. It does not, by itself, establish an empirical fact or justify an independent physical assumption.
- An `assume` makes a premise explicit without asserting that the premise is true in Nature.
- A `claim` records a proposition being asserted or examined. It is not automatically derived.
- A `derive` identifies an explicit result, its stated dependencies, and a concise reasoning path. A derivation written in this language is **not thereby validated**.
- Do not use a definition to smuggle in an independent physical law, an unproved theorem, or an assumption that the reasoning subsequently relies on.

### C. Make `derive` unambiguous

Require every derivation to state its intended result explicitly. Clarify the purpose of `from [NAMES]` as a list of proposed reasoning premises, not source attribution.

A dependency list is not proof that every relevant premise has been listed. The MRC reviewer must actively look for omitted premises, hidden assumptions, circular reasoning, invalid inference, and conclusions stronger than the stated premises support.

Do not add formal provenance fields or dependency-status propagation machinery.

### D. Define conditional scope

Clarify how `if`, `then`, and optional `else` are indented and interpreted.

The reader must be able to determine:

- Which condition governs each branch.
- Which consequences depend on that condition.
- Where the conditional scope ends.
- Whether a statement is unconditional or follows only under a premise.

A condition must be an identifiable proposition or an explicit condition, not a vague reference to surrounding prose. A branch must not be mistaken for proof that its condition actually holds.

Use a small, illustrative example to demonstrate scope and reference rules.

### E. Define `?` precisely

`?` means **unresolved or underspecified**, never “known false.”

Specify two clear forms:

- An indented `?` attached to a particular statement records an unresolved question about that statement.
- A top-level `?` records an unresolved question about the document as a whole.

The indentation and attachment rule must not depend on an ambiguous interpretation of the nearest preceding line.

When a proposition is known to be false, express the refutation through a counterexample, contradiction, or explicit conflicting reasoning—not `?`.

An unresolved question should state what is missing and, where possible, what evidence, premise, calculation, derivation, or experiment would resolve it.

### F. Preserve the boundary between representation and endorsement

Make the central invariant explicit:

**Representing a proposition or reasoning step does not endorse its truth, validity, physical applicability, or empirical correctness.**

The language must support speculative exploration and adversarial scrutiny. MRC should expose weaknesses and uncertainty without suppressing a hypothesis merely because it has not yet been established.

### G. Keep source fidelity without formal provenance syntax

For paper overviews, preserve the distinction between:

- What the paper explicitly states.
- What it derives or sketches.
- Results it cites from external sources.
- What the pseudocode author or AI reconstructs or infers.
- What remains unresolved.

Convey attribution through ordinary document prose, source notes, or a clearly separated explanation. Do not overload `from`, add provenance operators, or introduce a formal evidence-status taxonomy into the seven-construct language.

Update `CONVENTIONS.md` as needed so it cannot compete with `PSEUDO.md` as a second, contradictory specification. Prefer making it a concise pointer or compatibility note rather than duplicating all normative rules.

## 3. Create `MRC_REVIEW_PROTOCOL.md`

Create a short, operational, agent-readable protocol that explains how an adversarial reviewer should use `phys-pseudo` and existing MRC guidance to inspect physics reasoning.

This protocol is essential. A minimal language without a substantive review method risks becoming merely a notation for organizing claims and dependencies rather than a workflow for examining mathematical and physical reasoning.

The protocol must cover these review responsibilities:

1. **Reconstruct the target.** Identify the question, stated result, regime, and intended scope before evaluating an argument.
2. **Separate epistemic roles.** Distinguish definitions, givens, assumptions, source assertions, cited results, derivations, conjectures, and unresolved issues. Do not silently promote a source claim or AI reconstruction into a proved result.
3. **Check mathematical validity.** Independently examine each consequential derivation. Assess whether the listed premises suffice, whether any dependencies are omitted, whether a step is circular, and whether the result actually follows.
4. **Check mathematical well-formedness.** Examine relevant quantities, types, dimensions, domains, definitions, operator conditions, normalization requirements, boundary conditions, and applicable mathematical regimes. Apply only those checks relevant to the particular argument; do not turn this into a universal checklist that mechanically assumes every item matters.
5. **Check physical applicability.** Determine whether the mathematical result applies under the stated physical assumptions and regime. Do not confuse a mathematically valid result with evidence that the physical model describes Nature.
6. **Check empirical support separately.** Identify what empirical evidence is actually available. Do not invent experimental confirmation or treat a theoretical derivation as empirical validation.
7. **Locate the decisive gaps.** Use `?` for unresolved issues and state what would resolve them. Explicitly refute known-false propositions rather than relabeling them as unresolved.
8. **Report actionable findings.** For each material issue, identify the affected statement or reasoning step, explain the defect, provide the supporting reasoning or counterexample, and state the minimum correction or additional evidence needed. Distinguish consequential scientific defects from cosmetic preferences.

Use the existing `reality_check.md` or equivalent as advisory knowledge and reference it explicitly where appropriate. Do not silently replace it, duplicate its entire contents, or embed its full checklist into the language syntax.

The review protocol must remain useful when a hypothesis is speculative, a paper is incomplete, or a derivation cannot yet be settled. The reviewer should clarify the current evidential boundary and unresolved obligations, not manufacture certainty.

## 4. Preserve the separation from implementation-ready derivation specifications

`DERIVATION_SPEC_GUIDELINES.md` is a higher-rigor, normative standard for implementation-ready derivation specifications.

Explain this boundary clearly:

- `phys-pseudo` is the minimal language for communicating and inspecting reasoning.
- MRC is the adversarial review method for examining that reasoning.
- `DERIVATION_SPEC_GUIDELINES.md` governs the additional requirements necessary when a derivation is being specified for implementation and verification.

Do not require every exploratory hypothesis or paper overview to contain all the implementation-ready fields. Conversely, do not imply that a brief pseudocode derivation is ready for implementation merely because it is syntactically clear.

Keep the three roles complementary rather than coupling them into one oversized specification.

## 5. Validate the documents against the existing corpus

Use the current fixtures and Stage 3 findings as regression evidence for the specification. At minimum, verify that the revised documents clearly explain how a reader should recognize and handle these failure patterns:

- An unresolved marker misused for a known-false proposition.
- A conclusion that does not follow from its stated premises.
- A missing mathematical prerequisite or domain condition.
- An undeclared quantity or an essential dependency omitted from a derivation.
- A derivation without an explicit result.
- A conditional conclusion that is stronger than its condition permits.
- Circular reasoning or an assumption smuggled into a definition.
- A paper claim incorrectly presented as an independently established result.
- Theoretical validity incorrectly conflated with empirical truth.

These are adversarial examples, not a demand to certify every fixture as mathematically correct. Preserve deliberate counterexamples and flawed fixtures where they serve their test purpose. Change existing fixtures only when a concrete change is necessary to remove a documentation contradiction or keep the corpus usable under the canonical conventions; explain any such change.

Do not claim that an audit or validation was performed unless it was actually carried out.

## 6. Explicitly out of scope

Do **not** implement or introduce:

- A parser, linter, checker, or compiler.
- Formal provenance syntax or a provenance registry.
- Computed scientific truth, support, or validity statuses.
- Automatic propagation of dependency statuses.
- A universal physics operator catalogue or elaborate ontology.
- Mandatory type annotations or a global type system.
- CAS-based verification as a new milestone requirement.
- A large metadata schema for every pseudocode statement.
- New language constructs to patch individual fixture deficiencies.
- Another open-ended round of speculative design review.

Do not add machinery merely because it could theoretically be automated. Only revisit automation when a specific, reproducible failure demonstrates that documentation and the review protocol are insufficient.

## 7. Acceptance criteria

The task is complete when:

1. `PSEUDO.md` is the single authoritative, internally consistent specification of the seven constructs.
2. All syntax and scope ambiguities identified in Stage 3 have explicit, understandable resolutions.
3. `MRC_REVIEW_PROTOCOL.md` gives an AI reviewer a concrete process for challenging mathematical validity, physical applicability, source fidelity, and empirical support without conflating them.
4. The advisory role of existing MRC material and the higher rigor of implementation-ready derivation guidelines are preserved.
5. The existing documentation points consistently to the canonical specification rather than maintaining conflicting versions of the rules.
6. Representative fixtures can be read under the revised conventions, and deliberate defects remain useful adversarial tests.
7. No parser, checker, status engine, or other excluded feature has been introduced.
8. The result is concise enough for an AI coding or research agent to follow and for a human to inspect without studying a large framework.

**Primary success criterion:** An independent AI agent can read the language specification and review protocol, understand the intended reasoning, identify consequential weaknesses, and prepare a faithful next-step derivation or implementation without guessing about the language rules or silently inventing scientific premises.

## 8. Final report

After implementing the task, report:

- The exact files created or changed.
- The most consequential conventions clarified.
- How the MRC protocol differs from the language specification and from implementation-ready derivation guidelines.
- Which representative fixtures were checked and what those checks established.
- Any Stage 3 issues that remain unresolved, with reasons.
- Confirmation that the out-of-scope features were not added.

Keep the report factual and brief. Do not claim repository-wide correctness or scientific verification from documentation changes alone.