# Chapter 11: Tilt, Wiggling & Stress-Induced Distortion

## Overview

Chapter 10 dealt with the slit's width at each depth. This chapter deals with its **position**: where the slit's centerline is, at each depth and along its length, relative to the channel holes on either side and to the layers patterned later. Three kinds of error move the slit:

- **Tilt**: the slit is straight but leans, so its bottom is displaced from its top.
- **Wiggle**: the slit's centerline wanders from side to side along its length.
- **Distortion**: the slit is where the etch put it, but the wafer itself then moves when the stack releases its stress. Every later layer has to find the slit and the holes in their new positions.

Tilt and wiggle spend the clearance budget directly. Distortion spends the overlay budget of later layers. This chapter collects the sources of each, shows how big they are, and identifies which are worth fighting.

**Learning Objectives:**
- Combine the sources of tilt into a tilt budget and compare it with the clearance limit
- Explain how local wafer slope on the chuck produces apparent tilt
- Define wiggle and identify its main sources in slit etch
- Show by calculation why as-etched blocks do not buckle or collapse
- Estimate the anisotropic magnification produced by slit-induced stress release
- Describe die-level distortion between slit arrays and unslit regions, and its effect on overlay

---

## 11.1 Tilt

### 11.1.1 Sources

```
Source                          Where           Typical size        Chapter
──────────────────────────────────────────────────────────────────────────────
Edge sheath (ring mismatch)     Outer 5–10 mm   0–0.5°              9
Step-dependent edge mismatch    Outer 5–10 mm,  0–0.2°, in part of  9
                                deep part only  the depth
Global sheath asymmetry         Whole wafer     < 0.05°             5
(non-uniform plasma, chamber
asymmetry)
Local wafer slope on the chuck  Where the wafer 0.01–0.1°           11.1.2
                                is not flat
Charging asymmetry              Slit ends,      Local bending,      3
                                array edges     up to tenths of °
```

### 11.1.2 Apparent Tilt From Wafer Slope

Ions follow the electric field, which is normal to the sheath boundary. Far from the edge, that boundary is flat and horizontal, whatever the wafer underneath is doing. If the wafer is not perfectly flat on the chuck, its local surface is tilted relative to the ions. The slit is then etched vertically in the chamber frame but tilted relative to the wafer's own surface. When the wafer is released, the tilt stays with it:

```
Local slope from residual wafer shape on the chuck:

  θ_slope ≈ Δh / L

Example: a 2 µm height variation over 10 mm (a ridge left by a
particle under the wafer, or an incompletely seated edge):
  θ_slope = 2 × 10⁻⁶ / 10⁻² = 2 × 10⁻⁴ rad = 0.011°

Seated edge of a bowed wafer with a 20 µm lift over the last 5 mm:
  θ_slope = 20 × 10⁻⁶ / 5 × 10⁻³ = 4 × 10⁻³ rad = 0.23°
```

A well-seated wafer contributes little. A partly lifted edge contributes as much as a worn ring, and the two can be confused. A helium-leak excursion (Chapter 8, Section 8.4.3) correlated with edge tilt points to the chuck, not the ring.

### 11.1.3 Tilt Budget

```
Reference tilt budget at the critical sectors (Chapter 9, Section 9.2),
3 mm from the edge (illustrative):

  Edge sheath, mid-life ring, compensated     0.12°
  Step-dependent mismatch (ME-3 only)         0.05°  (affects deep part)
  Wafer slope (seated)                        0.03°
  Global asymmetry                            0.02°
  ──────────────────────────────────────────────────
  Linear sum                                  0.22°  ≤ 0.25° limit ✓
```

The sheath term dominates, and it moves through the life of the ring. The budget holds only while the edge compensation is current, which is why edge APC (Chapter 15) is as important as recipe control for slit yield.

### 11.1.4 Tilt Along the Depth

A slit does not always tilt by the same angle at every depth. If the mismatch changes between steps, the slit can be straight in one depth range and tilted in another, and its axis becomes a dog-leg:

```
  │         Uniform tilt:   bottom offset = D · tan θ
  │
   ╲        Dog-leg:        bottom offset = Σ (Δz_i · tan θ_i)
    ╲
     │      Example: 0.05° over 0–8 µm and 0.25° over 8–11.5 µm
     │        offset = 8.0 × 0.00087 + 3.5 × 0.00436
                     = 7.0 + 15.3 = 22.3 nm
```

What matters for clearance is the offset at each critical depth (Chapter 1, Section 1.4.3), so a dog-leg must be evaluated depth by depth, not as an average angle.

