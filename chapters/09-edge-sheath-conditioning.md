# Chapter 9: Edge Ring, Sheath Control & Chamber Conditioning

## Overview

At the center of the wafer, the sheath is flat, the ions arrive normal to the surface, and slits go straight down. Near the edge, the wafer ends and an **edge ring** takes over. If the ring's surface, and the sheath above it, do not match the wafer exactly, the sheath boundary bends, and ions arrive at an angle. In a slit 11.7 µm deep, an angle of a quarter of a degree moves the bottom 50 nm sideways, which is most of the clearance to the next row of channel holes. As the ring erodes, the angle changes. **Edge tilt is usually the slit parameter that limits yield at the wafer edge and sets the life of the edge ring.**

The rest of the chamber matters too. Over a 30-minute etch, polymer builds on the walls and the upper electrode erodes, and both change the chemistry the wafer sees. Particles shed from those surfaces can land on the mask and block a slit. This chapter covers the edge sheath and tilt, the edge ring and its compensation methods, and the conditioning and particle control that keep a slit chamber stable.

**Learning Objectives:**
- Explain how a height or sheath mismatch at the wafer edge tilts the ion flux
- Estimate tilt versus distance from the edge for a given mismatch
- Explain why tilt affects slits only in certain azimuthal sectors of the wafer
- Compute ring-wear limits and compare compensation methods
- Describe wall and electrode effects on a long etch and the role of waferless cleans
- Estimate the rate of slit-blocking particle events and their effect on good blocks

---

## 9.1 The Edge Sheath

### 9.1.1 Why the Sheath Bends

The plasma-sheath boundary sits one sheath thickness above each surface. Over the wafer, that is about 5 mm at the reference conditions (Chapter 7, Section 7.1.1). Over the ring, the boundary height depends on the ring's surface height and on its own sheath thickness, which depends on the RF voltage the ring develops:

```
Boundary height:  H_b = h_surface + s

Over the wafer:   H_b,w = h_w + s_w
Over the ring:    H_b,r = h_r + s_r

Mismatch:         Δ = H_b,r − H_b,w = (h_r − h_w) + (s_r − s_w)

  Δ = 0:   flat boundary; ions normal everywhere
  Δ < 0:   boundary dips over the ring (worn or low ring, or thin
           ring sheath); field lines tilt outward; ions arrive
           tilted toward the wafer edge
  Δ > 0:   boundary rises over the ring (high ring or thick ring
           sheath); ions tilt toward the wafer center
```

```
Worn ring (Δ < 0), cross-section at the wafer edge:

   plasma
  ──────────────────────────╮
                             ╲          ← sheath boundary dips
   sheath ↓  ↓  ↓  ↘  ↘       ╲─────────
  ═══════════════════════╗           ring sheath
       wafer             ║ ┌─────────────
                         ║ │ edge ring (eroded)
  ions tilt outward over the last few mm of the wafer
```

### 9.1.2 A Simple Tilt Model

The boundary bends over a lateral distance comparable to the sheath thickness. A useful first estimate takes the boundary slope, and so the ion tilt, to decay exponentially inward from the wafer edge with a length comparable to s:

```
θ(x) ≈ (Δ / (2s)) · exp(−x / s)     (radians)

x = distance inward from the wafer edge
s = sheath thickness (≈ 5.3 mm, reference)

Example: Δ = −0.10 mm (ring 0.1 mm low, equal sheaths)
  θ(0)     = 0.10 / 10.6 = 9.4 mrad = 0.54°
  θ(3 mm)  = 9.4 × exp(−0.57) = 5.3 mrad = 0.31°
  θ(5 mm)  = 9.4 × exp(−0.94) = 3.7 mrad = 0.21°
  θ(10 mm) = 9.4 × exp(−1.89) = 1.4 mrad = 0.08°
```

This model is illustrative. Real tilt profiles depend on the ring's electrical design, the gap between wafer and ring, and the plasma above. The shape is typical, though: tilt is concentrated in the outer 5–10 mm and grows roughly linearly with the mismatch. In practice, each chamber design is calibrated with a measured tilt-versus-mismatch curve.

### 9.1.3 Tilt Limit and Ring Wear

From Chapter 1, the reference slit tolerates ≤ 0.25° of tilt perpendicular to the slit. If the outermost yielding die extend to 3 mm from the edge:

```
Allowed mismatch at x = 3 mm:
  |Δ|_max = 0.25° / 0.31° × 0.10 mm ≈ 0.08 mm
```

