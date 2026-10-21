# Phys Pseudo — Conventions (pointer note)

**Status:** not a specification. `PSEUDO.md` is the single authoritative
specification of the seven constructs as of Stage 4. This page is kept only
as a pointer and compatibility note for readers holding Stage 1–3 documents.

**If you are writing or reviewing `phys-pseudo`, read [`PSEUDO.md`](PSEUDO.md)
first, then [`MRC_REVIEW_PROTOCOL.md`](MRC_REVIEW_PROTOCOL.md). Nothing here
adds to, qualifies, or overrides them.**

---

## What changed at Stage 4

The Stage 1 provisional conventions were consolidated after the Stage 3
adversarial review (`plan/final_REPORT_LOCKED.md`, PASS-WITH-AMENDMENTS).
The normative content moved as follows:

| Stage 1 text (this file, historically) | Now canonical |
|---|---|
| Seven-construct vocabulary and usage notes | `PSEUDO.md` §1–§6 |
| `given NAME = ... [from <source>]` | `given NAME:` — one spelling; attribution moved to prose (`PSEUDO.md` §8) |
| `assume <premise> [as LABEL]` / bare `[assume]` premises | `assume NAME:` — named when referenced; no unnamed premises (§2) |
| `?` attached to "the nearest preceding statement" | `?` mechanical attachment: the statement directly above, exactly one level deeper → statement; column 0 → document (§6) |
| §1 fidelity note: paper conclusion without displayed derivation is `claim` + `?` | `claim` + prose attribution; `?` only for a genuinely unresolved inference (`PSEUDO.md` §8, §9) |
| I1 — the MRC guide is advisory | `PSEUDO.md` §7 bullet + `MRC_REVIEW_PROTOCOL.md` ground rules |
| I2 — facts, not verdicts (representation ≠ endorsement) | `PSEUDO.md` §7 (central invariant) |
| I3 — no author-typed status | `PSEUDO.md` §7 |
| §3 "what tooling may assert" | Dropped as a separate rule; no tooling is specified, and no universal ceiling for future tools is prescribed (`PSEUDO.md` §10) |
| §4 minimal examples | Superseded by the audited conformance corpus, [`conformance/README.md`](conformance/README.md), and the illustrative examples in `PSEUDO.md` §9 |

## What this page no longer contains

No normative syntax, no invariants restated in full, no examples that could
be mistaken for canonical ones, no tooling ceiling, no scope promises. Any
older document citing this page for a rule should cite `PSEUDO.md` instead.

## History

- Stage 1: this page was the provisional conventions; `PSEUDO.md` was
  explicitly deferred until the vocabulary survived adversarial use.
- Stage 2: [`conformance/README.md`](conformance/README.md) corpus exercised
  them.
- Stage 3: adversarial review recorded in
  [`plan/final_REPORT_LOCKED.md`](plan/final_REPORT_LOCKED.md).
- Stage 4: `PSEUDO.md` + `MRC_REVIEW_PROTOCOL.md` written; this page demoted
  to a pointer.
- Final consistency amendment: selected improvements from the independent
  review under `plan/claude/` adopted into the three core documents
  (change log: [`plan/PSEUDO_STAGE4_AMENDMENT.md`](plan/PSEUDO_STAGE4_AMENDMENT.md)).
