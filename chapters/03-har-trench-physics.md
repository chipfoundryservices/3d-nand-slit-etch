# Chapter 3: High-Aspect-Ratio Trench Etch Physics

## Overview

At the top of a slit, the etch front sees the plasma directly. Eleven microns down, it sees the plasma only through a slot 60 times deeper than it is wide. Every species that etches, passivates, or charges the bottom must travel down that slot. Neutrals bounce off the walls in random directions. Ions arrive nearly straight but not perfectly so. Electrons arrive in every direction and are mostly stopped near the top. The etch rate at the bottom, the shape of the walls, and the charge on the bottom all follow from those three transport problems.

High-aspect-ratio etch physics is usually taught for holes. This chapter develops it for trenches and shows where the two differ. The key results are that a long slot transmits about three times more bouncing neutral flux than a hole of the same aspect ratio, about a hundred times more line-of-sight flux, and more of the ion flux too, because ions spread in only one direction across a slot. These differences explain why a slit etches faster than a channel hole of equal depth, why it stays ion-limited deeper, and why its typical failure modes are different.

**Learning Objectives:**
- Apply the ion–neutral synergy model of etch rate to the bottom of a deep feature
- Use transmission probabilities to compute neutral flux at a trench bottom, with and without sticking
- Explain why slots transmit neutrals better than holes and quantify the difference
- Estimate the fraction of ions reaching the bottom directly from the ion angular spread
- Compute the etch-rate decline with depth (ARDE) and the time to reach a given depth
- Describe differential charging in deep trenches and its effect on ion trajectories

---

## 3.1 What Sets the Etch Rate at the Bottom

### 3.1.1 The Synergy Model

Dielectric etching in fluorocarbon plasma needs both ions and neutrals. Neutrals (F, CFₓ, O) supply the chemistry. Ions supply the energy that mixes the reactants into the surface and drives off products. A simple and widely used model treats the two supplies as resistances in series:

```
1/ER = 1/ER_n + 1/ER_i

where ER_n = rate if ions were unlimited (neutral-supply limited)
      ER_i = rate if neutrals were unlimited (ion-energy-flux limited)

At the bottom of a feature of aspect ratio A:

  ER_n(A) = ER_n0 · K_n(A)      K_n = neutral transmission
  ER_i(A) = ER_i0 · K_i(A)      K_i = ion transmission
```

ER_n0 and ER_i0 are the open-field values. The whole of high-aspect-ratio etch physics, in this picture, is the calculation of K_n and K_i and what changes them.

### 3.1.2 Reference Parameters

```
Reference slit etch (illustrative, chosen to match an average rate of
0.40 µm/min through 11.5 µm of dielectric):

  ER_n0 = 8.0 µm/min      (abundant neutrals at the open surface)
  ER_i0 = 0.75 µm/min     (keV ions; ion-limited at the top)
  Open-field rate: 1 / (1/8.0 + 1/0.75) = 0.686 µm/min
```

At the top, the etch is strongly ion-limited: neutrals are ten times more plentiful than the ions can use. That reserve of neutrals is what lets the slit go deep before neutral starvation sets in.

---

## 3.2 Neutral Transport in Deep Features

### 3.2.1 Free-Molecular Flow

At slit-etch pressures (10–40 mTorr), the mean free path of a neutral is millimetres to centimetres. Inside a 200 nm slit, neutrals never collide with each other. They fly in straight lines from wall to wall. At each wall hit, a neutral either reacts or sticks (probability *s*) or is re-emitted in a random direction following a cosine distribution. This is the **Knudsen** regime, and the fraction of entering neutrals that reach the bottom is the **transmission probability** K_n.

### 3.2.2 Slot Versus Hole

The transmission of a non-sticking neutral (s = 0) depends only on geometry. The table below comes from a Monte Carlo calculation of free-molecular flow (cosine entry, diffuse re-emission). The hole values reproduce the classical Clausing factors, and the slot value at A = 1 reproduces the classical result for parallel plates.

```
Aspect ratio   Hole (cylinder)   Slot (long trench)   Slot / hole
   A = D/W        K_n              K_n
───────────────────────────────────────────────────────────────────
    1           0.514             0.681                1.32
    2           0.359             0.541                1.51
    5           0.191             0.357                1.86
   10           0.109             0.240                2.20
   20           0.060             0.155                2.60
   40           0.031             0.095                3.04
   60           0.021             0.071                3.37

Useful fits (A ≥ 5):
  Hole:  K_n ≈ 1 / (1 + 0.75 A)        (within ~8%)
  Slot:  K_n ≈ (ln A + 0.15) / A       (within ~3%)
```

