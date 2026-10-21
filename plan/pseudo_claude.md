Got it. The MRC moves out of the labels and into the operators as guards, so the metadata can mostly disappear. Here is the kernel.

```
# DECLARE: only what math cannot supply
given  NAME = value | form     from  measured(@src) | postulated
want   Y  vs  N                # one output, one generic competitor

# OPERATORS: the reality check as guards (no branch labels)
evolve(law, state0)          needs state0 ∈ given
average(f, domain, weight)   needs linear(f) or closure ∈ given
                             else result + OPEN(closure)
conserve(Q)                  needs symmetry(Q) ∈ given → "conserved"
                             elif forced by law's consistency → "identity" only
coarse(scale)                needs scale_separation ∈ given and flow ∈ given
fix(constant)                → always given      # no branch of math selects constants
bound(Y, data)               needs data ∈ measured, else OPEN(data)
rename(A, B)                 → alias; status(B) = status(A), adds nothing

# STATUS: computed, never typed
status(c) = OPEN(missing)    if guard(c) fails or any input is OPEN
          = DERIVED(G)       otherwise, G = givens in c's ancestry

# AGENT LOOP
for step in reasoning:
    if any symbol ∉ declared:  HALT              # the only hard error
    c = step.operator(args);  c.status = status(c)
if Y is OPEN:            print Y.missing         # the agenda, computed
elif N also yields Y:    Y = OPEN(observable separating Y from N)
else:                    print Y, G split into measured / postulated
```

**Worked check (backreaction)**

```
given law   = Raychaudhuri(dust, shear=0)        postulated
given parts = {void, wall}, weight = volume      postulated
given P(k)  = primordial spectrum                measured @CMB
want  q<0 from structure alone  vs  ΛCDM

a1 = average(Ḣ_i, parts, volume) → ä/a = −(4πG/3)ρ̄ + 2Var(H)   DERIVED(law, parts)
a2 = bound(Var(H) > Ωm·H²/4, data)  → OPEN(nonlinear Var(H): sims / Euclid)
a3 = fix(Λ)                         → given; cannot be derived
a4 = coarse(scale)                  → OPEN(scale_separation)
a5 = rename(morphon, evolving DE)   → alias, no gain
Y  = q<0 from structure alone       → OPEN(a2)      # weakest ancestor wins
```

The output matches the last revision of my answer, but it is now computed rather than argued.

**What Occam removed**

- **Mode flag (exploratory or paper derivation):** both use the same kernel. A paper yields mostly DERIVED with its givens listed, and an exploratory idea yields OPEN items.
- **Branch and map labels:** the operator carries its own guard.
- **Role and type labels on givens:** the role is the operator slot (`state0`, `closure`).
- **The five-rung ladder:** it collapses to two states. Derived versus postulated lives in the given-list, not in the status.
- **Confidence scores:** the weakest ancestor wins. Averaging scores hides the worst step, which is the same variance lesson as the cosmology.
- **Next-steps field:** the OPEN list is the agenda.
- **IDs, transactions, dedupe, audit:** these are infrastructure around the kernel, not reasoning.

**What is left:** three declaration forms, seven operators, one hard error, two states, and one label pair (`measured | postulated`, plus an optional `@src`).

**Caveats:** the guards come from the maps I actually read (calculus, geometry, emergence, invariants). Other physics ideas will need more operators, each guarded by what its map says is silent. The next cut I'd make is `vs N`, since derivations survive without it and only the empirical weight is lost. I kept it because a claim with no competitor can't be tested.

I can save this as a file or write it as Go types for the evaluator if you want.