Eighty microns of ring wear, if nothing else changes, uses up the whole tilt budget at the outer die. That is why ring wear, and not ring breakage or contamination, usually ends ring life in HAR etch unless the mismatch is compensated.

---

## 9.2 Tilt and Slit Orientation

### 9.2.1 Only the Perpendicular Component Matters

Edge tilt is radial. It points outward or inward along the wafer radius. A slit is a line. Tilt **along** the slit moves the slit within its own length and costs no clearance. Only tilt **perpendicular** to the slit moves it toward a row of channel holes:

```
Wafer with slits running left–right (along x):

                φ = 90° (12 o'clock)
                radial tilt ⟂ slits: full effect
                      ▲
                ┌─────┼─────┐
  φ = 180°  ◄───┤═════╪═════├───►  φ = 0° (3 o'clock)
  radial tilt   │═════╪═════│      radial tilt ∥ slits:
  ∥ slits:      │═════╪═════│      no clearance cost
  no cost       └─────┼─────┘
                      ▼
                φ = 270° (6 o'clock): full effect

Perpendicular tilt:  θ_⊥(r, φ) = θ_r(r) · |sin φ|
```

### 9.2.2 Consequences

```
Consequence                                   Detail
──────────────────────────────────────────────────────────────────────────
Edge yield loss concentrates in two sectors   Near 12 and 6 o'clock for
                                              slits running 3–9 o'clock
Tilt measurement must sample those sectors    A tilt map at 3 and 9
                                              o'clock understates the risk
Azimuthally non-uniform ring wear matters     Extra wear near the critical
mostly in those sectors                       sectors costs yield; elsewhere
                                              it barely matters
Holes and slits differ                        Channel holes feel tilt in
                                              every direction; slits in two
                                              sectors only
```

Within the critical sectors, the slit tilt and the channel-hole tilt (from a different etch, often in a different chamber and at a different point in ring life) may point the same way or opposite ways. If both tilt outward by similar amounts, they partly cancel in the clearance budget. If not, they add. The budget in Chapter 1 treats them as independent, which is the safe assumption.

### 9.2.3 Tilt Along the Slit

Tilt along the slit is not entirely harmless. At slit **ends**, where a slit stops (for example at a partial-slit boundary or at the far end of the staircase), along-slit tilt moves the end of the bottom relative to the end of the top. Slit ends near 3 and 9 o'clock can shift by tens of nanometres at depth. This matters where slit ends must meet other structures (Chapter 12).

---

## 9.3 The Edge Ring

### 9.3.1 Ring Stack

```
Typical edge-ring assembly (illustrative):

  ┌──────────────────────┐
  │ edge (focus) ring:   │ ← Si or SiC; plasma-facing; erodes
  │ Si or SiC            │
  ├──────────────────────┤
  │ coupling ring        │ ← sets RF coupling to the edge ring
  │ (dielectric/conductive)│
  ├──────────────────────┤
  │ insulator / cover    │ ← quartz or ceramic; protects ESC side
  └──────────────────────┘
  ESC and wafer sit inside the ring with a gap of ~0.5–1 mm
```

### 9.3.2 Materials

```
Material      Pros                               Cons
──────────────────────────────────────────────────────────────────────
Si            Same element as wafer; minimal     Erodes faster; Si release
              contamination; matches wafer       scavenges F (edge chemistry)
              electrically
SiC (CVD)     Erodes ~2–3× slower; longer life   Cost; different electrical
                                                 properties; C release adds
                                                 polymer at the edge
Quartz        Insulating covers only              Erodes fast in F plasmas;
                                                 O release at the edge
```

### 9.3.3 Ring Wear and Ring Life

```
Ring erosion rate (illustrative, Si, HAR conditions): 0.2 µm per RF hour
RF time per wafer (reference): ≈ 0.55 h
Wear per wafer: ≈ 0.11 µm

Without compensation:
  Wafers to 0.08 mm of wear: 80 / 0.11 ≈ 730 wafers
  At 1.6 WPH × 24 h ≈ 38 wafers/day → about 19 days

With compensation (Section 9.4), the limit becomes ring thickness or
mechanical integrity, typically ≥ 1 mm of usable wear:
  1000 / 0.11 ≈ 9000 wafers, ≈ 5000 RF hours
```

The ratio of these two lifetimes, more than an order of magnitude, is why every modern HAR chamber has some form of edge-sheath compensation.

