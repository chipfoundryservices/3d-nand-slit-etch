# Chapter 2: The Stack Beneath the Slit — Layers, Landing Stack & Stress

## Overview

A slit etch passes through every film between the top of the array and the source beneath it. Most of that depth is hundreds of alternating oxide and nitride layers. There are also cap and inter-deck oxides, select-gate and dummy layers with different thicknesses, thick staircase fill oxide where the slit crosses the staircase, and at the bottom a source stack that the slit must open into without breaking through. The stack's composition sets the average etch rate and the smoothness of the sidewall. The layer thicknesses set how deep the slit must go. The source stack sets the landing window. The stress stored in the stack decides what happens to the geometry once the slits are cut.

This chapter describes the stack from the slit's point of view: what each layer does to the etch, how much stack thickness varies, what the landing stack looks like in different architectures, and how stack stress and wafer bow change when the stack is cut into blocks.

**Learning Objectives:**
- Compute the average etch rate through an ON stack from the oxide and nitride rates
- Relate oxide/nitride rate mismatch to sidewall striation
- Estimate how stack-thickness variation becomes depth variation at the landing layer
- Describe substrate, poly-Si plate, and replacement-source landing stacks and their windows
- Estimate wafer bow from stack stress with the Stoney equation
- Explain how slits make wafer bow anisotropic

---

## 2.1 What the Slit Cuts Through

### 2.1.1 The Reference Stack

```
Depth (µm)   Layer                               Thickness     Notes
──────────────────────────────────────────────────────────────────────────────
0.00         SiON cap (part of hard mask)        —             removed with mask
0.00–0.30    Cap oxide (TEOS)                    300 nm        above top select gate
0.30–5.80    Upper deck: 100 ON pairs            5.50 µm       25 nm SiO₂ / 30 nm Si₃N₄
                (incl. drain-select and dummy
                levels)
5.80–6.00    Inter-deck oxide                    200 nm        joins the two hole decks
6.00–11.50   Lower deck: 100 ON pairs            5.50 µm       incl. source-select and
                                                               dummy levels
11.50–11.65  Upper n⁺ poly-Si (etch stop)        150 nm        part of source plate
11.65–11.66  SiO₂ liner                          10 nm
11.66–11.74  Sacrificial poly-Si                 80 nm         replaced via slit
11.74–11.75  SiO₂ liner                          10 nm
11.75–11.95  Lower n⁺ poly-Si                    200 nm        source plate
below        Oxide over CMOS interconnect        —             must never be reached

Slit target: bottom at ≈ 11.70 µm, inside the sacrificial layer
```

The stack above the source is 11.5 µm of dielectric: 11.0 µm of pairs plus 0.5 µm of cap and inter-deck oxide. In the array, 96% of the depth above the source stack is ON pairs.

### 2.1.2 Select-Gate and Dummy Levels

The top and bottom few pairs of each deck are often different. Select-gate levels may use thicker nitride for a longer gate. Dummy levels near the deck joint may use thicker oxide to buffer channel-hole bowing. To the slit, these layers are only small changes in local rate. They matter more to the endpoint signal (Chapter 15), which sees the sequence of layers as a modulated emission pattern.

### 2.1.3 The Staircase Region

Slits run through the staircases at both ends of the array (Chapter 1, Section 1.5.1). In the staircase, part of the stack has been etched away and replaced with thick fill oxide:

```
Cross-section along a slit through the staircase (simplified):

  cap oxide ═════════════════════════════════════════════════════
            │ array │        staircase region         │
  ON pairs  ████████████▄▄▄▄                          fill oxide
            ████████████████▄▄▄▄       (TEOS / HDP oxide)
            ████████████████████▄▄▄▄
            ████████████████████████▄▄▄▄
  source    ═════════════════════════════════════════════════════
            ◄── slit runs left to right along this whole line ──►

At position x along the staircase, the slit cuts through:
  (top) fill oxide of thickness H_fill(x), then (below) ON pairs
  of thickness H_ON(x), with H_fill(x) + H_ON(x) ≈ 11.5 µm
```

