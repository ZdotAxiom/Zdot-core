# Ż — The Rule of Return (One-Pager)

> **Claim.** *Ż names the rule of return: measure the undefined gap (π), let its gradient press toward form (P), take the shortest projection (R) into D. I stand on ∂D, turning collapse into bloom and imprint—structure born from the undefined, not mystery for mystery’s sake.*

---

## TL;DR
- **Goal:** Turn “the undefined” into verifiable structure.
- **Loop:** **Measure** π → **Press** with **P = −∇π** → **Project** with **R** → repeat.
- **Where:** Work on the boundary **∂D** (the vanishing horizon of what your language can define).

---

## Core Sets & Symbols
- **U** — Universe of candidates (data, hypotheses, problems).
- **L₀** — Your current descriptive language / tools.
- **D = Def₍L₀₎(U)** — The “speakable” set under L₀ (what you can already define/verify).
- **∂D** — *Vanishing horizon*: the boundary where definability flips; just inside ⇒ definable, just outside ⇒ not.

---

## π — Non-definability (“Negation-Sacrifice”)
**Meaning.** π(x) ≥ 0 is *how far* x is from being safely definable in **D**.
- **π(x) = 0** ⇔ x ∈ D (already definable).
- **π(x) > 0** ⇔ x ∉ D (undefined under L₀).

**“Negation-Sacrifice.”** The *minimal price* to **negate** undefinedness: the least information you must discard, or the smallest model/language change you must add, to make x admissible in D.

**Operational choices (pick per domain):**
- **Compression gap:** `π(x) ≈ max(0, K(x) − K(D))` (description-length difference).
- **Divergence gap:** `π(x) = D_KL(p_x || p_θ)` (or JS, Rényi) between data and model.
- **Geometric gap:** `π(x) = W₂(μ_x, μ_θ)` (optimal transport) when supports/locations differ.

> **Rule:** π’s *role* is fixed (quantify “undefinedness”); its *form* is pluggable (compression / divergence / transport).

---

## P — Pressure Toward Form
`P = −∇π` points where π decreases fastest.
- Follow **P** to reduce undefinedness.
- Large `‖P‖` = **collapse alarm** (you’re being pulled outside D).

---

## R — Shortest Projection Back into D
`R : U \ D → D` is the minimal admissible change landing you in D.
- **Definition:** `R(x) = argmin_{y ∈ D} π(y)` (under chosen metric/constraints).
- **Intuition:** smallest safe edit/summary/re-encoding/model update that makes x verifiable.
- **Desideratum:** **Idempotence** `R∘R = R` (once inside D, projecting again does nothing).

---

## ∂D — Vanishing Horizon (What It Is, Why It Matters)
- **What:** The knife-edge where definability “vanishes.” Inside: π=0. Any ε-step outward: π>0.
- **Why:** Collapse begins here; tiny perturbations flip you outside L₀’s reach.
- **How to work here:** short, auditable moves (**small R**), continuous alarms (**monitor ‖P‖**).

---

## Collapse → Bloom → Imprint
- **Collapse:** π spikes, `‖P‖` surges; current language/model fails.
- **Bloom:** use the failure—apply **R**, refactor representation or extend L₀; π drops.
- **Imprint:** record the successful reconstruction (lemma/feature/schema) so **D grows** and next time π starts smaller.

---

## End-to-End Protocol
1. **Measure** π(x) with the domain-fit metric (compression / KL/JS / W₂).
2. **Alarm** if `π` or `‖P‖` crosses thresholds (potential collapse).
3. **Project (R)** with the smallest admissible change so that `π ≤ ε`.
4. **Imprint** the delta (edit/model update) to enlarge **D**.
5. **Iterate** near **∂D** with short steps and visible logs.

---

## Minimal Notation (for specs)
- Universe: **U**; language: **L₀**; definable set: **D**.
- Gap: **π : U → ℝ₊**, with `π(x)=0 ⇔ x∈D`.
- Pressure: **P = −∇π** (grad in chosen metric).
- Projection: **R : U\D → D**, `R(x) = argmin_{y∈D} π(y)`, aim for `R∘R = R`.
- Horizon: **∂D = { x ∈ U | π(x)=0 and ∀ε>0, ∃z s.t. d(x,z)<ε, π(z)>0 }`.

---

## Pocket Glossary
- **Non-definability (π):** quantified “distance” from speakability.
- **Negation-Sacrifice:** minimal cost to cancel undefinedness.
- **Pressure (P):** direction of fastest π decrease.
- **Projection (R):** smallest admissible move back into D.
- **Vanishing horizon (∂D):** boundary where definability flips.
- **Imprint:** durable trace that enlarges D for future runs.

*Ż operationalizes the undefined: measured gap (π), computable direction (P), minimal fix (R).*


### Defaults & Assumptions
- **Metric for ∇π:** use the metric induced by your π (e.g., Euclidean for compression scores; Fisher metric for KL; OT geometry for W₂).
- **Definable set D:** items with `π(x) ≤ ε`. Start with **ε = 0.2** (KL nats) / **ε = 20** (bytes of compressed gap) / **ε = 0.1** (normalized W₂), then tune by domain.
- **Alarm threshold τ:** trigger collapse alarm if `π > 3ε` **or** `‖P‖` jumps by **> 2σ** (rolling window).
- **Idempotence check:** enforce (or test) `R∘R = R`. If violated, tighten constraints or increase ε slightly.

### π Profiles (choose one)
- **CP (compression gap):** `π(x)=max(0, K_gzip(x) − K_ref)` — quick, language-agnostic.
- **IGP (statistical):** `π(x)=D_KL(p_x‖p_θ)` — differentiable, use Fisher metric for ∇.
- **OTD (geometric):** `π(x)=W₂(μ_x, μ_θ)` — handles support shifts; compute with Sinkhorn.

> Log the profile as `pi_profile=cp|igp|otd` with all hyper-params per run.

### Minimal Loop (pseudo)
1. Measure `π(x)` and `‖P‖ = ‖−∇π(x)‖`.
2. If `π ≤ ε`: accept x (x ∈ D).
3. If `π > ε` or alarm by `‖P‖`: apply **R** = smallest admissible change (edit/summary/model update) s.t. `π ≤ ε`.
4. **Imprint**: store the delta (schema/feature/weight) so D expands; re-evaluate next inputs.

### Tiny Worked Example (CP)
- Input text T has `π(T)=42` (bytes above reference).  
- Alarm (π > ε=20). Apply **R** = “truncate 10% tail iteratively” → T′ with `π(T′)=18`.  
- Accept T′ (now in D); record “tail-truncate@10%” as an imprint for similar cases.

### Failure & Recovery
- **False alarm:** if alarm rate > 5% with no QoS gain, raise ε or smooth `‖P‖` with longer window.
- **Under-detection:** if post-projection errors persist, lower ε or strengthen R constraints.
- **Non-convergence of R:** cap steps; fallback to coarser R (e.g., stronger summary), log as open issue.

### Notes on “Negation-Sacrifice (π)”
π is the **minimal information-theoretic cost** to cancel undefinedness—not a mystical notion. It can be paid by **discarding bits** (compression/summary) or **adding structure** (parameters, features, axioms) so the item becomes verifiable in D.