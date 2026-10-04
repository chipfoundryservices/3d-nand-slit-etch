# Chapter 10: Profile Control — Bowing, Taper, Striation & Bottom CD

## Overview

A slit's profile is the width of the trench at every depth. Ideally the walls would be perfectly vertical, so the width would be the same at the top, the middle, and the bottom. Real slits bulge outward a little below the top (**bow**), narrow steadily toward the bottom (**taper**), show fine ridges where oxide and nitride layers meet (**striation**), and end in a bottom that may be flat, rounded, or notched at its corners. Each feature comes from a specific imbalance between etching and protection at that depth, and each one spends a specific part of the clearance budget or the downstream steps' margin.

This chapter explains how bow forms and what moves it, why a fraction of a degree of taper costs tens of nanometres at the bottom, where striation and bottom-shape defects come from, and how the levers that fix one feature affect the others.

**Learning Objectives:**
- Define the profile parameters of a slit and their specifications
- Explain bow formation by mask-facet reflection and estimate bow depth and magnitude
- Relate taper angle to bottom-CD loss and explain taper runaway
- Distinguish horizontal (interface) striation from vertical (mask-edge) striation
- Explain bottom-corner microtrenching and bottom rounding
- Use a lever-response matrix to fix one profile feature without breaking another

---

## 10.1 Profile Vocabulary

```
Slit profile (cross-section perpendicular to the slit, exaggerated):

        ◄─ W_t ─►              top CD (at stack top, after mask removal)
     ───┐       ┌───
         ╲     ╱               neck (sometimes, under a polymer overhang)
          │   │
        ╱       ╲   ← z_bow    bow: maximum CD W_bow, 1–2 µm down
        │       │
         │     │               taper: steady narrowing with depth
          │   │
          │   │
           │ │                 bottom CD W_b (at the stack bottom)
           └─┘                 bottom shape: flat, rounded, or with
                               corner microtrenches

Specifications (reference, from Chapter 1):
  W_t = 200 ± 6 nm (3σ)
  W_bow − W_t ≤ 30 nm
  W_b ≥ 130 nm (≥ 65% of W_t)
  Striation ≤ 3 nm amplitude
```

---

## 10.2 Bow

### 10.2.1 Formation by Facet Reflection

The top corners of the carbon mask are eroded faster than its flat top, because sputter yield peaks at oblique incidence. Over the etch, the corners become **facets**: sloped surfaces at the edge of each mask opening. Ions that strike a facet at grazing incidence reflect forward with much of their energy. A facet inclined by β from vertical deflects a normally incident ion by 2β. The ion crosses the slit and hits the opposite wall:

```
Facet reflection (schematic):

      ion ↓
     ─────╲         ← facet inclined β from vertical
           ╲
            ╲ ↘  reflected ion, deflected 2β
     mask   │  ╲
     ───────┤    ╲
     stack  │      ╲
            │        ✕  ← strikes opposite wall at depth z_hit
            │
z_hit ≈ W / tan(2β)   (measured from the bottom of the facet)

  β = 2°: z_hit ≈ 0.20 µm / tan 4° = 2.9 µm
  β = 3°: z_hit ≈ 0.20 µm / tan 6° = 1.9 µm
  β = 5°: z_hit ≈ 0.20 µm / tan 10° = 1.1 µm
```

A real facet has a range of inclinations, so reflected ions spread over a band of depths. The bow is the envelope of their impacts, weighted by how much ion energy each inclination reflects. Its peak typically sits 1–2 µm below the top of the stack, where the commonest facet angles send their ions.

### 10.2.2 Bow as a Balance

At each depth on the sidewall, the net lateral etch rate is the reflected-ion etching minus the polymer protection:

```
LER(z) = Y_side(E_refl, angle) · Γ_refl(z) − R_dep(z)

Bow width growth over the etch:
  ΔW(z) = 2 · ∫ max(0, LER(z, t)) dt

Example: net LER at the bow depth averages 0.5 nm/min over 30 min
  ΔW = 2 × 0.5 × 30 = 30 nm  → bow at the specification limit
```

Because the facet grows as the mask erodes, Γ_refl and the reflected energy both rise through the etch. **Most of the bow is cut in the second half of the etch, even though it sits near the top.** A recipe can look clean at a depth-series wafer stopped after ME-1 and still bow at full length. Depth series must therefore be read for bow at every stop, not only the first.

### 10.2.3 What Moves Bow