Fill oxide etches differently from ON pairs in the same chemistry. It is usually somewhat faster and polymerizes differently. The result is a slit whose depth, profile, and landing vary along the staircase (Chapter 12).

---

## 2.2 Etch-Relevant Film Properties

### 2.2.1 Properties

```
Property (PECVD, illustrative)     SiO₂ (TEOS)      Si₃N₄ (SiH₄/NH₃)
──────────────────────────────────────────────────────────────────────────
Density (g/cm³)                    2.15–2.25        2.5–2.8
Hydrogen content (at.%)            1–4 (as Si–OH)   12–25 (Si–H, N–H)
Refractive index (633 nm)          1.45–1.47        1.85–2.05
Intrinsic stress (MPa)             −100 to −350     −200 to +400 (tunable)
                                   (compressive)    (sign depends on recipe)
Bond energy (Si–O vs Si–N, eV)     ~8.3             ~4.6
Main etch products (fluorocarbon)  SiF₄, CO, CO₂,   SiF₄, FCN, N₂,
                                   COF₂             HCN (with H)
```

The two films behave very differently in fluorocarbon plasma. Oxide releases oxygen that consumes surface polymer, so it etches through thinner polymer. Nitride has no oxygen and builds a thicker steady-state polymer layer, but it has weaker bonds. In a strongly ion-driven, non-selective regime at keV energies, the two rates can be brought close together. The art of slit chemistry is keeping them close at every depth (Chapter 4).

### 2.2.2 Average Rate Through Pairs

The time to etch one pair is the sum of the times for its two layers:

```
t_pair = t_ox / ER_ox + t_N / ER_N

ER_avg = p / t_pair  (a thickness-weighted harmonic mean)

Reference (rates at a given depth, illustrative):
  ER_ox = 420 nm/min, ER_N = 380 nm/min
  t_pair = 25/420 + 30/380 = 0.0595 + 0.0789 = 0.1385 min
  ER_avg = 55 / 0.1385 = 397 nm/min ≈ 0.40 µm/min
```

Because it is a harmonic mean, the slower film counts for more. Raising the faster rate gains little. Raising the slower rate gains a lot. If ER_N fell to 300 nm/min with ER_ox unchanged, ER_avg would drop to 55 / (0.0595 + 0.100) = 345 nm/min, a 13% loss from a 21% change in one film.

### 2.2.3 Rate Mismatch and Sidewall Striation

At the trench bottom, the two films alternate in time. On the sidewall, they sit side by side, permanently exposed to whatever lateral etching occurs. If one film recedes laterally faster than the other, the sidewall becomes scalloped at the pair pitch:

```
Sidewall striation (exaggerated):

     oxide   ─────┐
     nitride      └──┐      ← nitride recessed by δ_s
     oxide       ┌───┘
     nitride     └──┐
     oxide       ┌──┘

Striation amplitude:
  δ_s ≈ |LER_ox − LER_N| · t_exposed

where LER = lateral etch rate at the sidewall and t_exposed is the
time that depth of sidewall has been exposed.
```

Lateral rates are small, typically 0.1–1% of the vertical rate under good sidewall passivation, but exposure is long near the top. A layer 1 µm below the top is exposed for most of a 29-minute etch:

```
Example: LER_N − LER_ox = 0.10 nm/min, t_exposed = 25 min
  δ_s = 2.5 nm
```

A few nanometres of striation matter later. The slit liner and metal recess both follow the sidewall. A nitride level that is recessed becomes a word-line level whose metal sits closer to the slit, so the metal recess has to work harder there (Chapter 16). Striation is also a symptom: it reports the oxide/nitride balance of the sidewall chemistry directly (Chapter 10).

### 2.2.4 Nitride Composition

