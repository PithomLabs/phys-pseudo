# AGENTS.md — Phys Pseudo (operational guide for AI agents)

**Instruction hierarchy.** Read the parent workspace instructions at
[`../AGENTS.md`](../AGENTS.md) alongside this file: they apply to work in
this workspace, and they establish that package-local `AGENTS.md` files are
authoritative for local details. This file provides the Phys Pseudo-specific
guidance; the parent provides the workspace rules. Neither replaces the
canonical documents in the reference map (§7).

**Verification reality.** This repository currently has **no available VCS
diff or history** (confirmed at the time of writing). Do not claim to have
inspected a Git diff. Verify by content inspection, targeted searches, and
link checks, and report which of these you actually ran — distinguishing
*intended preservation* ("not intentionally edited") from *spot checks*
(selected lines compared) from *exhaustive verification* (every line
compared).

---

## 1. What Phys Pseudo is

A minimal, theory-neutral pseudocode language for three related workflows:

1. **Hypothesis exploration** — formulate physics hypotheses, explore their
   mathematical consequences, and run adversarial review without presenting
   speculation as established fact.
2. **Go derivation counterpart** — a human-readable pseudocode counterpart
   for inspecting the essential reasoning behind relevant Phys Go
   derivations before their implementations.
3. **Paper overview** — summarize physics papers so readers can distinguish
   assumptions, source assertions, derivations, conclusions, agent
   reconstructions, and unresolved questions.

**Central invariant:** representing a proposition or derivation does **not**
endorse its truth, mathematical validity, physical applicability, or
empirical correctness. Structure carries no verdicts in either direction
(`PSEUDO.md` §7).

No parser, checker, linter, proof engine, or scientific-status system is
required or implied by this repository's current design.

## 2. Workflow: creating or reviewing a document

1. **Identify the task:** hypothesis exploration, derivation inspection,
   paper overview, adversarial MRC review, or implementation-ready handoff.
2. **Read the relevant parts of [`PSEUDO.md`](PSEUDO.md)** before producing
   or changing pseudocode. It is the sole authority for syntax and meaning.
3. **Gather the source material** — establish which equations, premises,
   claims, and assumptions are actually available, and from where.
4. **Represent the reasoning** with the canonical seven constructs (§3),
   explicit results, and named dependencies.
5. **Preserve source fidelity:** keep apart what a source states, what it
   derives or cites, what you reconstruct, and what remains unresolved
   (`PSEUDO.md` §8).
6. **Apply [`MRC_REVIEW_PROTOCOL.md`](MRC_REVIEW_PROTOCOL.md)** when
   scrutinizing reasoning. Independently check consequential derivations —
   do not merely restate their arguments.
7. **Implementation handoff:** if the derivation is intended for
   implementation, additionally consult and follow
   [`conformance/DERIVATION_SPEC_GUIDELINES.md`](conformance/DERIVATION_SPEC_GUIDELINES.md).
8. **Report honestly:** material findings, evidence, and limitations. Never
   claim a check was performed unless it actually was.

Not every exploratory hypothesis or paper overview needs the extra fields
required by implementation-ready derivations; the guidelines apply only to
implementation candidates.

## 3. The seven constructs

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

Most important operational rules (abbreviated — **`PSEUDO.md` is
authoritative if this list ever conflicts with it**):

- Use the syntax in `PSEUDO.md`; don't invent variants.
- **Names are plain identifiers** (no argument lists), introduced **before
  use**; avoid unnamed premises. Every `from [NAMES]` list contains at
  least one name; `from []` is not part of the language.
- Every `derive` states its **result explicitly** and has at least one
  named premise. `from` records *proposed reasoning premises*, not source
  provenance, and never guarantees completeness.