---

## 11.2 Wiggle

### 11.2.1 Definition

Wiggle is the lateral deviation of the slit centerline from a straight line along the slit's length, together with the associated local CD variation:

```
Plan view of a slit at some depth (exaggerated):

  designed:   ═══════════════════════════════════════════
  actual:     ═══════╲═══╱════════╲══╱═══════════════════
                     ◄── λ ──►
  Wiggle amplitude: 3σ of centerline position along the slit
  Wavelength λ: typically 0.5–5 µm
```

Short-wavelength roughness (below a few hundred nanometres) is usually called line-edge roughness and mostly smooths out during the etch. Wiggle is the long-wavelength part that does not.

### 11.2.2 Sources

```
Source                                  Mechanism                       Where
───────────────────────────────────────────────────────────────────────────────────────
Mask edge roughness, long wavelength    Printed by lithography; carried  Everywhere
                                        through a-C open and main etch
Mask-line buckling                      Compressive a-C stress, raised   Narrow mask lines:
                                        by fluorine uptake during etch,  partial slits,
                                        buckles narrow lines             select-gate cuts,
                                                                         closely spaced
                                                                         slit pairs
Local charging asymmetry                Lateral fields deflect ions      Near slit ends,
                                        (Chapter 3, Section 3.5)         junctions, mask
                                                                         defects
Local loading asymmetry                 Polymer and etchant supply       Next to large open
                                        differ on the two sides          or dense regions
Hole proximity (rare)                   Filled channel holes beside the  Where clearance is
                                        slit change local sidewall       very small
                                        etch
```

### 11.2.3 Mask-Line Buckling

A compressively stressed line on a substrate buckles sideways once its stress exceeds a critical value that falls with the line's height-to-width ratio. Empirically, a-C lines become prone to wiggling when the height-to-width ratio exceeds about 3–4 at compressive stresses near 1 GPa, which fluorinated carbon can reach.

```
Mask lines in the reference slit layout:

  Array (between slits):      width 1.8 µm, height 3.0 µm → h/w = 1.7  (safe)
  Between a slit and a narrow partial slit, 0.4 µm apart:
                              h/w = 7.5  (at risk late in the etch,
                                         as fluorine raises stress)
  As the mask erodes, h falls and h/w improves, but fluorination
  increases stress at the same time.
```

The main array is safe because its mask lines are wide. Narrow lines in special structures are where mask buckling causes wiggle. The remedies are layout (avoid narrow mask lines), lower-stress or doped carbon, thinner masks, and recipes that limit fluorine uptake in the carbon.

### 11.2.4 Wiggle in the Budget

The reference clearance budget carries 5 nm (3σ) of wiggle, combined in quadrature with overlay. Wiggle above about 10 nm starts to matter, both for clearance and for downstream steps: the slit spacer and the metal recess follow the wiggle, and the source-line conductor in the slit is narrowed at the wiggle's tight points.

---

## 11.3 Do the Blocks Move?

Once the slits are open, each block is a long wall about 1.8 µm wide and 11.5 µm tall, attached only at its base. It is natural to ask whether these walls lean, buckle, or collapse. For the as-etched stack, the answer is no. They are far too stiff.

### 11.3.1 Buckling Under the Retained Stress

Stress along the slits is retained (Chapter 2, Section 2.5.3). Each wall is a long plate under axial compression, clamped at its base and free at its top. The critical stress for such a plate:

```
σ_cr = k · π² · E / (12 (1 − ν²)) · (t / h)²

k ≈ 1.28 (long plate, one edge clamped, opposite edge free)
E ≈ 100 GPa (ON stack, illustrative), ν ≈ 0.2
t = wall width = 1.8 µm, h = wall height = 11.5 µm

σ_cr = 1.28 × 9.87 × 100 GPa / 11.5 × (1.8 / 11.5)²
     = 1.28 × 9.87 × 8.70 GPa × 0.0245
     ≈ 2.7 GPa

Retained stress ≈ 0.08 GPa ≪ 2.7 GPa → no buckling
```

Even a wall 1.0 µm wide and 16 µm tall has σ_cr ≈ 0.4 GPa, still five times the stack stress. Global wall buckling is not a slit-etch failure mode for realistic block widths.

### 11.3.2 Capillary Forces in Wet Steps

After the etch, the slits are cleaned and later filled with liquids. When a liquid dries in a gap between two walls, surface tension pulls the walls together:

```
Capillary pressure in a 0.2 µm gap (water, contact angle 0°):
  ΔP = 2γ / g = 2 × 0.072 / 0.2 × 10⁻⁶ ≈ 0.72 MPa

Deflection of the wall top (cantilever, uniform pressure per unit length):
  δ = ΔP · h⁴ / (8 E I),  I = t³/12 per unit length

  δ = 0.72 × 10⁶ × (11.5 × 10⁻⁶)⁴ / (8 × 10¹¹ × (1.8 × 10⁻⁶)³ / 12)
    ≈ 3 × 10⁻¹⁴ m
```

The deflection is negligible. **As-etched blocks are mechanically robust.** The vulnerable stage comes later: after the nitride is removed, each block is a stack of thin oxide shelves held apart only by the channel holes, with no solid wall. Leaning and collapse in that state belong to the replacement-gate module and are discussed in Chapter 16. The slit etch contributes to that later risk through its bottom CD and straightness, since a narrow, wiggling slit is harder to wet, rinse, and dry evenly.

### 11.3.3 Local Relaxation at the Top

The walls do relax a little at the top. A compressively stressed wall freed on both sides expands sideways into the slits:

```
Relaxed lateral strain (compressive stack, E ≈ 100 GPa, ν ≈ 0.2):
  ε ≈ |σ| (1 − ν) / E × f_rel = 82 MPa × 0.8 / 100 GPa × 0.84 ≈ 5.5 × 10⁻⁴

Expansion of a 1.8 µm wall: 1.8 µm × 5.5 × 10⁻⁴ ≈ 1.0 nm
Each slit narrows by ~1 nm at the top (0.5 nm from each wall)
```

This is small but systematic, and it is the reason the top CD measured after etch can be slightly smaller than the CD the etch actually cut. It is negligible against the 6 nm top-CD tolerance.

---

## 11.4 Wafer-Level Distortion

### 11.4.1 From Bow Change to Overlay

The slits release stack stress across the slit direction (Chapter 2, Section 2.5). That changes the wafer's curvature anisotropically. When the wafer is later held flat on a lithography chuck, the change in curvature appears as **in-plane displacement** of every feature on the front surface. For a uniform curvature change, the displacement is linear in position, which is a magnification:

```
Front-surface in-plane displacement from a curvature change Δκ:
  u(x) ≈ (h_s / 2) · Δκ · x       (magnification m = (h_s/2)·Δκ)

Reference saddle (Chapter 2, Section 2.5.4):
  Across slits: bow −60 µm → +248 µm
  κ = 2δ / r²:  −5.3 × 10⁻³ → +2.20 × 10⁻² m⁻¹
  Δκ_⊥ = 2.74 × 10⁻² m⁻¹
  Along slits: Δκ_∥ ≈ 0

  m_⊥ = (775 × 10⁻⁶ / 2) × 2.74 × 10⁻² ≈ 1.06 × 10⁻⁵ = 10.6 ppm
  m_∥ ≈ 0

  At the wafer edge (x = 150 mm): u_⊥ ≈ 1.6 µm
```

A 1.6 µm shift at the wafer edge sounds catastrophic, but it is a linear magnification, different in two directions. Lithography scanners correct linear terms, including anisotropic magnification, with their standard wafer alignment model. **The global saddle is correctable.** What remains is the part that is not linear.

### 11.4.2 Die-Level Distortion

Inside each die, only the array is slit. The staircases and periphery remain continuous films. The change in film force is therefore patterned at die scale:

```
Within a die (cross-slit direction):

  periphery │  array (slit)  │ staircase │ array (slit) │ periphery
  no change │ force released │ no change │ released     │ no change

Local front-surface strain where the force is released (regions much
larger than the wafer thickness, ~0.8 mm):
  ε ≈ 4 · Δ(σ h_f) / (M_s · h_s)
    = 4 × 758 N/m / (180 GPa × 775 µm) ≈ 2.2 × 10⁻⁵

(Δ(σ h_f) = 0.84 × 902 N/m, from Chapter 2.)

Over a 4 mm array plane: displacement difference ≈ 2.2 × 10⁻⁵ × 4 mm
                                               ≈ 90 nm (illustrative upper bound)
```

The actual displacement is smaller than this bound, because the stiff substrate spreads the strain over the neighboring regions. It is still a die-scale pattern of tens of nanometres. Scanners can correct part of it with intrafield (per-field) models, but a residual of several nanometres typically remains. The pattern repeats in every die, so it is systematic and can be partly corrected by a fixed per-product intrafield correction.

### 11.4.3 Who Pays

