Plan v2 is a substantial improvement. I approve its overall direction and the sequence Stage 1 → Stage 2 → Stage 3 → Stage 4, with one mathematical correction required before the conformance corpus is treated as a baseline.

The revision correctly removes computed scientific verdicts, keeps the MRC guide advisory, and makes the Markdown corpus—not a grammar or parser—the first real test of the pseudocode.&#x20;

plan2.md

plan2.md



## 1. One remaining mathematical error

The proposed operator-composition fixture still contains an incorrect counterexample. The plan correctly identifies it as an issue to audit, but the expected values should be fixed before it becomes the golden fixture.&#x20;

plan2.md



By the product rule,

\\[ (a\partial_a)^2 f = a\partial_a(af') = af'+a^2f''. \\]

Choose \\(f(a)=a^2\\). Then

\\[ (a\partial_a)^2f=4a^2, \qquad a^2\partial_a^2f=2a^2. \\]

So the expressions are not equal. The fixture's current RHS value is wrong.

This is precisely why our conformance tests need independently derived expected results. I would also slightly refine the audit rule: for a published-paper equation, verify the original source and independently check the derivation; for an elementary mathematical identity, verify the operator definition and independently work through the mathematics. The same audit principle applies, but not every mathematical fixture needs a physics paper as its primary source.

## 2. Answers to the implementation agent's open questions

### Question 1 — Sequencing approval

Approved: Stage 1 → Stage 2 → Stage 3 → Stage 4.

Begin with provisional conventions, construct the Markdown corpus, challenge it with counterexamples, and only then freeze the surviving conventions into `PSEUDO.md`. A checker remains optional and shallow. It must never certify mathematical truth.

### Question 2 — Fixture sources

Use the two auditable examples and symbolic/toy fixtures for the first corpus cut.

Correct and independently verify the operator-composition example. Retain the ladder-operator example only after its assumptions and expected derivation have been checked. Use symbolic examples for conditional reasoning and missing prerequisites rather than delaying the entire milestone while selecting additional physics references.

Add the Raychaudhuri fixture when its exact cited equation, conventions, and source mapping have been verified. Ellis–van Elst is a possible reference to evaluate, not an automatic approval of the fixture.

## 3. One constraint to keep especially visible

The new dependency-provenance design is the right correction: the system may report which assumptions, citations, and unresolved annotations a conclusion depends upon. It must not infer that the conclusion is true merely because its references resolve or because no `?` appears in its ancestry. The revised plan explicitly protects this boundary.&#x20;

plan2.md



That distinction should remain binding throughout implementation.

My recommendation: proceed with Stage 1, correct the operator-composition fixture before it enters the golden corpus, and use the first conformance round to discover whether the seven constructs genuinely suffice across exploratory reasoning and source-faithful derivations. No further architecture expansion is warranted yet.