### 9.3.4 Ring Temperature

The edge ring is not cooled as effectively as the wafer, and it absorbs ion power. Its temperature rises during the etch, sometimes by 100 °C or more. A hot ring collects less polymer and releases more Si or C into the edge plasma. Edge CD, bow, and edge mask erosion can drift with ring temperature through the etch and through the first wafers after an idle period. Rings with thermal contact pads or with controlled cooling reduce this drift.

---

## 9.4 Compensating the Edge

### 9.4.1 Methods

```
Method                          How it works                  Typical range
─────────────────────────────────────────────────────────────────────────────
Ring lift (motorized)           Raises the ring to restore    Tens to hundreds
                                h_r as it wears               of µm; step size
                                                              a few µm
Tunable edge RF / DC            Changes the ring voltage,     Equivalent to
                                and so its sheath thickness   ~±0.1–0.3 mm of
                                s_r                           height
Coupling-ring design            Fixes the initial match       Set at design
Replacement                     New ring at nominal height    —
```

### 9.4.2 Sheath-Thickness Tuning

From the Child law, sheath thickness scales as V^(3/4). To offset a height deficit Δh with ring voltage:

```
Δs_r / s_r ≈ (3/4) · ΔV_r / V_r

To offset Δh = 0.10 mm with s_r = 5.3 mm:
  Δs_r / s_r = 0.10 / 5.3 = 1.9%
  ΔV_r / V_r = 1.9% / 0.75 = 2.5%
```

A few percent of ring voltage compensates a tenth of a millimetre of wear. Tunable edge systems therefore offer fine, fast control, which can even be changed within a recipe, step by step, if the sheath thickness changes between steps.

### 9.4.3 Step-Dependent Mismatch

The wafer sheath thickness differs between recipe steps, because bias voltage and ion flux change (ME-1 lower bias, ME-3 higher). If the ring sheath does not scale the same way, the mismatch Δ, and so the tilt, changes from step to step. Tilt can be well matched in ME-2 and still be mismatched in ME-3, so the deep part of the slit bends at the edge. Tunable edge systems can apply a different setting in each step. Ring lift cannot.

```
Diagnosis: a slit at the edge that is straight in its upper half and
tilted only in its lower half points to a step-dependent mismatch in
the deep steps, not to ring wear (which tilts the whole slit).
```

### 9.4.4 Control Strategy

```
Feed-forward:  edge setting = f(ring RF hours), from a calibrated
               wear curve
Feedback:      measured edge tilt on monitor wafers or product
               (Chapter 15) corrects the curve
Limits:        ring replaced when thickness, compensation range, or
               particles reach their limits
```

---

## 9.5 Chamber Conditioning

### 9.5.1 Within-Wafer Drift

Over a 30-minute etch, polymer accumulates on the chamber walls, confinement rings, and upper electrode. Wall polymer absorbs and releases fluorocarbon fragments and fluorine, so the gas-phase chemistry drifts through the etch. A recipe developed from short tests can behave differently at full length because of this. Depth-series experiments (Chapter 7, Section 7.6.2) partly capture it, since each partial etch also has its own wall history.

### 9.5.2 Waferless Clean

```
Waferless autoclean (WAC) between wafers (illustrative):
  O₂ (± small NF₃) plasma, 60–120 s, no wafer (or a cover wafer)
  Removes wall polymer to a reproducible state before each wafer
  NF₃ removes Si-containing deposits that O₂ alone leaves
```

WAC turns the chamber into a reset state at the start of each wafer, so every wafer sees the same wall history. Incomplete WAC lets polymer accumulate over many wafers. That causes wafer-to-wafer drift and eventually flaking.

### 9.5.3 Upper Electrode Aging

The silicon showerhead erodes under ion bombardment. Its holes widen, which changes gas distribution, and it releases silicon, which scavenges fluorine and so adds polymer. Over the electrode's life (often a few thousand RF hours), center rate and polymer drift slowly. APC tracks this with an electrode-age term (Chapter 15).

### 9.5.4 Seasoning After Maintenance

After a wet clean or part replacement, the chamber walls are bare. Bare walls consume fluorocarbon fragments and release oxygen and moisture. A seasoning sequence of dummy wafers or long plasma runs restores the normal wall state before product is run. The first wafers after seasoning are checked for depth, top CD, and edge tilt.

---

## 9.6 Particles and Blocked Slits

