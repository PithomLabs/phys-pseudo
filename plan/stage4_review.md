The Stage 4 output is structurally on the right track. It has established the intended separation between the canonical language, the adversarial review protocol, and implementation-ready derivation requirements. It also preserves the seven-construct vocabulary and keeps automated checking out of scope.&#x20;

PSEUDO.md

MRC_REVIEW_PROTOCOL.md



I would not quite close the milestone yet. I found three consistency issues worth fixing with one small amendment—not another design or review stage.

## Findings

1\. The canonical syntax has two inconsistencies.

`PSEUDO.md` §1 specifies `else <alternative>`, but the worked example uses `else: this argument does not establish convergence`. The same example has a line beginning `| a claim at document level` after `claim H`; the specification only defines `|` as the separator in a `derive` statement and identifies `#` as the comment marker.&#x20;

PSEUDO.md

PSEUDO.md



Correction: Choose one `else` spelling and use it in the template and example. Replace the leading-pipe annotation with a `#` comment or prose outside the code block.

2\. The README overstates what remained unchanged.

The README says the corpus has “unchanged documents” and later that the documents are “byte-identical to Stage 2.”&#x20;

README.md

README.md



The implementation report describes edits to fixture metadata, expected findings, status lines, and audit-history sections, while preserving the original `Document` blocks. Those are different claims.

Correction: Say that the original `Document` blocks are preserved verbatim, while fixture metadata and expected findings were revised. Only claim byte identity where it was actually checked, and specify exactly which material was compared.

3\. Clarify the boundary between scientific statuses and corpus audit labels.

`PSEUDO.md` prohibits author-typed status labels such as `PROVEN`, `VERIFIED`, and `SUPPORTED`. Meanwhile, the corpus README uses `GOLDEN`, `TOY`, `ILLUSTRATIVE`, and `ANTI-PATTERN` as audit and fixture classifications.&#x20;

PSEUDO.md

README.md



These can coexist: one describes the audit history or purpose of a test fixture; the other would assert the truth or validity of scientific content. But the distinction should be explicit.

Correction: Clarify that corpus metadata records audit provenance and test purpose, not a scientific truth verdict. Keep such metadata outside the pseudocode claims and derivations.

## Recommended next action

Give the coding agent a tightly bounded cleanup task:

Make a final consistency-only amendment to the Stage 4 `phys-pseudo` documentation.

1. In `PSEUDO.md`, make the canonical `else` syntax consistent between the seven-construct template and the worked conditional example. Replace the unexplained leading-pipe annotation after `claim H` with a `#` comment or explanatory prose outside the pseudocode block.
2. In the conformance corpus README, distinguish preserved `Document` blocks from edited fixture metadata, expected findings, status lines, and audit history. Remove any claim that entire fixture documents are byte-identical unless that exact comparison was performed.
3. Clarify that `GOLDEN`, `TOY`, `ILLUSTRATIVE`, and `ANTI-PATTERN` are corpus audit/test-purpose metadata, not claims that scientific propositions are true, valid, or empirically supported. Preserve the prohibition on author-typed scientific truth or validity statuses in pseudocode.
4. Make only the necessary documentation changes. Do not rewrite fixture `Document` blocks, alter their scientific reasoning, add language constructs, introduce tooling, or reopen the Stage 3 design decisions.
5. Report exact changed files and verify that the template, examples, README, and conventions pointer no longer contradict one another. Distinguish checks actually performed from assumptions.

Stop after this consistency pass; do not start another review stage.

Scope note: I reviewed the uploaded canonical specification, protocol, conventions note, and corpus README. The individual fixture files were not included, so I have not independently verified every revised expected finding against the Stage 3 report. That remains distinct from this document-level consistency check.



## consolidated

I reviewed the three files from the separate agent and consolidated them with my previous findings. The separate agent substantially improves the MRC review protocol and simplifies the language specification, but I would not adopt the files verbatim. A few changes conflict with previously settled rules, and the revised specification contains its own inconsistencies.

The right next step is a single, bounded consistency amendment—not another design or adversarial-review stage.
1. What I would adopt from the separate agent

The stronger MRC review protocol

Retain its practical guidance: reconstruct the target and scope; verify source attribution; independently rederive consequential steps; test simple cases and counterexamples; inspect domains, dimensions, operator conditions, normalization and limiting cases when relevant; distinguish theoretical validity from physical applicability and empirical evidence; and report the minimum corrective action. 
MRC_REVIEW_PROTOCOL.md
MRC_REVIEW_PROTOCOL.md

The requirement to report what was actually checked, how it was checked, and what remains unresolved is particularly valuable. 
MRC_REVIEW_PROTOCOL.md





The more concise PSEUDO.md

Keep its plain identifier convention, declaration-before-use rule, explicit separation of definitions and premises, conditional scope, ordinary-prose source attribution, and the principle that a derivation proposes an inference without validating it. The test of substituting a definition with its right-hand side is a helpful way to expose assumptions concealed inside definitions. 
PSEUDO.md
PSEUDO.md





A compatibility-only CONVENTIONS.md

Keep the shortened pointer instead of maintaining two competing specifications. Its migration table is useful for readers encountering legacy fixtures and earlier documents. 
CONVENTIONS.md