PECVD nitride composition, the Si/N ratio and hydrogen content, varies with deposition conditions and drifts across a deposition chamber's maintenance cycle. Silicon-rich, hydrogen-poor nitride etches more slowly in fluorocarbon plasma. A 10–20% change in nitride rate between stacks deposited in different chambers is plausible. By the harmonic mean, that shifts the average rate by 5–11% and moves the time to landing. That is one reason the main etch is followed by a selective landing step instead of being timed to the landing layer (Chapter 12).

---

## 2.3 Stack Thickness Variation and Depth to Landing

### 2.3.1 Cumulative Thickness

Each deposited layer has a thickness error. The depth to the source stack is the sum of all of them:

```
H_total = Σ t_i   (≈ 400 layers + cap + inter-deck)

Systematic (radial) variation, correlated layer to layer:
  δH_sys = H_total × (fractional systematic error)
  Reference: 1.0% radial non-uniformity → 115 nm across the wafer

Random layer-to-layer variation, uncorrelated:
  δH_rand = σ_layer × √N_layers
  Reference: σ = 0.3 nm per layer, N = 400 → 6 nm
```

The systematic part dominates. Deposition chambers have center-to-edge thickness profiles, and the same profile repeats in every layer. Stack thickness therefore varies by about 1% across the wafer, while layer-to-layer randomness averages out.

### 2.3.2 Depth Variation Seen by the Etch

The slit etch adds its own rate non-uniformity, which is also mostly radial:

```
Time to reach the source stack at a point on the wafer:

  t_land(r) = H(r) / ER_avg(r)

Fractional variation (small errors add):
  δt/t ≈ δH/H − δER/ER

Reference: stack +1.0% at edge, etch rate −2.0% at edge
  δt/t = +1.0% − (−2.0%) = +3.0% (edge reaches the stop 3% later)
  Δt = 0.03 × 29 min = 52 s
  Equivalent depth: 0.03 × 11.5 µm = 345 nm
```

A 345 nm spread in arrival time at the source compares with a sacrificial layer of 80 nm. **No timed etch can land in the window by itself.** The upper poly-Si etch stop exists to absorb this spread: the main etch overetches into a layer it etches slowly, the early regions wait on the stop, and the late regions catch up. Chapter 12 sizes the selectivity this requires.

---

## 2.4 Source and Landing Stacks

### 2.4.1 Three Architectures

```
(a) Substrate source (non-CuA)       (b) Poly-Si source plate        (c) Replacement source
                                         (bottom contact via hole)       (CuA, sidewall contact)

  ON stack                             ON stack                        ON stack
  ───────────────                      ───────────────                 ───────────────
  Si substrate (p-well)                n⁺ poly-Si plate                n⁺ poly-Si (etch stop)
  slit lands ~30–80 nm into Si;        slit lands in or on plate;      oxide liner
  n⁺ implanted through slit;           channel contacts plate through  sacrificial layer ← target
  ACS conductor fills slit             punched bottom of hole          oxide liner
                                                                       n⁺ poly-Si
                                                                       slit lands in sacrificial
                                                                       layer; it is replaced
                                                                       through the slit
```

### 2.4.2 Landing Windows

```
Architecture          Must reach                 Must not reach           Window
──────────────────────────────────────────────────────────────────────────────────────
(a) Substrate         Si surface + recess for    Deep into well (junction  50–150 nm
                      contact (≥ 30 nm)          depth, leakage)
(b) Poly plate        Poly plate surface         Through the plate         100–250 nm
                                                 (CMOS below)
(c) Replacement       Sacrificial layer          Lower poly-Si (and never  ~80 nm
    source            (exposed at slit bottom)   the CMOS interconnect)    (sacrificial
                                                                           thickness)
```

Architecture (c) has the narrowest window and is the reference case in this book. The landing is achieved in two stages:

1. **Main etch** through the dielectric, ending with an overetch that stops on the upper poly-Si. The overetch absorbs the 3% arrival spread (Section 2.3.2).
2. **Landing etch** through the poly-Si and the thin oxide liner into the sacrificial layer, using a chemistry that is selective in the other direction (Chapter 4, Section 4.6).

