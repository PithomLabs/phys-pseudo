Got it. The compression target is this: **the entire math reality check + governance layer folds into a single question asked of every ingredient — "how does a dispute about this get settled?"** Everything else was metadata. Here is the kernel.

```text
// ============================================================
// PHYSICS-IDEA REASONING KERNEL — minimal spec
// Per-ingredient metadata budget: ONE label (kind)
// Per-claim status budget:        ONE label (status)
// ============================================================

// ---------- 0. THE ONLY TYPES ----------
// kind   : PROOF  — dispute settled by re-derivation (where math shines)
//          DATA   — dispute settled only by measurement (where math is silent)
//          CHOICE — settled by declaration: gauge, measure, observer (never argued)
// status : PROVEN | MEASURED | UNDECIDED | FAILED
// (everything else — hypothesis, conjecture, analogy, model — is not a type;
//  it is language and gets rejected at the gate unless restated as one of the above)

// ---------- 1. DECLARATIONS — the data dictionary, upfront ----------
// 1a. CHOICE — declared once, inherited by all downstream reasoning
declare clock    : worldline -> duration        // proper time; the only time in GR
declare measure  : domain D -> average op       // must exist BEFORE any ⟨·⟩ is legal
declare observer : set of clocks                // whose seconds stamp the instruments

// 1b. PROOF — exact mathematics only
axiom   EFE                                     // Einstein field equations
theorem raychaudhuri                           // dθ/dτ = −θ²/3 − σ² − R(u,u)
theorem buchert(D)                             // ä_D/a_D = −(4πG/3)⟨ρ⟩_D + 𝒬_D/3
                                               //   [identity, irrotational dust]
theorem noncommute                             // ∂_t⟨A⟩ ≠ ⟨∂_t A⟩
// deliberately absent: "𝒬 ≥ 0" — not a theorem; shear may dominate the variance term

// 1c. DATA — magnitudes, domain-typed (the Buchert lesson: D is an argument, not a footnote)
data ρ, θ, σ        : fields                   // structure surveys
data f_v(z)         : void volume fraction
data SN, BAO, CMB   : distance–redshift records
data 𝒬_sim          : small (10⁻³–10⁻²)        // measured IN simulated ΛCDM boxes —
                                               //   NOT the same symbol as 𝒬_ours

// 1d. DERIVED — caches, never sources
derived H_eff, w_eff : f(EFE, measure, data)   // auto-reverts to UNDECIDED on any
                                               //   change above (no stale "70%")

// ---------- 2. THE AGENT LOOP (if / then / else / when) ----------
on claim c:
  // gate 0 — the reality check as a type checker
  if c asserts a magnitude while citing only PROOF ingredients: reject GRAMMAR_NOT_ENGINE
  if c uses ⟨·⟩ and measure undeclared:                         reject UNNAMED_AVERAGE
  // gate 1 — resolve strictly by kind
  switch c.kind:
    case PROOF:  if derive(c, from declared axioms): c.status = PROVEN
                 else:                               c.status = UNDECIDED
    case DATA:   if measurement(c) exists and passes: c.status = MEASURED
                 else:                               c.status = UNDECIDED
    case CHOICE: c.status = MEASURED                // declared, not debated
  // gate 2 — quarantine semantics: UNDECIDED is a state, not an error.
  //          Nothing is deleted. Ever.

when new_data arrives:
  for c in UNDECIDED where c.kind == DATA: re-run gate 1
  invalidate every derived                          // resubmit-on-change

when derive(c) succeeds:
  c: UNDECIDED -> PROVEN
  invalidate every derived depending on c

when a paper claims c.kind == PROOF:
  re-derive before ingestion; failure => c.status = FAILED   // corrections ledger as a status

// ---------- 3. THE IDEA, LOADED ----------
load idea: "cosmic acceleration is clock-variance bookkeeping, not a substance"

  c0 "𝒬 ≥ 0 for structure formation"        kind=PROOF  re-derivation fails   -> FAILED
  c1 "a mechanism exists"                    kind=PROOF  via noncommute+buchert-> PROVEN
  c2 "𝒬_ours ~ 0.7·ρ_crit"                   kind=DATA   no such measurement   -> UNDECIDED
  c3 "w_eff crosses −1 under measure<D>"     kind=DATA                         -> UNDECIDED
  c4 "observer = wall clocks; voids dominate volume" kind=CHOICE                -> declared

// c2 is the entire open problem. The kernel has nothing more to say about it.
```

## The Occam ledger

| Removed | Replaced by | Why it was not essential |
|---|---|---|
| UUIDs, IDs | Content of the claim itself | A claim's identity is what it says; duplicates of the same text are the same claim |
| Timestamps, version numbers | Re-derivation | Provenance = anyone can re-run gate 1; reproducibility replaces bookkeeping |
| Exploratory vs. derivation modes | One loop | Modes differ only in which UNDECIDED pool is drained — forward (attempt proofs) or backward (re-derive the paper's claimed PROVENs) |
| Hypothesis / conjecture / analogy labels | Nothing | Not representable. An analogy must be cashed out as PROOF or DATA or it is rejected — brutal, by design |
| Pick lists, controlled vocabularies | The 3-kind type system | The vocabulary is the type system |
| Quarantine subsystem | The UNDECIDED status | A state, not machinery |
| Rate limits, pagination, 429 | Out of scope | The survey pipeline's problem, not the reasoner's |
| "Tension" / "anomaly" vocabulary | Domain-typed symbols + status | 𝒬_sim ≠ 𝒬_ours is an argument difference, not a crisis |

**Kept, because each is load-bearing:** one kind label (mis-typing is *the* historical failure mode), UNDECIDED persistence (quarantine is what kept timescape alive), derived-as-cache invalidation (the stale 70% was the original sin), and domain as an argument on averages (unnamed averages are illegal).

## Reality check on the kernel itself

- **★ Shines:** gate 0 is cheap, symbolic, and total — no claim can be ill-typed, unnamed, or mode-ambiguous. Litigation becomes impossible because every statement has exactly one resolution path.
- **✗ Silent:** it computes nothing new. c2 stays UNDECIDED no matter how elegant the kernel. This is a gate, not an engine.
- **⚠ Residual risk:** CHOICE ingredients are load-bearing and unjustified by the kernel. A wrong `measure` or wrong `observer` declaration poisons every downstream PROVEN and MEASURED while remaining perfectly type-correct. The kernel can be flawlessly governed and entirely wrong about the world — that failure mode has a name, and it is Euclid's job.

**One-paragraph summary:** The design collapses two layers of prior machinery into a type system of three kinds and four statuses, with the math reality check running as gate 0 on every step: proof-claims must re-derive, data-claims must cite measurement, choice-claims are declared once and never argued, and anything that cannot declare its kind is language masquerading as computation and is rejected outright. The timescape idea loads into five lines — one retraction, one theorem, two open magnitudes, one declaration — and the whole open problem compresses to a single UNDECIDED symbol awaiting data. The kernel does not think for the physicist; it makes forgetting the distinction between grammar, evidence, and convention structurally impossible — which, after four rounds of corrections ledgers and duplicated column names, is the only feature that was ever essential.
