Got it. The data dictionary is not a metadata database. It is the pseudocode declaration of everything an AI agent needs to reason about a physics idea without silently inventing missing ingredients.

We should optimize for maximum mathematical meaning with minimum labels.

## 1. One minimal pseudocode format, two entry points

The exploratory workflow and published-paper workflow should use the same pseudocode vocabulary. They differ in where the information comes from and what the agent is allowed to conclude.

### A. Exploration

Input: a human statement, article, intuition, or conjecture.

```
input "Could inhomogeneity explain acceleration?"

define Q_D := ...
assume dust, foliation, domain D

hypothesis H:
    Q_D can explain the target acceleration

if Q_D satisfies the required condition:
    then H holds within this model
else:
    H fails within this model

? Q_D cannot yet be evaluated:
    metric and initial data are unspecified
```

Schematic example only; no physical result is established.

### B. Published-paper derivation

Input: an existing physics paper and its actual equations.

```
source paper §N, Eq. (N)

assume [paper's stated assumptions]
define Q_D := [paper's definition]

derive step_1 from [declared premises]
derive step_2 from step_1, [other premises]

claim result := [paper's conclusion]

? [intermediate step not shown in paper]
```

Illustrative format; the extraction must follow the actual paper.

The crucial distinction: exploration may introduce hypotheses freely. Paper extraction must faithfully represent what the authors actually define, assume, derive, cite, or leave unexplained. An assertion in a paper must not be rewritten as a derivation simply because an agent believes it is correct.

## 2. The minimum vocabulary

I would start with only these constructs:

| Construct          | Purpose                                                                       |
| ------------------ | ----------------------------------------------------------------------------- |
| `input`            | The statement, source, or problem being investigated                          |
| `assume`           | A premise accepted provisionally for the current reasoning                    |
| `define`           | The meaning of a symbol, quantity, or mathematical object                     |
| `claim`            | A proposition being considered, without presuming it is true                  |
| `derive`           | A conclusion obtained from explicit premises and reasoning                    |
| `hypothesis`       | A conjecture introduced during exploration                                    |
| `if / then / else` | Conditional reasoning and its alternative branches                            |
| `?`                | A missing definition, ambiguity, unsupported step, or unresolved prerequisite |

Source references should be inline where needed, rather than repeated through a large metadata structure. Existing PhysMath or PhysLib references can be reused when an exact match exists; unknown concepts should remain locally defined instead of forcing a premature universal taxonomy.

## 3. Apply MRC at every step—but emit only what matters

The agent should internally check each declaration and inference:

- Are the symbols defined?
- Are the assumptions and applicable regime explicit?
- Are the mathematical types, units, dimensions, and domains compatible where relevant?
- Does the conclusion actually follow from the preceding steps?
- Is this result derived, assumed, quoted, or merely conjectured?

The output should not be a report listing every successful check. It should be the pseudocode itself, with a concise `?` annotation exactly where the reasoning encounters a meaningful gap.

A missing metric, for example, is not a generic warning. If the next step requires calculating \\(Q_D\\) from a physical solution, the pseudocode identifies that missing dependency at the calculation that needs it.

Crucially, a conjecture does not need to pass a proof test before it can be explored. The agent can continue reasoning conditionally. MRC simply prevents the conjecture from being misrepresented as an established result.

## 4. What we remove

For this scope, we do not need a transaction engine, a two-phase commit protocol, elaborate status taxonomies, a global identifier for every symbol, or a separate metadata record for every successful reasoning step.

We add complexity only when a concrete use case demonstrates that the simpler representation cannot preserve mathematical meaning or provenance.

The data dictionary itself becomes the compact, inspectable pseudocode preamble an AI agent reads before continuing its reasoning. Phys can generate it from a human's idea or a published paper, and the same representation can later support deeper verification without requiring us to build that verification machinery now.

That is the Occam-aligned design: declare the ingredients, make the logic explicit, expose the gaps, and leave the agent free to explore.
