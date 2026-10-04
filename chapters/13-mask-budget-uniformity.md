# Chapter 13: Mask Budget, Loading & Uniformity

## Overview

A slit is only as good as the mask that defines it. The carbon mask has to last the whole etch, keep its edges sharp enough that the top of the slit does not widen, and erode evenly enough across the wafer that the edge does not run out first. At the same time, every slit on the wafer has to be etched to the same depth, width, and profile, whether it sits at the center or 3 mm from the edge, in a dense array or beside an open region, on a product with a large array fraction or a small one.

This chapter completes the mask budget started in Chapter 4, adding faceting, edge erosion, and scaling to deeper stacks. It then covers loading, the ways the pattern itself changes the chemistry, and within-wafer uniformity of depth, CD, and profile, with the hierarchy of knobs used to control them.

**Learning Objectives:**
- Build a complete mask budget with planar loss, facet allowance, and edge erosion
- Explain what happens to the top CD when the mask runs out
- Compute the a-C thickness required as the stack deepens
- Describe macroloading and microloading in slit etch and their sources
- Explain why radial tuning for depth and for CD can conflict
- Set up a compensation hierarchy from hardware to per-wafer APC

---

## 13.1 The Complete Mask Budget

### 13.1.1 Planar Loss

From Chapter 4, Section 4.5.3, for the reference process:

```
Starting a-C                                    3.00 µm
Mask open and cap loss                         −0.05 µm
Main etch (28.4 min at 0.069 µm/min)           −1.95 µm
Landing stages                                 −0.12 µm
──────────────────────────────────────────────────────────
Remaining (planar, wafer center)               ≈ 0.88 µm
```

### 13.1.2 Facets

The mask edge does not stay square. Its corner erodes into a facet that grows downward through the etch. The facet's vertical extent h_f, measured from the mask top down to where the facet meets the vertical mask sidewall, grows roughly in proportion to the planar erosion:

```
h_f ≈ k_f × (planar mask loss)      k_f ≈ 0.10–0.20 (illustrative)

Reference: k_f = 0.15 → h_f ≈ 0.15 × 2.12 µm ≈ 0.32 µm at the end

The facet must not reach the stack top:
  Remaining planar mask > h_f
  0.88 µm > 0.32 µm ✓ (margin 0.56 µm)
```

### 13.1.3 What Happens When the Mask Runs Out

```
Stage                         What the top of the slit sees
──────────────────────────────────────────────────────────────────────
Mask thick, facet small       Top CD set by the mask's lower sidewall;
                              stable
Facet reaches the stack top   Ions reflect off a facet that now ends
                              at the cap oxide; cap oxide at the slit
                              edge begins to erode → top CD grows
Mask gone at the edge of the  Cap oxide etched; top CD grows rapidly;
opening                       the top select-gate region is exposed
                              to direct ion bombardment
```

Top CD growth late in the etch reduces clearance at the very top, but more importantly it can thin the cap oxide over the top select gates. The specification of ≥ 0.5 µm remaining planar mask keeps the facet well above the stack, with margin for the edge effects below.

### 13.1.4 Edge Erosion

Mask erosion is not uniform across the wafer. At the extreme edge, ion flux and ion energy can be higher, the wafer can be warmer, and the edge ring's chemistry differs:

```
Mask loss profile (illustrative):

  Radius (mm)        0       100      140      147
  Relative loss      1.00    1.01     1.05     1.12

Remaining at 147 mm:
  3.00 − 0.05 − 1.12 × (1.95 + 0.12) = 3.00 − 0.05 − 2.32 = 0.63 µm
  Facet at 147 mm: 0.15 × 2.37 ≈ 0.36 µm → margin 0.27 µm
```

The center has 0.56 µm of facet margin, but the extreme edge has only 0.27 µm. **The mask budget, like the tilt budget, is decided at the edge.**

### 13.1.5 Scaling to Deeper Stacks

Mask loss grows faster than depth, because the stack's average rate falls with depth while the mask keeps eroding at its open-field rate:

```
Using the Chapter 3 ARDE model (reference chemistry, 200 nm slit) and
r_m = 0.069 µm/min:

  Stack above    Main etch   Avg rate    Mask loss   Effective    a-C needed*
  source (µm)    (min)       (µm/min)    (µm)        selectivity  (µm)
  ───────────────────────────────────────────────────────────────────────────
  11.5           28.4        0.405       1.95        5.9          2.6
  13.0           33.6        0.387       2.30        5.6          3.0
  15.0           41.0        0.366       2.81        5.3          3.5
  18.0           53.2        0.338       3.65        4.9          4.3

  * planar loss + 0.17 µm (open + landing) + 0.5 µm reserve,
    at wafer center; add ~10% for the edge
```