```
Lever                              Effect on bow       Mechanism
──────────────────────────────────────────────────────────────────────────
Lower ion energy in ME-1           Smaller             Slower facet growth;
                                                       fewer energetic
                                                       reflections
Higher C₄F₆ fraction (ME-1/2)      Smaller             Thicker sidewall polymer
                                                       at bow depth; mask
                                                       protected
Bias pulsing (off-phase            Smaller             Polymer without ion
deposition)                                            removal (Chapter 6)
Colder wafer                       Smaller             Thicker polymer
                                                       (Chapter 8)
Less O₂                            Smaller             Thicker polymer
Higher mask selectivity            Smaller, later      Facet forms later
(denser a-C)
Passivating additive (e.g., COS)   Smaller (reported)  Harder upper-sidewall
                                                       and mask-corner film
Lower pressure                     Smaller             Narrower ion angles;
                                                       fewer direct wall hits
```

Almost every lever that reduces bow adds polymer or reduces ion energy. Both of those also affect the bottom. That is the central conflict of slit profile control (Section 10.6).

### 10.2.4 Bow and the Clearance Budget

The upper-deck bow depth is also where the channel holes are widest (Chapter 1, Section 1.4.2). Two strategies are open:

```
Strategy                          How                           Gain
──────────────────────────────────────────────────────────────────────────
Reduce slit bow                   Levers in Section 10.2.3      ~0.5 nm clearance
                                                                per nm of CD
Move slit bow away from the       Shift facet angle (mask       Clearance gained
hole bow                          stack, ME-1 energy) to put    where the hole is
                                  the slit bow deeper or        narrower; depends
                                  shallower than the hole bow   on both profiles
```

The second strategy is often overlooked. If the hole bow is at 1.5 µm and the slit bow can be moved to 2.5 µm, where the hole has narrowed by 5–10 nm, the clearance gain is comparable to removing 10–20 nm of slit bow.

---

## 10.3 Taper and Bottom CD

### 10.3.1 Taper Angle and Bottom-CD Loss

Below the bow, the slit narrows steadily. A taper angle α from vertical, on both walls, reduces the width by 2·tan α per unit depth:

```
W(z) = W_bow − 2 (z − z_bow) tan α

Reference: W_bow = 230 nm at 1.5 µm; W_b = 130 nm at 11.7 µm
  tan α = (230 − 130) / (2 × 10 200) = 0.0049
  α = 0.28°  (sidewall angle 89.72°)

Sensitivity of bottom CD to taper:
  dW_b / dα = −2 × 10.2 µm × (π/180) per degree = −356 nm per degree
  An extra 0.1° of taper → −36 nm of bottom CD
```

**A taper change too small to see in a cross-section image costs a quarter of the bottom-CD margin.** Bottom CD must be measured, not inferred from a sidewall angle.

### 10.3.2 Where Taper Comes From

Taper forms where deposition on the lower sidewall exceeds removal. Unlike the bow, the lower sidewall is rarely hit by energetic reflected ions. It is shaped mostly by polymer:

```
Contributors to taper:
  - Low-sticking precursors that reach the lower sidewall (Chapter 3,
    Section 3.2.4); slits receive more than holes
  - Bottom polymer that is not fully cleared at the corners, so each
    new increment of depth starts slightly narrower
  - Ion angular spread: ions that clip the sidewall near the bottom
    clean it; narrower IAD at high energy reduces that cleaning
  - Redeposition of etch products (Si-, C-containing) on the walls
```

### 10.3.3 Taper Runaway

Taper feeds itself. A narrower slit has a higher aspect ratio at the same depth, so fewer ions and neutrals reach the bottom (Chapter 3), and the deposition-to-etch balance shifts further toward deposition:

```
Narrower bottom → higher local A → lower ion flux at bottom
  → less polymer cleared at corners → more taper → narrower bottom

If the walls converge, the slit ends in a V and stops:
  z_stop ≈ z_bow + W_bow / (2 tan α)
  Reference: 1.5 + 0.230 / (2 × 0.0049) µm = 1.5 + 23.5 = 25 µm
  (far below the stack: safe)
  If α = 0.6°: 1.5 + 0.230 / (2 × 0.0105) = 1.5 + 11.0 = 12.5 µm
  → V-closed just below the stack: landing fails
```

The reference process has a comfortable margin against closure, but doubling the taper angle would close the slit right at the landing depth. Taper margin shrinks as stacks get deeper, which is why ME-3 is tuned specifically against taper.