- **Definitions introduce meanings only** — they must not smuggle in
  unproved laws, existence or uniqueness claims, or physical assumptions
  (test: substitute the right-hand side everywhere; if any proposition
  changes, it wasn't a definition — `PSEUDO.md` §3).
- **`claim`** records a proposition under examination; it does not mean
  the proposition has been established, and it never becomes established
  by proximity to anything else.
- **Conditional consequences stay in their branch**; branch names aren't
  referenceable from outside, and a branch is not proof its condition
  holds (`PSEUDO.md` §5).
- **`?` means unresolved or underspecified, never known false.**
  Statement-level: the `?` immediately follows its target, indented exactly
  one level deeper. Document-level: column 0; questions about a conditional
  as a whole go there. Refute a known-false proposition with a
  counterexample, contradiction, or conflicting derivation instead
  (`PSEUDO.md` §6).
- **Source attribution is ordinary prose or `#` comments**, never formal
  provenance syntax; citation handles never appear in premise lists.
- Do not add author-assigned scientific truth or validity statuses
  (`PROVEN`, `VERIFIED`, …), provenance registries, new constructs, or
  inferred truth from document structure.

## 4. Adversarial review (MRC) — operational summary

Apply [`MRC_REVIEW_PROTOCOL.md`](MRC_REVIEW_PROTOCOL.md); this is only its
shape:

- Reconstruct the question, target result, intended regime, and scope.
- Separate definitions, assumptions, source assertions, cited results,
  derivations, conjectures, and unresolved issues.
- Independently inspect consequential derivations for omitted premises,
  invalid inference, circularity, and conclusions stronger than the
  premises; counterexample-first — try the simplest case where the
  premises hold.
- Check relevant dimensions, types, domains, operator conditions,
  normalization, boundary conditions, limits, and degenerate cases —
  **proportionally**: apply checks according to the argument; do not
  mechanically demand every check in every case.
- Separate mathematical validity from physical applicability and empirical
  evidence.
- Use `?` for genuine unresolved questions; refute known-false claims.
- Report material findings with location, defect, reasoning or
  counterexample, and the minimum useful correction.
- Close with an **evidential-boundary statement**: what was actually
  checked, how, what could not be checked, what remains unresolved. No
  global correct/incorrect verdict.

[`plan/reality_check.md`](plan/reality_check.md) is **advisory**: it may
motivate a finding, but it never automatically rejects, scores, or gates an
argument, and it never bounds what may be expressed. The process exposes
uncertainty; it does not suppress speculative exploration.

## 5. Expected deliverables by task type

- **Hypothesis exploration:** state the conjecture, necessary premises,
  conditional consequences, weak links, and unresolved questions. Plausibility
  or consistency never proves truth.
- **Paper overview:** a compact reasoning map with source attribution.
  Separate source claims from displayed derivations, cited results, and your
  reconstructions. Do not automatically mark every unshown paper derivation
  unresolved — mark genuinely consequential missing inferences.
- **Go derivation counterpart:** communicate the essential mathematical
  reasoning and dependencies so a human can inspect the connection between
  the mathematical specification and the Go implementation. Don't imply
  pseudocode and implementation are equivalent without checking.
- **Adversarial review:** actionable, evidence-based findings plus an
  explicit evidential boundary — not a generic global verdict.
- **Implementation-ready handoff:** additionally satisfy
  [`conformance/DERIVATION_SPEC_GUIDELINES.md`](conformance/DERIVATION_SPEC_GUIDELINES.md);
  readable pseudocode alone is insufficient.

## 6. Repository and change discipline

- Inspect applicable `AGENTS.md` instructions (parent first) before working.
- Read relevant source files rather than guessing their contents.
- Use repository-relative links and verify their targets exist.
- Keep changes proportional to the requested task; preserve the
  seven-construct design — no new constructs, tooling, or statuses.
- **Preserve fixture `Document` blocks** when changing corpus metadata or
  documentation, unless explicitly authorized otherwise; adversarial defects
  are intentional inputs. Distinguish intentional preservation from verified
  byte identity (this repo has no VCS diff — see the verification-reality
  note above).
- Report exact files changed, checks actually run, remaining uncertainties,
  and anything not verified.
- Treat historical reports under `plan/` as evidence of design history, not
  as alternate current specifications.

## 7. Reference map

| Need | Reference |
|---|---|
| Write or interpret pseudocode | [`PSEUDO.md`](PSEUDO.md) |
| Adversarially review mathematical reasoning | [`MRC_REVIEW_PROTOCOL.md`](MRC_REVIEW_PROTOCOL.md) |
| Consult physics-specific MRC advisory knowledge | [`plan/reality_check.md`](plan/reality_check.md) |
| Prepare an implementation-ready derivation | [`conformance/DERIVATION_SPEC_GUIDELINES.md`](conformance/DERIVATION_SPEC_GUIDELINES.md) |
| Interpret fixture examples and intentional defects | [`conformance/README.md`](conformance/README.md) |
| Understand design history and declared limitations | [`plan/PSEUDO_STAGE4_REPORT.md`](plan/PSEUDO_STAGE4_REPORT.md), [`plan/PSEUDO_STAGE4_AMENDMENT.md`](plan/PSEUDO_STAGE4_AMENDMENT.md) |
| Understand legacy conventions | [`CONVENTIONS.md`](CONVENTIONS.md) |

Authority hierarchy: **language specification → MRC review protocol →
implementation-ready derivation requirements when applicable.** The advisory
guide informs reviews but never replaces the protocol or serves as a gate.