For a hole, transmission falls as 1/A. For a slot, it falls as (ln A)/A. The slot keeps a logarithmic advantage that grows with depth: **at the reference aspect ratio of 58, a slit transmits about 3.3 times the neutral flux of a hole of the same width.**

### 3.2.3 Why the Slot Wins

A neutral re-emitted from a slot wall can fly a long way along the slot without hitting anything, because the slot is open in that direction. Those long flights carry it down the slot as well. In a hole, every direction except straight down or up is blocked within one diameter. The slot is a two-dimensional channel, and diffusion in two dimensions is more effective than in one.

### 3.2.4 Sticking Species

Many important neutrals react on the walls. Polymer precursors such as CF₂ and larger CₓFᵧ fragments stick with probabilities from ~0.01 to ~0.1 or more. Oxygen atoms recombine or react with sidewall polymer. With sticking, transmission falls steeply. Again, the slot fares far better:

```
Monte Carlo transmission with sticking probability s per wall hit:

                 A = 10                 A = 40
  s          Hole      Slot         Hole       Slot
───────────────────────────────────────────────────────
  0          0.109     0.240        0.031      0.095
  0.05       0.015     0.132        < 10⁻⁴     0.016
  0.2        0.004     0.073        < 10⁻³     0.015
```

At high sticking, only **line-of-sight** flux reaches the bottom: molecules that enter at an angle steep enough to reach the bottom without touching a wall. For a slot, that fraction is about 1/(2A). For a hole, it is about 1/(4A²):

```
Line-of-sight fraction:
  Slot: K_LOS ≈ √(1 + A²) − A ≈ 1/(2A)
  Hole: K_LOS ≈ 1/(4A²)  (for A ≫ 1)

At A = 58:
  Slot: 1/116 = 8.6 × 10⁻³
  Hole: 1/13 456 = 7.4 × 10⁻⁵
  Ratio ≈ 116
```

**Sticking species reach a slit bottom roughly a hundred times more readily than a hole bottom.** For an etchant, this is an advantage. For a polymer precursor, it is a risk. Deposition at the bottom of a slit can be much heavier than at the bottom of a hole etched with the same chemistry. A chemistry tuned for holes may therefore taper or even stop in a slit. Slit recipes run leaner in polymer than hole recipes for this reason (Chapter 4).

### 3.2.5 The Sidewall as a Sink

Sticking does not only reduce bottom flux. It also decides where the deposit goes. Polymer precursors with high *s* deposit near the top of the slit, which is the passivation that protects against bow. Precursors with low *s* spread deposition deeper. Chemistry choice is therefore also a choice of **where on the sidewall protection is placed** (Chapter 10).

---

## 3.3 Ion Transport

### 3.3.1 Ion Angular Distribution

Ions are accelerated across the sheath and arrive nearly normal to the wafer. Their angular spread comes from their transverse thermal motion at the sheath edge and from any collisions in the sheath:

```
Collisionless sheath:  θ_rms ≈ √(kT_i / (2 E_i))  per transverse axis

Reference: kT_i ≈ 0.05 eV at the sheath edge, E_i ≈ 3 keV
  θ_rms ≈ √(0.05 / 6000) = 2.9 × 10⁻³ rad ≈ 0.17°

Collisions and RF modulation of the sheath broaden this. A
representative effective spread for slit etch is σ_θ ≈ 4 × 10⁻³ rad
(0.23°) per axis.
```

### 3.3.2 Direct Transmission to the Bottom

An ion entering at position *x* across a slot of width *W* with angle θ in the cross-slot plane reaches the bottom without touching a wall if its sideways displacement D·tan θ does not carry it past the wall. For a slot, only the cross-slot component of angle matters, because motion along the slot is unrestricted. For a hole, both components matter:

```
For small A·σ_θ (ions mostly transmitted):

  Slot: K_i ≈ 1 − √(2/π) · A · σ_θ ≈ 1 − 0.80 A σ_θ
  Hole: K_i ≈ 1 − (4/π)·√(π/2) · A · σ_θ ≈ 1 − 1.60 A σ_θ

Reference, A = 58, σ_θ = 4 × 10⁻³:
  A σ_θ = 0.232
  Slot: K_i ≈ 1 − 0.80 × 0.232 = 0.81
  Hole: K_i ≈ 1 − 1.60 × 0.232 = 0.63
```

**A hole loses ions to its wall about twice as fast as a slot.** Ions that strike the wall at grazing angles are not all lost. Many reflect forward with part of their energy and still reach the bottom, often near its corners. That reflected flux is a main cause of bottom-corner effects (Chapter 10). For the rate model, direct transmission is a conservative estimate.

### 3.3.3 What Ion Angle Does to the Sidewall

Ions that do hit the wall at grazing incidence etch it slowly, because sputter and ion-enhanced yields fall steeply at glancing angles. The sidewall is therefore protected mostly by geometry and by polymer. That protection fails where ions arrive at larger angles. The main sources of large-angle ions are:

```
Source                                  Where the damage appears
────────────────────────────────────────────────────────────────────────
Reflection off a faceted mask edge      Bow, 1–2 µm below the top
                                        (Chapter 10)
Tilted sheath at the wafer edge         Whole profile tilts (Chapter 9)
Collisional sheath (high pressure)      General taper or bow
Charging-induced deflection             Local twisting, bending at
                                        asymmetric features (Section 3.5)
```

---

## 3.4 Aspect-Ratio-Dependent Etching (ARDE)

### 3.4.1 Etch Rate Versus Depth

Combining the neutral and ion transmissions with the synergy model gives the etch rate at each depth. For the reference parameters, with the top CD of 200 nm used as the width:

```
Depth    A      Slot                               Hole (same width)
(µm)            K_n    K_i    ER_n   ER_i   ER     K_n     K_i    ER
                                     (µm/min)                     (µm/min)
──────────────────────────────────────────────────────────────────────────────
0.0      0     1.00   1.00   8.00   0.75   0.69   1.00    1.00   0.69
1.0      5     0.352  0.98   2.82   0.74   0.59   0.211   0.97   0.51
2.0     10     0.245  0.97   1.96   0.73   0.53   0.118   0.94   0.40
4.0     20     0.157  0.94   1.26   0.70   0.45   0.063   0.87   0.28
6.0     30     0.118  0.90   0.95   0.68   0.40   0.043   0.81   0.22
8.0     40     0.096  0.87   0.77   0.65   0.35   0.032   0.75   0.18
10.0    50     0.081  0.84   0.65   0.63   0.32   0.026   0.68   0.15
11.6    58     0.073  0.82   0.58   0.61   0.30   0.023   0.63   0.13
```

Two conclusions follow.

**First, a slit etches about twice as fast as a hole at depth.** At A = 58, the slot rate is 0.30 µm/min, compared with 0.13 µm/min for the hole. The average rate through 11.5 µm is 0.405 µm/min for the slit and 0.22 µm/min for a hole of the same width.

**Second, the slit stays ion-limited almost to the bottom.** The neutral-limited rate ER_n falls to equal the ion-limited rate ER_i only near A ≈ 55. For the hole, the crossover happens near A ≈ 10. Below the crossover, the rate depends on neutral supply and becomes very sensitive to chemistry, pressure, and sticking. The slit spends nearly all of its etch in the more robust ion-limited regime.

### 3.4.2 Time to Depth

```
Time to reach depth z: t(z) = ∫₀ᶻ dz' / ER(z')

Reference slit:
  Depth (µm)      1     2     4     6      8      10     11.5
  Time (min)     1.6   3.4   7.5   12.2   17.6   23.6   28.4

Average rate to 11.5 µm: 11.5 / 28.4 = 0.405 µm/min
The last 1.5 µm takes 4.8 min (0.31 µm/min); the first 1.5 µm
takes ~2.5 min.
```

The decline in rate with depth is mild for a slit: the bottom rate is 43% of the top rate. That has a practical consequence. Depth is nearly linear in time, so etch time is a reasonable proxy for depth, and endpoint timing errors translate into depth errors in a predictable way (Chapter 15).

### 3.4.3 Width Matters as Much as Depth

Aspect ratio depends on width as well as depth. A slit that is narrower than nominal, from mask CD variation or taper, reaches a given aspect ratio sooner and etches more slowly at the bottom. Near the bottom, the slope is dER/dA ≈ −0.0027 µm/min per unit of A:

```
Bottom of reference slit (D = 11.5 µm):
  W = 200 nm → A = 57.5, ER ≈ 0.299 µm/min
  W = 190 nm → A = 60.5, ER ≈ 0.291 µm/min

Integrated time to 11.5 µm:
  W = 200 nm: 28.4 min
  W = 190 nm: 28.9 min  (+1.9%)
  W = 180 nm: 29.5 min  (+3.9%)

A 5% narrower slit arrives at the source stack about 2% later.
```

That is small next to the 3% radial arrival spread in Chapter 2, but it is not random. Narrow slits lag systematically. In the staircase region and at slit ends, where the local geometry changes, the effect can be larger (Chapter 12).

### 3.4.4 Inverse RIE Lag and Its Absence

When deposition dominates at the bottom of wide features, narrow features can etch faster than wide ones (inverse RIE lag). Slits operate far from that regime at depth, but it can appear briefly near the top in polymer-rich steps. Slits of different widths in the same die, such as main slits and narrower partial slits, should be checked for both normal and inverse lag (Chapter 14).

---

## 3.5 Charging in Deep Trenches

### 3.5.1 Electron Shading

Ions arrive nearly normal to the wafer. Electrons arrive nearly isotropically, with energies of a few eV, and can reach the wafer only during the brief part of each RF cycle when the sheath collapses. Deep in a narrow feature, electrons are blocked by the walls, and the bottom collects a net positive charge. The upper sidewalls collect a net negative charge.

```
Charging in a deep slit (schematic):

   electrons (isotropic)        ions (directional)
       ↘ ↓ ↙                         ↓ ↓ ↓
   ─ ─ ─ ─ ┐       ┌─ ─ ─ ─
   (−)     │       │     (−)   ← upper walls charge negative
           │       │
           │       │
           │       │
       (+) │       │ (+)
           └─(+++)─┘           ← bottom charges positive

Steady state: the bottom potential V_b rises until the ion current
reaching the bottom equals the electron current reaching it.
```

### 3.5.2 Effects on Ions

The bottom potential decelerates arriving ions. For keV ions, a bottom potential of 100–300 V costs only a few percent of their energy. The more damaging effect is **lateral deflection** by any asymmetry in the charge on the two sidewalls:

```
Deflection of an ion by a lateral field E_⊥ acting over a path L:

  θ_defl ≈ q · E_⊥ · L / (2 E_i)    with E_⊥ ≈ ΔV / W

Example: ΔV = 20 V across W = 0.15 µm, acting over L = 0.5 µm,
         E_i = 3 keV
  θ_defl ≈ 20 × 0.5 / (2 × 3000 × 0.15) = 0.011 rad ≈ 0.64°
```

A 20 V asymmetry is enough to bend the ion path by more than the whole tilt budget of Chapter 1. In holes, random asymmetries in sidewall charge are thought to drive **twisting**, the random sideways wandering of deep hole bottoms.

### 3.5.3 Why Trenches Charge More Symmetrically

In a long slot, the two sidewalls are nearly identical by symmetry along most of the slit's length. Charge builds up equally on both, and the lateral fields cancel in the middle of the slot. Electrons also reach a slot bottom more easily than a hole bottom, through the same one-dimensional geometry that helps neutrals. Slits are therefore less prone to random twisting than holes.

The symmetry fails at specific places:

```
Location                          Asymmetry                    Effect
──────────────────────────────────────────────────────────────────────────
Slit end                          Wall on three sides          Bending, end
                                                               depth loss
Junction with a partial slit      Extra opening on one side    Local bending
Edge of the slit array            Neighbor slit on one side    First slit bends
                                  only                         toward/away from
                                                               the array
Local mask defect or CD bump      Locally wider on one side    Local wiggle
Wafer edge                        Tilted ion flux; asymmetric  Adds to tilt
                                  electron access
```

Slits are judged by their worst point, so these local asymmetries matter even though the body of the slit is well behaved. Pulsed operation, which lets electrons and negative ions reach the bottom during the off phase, is the main hardware remedy (Chapter 6).

### 3.5.4 Sidewall Conduction