### 10.3.4 Bottom-CD Levers

```
Lever (applied in ME-3)             Bottom CD     Cost
──────────────────────────────────────────────────────────────────────
+O₂ (a few sccm)                    Larger        Mask erosion; slight
                                                  bow if applied early
+NF₃ (small)                        Larger        Mask erosion; striation
                                                  if ox:N shifts
Higher bias                         Larger        Heat, mask, edge ring
Warmer wafer                        Larger        Mask; bow if early
Lower C₄F₆ fraction                 Larger        Mask, bow
Lower pressure                      Larger        Neutral supply at depth
```

These levers are applied **late**, in ME-3, so that their costs (mostly to bow and mask) are paid at a time when the bow region is already protected and the mask has been budgeted for them.

---

## 10.4 Striation

### 10.4.1 Two Kinds

```
Kind                      Direction            Origin
──────────────────────────────────────────────────────────────────────────
Horizontal (interface)    Rings around the     Oxide and nitride recede
striation                 slit at each layer   laterally at different rates
                          (period = pair       (Chapter 2, Section 2.2.3)
                          pitch)
Vertical striation        Ridges running down  Mask line-edge roughness
                          the wall             transferred and amplified
                                               through the etch
```

### 10.4.2 Horizontal Striation

Horizontal striation measures the sidewall oxide/nitride balance directly. A nitride-recessed sidewall means the nitride lateral rate exceeds the oxide lateral rate. Its amplitude grows with exposure time, so it is largest near the top (Chapter 2). The fix is chemical: adjust CH₂F₂ or O₂ to bring the sidewall rates together (Chapter 4, Section 4.3). Because the sidewall environment changes with depth, a recipe can show nitride recess near the top and oxide recess deeper, which reveals a depth-dependent imbalance that a ramp can correct.

### 10.4.3 Vertical Striation

Roughness on the mask edge is printed into the stack. Short-wavelength roughness (tens of nanometres along the slit) tends to be smoothed during the etch, because polymer fills small notches. Long-wavelength roughness (hundreds of nanometres to microns) is transferred nearly unchanged and appears as slow CD and position variation along the slit, which is **wiggle** (Chapter 11). The mask-open step has the most influence: an a-C open with good sidewall passivation and low LER sets the starting point.

### 10.4.4 Why Striation Matters Downstream

```
Downstream step         Effect of striation
──────────────────────────────────────────────────────────────────────
Slit liner (if any,     Liner follows the ridges; thin spots at sharp
before nitride          notches
removal)
Nitride removal         Recessed nitride levels start the lateral
                        etch slightly ahead; small effect
Metal recess            Recessed word-line levels hold metal closer
                        to the slit; recess must remove more there
                        (Chapter 16)
Slit spacer             Spacer thickness varies with the ridges;
                        local thin spots raise leakage risk
```

---

## 10.5 Bottom Shape

### 10.5.1 Microtrenching

Ions reflected from the lower sidewall at grazing angles are focused toward the bottom corners. The corners receive more ion flux than the center and etch deeper, leaving small trenches at each side of the bottom:

```
Bottom shape (exaggerated):

  Flat              Rounded            Microtrenched
  │      │          │      │           │      │
  │      │           ╲    ╱            │      │
  └──────┘            ╰──╯             └╮    ╭┘
                                        ╰────╯  ← corners deeper
```

Microtrenches make the slit reach the landing layer first at its corners. In a replacement-source landing (Chapter 12), that can punch the corners through the poly-Si stop before the center clears it. Mild microtrenching is harmless at the poly stop if LS-1 selectivity is high. Strong microtrenching shows up as a corner punch-through in the lower poly-Si.

### 10.5.2 Rounding

Excess bottom polymer, or a broad ion angular distribution, rounds the bottom. A rounded bottom reaches the stop first at its center, and the corners clear last. It needs more overetch in LS-1 to clear corners fully, which costs poly-Si loss at the center.

### 10.5.3 The Goal

A flat bottom is the best starting point for landing. Bottom shape is tuned in ME-3 and LS-1 by the polymer level and the ion energy: more polymer rounds, more energy and less polymer flattens and then microtrenches.

---

## 10.6 The Lever-Response Matrix