2. What should not be adopted without correction
Issue	Consolidated decision
Empty premise lists	Preserve the existing requirement that from [NAMES] contains at least one named premise. The new specification allows from [], which conflicts with the previous canonical rule.  PSEUDO.md PSEUDO.md
? attachment	Retain a deterministic rule: a statement-level ? immediately follows its target and is indented one level deeper; document-level questions begin at column zero. Use a document-level question for a conditional or branch-wide uncertainty unless a separate branch-attachment rule is explicitly defined.
Paper assertions without derivations	Do not automatically attach ? every time a paper states a conclusion without displaying its derivation. Represent the assertion faithfully as a claim, attribute it to the paper, and add ? only when the missing justification or inference is genuinely unresolved. The new specification's table currently makes that attachment automatic.  PSEUDO.md
Future tooling	Do not reintroduce an absolute restriction that any future tool may check only document form. Keep tools out of this milestone; future capabilities should receive their own specification and review. The current specification need not decide every future tool's limits.  PSEUDO.md
Scientific and corpus statuses	Preserve the distinction between scientific truth claims and fixture audit metadata. Labels such as GOLDEN or ANTI-PATTERN may describe a fixture's audit history or purpose; they must not imply that its scientific propositions are true.
There is also a concrete internal inconsistency in the revised language example: its ? about the sign of \(s\) is at the same indentation as derive s_below, despite the specification's own rule requiring a statement-level ? to be more deeply indented. Moreover, the question concerns the branch's remaining uncertainty, not whether the stated inequality \(s\leq a\) follows. Correct the example as well as the rule. 
PSEUDO.md
PSEUDO.md

Finally, two issues from my previous review remain open: the corpus README's assertion of byte identity needs to be reconciled with the reported metadata edits, and the corpus classifications need an explicit explanation that they are audit metadata rather than scientific verdicts. The README uploaded earlier claims the documents are byte-identical to Stage 2, while the implementation report describes changes outside the Document blocks. 
README.md

3. Consolidated prompt for the coding agent
Task: Final Consistency Amendment to Phys Pseudo Stage 4
Objective
Reconcile the latest PSEUDO.md, MRC_REVIEW_PROTOCOL.md, and CONVENTIONS.md with the previously settled Stage 4 decisions and the most recent independent review.

Make only the minimum necessary amendments. Do not reopen the seven-construct design, rewrite the adversarial fixture documents, introduce tooling, or start another review stage.
Required changes
1. Preserve the canonical language contract.
   - Retain the seven constructs and the separation between language, MRC review, and implementation-ready derivation specifications.
   - Retain declaration-before-use, named premises, explicit derivation results, and the ban on using definitions to smuggle independent assumptions.
   - Restore the existing requirement that every from [NAMES] list contains at least one name. Do not introduce from [] in this amendment.
2. Resolve ? semantics and examples.
   - Make the attachment rule deterministic and internally consistent.
   - A statement-level ? must immediately follow its target statement and be indented one level deeper.
   - A document-level ? begins at column zero.
   - Questions about a conditional as a whole should use the document-level form unless the specification explicitly and unambiguously defines a separate branch-attachment form.
   - Correct the worked example: its unresolved question about the sign of s must not appear to question the already-established inequality s ≤ a.
   - Keep ? for unresolved questions only. Known-false propositions require a counterexample, contradiction, or conflicting derivation.
3. Preserve source fidelity without overusing ?.
   - Paper assertions without displayed derivations may be represented by claim with honest prose attribution.
   - Add ? only when a consequential inference, justification, or supporting result is genuinely unresolved or underspecified.
   - Do not convert the mere absence of a displayed derivation into an automatic unresolved status when the source's assertion and attribution are already clear.
   - Keep source attribution outside formal from [NAMES] syntax.
4. Keep tooling out of scope.
   - State that this milestone defines no parser, checker, or other tooling.
   - Do not prescribe a universal capability ceiling for all possible future tools.
   - Retain the central invariant: representing a statement or derivation does not establish its mathematical validity, physical applicability, or empirical truth. No tool output acquires such authority merely by being represented in this language.
5. Strengthen the MRC protocol using the valid independent-agent additions.
   Retain the practical guidance to:
   - reconstruct the target, regime, and intended scope;
   - check source fidelity and distinguish source assertions from derivations and reconstructions;
   - independently examine consequential derivations, including omitted premises, circularity, and conclusions stronger than the premises;
   - use counterexamples or simple test cases where useful;
   - inspect dimensions, types, domains, operator conditions, normalization, boundary conditions, limits, and degenerate cases when relevant;
   - assess physical applicability and empirical evidence separately;
   - report what was actually checked, how it was checked, what remains unresolved, and the minimum useful correction.
   Keep checks proportional to the argument. Do not turn the guidance into a mandatory universal checklist or a system of computed scientific statuses.
6. Reconcile cross-document claims and references.
   - Inspect the actual repository paths for reality_check.md and DERIVATION_SPEC_GUIDELINES.md; use consistent relative links in all three documents.
   - Keep CONVENTIONS.md as a pointer and migration note, not a competing specification.
   - Inspect the actual conformance README. Distinguish verbatim-preserved Document blocks from edited metadata, expected findings, headers, status lines, and audit history.
   - Claim byte identity only for content that was actually compared.
   - Clarify that corpus labels such as GOLDEN, TOY, ILLUSTRATIVE, and ANTI-PATTERN describe audit provenance or test purpose, not scientific truth or validity.
Constraints
Do not rewrite the fixture Document blocks. Do not change their scientific reasoning or erase deliberately flawed adversarial examples. Do not create a parser, checker, linter, computed-status engine, provenance registry, or new syntax. Do not reopen the language-design debate.
Completion report
List the exact files changed, summarize the corrections, identify any remaining uncertainty, and state the checks actually performed. Stop after this amendment.




Bottom line: adopt the separate agent's stronger review methodology, keep the concise language specification, and apply the corrections above. That gives Phys a practical MRC process without weakening the already settled language contract or turning the review protocol into a new software framework.