Thicker masks have their own problems. A 4.3 µm a-C mask is harder to deposit with low stress, harder to see through for alignment, and harder to open with vertical walls. Its own aspect ratio (4.3/0.2 ≈ 22) also adds to the slit's transport problem from the first minute. At some depth it becomes better to change the mask material (denser or doped carbon, Chapter 4), the chemistry (cryogenic etch, Chapter 8), or the scheme (multi-step slits, Chapter 14) than to keep thickening the mask.

---

## 13.2 Loading

### 13.2.1 What Is Exposed

```
Open (etching) area in the slit layer (reference layout, illustrative):

  Array: slit width / slit pitch = 0.2 / 2.0 = 10%
  Array fraction of wafer area ≈ 0.65
  Staircase slits and dummy patterns: small additional area
  ─────────────────────────────────────────────────────────────
  Total open area ≈ 7% of the wafer
  Mask (a-C) area ≈ 93% of the wafer
```

Slit etch is a **low-open-area** process. The plasma sees mostly carbon mask. Etch products from the stack are a small part of the gas load, but mask erosion products (CO, CO₂, CₓFᵧ, and with nitrogen-containing gases, CN species) are a large part.

### 13.2.2 Macroloading by the Mask

Because the mask dominates the exposed area, the chemistry depends on how much mask there is and how fast it erodes:

```
Effect of mask-derived species:
  - Carbon from the mask adds to the polymer budget (lowers effective
    F/C) → more polymer than the feed gases alone would give
  - Oxygen consumption by mask erosion → less free O for polymer
    control

Consequences:
  - Products with different array fractions (different open-area and
    mask fractions) need different recipes or APC offsets
  - A monitor wafer with a different pattern density does not
    reproduce the product chemistry
  - Mask-material changes (e.g., a denser a-C) change the chemistry
    even if the recipe does not change
```

### 13.2.3 Microloading

Within a die, slits sit in different neighborhoods:

```
Neighborhood                         Local effect (illustrative)
──────────────────────────────────────────────────────────────────────
Dense array interior                 Reference
Last slit beside a large mask area   More mask-derived polymer nearby
(array edge, periphery)              → slightly narrower, more tapered
Slit beside a large open area        Local etchant depletion and
(e.g., a large etched region in      product build-up → slower,
the same layer, if present)          more polymer
Staircase slits                      Different neighbors (fill oxide,
                                     word-line contact areas)
```

Microloading in slit etch is usually a few percent in rate and a few nanometres in CD, smaller than in high-open-area etches. It concentrates at the array edges, which is another reason for dummy slits there (Chapter 12, Section 12.4.5).

### 13.2.4 The Wafer Edge Region

At the very edge of the wafer, outside the last die, the films and the mask may be removed by edge-bead and bevel processing. If the stack is exposed without mask there, a ring of open area surrounds the patterned region. That ring etches as an open field, consumes etchant, releases products, and can change the chemistry seen by the outermost die. Bevel films, if left, can also flake or arc under kilovolt bias. The edge-exclusion design of the mask and stack layers, and of the bevel cleans before slit etch, is part of slit-etch edge control.

---

## 13.3 Within-Wafer Uniformity

### 13.3.1 What Must Be Uniform

```
Parameter          Typical spec (3σ,            Main radial sources
                   illustrative)
──────────────────────────────────────────────────────────────────────────
Depth / arrival    ±3% before landing           Ion flux, stack thickness,
                                                gas distribution
Top CD             ±6 nm                        Mask CD (litho, a-C open),
                                                ESC temperature
Bow                ±5 nm                        Temperature, polymer, mask
                                                facet (edge)
Bottom CD          ±8 nm                        Polymer, ion energy,
                                                temperature
Tilt               ≤ 0.25° (critical sectors)   Edge sheath
Remaining mask     ≥ 0.5 µm everywhere          Edge ion flux, temperature
```

### 13.3.2 Knobs and Their Radial Reach

```
Knob                          Radial reach         Moves mainly
──────────────────────────────────────────────────────────────────────
VHF electrode / power         Center ↔ edge        Ion flux → rate
distribution                  (broad)
Center:edge gas split         Broad                Rate, polymer, CD
Edge gas injection            Outer ~10–20 mm      Edge polymer, CD, bow
ESC temperature zones         Per zone             Polymer: CD, bow, bottom
                                                   CD, mask
Edge ring height / voltage    Outer ~5–10 mm       Tilt; edge ion flux,
                                                   edge rate, edge mask
```

### 13.3.3 Conflicting Goals

Different parameters want different radial corrections:

```
Example (illustrative): at the edge, depth is 2% low and bottom CD is
6 nm small.

  Option A: raise edge ion flux (edge ring voltage +)
    → edge depth recovers; edge bottom CD opens (+)
    → but edge mask erosion rises and edge tilt changes
  Option B: warm the edge zone +3 °C
    → edge bottom CD opens (+1.2 nm, Chapter 8)
    → edge bow grows (+1.5 nm); edge mask erodes faster (−3%)
    → depth barely changes
  Option C: edge gas with slightly more O₂
    → edge bottom CD opens; edge rate rises a little
    → edge mask erosion rises; edge bow may grow if applied early

No single knob fixes depth and bottom CD without costing mask or tilt.
```

