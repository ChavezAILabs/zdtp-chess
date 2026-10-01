# ZDTP Chess — Corrections Register

A public, append-only record of errors found in ZDTP Chess documentation and code. Entries are never deleted; a corrected entry keeps its original text and gains a `Corrected` block underneath.

This register follows the format of the [CAIL-rh-investigation CORRECTIONS.md](https://github.com/ChavezAILabs/CAIL-rh-investigation/blob/main/CORRECTIONS.md). ZDTP Chess entries live here rather than there because the claims belong to this repository, the same reasoning that gave the Canonical Six corrections their own register.

**Severity scale:** 1 cosmetic · 2 documentation error (reader misled, no result changes) · 3 interpretation error · 4 result error (published claim unsupported or false).

---

## Index

| ID | Title | Sev | Status |
|---|---|---|---|
| C-001 | README cited a superseded, vacuous Lean file as formal grounding | 4 | **Corrected** |

---

## Entries

### C-001 — README cited a superseded, vacuous Lean file as formal grounding
**Found:** 2026-10-01 · **By:** Paul Chavez (README correction handoff) / Claude Code · **Severity:** 4 · **Status:** **Corrected**
**Affects:** `README.md` (Features, The Math Section, How It Works, Architecture, Mathematical Foundation, Applications, Roadmap, install URLs); `zdtp_chess_mcp/dimensional_portal.py`; `zdtp_chess_mcp/zdtp_chess_server.py`
**Cross-references:** CAIL-rh-investigation C-016 (vacuous `CD4_mul`), C-018 (scope of the replacement file)

**The claim as published:** "ZDTP Chess v2.0 features are grounded in machine-verified proofs from `ChavezTransform_Specification_aristotle.lean`", listing Theorem 5 (`K_Z(P,Q,x) ≤ 4(‖P‖² + ‖Q‖²)‖x‖²`), Theorem 3 (`(1 + ‖x‖²)^(−d/2) ≤ 1`), and a stability constant `M = (‖P‖² + ‖Q‖²) · √(π/α)`. The README also stated that information moves "losslessly" between 16D, 32D and 64D, and that gateway convergence identifies "framework-independent optimal moves with mathematical certainty."

**Why it is wrong:**
1. `ChavezTransform_Specification_aristotle.lean` defines `CD4_mul` as the zero function, so every theorem that depends on multiplication is vacuous (CAIL-rh-investigation C-016). It was superseded by `ChavezTransform_genuine.lean` on 2026-04-16.
2. The stability constant in the README does not match the verified one. `ChavezTransform_genuine.lean` defines `stability_constant P Q α = 2(‖P‖² + ‖Q‖²)/(α·e)`, from the sharp bound `x²·exp(−αx²) ≤ 1/(α·e)`.
3. Even against the genuine file, the bilateral kernel result is an exact equality on the e₀ scalar channel only, where the zero-divisor structure is not exercised (CAIL-rh-investigation C-018). It cannot ground a feature whose motivation is zero-divisor behaviour.
4. "Lossless" preservation holds because each smaller vector is copied as a prefix of the larger one. That is preservation by construction, not a consequence of the algebra. `transmission_fidelity` was the literal `1.0`, not a measurement.
5. Gateway convergence is a stability signal across feature weightings, not a proof of optimality.

**What is true instead:** `tactical_ceiling` (Dim 52), `mobility_occlusion` (Dim 54) and the Master Dampener threshold (`M = 0.5`, empirically tuned) are heuristics informed by the Chavez Transform analysis, not consequences of verified theorems about the chess evaluation. Whether the gateway-derived dimensions (24–27, 52, 56–59, 63) contribute signal at all is untested; the ablation that would settle it is named in the README's Open Questions section.

**Corrected:** 2026-10-01. `README.md` "Formal Verification (Session 0.1)" replaced by "Analytic Grounding (Session 0.1)" with an explicit scope statement and retraction note; transmission, convergence and roadmap language rewritten; Open Questions section added; repository URLs moved from `pchavez2029` to `ChavezAILabs`. In code, the hardcoded `transmission_fidelity` and `overall_fidelity` keys were removed from `dimensional_portal.py`, along with the "Transmission Fidelity" line in the dimensional analysis output. `lean/ChavezTransform_Specification_aristotle.lean` is retained for provenance, with `lean/README.md` marking it as superseded.

**Not done, and not claimed to be done:**
- Code docstrings and comments in `strategic_analyzer.py` and `test_session_01_verification.py` still describe dims 44–55 as "formally verified" and cite the superseded file.
- `zdtp_showcase.py` reports a "Transmission Fidelity" that measures only whether dims 0–15 were copied, and labels it as zero-divisor verification.
- `_reduce_gateway_features` (`dimensional_portal.py`) sorts gateway interaction coefficients by magnitude, which discards which basis element each came from.
- The gateway-dimension ablation (dims 24–27, 52, 56–59, 63) has not been run.

---

## Log

| Date | Change |
|---|---|
| 2026-10-01 | Register opened. C-001 entered and closed as **Corrected**. |

---

*Chavez AI Labs LLC — Applied Pathological Mathematics*
