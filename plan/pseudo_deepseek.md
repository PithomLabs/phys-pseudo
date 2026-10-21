# Minimal Data Dictionary + Reality-Check Pseudocode

Three type declarations. One record. Four rules. That is the entire metadata surface. Anything else (source: paper/exploratory, timestamps, notes, rate limits, transaction names, field UUIDs) is stripped — Occam's razor.

```
-- ============================================
-- DATA DICTIONARY (declared once, upfront)
-- ============================================

Branch  := arith|geom|alg|calc|topo|spec|cplx|dof
         | dual|emrg|entr|inv|lang|sym

Address := UUID | NAME       -- observable vs theoretical vocabulary

State   := PENDING | COMPLETE | FAILED
         | BLOCKED.{ NOT_IN_BRANCH
                   | OUT_OF_SCOPE
                   | NON_WRITABLE
                   | MIXED_ADDRESS
                   | WEAK_EVIDENCE }

-- ============================================
-- RECORD (the only structure)
-- ============================================

Idea := { branch  : Branch
          claim   : str
          address : Address
          state   : State
          evidence: str? }

-- ============================================
-- RULES (math reality check at each step)
-- ============================================

check(i: Idea, a: Assertion) :=
  a ∩ silence[i.branch]   → i.state := BLOCKED.NON_WRITABLE
  a ⊄ capacity[i.branch]  → i.state := BLOCKED.NOT_IN_BRANCH
  a ⊄ scope[i.branch]     → i.state := BLOCKED.OUT_OF_SCOPE
  i.address = MIXED       → i.state := BLOCKED.MIXED_ADDRESS
  else                    → i.state := PENDING

advance(i: Idea, e: Evidence) :=
  e sufficient[i.branch]  → i.state := COMPLETE, i.evidence := e
  else                    → i.state := BLOCKED.WEAK_EVIDENCE

read(i: Idea) :=
  i.state ≠ COMPLETE      → HALT
  else                    → i.evidence

compose(a: Idea, b: Idea) :=
  a.address ≠ b.address   → BLOCKED.MIXED_ADDRESS
  a.state ≠ COMPLETE      → PENDING
  b.state ≠ COMPLETE      → PENDING
  else                    → COMPLETE
```

---

## Why each field survives Occam's razor

| Field | Cannot remove because |
|---|---|
| `branch` | Without it, `check` has nothing to route against. It *is* the reality check. |
| `claim` | The assertion being tested. |
| `address` | Distinguishes observable (UUID) from theoretical construct (NAME). Mixed = rejected. This is the Claravine/UUID discipline; it is the only field that catches "dark energy is an illusion" as a category error. |
| `state` | The status-before-data gate. Typed subtypes route the next query. |
| `evidence` | The only field that can flip PENDING → COMPLETE. |

**Removed**: source (paper/exploratory — the template is invariant to this, so it cannot appear in the record), timestamp, transactionName, fieldUuids array, notes, rate-limit fields (abstracted into `scope`), pagination (abstracted into `scope`), headers.

---

## Worked example — the dark-energy claim, same template

```
-- derivation-mode or exploratory-mode, identical record:

idea_1 := {
  branch   : geom,
  claim    : "Q_D reproduces observed acceleration",
  address  : UUID,                     -- distance-redshift relation
  state    : PENDING,
  evidence : null
}

-- step 1: apply reality check to the framework claim
check(idea_1, "Q_D has the right form") :
  in capacity(geom)?   yes              -- homogenization is native
  in scope(geom)?      yes
  in silence(geom)?    no
  → state := PENDING

-- step 2: apply reality check to the numerical claim
check(idea_1, "Q_D is large enough") :
  in capacity(geom)?   yes              -- framework exists
  in scope(geom)?      yes
  in silence(geom)?    no               -- magnitude not a silence; it is scope
  → state := PENDING

-- step 3: evidence required
advance(idea_1, "numerical relativity simulations done") :
  simulation absent    → state := BLOCKED.WEAK_EVIDENCE

-- step 4: read gate
read(idea_1) :
  state ≠ COMPLETE     → HALT
  → verdict unavailable; transaction remains PENDING

-- step 5: forbidden step, catches itself
check(idea_1, "therefore Λ = 0") :
  a ∩ silence(geom)    yes              -- geom is silent on parameter selection
  → state := BLOCKED.NON_WRITABLE
```

The result the pseudocode emits is the honest one: **framework well-posed, magnitude unverified, verdict blocked.** It cannot emit "dark energy doesn't exist," because the only rule that could have emitted it returns `NON_WRITABLE` at step 5.

---

## The invariants that make this work

1. **One record type for both modes.** Derivation and exploration use the same `Idea` — the difference is only the *threshold* inside `sufficient[branch]` (published result vs. back-of-envelope estimate), which is a per-branch constant, not a per-idea field.
2. **Every assertion goes through `check` before it advances.** No assertion skips the gate.
3. **`read` refuses non-COMPLETE.** Verdicts cannot be read from PENDING or BLOCKED states — this is the Claravine "status before data" discipline.
4. **`compose` enforces consistent addressing.** You cannot mix a UUID-addressed observable with a NAME-addressed theoretical construct in a multi-idea chain.
5. **Typed silences route the next query.** `BLOCKED.NOT_IN_BRANCH` → try another branch. `BLOCKED.OUT_OF_SCOPE` → get more data or simulate. `BLOCKED.NON_WRITABLE` → stop; this branch cannot answer; go to experiment. `BLOCKED.WEAK_EVIDENCE` → get stronger evidence. `BLOCKED.MIXED_ADDRESS` → re-address consistently.

The whole design is 9 lines of type declaration, 1 record, 4 rules. If a line can be removed and reasoning still works, it is metadata bloat — and it is gone.