```
Lever (where applied)          Bow     Top CD  Bottom CD  Striation  Mask     Rate
──────────────────────────────────────────────────────────────────────────────────────
−Bias, ME-1                    −−      0       −          0          +        −
+C₄F₆, ME-1                    −       −       −          ±          +        −
Pulsing, ME-1                  −−      0       −          0          +        −
+CH₂F₂, ME-2                   0       0       ±          N recess−  +        0/+
+O₂, ME-3                      +(if    0       ++         ±          −        +
                               early)
+Bias, ME-3                    0       0       ++         0          −        ++
Colder ESC (whole etch)        −       −       −−         ±          ++       −
Lower pressure (whole etch)    −       0       +          0          −        −/+

(+ = increases; − = decreases; doubled = strong. Illustrative.)
```

Reading across a row shows what else a lever moves. Reading down a column shows the candidates for fixing one feature. The general pattern:

- **Bow** is fixed early, with lower energy and more protection near the top.
- **Bottom CD** is fixed late, with more energy and less polymer near the bottom.
- **Whole-etch levers**, such as ESC temperature and pressure, move bow and bottom CD in opposite directions and are best avoided for profile fixes.

### 10.6.1 Worked Example

```
Starting point (illustrative): bow 38 nm (spec ≤ 30); bottom CD 136 nm
(spec ≥ 130); remaining mask 0.80 µm (spec ≥ 0.5)

Change 1: ME-1 bias −15%, ME-1 duration +6% to keep depth
  Bow:        −9 nm  → 29 nm  ✓
  Bottom CD:  −4 nm  → 132 nm (marginal)
  Mask:       +0.04 µm → 0.84 µm

Change 2: ME-3 O₂ +2 sccm
  Bottom CD:  +7 nm  → 139 nm ✓
  Mask:       −0.08 µm → 0.76 µm ✓
  Bow:        unchanged (bow region protected by then)

Net: bow 29 nm, bottom CD 139 nm, mask 0.76 µm
```

The two changes are applied at opposite ends of the etch, each where it does the most good and the least harm. Applying either one to the whole etch would have moved both features the wrong way.

---

## 10.7 Summary & Key Takeaways

1. **Bow comes from ions reflected off the mask facet.** A facet inclined 2–5° from vertical sends its ions to a depth of 1–3 µm in a 200 nm slit.

2. **Bow is cut mostly late in the etch, near the top.** The facet grows as the mask erodes. Depth series must be checked for bow at every stop.

3. **Taper is cheap in angle and expensive in CD.** 0.1° of extra taper costs about 36 nm of bottom CD over 10 µm. Taper feeds on itself through aspect ratio.

4. **Striation reports chemistry.** Horizontal striation measures the oxide/nitride sidewall balance. Vertical striation comes from the mask edge and becomes wiggle at long wavelengths.

5. **Bottom shape sets up the landing.** Microtrenched corners punch first, and rounded bottoms clear their corners last. A flat bottom is the goal.

6. **Fix bow early and bottom CD late.** Levers applied in the step where they help most cost the least elsewhere.

---

## Study Questions

1. A mask facet has inclinations between 2.5° and 4° from vertical. For a 180 nm slit, compute the range of depths struck by reflected ions. Where would you expect the bow peak?

2. A slit has W_bow = 225 nm at 1.6 µm and W_b = 140 nm at 11.5 µm. Compute the taper angle. A recipe change increases taper by 0.05°. What is the new bottom CD? Is it within the reference specification?

3. Using the closure formula, compute the depth at which the slit in Question 2 would close at its original and new taper angles. How much margin does each leave below a 12.0 µm landing depth?

4. Horizontal striation measured by cross-section is 3 nm of nitride recess at 1 µm depth and 1 nm of oxide recess at 9 µm depth. What does this say about the sidewall chemistry at the two depths? Which gas would you ramp, in which direction, and through which steps?

5. A process engineer proposes lowering the ESC temperature by 5 °C over the whole etch to fix a 6 nm bow excess. Using the sensitivities in Chapter 8, Section 8.1.1, estimate the effect on bow, bottom CD, and mask selectivity. Propose an alternative using step-specific levers.

6. Microtrenches at the slit bottom are 25 nm deeper than the center. In LS-1, the stack:poly-Si selectivity is 15. How much extra poly-Si loss do the corners see compared with the center during the overetch? Is this a concern for a 150 nm poly-Si stop?

---

**Next Chapter:** [Chapter 11: Tilt, Wiggling & Stress-Induced Distortion](./11-tilt-wiggling-distortion.md)

---

**Chapter 10 Development Status:** Complete  
**Version:** 1.0