### 2.4.3 Alternative Etch Stops

Polysilicon is the most common stop because it is already part of the source plate and it etches slowly in oxygen-lean fluorocarbon plasmas. Other stops have been proposed or used:

```
Etch stop            Selectivity to ON           Concern
                     (fluorocarbon, illustrative)
──────────────────────────────────────────────────────────────────────────
Poly-Si              10–30                       Must be opened by a
                                                 second chemistry
Metal oxide          > 50                        Metal residue in the slit;
(e.g., Al₂O₃)                                    must be removed before
                                                 wet steps
Tungsten or WSi      > 30                        Contamination; stress
Thick nitride        2–5 (weak in non-selective  Little benefit; used only
                     chemistry)                  as a marker
```

A metal-oxide stop with very high selectivity makes the main etch landing nearly uniform but introduces a non-volatile layer at the bottom of every slit. Its removal at aspect ratio 60 is a process of its own, usually a wet clean. Most production flows accept the lower selectivity of poly-Si.

---

## 2.5 Stack Stress and Wafer Bow

### 2.5.1 Stress in the Stack

Each film carries intrinsic stress from deposition and thermal stress from the mismatch with silicon. The stack acts like a single film with a thickness-weighted average stress:

```
σ_stack = (t_ox · σ_ox + t_N · σ_N) / p

Reference (illustrative): σ_ox = −300 MPa, σ_N = +100 MPa
  σ_stack = (25 × (−300) + 30 × (+100)) / 55
          = (−7500 + 3000) / 55 = −82 MPa  (net compressive)
```

### 2.5.2 Stoney Estimate of Bow

```
Stoney equation:

  κ = 6 · σ_f · h_f / (M_s · h_s²)

where κ   = curvature (1/m)
      σ_f h_f = film force per unit width (N/m)
      M_s = biaxial modulus of Si(100) ≈ 180 GPa
      h_s = substrate thickness = 775 µm

Bow (sagitta) over a 300 mm wafer:  δ = κ · r² / 2, r = 0.15 m

Reference stack alone: σ_f h_f = 82 MPa × 11.0 µm = 902 N/m
  κ = 6 × 902 / (180 × 10⁹ × (775 × 10⁻⁶)²)
    = 5412 / (1.081 × 10⁵) = 0.050 m⁻¹   (R ≈ 20 m)
  δ = 0.050 × 0.0225 / 2 = 5.6 × 10⁻⁴ m ≈ 560 µm
```

A bow of 560 µm is far beyond what lithography and chucks can handle. Production flows tune nitride stress and deposit **backside compensation films** to bring the net bow to roughly ±50–150 µm before critical steps. The compensation is isotropic: it pushes back equally in every direction.

### 2.5.3 What Slits Do to Stress

Before the slit etch, the stack is a continuous film, and its stress is biaxial and equal in all directions. After the slit etch, the array part of the stack is a set of long walls:

```
After slit etch (cross-section perpendicular to slits):

   ┃wall┃  ┃wall┃  ┃wall┃  ┃wall┃      wall width w_b ≈ 1.8 µm
   ┃    ┃  ┃    ┃  ┃    ┃  ┃    ┃      wall height h ≈ 11.5 µm
   ┃    ┃  ┃    ┃  ┃    ┃  ┃    ┃      free surfaces on both sides
  ═╩════╩══╩════╩══╩════╩══╩════╩═  substrate

Stress along the slits (σ_∥):    unchanged; walls are continuous
Stress across the slits (σ_⊥):   relaxed, except within roughly one
                                 wall width of the base
```

A simple estimate of the fraction of cross-slit force released:

```
f_rel ≈ 1 − c · (w_b / h),   c ≈ 1

Reference: f_rel ≈ 1 − 1.8/11.5 ≈ 0.84
```