```
Later layer                     Overlay concern
──────────────────────────────────────────────────────────────────────
Word-line contacts on the       Contacts must land on treads near the
staircase (Book #23; Contact-   array/staircase boundary, where die-level
Hole Etch companion)            distortion changes fastest
Bit-line contacts on channel    Contacts must land on channel plugs; the
holes                           array has moved relative to the alignment
                                marks
Source-line contacts            Must land on the filled slit
Any layer aligned to marks in   Marks in unslit regions move differently
unslit regions                  from the array features they stand for
```

The slit etch does not see the overlay error it causes. It appears in the lithography of later layers. Recognizing the slit step as the origin of a die-level overlay signature, and placing alignment marks where they move with the array, are integration responsibilities.

### 11.4.4 Later Steps Change It Again

The saddle and the die-level pattern after slit etch are not final. Nitride removal releases stress in the opposite way to deposition. Tungsten or molybdenum fill adds strong tensile stress in the word-line layers. Slit fill adds its own. The overlay signature seen at bit-line contact is the sum of all of them. The slit etch is the step that first makes the stress anisotropic, and later steps build on that pattern.

---

## 11.5 Putting Position Errors Together

```
Error            Spends                 Main control                        Chapter
───────────────────────────────────────────────────────────────────────────────────────
Tilt (edge)      Clearance at depth     Edge sheath compensation; ring life  9, 15
Tilt (slope)     Clearance at depth     Chucking; particle control under     8
                                        the wafer
Dog-leg tilt     Clearance at a depth   Step-dependent edge settings         9
                 range
Wiggle           Clearance (random      Mask LER; layout of narrow lines;    10, 14
                 part)                  mask stress; charging at ends
Top relaxation   Top CD (≈1 nm)         None needed                          —
Global saddle    Later overlay          Scanner linear correction            15
                 (correctable)
Die-level        Later overlay          Intrafield correction; mark          15, 16
distortion       (partly correctable)   placement
```

---

## 11.6 Summary & Key Takeaways

1. **Tilt has one dominant source and several small ones.** The edge sheath dominates. A partly lifted wafer edge can mimic it, and helium leak data tells them apart.

2. **Evaluate tilt depth by depth.** Step-dependent edge mismatch produces dog-leg slits whose offset at the critical depth differs from what an average angle suggests.

3. **Wiggle lives where mask lines are narrow.** The main array's wide mask lines are safe. Partial slits, select-gate cuts, and slit pairs are where carbon buckling and charging cause wiggle.

4. **As-etched blocks do not buckle or collapse.** Their critical buckling stress is tens of times the stack stress, and capillary deflection is negligible. Mechanical risk comes after nitride removal.

5. **Slits make the wafer's magnification anisotropic.** In the reference case, that is about 10 ppm across the slits. The global part is correctable by the scanner.

6. **Die-level distortion is the lasting cost.** Slit arrays and unslit regions strain differently, leaving a repeating intrafield pattern of tens of nanometres that later layers must correct.

---

## Study Questions

1. An edge region has 0.10° of sheath tilt, and the wafer edge is lifted 15 µm over its last 6 mm on the chuck, in the same direction. Compute the total tilt and the bottom offset at 11.5 µm depth. Is the reference tilt limit met?

2. A slit tilts 0.02° in ME-1 (0–3 µm), 0.08° in ME-2 (3–8 µm), and 0.30° in ME-3 (8–11.3 µm). Compute the lateral offset at 7.2 µm and at 11.3 µm. Compare with the Chapter 1 tilt limits at those depths.

3. A partial-slit layout places a 0.35 µm wide mask line between a main slit and a partial slit. The a-C mask is 3.0 µm thick at the start and 1.0 µm at the end. Compute h/w at the start and end. At what point in the etch is buckling most likely, given that fluorine uptake raises compressive stress through the etch?

4. Compute the critical buckling stress for a wall 0.8 µm wide and 14 µm tall (E = 100 GPa, ν = 0.2, k = 1.28). Compare with a stack stress of −120 MPa. What wall width would make the two equal?

5. A product's post-slit bow changes by +200 µm across the slits and +20 µm along them (300 mm wafer, 775 µm thick). Compute the anisotropic magnification in ppm in each direction and the displacement at the wafer edge. Which part can a scanner correct?

6. Explain why an alignment mark in the periphery of a die can mislead the scanner about the position of the array after slit etch. Propose two ways to reduce the resulting overlay error at bit-line contact.

---

**Next Chapter:** [Chapter 12: Landing, Etch Stop & ARDE Across Regions](./12-landing-arde-regions.md)

---

**Chapter 11 Development Status:** Complete  
**Version:** 1.0
