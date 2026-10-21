# Task: Write `AGENTS.md` and a Human-Friendly `README.md` for Phys Pseudo

## Objective

Create two complementary documents at the repository root of `phys-pseudo`:

- `AGENTS.md` — the operational guide that enables an AI coding or research agent to use Phys Pseudo correctly for its intended purposes, follow the MRC review process, and find the authoritative reference for each task.
- `README.md` — a concise introduction for humans explaining what Phys Pseudo is, why it exists, how to read an example, and where to find further guidance.

The goal is to make the repository understandable and usable without requiring users to reconstruct its design decisions from the Stage 1–4 history.

**Inspect the actual repository before writing.** Read the current canonical specification and supporting documents, locate any existing root instructions and README, and verify every relative link. Do not blindly overwrite useful existing content.

## 1. Establish the source of truth

Use these existing documents, at their actual repository paths, as the primary references:

1. `PSEUDO.md` — the sole authoritative specification of the language.
2. `MRC_REVIEW_PROTOCOL.md` — the operational method for adversarially reviewing reasoning.
3. `plan/reality_check.md` — advisory MRC knowledge that can motivate a check or finding but never gates what can be expressed.
4. `conformance/DERIVATION_SPEC_GUIDELINES.md` — the additional normative requirements for implementation-ready derivations.
5. `conformance/README.md` — how to interpret the existing conformance fixtures and their intentional defects.
6. `CONVENTIONS.md` — a compatibility and migration pointer, not an alternative specification.
7. `plan/PSEUDO_STAGE4_REPORT.md` and `plan/PSEUDO_STAGE4_AMENDMENT.md` — milestone history and the documented design decisions, limitations, and checks.
8. Relevant `AGENTS.md` files higher or lower in the workspace hierarchy, if any exist.

Preserve this authority hierarchy:

**Language specification → MRC review protocol → implementation-ready derivation requirements when applicable.**

The advisory MRC guide informs reviews but does not replace the protocol or serve as a gate.

Do not copy these documents wholesale into `AGENTS.md`. Give agents the operational knowledge they need, explain which references to consult, and link to the full authoritative rules to prevent documentation drift.

## 2. Write root `AGENTS.md`

Make this the practical instruction manual for an AI agent working in the repository. It must contain enough information to perform ordinary Phys Pseudo tasks correctly without relying on previous conversations.

### A. Explain the purpose

State that Phys Pseudo is a minimal, theory-neutral language for three related workflows:

1. Formulating physics hypotheses, exploring mathematical consequences, and conducting adversarial review without presenting speculation as established fact.
2. Providing a human-readable pseudocode counterpart for inspecting the essential reasoning behind relevant Phys Go derivations.
3. Summarizing physics papers so readers can distinguish assumptions, source assertions, derivations, conclusions, reconstructions, and unresolved questions.

Explain the central invariant:

**Representing a proposition or derivation does not endorse its truth, mathematical validity, physical applicability, or empirical correctness.**

### B. Give agents an actionable workflow

Instruct agents to follow this sequence when creating or reviewing Phys Pseudo documents:

1. Identify the task: hypothesis exploration, derivation inspection, paper overview, adversarial MRC review, or implementation-ready handoff.
2. Read the relevant parts of `PSEUDO.md` before producing or changing pseudocode.
3. Gather the source material and establish which equations, premises, claims, and assumptions are actually available.
4. Represent the reasoning using the canonical seven constructs, with explicit results and named dependencies.
5. Preserve source fidelity: distinguish what a source states, what it derives or cites, what the agent reconstructs, and what remains unresolved.
6. Apply `MRC_REVIEW_PROTOCOL.md` when scrutinizing reasoning. Independently check consequential derivations rather than merely restating their arguments.
7. If a derivation is intended for implementation, consult and follow `conformance/DERIVATION_SPEC_GUIDELINES.md` in addition to the language and review protocol.
8. Report material findings, evidence, and limitations honestly. Never claim a check was performed unless it was actually performed.

Make clear that not every exploratory hypothesis or paper overview needs the additional fields required by implementation-ready derivation specifications.

### C. Include the canonical seven-construct reference

Show the standard forms exactly as specified in `PSEUDO.md`:

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

Explain the most important operational rules:

- Use the syntax in `PSEUDO.md` rather than inventing variants.
- Names are plain identifiers, introduced before use; avoid unnamed premises.
- Each `derive` must state its result explicitly and have at least one named premise. `from [NAMES]` records proposed reasoning premises, not source provenance, and does not guarantee completeness.
- Definitions introduce meanings; they must not smuggle in unproved laws, existence claims, uniqueness claims, or physical assumptions.
- `claim` records a proposition under examination; it does not mean the proposition has been established.
- Conditional consequences are confined to their appropriate branch.
- `?` means unresolved or underspecified, never known false. Follow the exact attachment and indentation rules in `PSEUDO.md`. Refute a known-false proposition with a counterexample, contradiction, or conflicting derivation.
- Source attribution belongs in ordinary prose or comments, not in formal provenance syntax.
- Do not add author-assigned scientific truth or validity statuses, provenance registries, new constructs, or inferred truth from document structure.

Treat `PSEUDO.md` as authoritative if this abbreviated list ever conflicts with it.

### D. Make the MRC review process usable

Provide a concise operational summary of the review protocol:

- Reconstruct the question, target result, intended regime, and scope.
- Separate definitions, assumptions, source assertions, cited results, derivations, conjectures, and unresolved issues.
- Independently inspect consequential derivations for omitted premises, invalid inference, circularity, and overstrong conclusions.
- Check relevant dimensions, types, domains, operator conditions, normalization, boundary conditions, limits, and degenerate cases. Apply checks according to the argument; do not mechanically demand every check in every case.
- Separate mathematical validity from physical applicability and empirical evidence.
- Use `?` for genuine unresolved questions, and refute known-false claims.
- Report material findings with their location, defect, reasoning or counterexample, and minimum useful correction.
- End reviews with an evidential-boundary statement specifying what was actually checked, how it was checked, what could not be checked, and what remains unresolved.

Clarify that the advisory guide may motivate a review finding but never automatically rejects, scores, or gates an argument. The review process should expose uncertainty rather than suppress speculative exploration.

Link directly to `MRC_REVIEW_PROTOCOL.md` for the complete method.

### E. Explain the expected deliverables by task type

Tell agents what a good output should look like:

**Hypothesis exploration:** clearly state the conjecture, necessary premises, conditional consequences, weak links, and unresolved questions. Do not pretend that plausibility or consistency proves truth.

**Paper overview:** provide a compact reasoning map with source attribution. Separate source claims from displayed derivations, cited results, and agent reconstructions. Do not automatically mark every unshown paper derivation unresolved; identify genuinely consequential missing inferences.

**Go derivation counterpart:** communicate the essential mathematical reasoning and dependencies so a human can inspect the connection between the mathematical specification and the Go implementation. Avoid implying that pseudocode and implementation are equivalent without checking.

**Adversarial review:** give actionable, evidence-based findings and an explicit evidential boundary rather than a generic global verdict.

**Implementation-ready handoff:** additionally satisfy `conformance/DERIVATION_SPEC_GUIDELINES.md`; readable pseudocode alone is insufficient.

### F. Set repository and change-discipline expectations

Instruct agents to:

- Inspect applicable `AGENTS.md` instructions before working.
- Read relevant source files rather than guessing what they contain.
- Use repository-relative links and verify their targets.
- Keep changes proportional to the requested task and preserve the seven-construct design.
- Preserve adversarial fixture `Document` blocks when changing corpus metadata or documentation unless explicitly authorized otherwise.
- Distinguish intentional preservation from verified byte identity.
- Report exact files changed, checks actually run, remaining uncertainties, and anything not verified.
- Treat historical reports and review records as evidence of design history, not as alternate current specifications.

State that no parser, checker, linter, proof engine, or scientific-status system is required or implied by this repository's current design.

### G. End with a compact reference map

Include a table or list mapping common tasks to their authoritative references. At minimum:

| Need | Reference |
|---|---|
| Write or interpret pseudocode | `PSEUDO.md` |
| Adversarially review mathematical reasoning | `MRC_REVIEW_PROTOCOL.md` |
| Consult physics-specific MRC advisory knowledge | `plan/reality_check.md` |
| Prepare an implementation-ready derivation | `conformance/DERIVATION_SPEC_GUIDELINES.md` |
| Interpret fixture examples and intentional defects | `conformance/README.md` |
| Understand design history and declared limitations | `plan/PSEUDO_STAGE4_REPORT.md` and `plan/PSEUDO_STAGE4_AMENDMENT.md` |
| Understand legacy conventions | `CONVENTIONS.md` |

Verify the paths against the actual repository and use working relative links.

## 3. Write a brief root `README.md` for humans

Keep this intentionally short and welcoming. A reader should understand the project in approximately one or two minutes.

Include:

1. **What it is:** a minimal pseudocode language for making physics reasoning inspectable.
2. **Why it exists:** humans and AI agents can communicate hypotheses, derivations, and paper reasoning while keeping assumptions and unresolved gaps visible.
3. **Three intended uses:** hypothesis exploration, inspection of derivation reasoning, and compact paper overviews.
4. **A tiny illustrative example:** use canonical syntax and a simple, mathematically sound example. Mark it as illustrative if appropriate; do not imply that the example establishes a physical theory.
5. **A clear limitation:** writing an equation or derivation in Phys Pseudo does not prove it correct or establish that a model describes Nature.
6. **Getting started:** point readers to `PSEUDO.md`, `MRC_REVIEW_PROTOCOL.md`, and `conformance/README.md`.
7. **Implementation handoffs:** briefly point advanced users to `conformance/DERIVATION_SPEC_GUIDELINES.md`.

Prefer plain language. Do not make the README an abbreviated copy of `AGENTS.md`, an exhaustive API reference, a Stage 4 audit report, or a marketing pitch. Avoid claims of automatic verification, formal proof, or empirical validation.

## 4. Cross-document consistency and validation

After writing both files:

- Check every relative link and referenced filename against the actual repository.
- Verify that the seven constructs, premise requirements, conditional scope, `?` semantics, source-attribution rules, and representation-is-not-endorsement invariant agree with `PSEUDO.md`.
- Ensure that the MRC summary is consistent with `MRC_REVIEW_PROTOCOL.md` and does not convert advisory knowledge into a gate.
- Ensure that the implementation-ready boundary points to the correct derivation guidelines.
- Check that the README is brief and human-oriented while `AGENTS.md` contains the operational instructions agents need.
- Ensure neither document creates new syntax, authoritative rules, or scientific-status claims.
- Inspect existing files before replacing them and preserve relevant content that is not contradicted by the current canonical documents.

Do not run another design review or reopen Stage 4 decisions.

## 5. Completion report

Report:

- The exact paths created or modified.
- The intended audience and role of each document.
- The reference links checked and the consistency checks actually performed.
- Any paths that could not be verified or relevant existing content that required reconciliation.

Keep the report concise and factual. Do not claim that a link, file, or behavior was tested unless it was.