The usual resolution is to rank the parameters by their margin. In the reference process, edge mask margin (0.27 µm facet margin at 147 mm) and edge tilt are the tightest, so knobs that erode edge mask or move tilt are used sparingly. Depth non-uniformity is left to the landing stop, which is designed to absorb it (Chapter 12). Bottom CD is fixed with ME-3-only polymer changes.

---

## 13.4 Wafer-to-Wafer and Chamber-to-Chamber Variation

```
Source                                   Affects                Control
──────────────────────────────────────────────────────────────────────────────
Stack thickness (deposition chamber,     Arrival time           Feed-forward of
time since clean)                                               measured thickness
Nitride composition                      Rate, ox:N balance     Feed-forward by
                                                                deposition chamber
a-C thickness and density                Mask budget, facet     Feed-forward;
                                                                incoming spec
Lithography CD                           Top CD, aspect ratio   Feed-forward to
                                                                a-C open / trim
Product (array fraction)                 Chemistry via mask     Product-specific
                                         loading                offsets
Chamber hardware (Chapter 5, Section     Everything             Matching; chamber
5.7)                                                            offsets
Ring and electrode life                  Tilt; center rate      Life-based feed-
                                                                forward
```

---

## 13.5 The Compensation Hierarchy

```
Level   What                        Timescale        Example
──────────────────────────────────────────────────────────────────────────────
1       Hardware design and         Tool life        Electrode shape, ring
        calibration                                  design, ESC zones
2       Recipe radial tuning        Process qual     Gas split, zone
                                                     setpoints, edge settings
3       Life-based feed-forward     Per wafer,       Ring height or voltage
                                    by RF hours      vs. ring life; electrode
                                                     age offset
4       Per-wafer feed-forward      Per wafer        Main-etch time from
                                                     stack thickness; a-C open
                                                     trim from litho CD
5       Feedback                    Per lot/day      Time and edge corrections
                                                     from post-etch metrology
                                                     (Chapter 15)
```

A rule of thumb: fix problems at the lowest level that can fix them. A radial rate non-uniformity that is corrected every day by APC (level 5) but has a hardware cause (level 1) costs metrology, drifts between corrections, and differs between chambers.

---

## 13.6 Summary & Key Takeaways

1. **The mask budget is planar loss plus facet plus edge.** The reference process keeps 0.88 µm planar at center and 0.63 µm at the extreme edge, with facet margins of 0.56 µm and 0.27 µm.

2. **When the facet reaches the stack, the top CD grows.** The remaining-mask specification exists to keep the facet above the cap oxide everywhere.

3. **Mask need grows faster than depth.** Effective selectivity falls from 5.9 at 11.5 µm to about 4.9 at 18 µm, and the a-C needed rises from 2.6 to about 4.3 µm. At some point, other changes beat a thicker mask.

4. **Slit etch is a low-open-area process.** The mask makes up about 93% of what the plasma sees, so mask erosion products shape the chemistry, and products with different array fractions need their own offsets.

5. **Radial goals conflict.** Edge depth, edge bottom CD, edge mask, and edge tilt cannot all be fixed with one knob. Rank by margin and let the landing stop absorb depth spread.

6. **Compensate at the lowest level that works.** Hardware, then recipe, then life-based feed-forward, then per-wafer feed-forward, then feedback.

---

## Study Questions

1. A product uses 3.2 µm of a-C with the reference chemistry. At the extreme edge, mask loss is 1.15× the center. With k_f = 0.18, compute the remaining planar mask and the facet margin at the center and at the edge.

2. A stack grows to 14.0 µm above the source. Estimate the main-etch time and mask loss by interpolating the table in Section 13.1.5. What starting a-C thickness keeps 0.5 µm at the center, and what does the edge factor of 1.12 add?

3. A product's array fraction is 0.50 instead of 0.65. Estimate its open area. Would you expect more or less mask-derived polymer per unit of open area than in the reference product? What would you expect to happen to bottom CD if the same recipe were used?

4. The edge depth is 2% low and edge tilt is 0.20° (limit 0.25°). Edge mask facet margin is 0.25 µm. Which knob from Section 13.3.2 would you use to correct the depth, if any? Justify your choice with the margins.

5. A fab corrects a center-fast rate profile every day with an APC time offset that changes by ±2% from day to day. Explain why this is a level-5 fix for what may be a level-1 problem. What hardware checks would you make?

---

**Next Chapter:** [Chapter 14: Advanced Slits — Multi-Deck, Partial Slits, Select-Gate Cuts & Cryo](./14-advanced-slit-schemes.md)

---

**Chapter 13 Development Status:** Complete  
**Version:** 1.0