### 9.6.1 Why Slits Are Sensitive

A particle that lands on the mask over a slit opening shadows the etch beneath it. If it is large enough to bridge the opening, the slit below stops etching or is left with a partial bridge. That bridge later shorts the word lines of the two adjacent blocks (Chapter 1, Section 1.2.2). The particle need not survive the etch. It only has to be present long enough to leave an unetched segment.

### 9.6.2 Event Rate

```
Example (illustrative):

  Particle adders during etch ≥ 100 nm:  0.02 /cm²
  Per wafer: 0.02 × 707 cm² ≈ 14 particles

  Probability a particle lands on a slit opening in the array:
    array fraction of wafer area ≈ 0.65
    capture width ≈ (slit width + particle size) / slit pitch
                  ≈ (0.20 + 0.10) / 2.0 = 0.15
    → 0.65 × 0.15 ≈ 0.10

  Expected slit-blocking events: 14 × 0.10 ≈ 1.4 per wafer
```

### 9.6.3 Effect on Yield

NAND devices tolerate a small number of bad blocks. Each die has spare blocks, and bad blocks are mapped out at test. A bridge between two blocks costs those two blocks, not the die, as long as the die stays within its bad-block allowance:

```
Die with ~4000 blocks and a bad-block allowance of ~2% (~80 blocks)
At ~1.4 events per wafer spread over ~650 die (1 cm² each):
  ~0.002 events per die → ~0.004 bad blocks per die from this cause

Negligible against the allowance, unless particles cluster (a flake
shedding many particles in one area) or a systematic defect repeats.
```

Particle control matters most for **clustered** events: a single wall flake that sheds hundreds of particles over one region of the wafer. Those can push the die in that region past the bad-block limit. Wall-polymer management (Section 9.5.2) and part-life control are therefore defect-control measures, not just process-stability measures.

---

## 9.7 Summary & Key Takeaways

1. **Tilt comes from a bent sheath at the wafer edge.** A boundary mismatch Δ over the ring tilts ions over the outer 5–10 mm. In the reference model, 0.1 mm of mismatch gives about 0.3° at 3 mm from the edge.

2. **Slits feel tilt in two sectors only.** Only the component perpendicular to the slit costs clearance, so edge yield loss concentrates where the radius is perpendicular to the slits.

3. **Ring wear sets ring life unless it is compensated.** About 80 µm of wear uses the reference tilt budget. That is weeks without compensation and thousands of RF hours with it.

4. **Ring voltage is a fine edge knob.** A few percent of ring voltage offsets 0.1 mm of wear. Tunable systems can apply a different value in each recipe step.

5. **A long etch changes its own chamber.** Wall polymer, electrode erosion, and ring heating all drift during and between wafers. WAC resets each wafer to a reproducible start.

6. **Particles block slits; clusters matter most.** Single events cost two blocks within the bad-block allowance. Flakes that shed many particles in one area cost die.

---

## Study Questions

1. Using θ(x) = (Δ/(2s))·exp(−x/s) with s = 5.3 mm, compute the tilt at x = 2, 4, and 6 mm for Δ = −0.06 mm. If the tilt limit is 0.25°, what is the closest yielding die position for this mismatch?

2. A wafer has slits running along x. At a point 4 mm from the edge at φ = 30° from the slit direction, the radial tilt is 0.30°. What is the tilt component perpendicular to the slits? Is the clearance budget of Chapter 1 met there?

3. A chamber switches from Si to SiC edge rings with one-third the erosion rate. Using the numbers in Section 9.3.3, compute the uncompensated ring life in wafers and in days. What other edge effects might change with the material switch?

4. ME-3 runs 20% higher bias voltage than ME-2. The ring sheath scales as the wafer sheath in ME-2 but only half as much in ME-3 (its voltage rises 10% instead of 20%). With s = 5.3 mm in ME-2, estimate the mismatch Δ created in ME-3 and the tilt at x = 3 mm.

5. A cluster of 300 particles from one flake lands in a 2 cm² area of a wafer. Using the capture fraction from Section 9.6.2, estimate the number of slit-blocking events in that area. If the die are 1 cm² with 4000 blocks and an 80-block allowance, do any die fail?

---

**Next Chapter:** [Chapter 10: Profile Control — Bowing, Taper, Striation & Bottom CD](./10-profile-bow-taper.md)

---

**Chapter 9 Development Status:** Complete  
**Version:** 1.0