Only the array is slit. The staircase and periphery remain continuous. If the array covers 65% of the wafer area, the wafer-level release of cross-slit stack force is about 0.65 × 0.84 ≈ 55%.

### 2.5.4 Worked Example: The Saddle

```
Before slit etch (illustrative, signs: + = one bow direction):
  Stack contribution:       −560 µm in both directions
  Backside compensation:    +500 µm in both directions
  Net bow:                  −60 µm, isotropic (bowl shape)

After slit etch:
  Along slits:   −560 + 500           = −60 µm  (unchanged)
  Across slits:  −560 × (1 − 0.55) + 500 = −252 + 500 = +248 µm

Result: −60 µm in one direction, +248 µm in the other
        → saddle-shaped wafer, ~310 µm of anisotropy
```

The numbers are illustrative, and later steps change them again. The tungsten word-line fill adds strong tensile stress, and the slit fill adds its own. The direction of the effect is general, though: **the slit etch turns an isotropic bow into an anisotropic one**. Chapter 11 follows the consequences for chucking during later etches, for block leaning, and for overlay of the layers patterned afterward.

### 2.5.5 Bow During the Slit Etch Itself

The slit etch begins with the wafer in its pre-slit state and ends in its post-slit state. The release happens progressively as the slit deepens. Most of the release occurs once the slit is deep enough that the walls have a high aspect ratio, which happens partway through the etch. The wafer is held by the electrostatic chuck the whole time. Its shape change appears as a gradual change in the clamping force and helium backside leak rate during the etch (Chapter 8).

---

## 2.6 Summary & Key Takeaways

1. **The slit sees mostly two films.** About 96% of the depth above the source is ON pairs. The average rate is a harmonic mean, so the slower film counts for more.

2. **Oxide/nitride balance shows on the sidewall.** A lateral-rate difference of 0.1 nm/min produces a few nanometres of striation near the top over a full etch.

3. **Stack thickness varies by about 1%, mostly radially.** Combined with etch-rate non-uniformity, the arrival time at the source can differ by 3%, or about 345 nm of equivalent depth.

4. **The landing window is narrower than the depth spread.** In replacement-source flows, the target layer is ~80 nm thick. A selective stop must absorb the spread, and a second step completes the landing.

5. **The stack is a highly stressed film.** On its own it could bow a wafer by hundreds of microns, so backside films compensate.

6. **Slits release stress in one direction.** The bow becomes a saddle. The effect starts during the etch and carries into every later step.

---

## Study Questions

1. A stack has 28 nm oxide and 32 nm nitride per pair. At a given depth, ER_ox = 450 nm/min and ER_N = 350 nm/min. Compute ER_avg. By how much does ER_avg rise if ER_N is raised to 400 nm/min? If ER_ox is raised to 500 nm/min instead?

2. A slit etch has a nitride lateral rate 0.15 nm/min higher than the oxide lateral rate in the top 2 µm. The etch lasts 32 minutes, and the top 2 µm is reached in the first 4 minutes. Estimate the striation amplitude at 0.5 µm and at 2.0 µm depth.

3. Stack thickness is 0.8% thicker at the edge than at center, and the etch rate is 1.5% lower at the edge. The stack above the source is 13.0 µm, etched at an average of 0.42 µm/min. Compute the difference in arrival time at the source between center and edge, and the equivalent depth difference.

4. Using the Stoney equation, compute the bow from a 13.0 µm stack with an average stress of −60 MPa on a 775 µm, 300 mm wafer. What backside film (thickness × stress) would cancel it exactly?

5. For walls 1.4 µm wide and 14 µm tall, covering 70% of the wafer, estimate the fraction of cross-slit stack force released. Using your answer to Question 4 and assuming a compensated pre-slit bow of 0 µm, estimate the bow across the slits after the etch.

---

**Next Chapter:** [Chapter 3: High-Aspect-Ratio Trench Etch Physics](./03-har-trench-physics.md)

---

**Chapter 2 Development Status:** Complete  
**Version:** 1.0