Charge can leak along the sidewall through the polymer film and the surface of the dielectric. A conductive sidewall film equalizes charge and reduces both bottom potential and lateral fields. Fluorocarbon polymer is normally a poor conductor, but its conductivity rises under ion bombardment and with carbon-rich composition. That is one reason why changes in polymer composition, made for profile reasons, can also change charging behavior.

---

## 3.6 Preview: From Transport to Profile

Transport sets the rate at the bottom. Profile depends on what happens on the sidewall:

```
Profile feature       Transport cause                        Chapter
────────────────────────────────────────────────────────────────────────
Bow                   Ions reflected from mask facet strike  10
                      the wall 1–2 µm down; local polymer
                      protection too thin there
Taper                 Polymer precursor deposition on lower  10
                      sidewall exceeds removal
Bottom CD loss        Taper accumulated over depth;          10
                      polymer at bottom corners
Tilt                  Ion flux not normal to wafer           9, 11
Striation             Oxide/nitride lateral rates differ     2, 10
Bending, end loss     Asymmetric charging                    11, 12
```

A simple estimate shows where reflected ions land. An ion falling vertically onto a mask facet tilted by angle β from vertical is deflected by 2β. It crosses the slit and strikes the opposite wall at a depth of roughly:

```
z_hit ≈ W / tan(2β)

Example: W = 0.20 µm, β = 3°
  z_hit ≈ 0.20 / tan 6° = 0.20 / 0.105 = 1.9 µm
```

This is close to the observed depth of maximum bow, 1–2 µm below the top. Chapter 10 develops the model in full.

---

## 3.7 Summary & Key Takeaways

1. **Bottom rate is set by two transmissions in series.** The neutral transmission K_n and the ion transmission K_i, combined in the synergy model, give the etch rate at any depth.

2. **Slots transmit neutrals far better than holes.** Without sticking, the slot advantage grows from 1.3× at A = 1 to 3.4× at A = 60. Transmission falls as (ln A)/A, not 1/A.

3. **Sticking species favor slots even more.** Line-of-sight flux is about 1/(2A) for a slot and 1/(4A²) for a hole, a ratio of about 100 at A = 58. This helps etchants and risks bottom polymer.

4. **Ions spread in one dimension in a slot.** Direct ion transmission is about 0.81 at A = 58 for the reference spread, against 0.63 for a hole.

5. **The slit stays ion-limited almost to the bottom.** For the reference process, the bottom rate is 43% of the top rate, and depth is nearly linear in time. The average rate is 0.405 µm/min, and the source stack is reached in about 28 minutes.

6. **Trenches charge more symmetrically than holes, except at asymmetries.** Slit ends, junctions, array edges, and local defects are where charging bends slits.

---

## Study Questions

1. Using the slot fit K_n ≈ (ln A + 0.15)/A and the reference parameters (ER_n0 = 8.0, ER_i0 = 0.75 µm/min, σ_θ = 4 × 10⁻³), compute the etch rate at A = 70. What fraction of the open-field rate is this? At what aspect ratio does ER_n equal ER_i?

2. A channel-hole recipe is run on a slit pattern. It uses a polymer precursor with an effective sticking probability of 0.05. Using the Monte Carlo table, compare the precursor flux reaching the bottom of the slit and of the hole at A = 40. Explain why the slit might taper or stop while the hole etches normally.

3. The ion angular spread doubles to σ_θ = 8 × 10⁻³ because of a higher operating pressure. Compute K_i at A = 58 for slot and hole. Recompute the slot etch rate at A = 58 with the reference ER_n0 and ER_i0.

4. Compute the line-of-sight fraction for a slot and a hole at A = 30 and A = 80. By what factor does the ratio change between the two aspect ratios?

5. A slit end has a 10 V potential asymmetry between its end wall and the opposite side, acting over 0.8 µm of depth in a 0.18 µm wide slit. For 2.5 keV ions, estimate the deflection angle. Over the remaining 6 µm of depth, how far does the bottom of the slit end move?

6. An ion is reflected from a mask facet tilted 2° from vertical. Where does it strike the opposite wall of a 180 nm slit? If the facet tilt grows to 4° as the mask erodes, where does the strike point move? What does this imply for the depth of the bow over the course of the etch?

---

**Next Chapter:** [Chapter 4: Slit Etch Chemistries & the Hard-Mask System](./04-chemistry-hardmask.md)

---

**Chapter 3 Development Status:** Complete  
**Version:** 1.0
