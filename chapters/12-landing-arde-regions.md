# Chapter 12: Landing, Etch Stop & ARDE Across Regions

## Overview

A slit has to end in the right place. In the reference replacement-source flow, that place is an 80 nm sacrificial layer about 11.7 µm below the top of the stack. The bottom must expose that layer across the whole slit width, along every slit, at every point on the wafer. It must not break through into the polysilicon beneath, and it must never reach the interconnect of the CMOS under the array.

Chapter 2 showed that the time to reach the source stack varies by about 3% across the wafer, or roughly 345 nm of equivalent depth, from stack-thickness and etch-rate non-uniformity alone. This chapter adds the local sources of arrival spread (slit width, slit ends, junctions, and above all the staircase region), sizes the poly-Si stop and the overetch that absorbs them, designs the breakthrough into the sacrificial layer, and describes what goes wrong when a slit lands short or punches through.

**Learning Objectives:**
- Build an arrival-time map from radial, width, and regional sources
- Compute LS-1 overetch time, poly-Si loss, and the selectivity required
- Design a breakthrough step that lands inside the sacrificial layer
- Explain ARDE at slit ends and junctions and the layout remedies for each
- Compute the arrival offset of slits crossing the staircase and its effect on the stop
- Describe the failure modes of short landing and punch-through

---

## 12.1 The Landing Problem

### 12.1.1 Window Versus Spread

```
Reference source stack (Chapter 2):

  Depth below stack top     Layer                   Role
  ──────────────────────────────────────────────────────────────
  11.50 µm                  ── top of source stack
  11.50–11.65               n⁺ poly-Si (150 nm)     Etch stop (LS-1)
  11.65–11.66               SiO₂ liner (10 nm)      Second stop (LS-2b)
  11.66–11.74               Sacrificial (80 nm)     LANDING WINDOW
  11.74–11.75               SiO₂ liner (10 nm)
  11.75–11.95               n⁺ poly-Si (200 nm)     Must not be reached
                                                    in a way that removes
                                                    the bottom liner

Window for the slit bottom: inside the sacrificial layer, ideally at
its mid-depth (≈ 11.70 µm), with ≥ 20 nm to either boundary.

Arrival spread at the top of the source stack (radial only):
  ≈ 3% of 11.5 µm ≈ 345 nm equivalent, 52 s at main-etch rates
```

The spread is four times the window. The landing therefore uses the two stages introduced in Chapter 4: a selective stop to equalize the front, then a short, controlled breakthrough.

### 12.1.2 Sources of Arrival Spread

```
Source                               Sign / location              Typical size
                                                                  (illustrative)
──────────────────────────────────────────────────────────────────────────────────
Stack thickness (radial)             Thicker edge → later         ±1%
Etch rate (radial)                   Slower edge → later          ±2%
Slit width (CD variation)            Narrower → later (Ch. 3)     ~0.4% per 1% CD
Nitride composition (deposition      Wafer-to-wafer, chamber-     ±2–5%
chamber)                             to-chamber
Slit ends and junctions              Ends later; junctions        Local, ±5–15%
                                     earlier
Staircase region                     Fill-oxide-rich slits        Up to ~10%
                                     arrive earlier (Section       earlier
                                     12.4)
```

Wafer-to-wafer variation is handled by APC: feed-forward from measured stack thickness and nitride composition sets the main-etch time for each wafer (Chapter 15). Within-wafer and within-die spreads are what the stop must absorb.

---

## 12.2 Stage 1: The Poly-Si Stop

### 12.2.1 Timing the Switch

The main etch ends, and LS-1 begins, shortly before the **earliest** region reaches the poly-Si. From then on, the early regions sit on poly-Si, which etches slowly, while the late regions finish their remaining stack at the LS-1 rate.

### 12.2.2 Overetch Time

```
LS-1 rates at the slit bottom (Chapter 4, Section 4.6.1):
  Stack (ON):   R_ON   = 0.25 µm/min
  Poly-Si:      R_poly = 0.015 µm/min   → selectivity S = 16.7

Latest region's remaining stack when LS-1 starts:
  δ_late = arrival spread in depth = 345 nm (radial only)

LS-1 time to clear it: t₁ = δ_late / R_ON = 0.345 / 0.25 = 1.38 min
With 20% margin: T₁ = 1.66 min ≈ 100 s
```

The LS-1 rate for the stack is lower than the main-etch rate at the bottom (0.30 µm/min), because LS-1 is more polymerizing. The overetch must be sized with the LS-1 rate, not the main-etch rate.

### 12.2.3 Poly-Si Loss

```
Earliest region sits on poly-Si for the whole of T₁:
  Loss_max = R_poly × T₁ = 0.015 × 1.66 = 25 nm

Latest region reaches poly-Si only at the end (plus margin):
  Loss_min ≈ R_poly × (0.2 × 1.38) ≈ 4 nm

Poly-Si remaining after LS-1: 125–146 nm (of 150 nm)
Spread handed to LS-2: ≈ 21 nm
```

**The stop has converted 345 nm of arrival spread into 21 nm of thickness spread.** The conversion factor is the selectivity: 345/16.7 ≈ 21 nm.

### 12.2.4 Required Selectivity

```
General condition: the earliest region must not lose more poly-Si
than an allowed amount L_allow during the overetch:

  S_min = (1 + margin) × δ_spread / L_allow

Reference: δ_spread = 345 nm, margin 20%, L_allow = 75 nm (half the stop)
  S_min = 1.2 × 345 / 75 = 5.5

With S = 16.7, the stop is used at a third of its capacity.
```

The margin looks generous until the other spread sources are added (Section 12.5). Including the staircase region, the required selectivity roughly triples.

### 12.2.5 Corners and Microtrenches

The poly-Si loss above applies at the slit's center. Microtrenched corners (Chapter 10, Section 10.5.1) arrive earlier and lose more. Rounded bottoms do the opposite. The stop must cover the worst local point, so bottom shape adds to the spread.

---

## 12.3 Stage 2: Breakthrough Into the Sacrificial Layer

### 12.3.1 Option (a): Timed Fluorine-Rich Breakthrough

```
Target: bottom at 11.70 µm (40 nm into the 80 nm sacrificial layer)
Material to remove from the poly-Si top (after LS-1):
  remaining poly-Si 125–146 nm + liner 10 nm + 40 nm sacrificial
  ≈ 175–196 nm

LS-2a rates at the bottom (illustrative):
  poly-Si ≈ oxide ≈ 0.12 µm/min (non-selective, ion-driven)

Time: ≈ 186 nm / 0.12 = 1.55 min (to the mean target)

Variation in final position:
  Inherited from LS-1: ±10.5 nm (half of 21 nm)
  LS-2a rate non-uniformity ±5% of ~186 nm: ±9 nm
  RSS: ±14 nm

Window: 40 nm from either boundary of the sacrificial layer → ✓
```

### 12.3.2 Option (b): Selective Poly-Si Etch, Then Liner Punch

```
LS-2b-1: poly-Si etch selective to oxide (e.g., HBr- or Cl₂-assisted
          chemistry with low fluorine), stopping on the 10 nm liner
          poly:oxide selectivity ≥ 20
          Removes the 21 nm spread: liner loss ≤ 21/20 ≈ 1 nm
LS-2b-2:  short fluorocarbon punch: 10 nm liner + 40 nm sacrificial
          Variation: ±5% of 50 nm ≈ ±2.5 nm

Final position: ≈ ±3 nm about the target
```

Option (b) lands an order of magnitude more precisely, at the cost of a slower, more complex step at A ≈ 58. Halogen chemistries that etch poly-Si selectively also etch slowly at high aspect ratio, and their products are less volatile. Option (a) is adequate when the landing window is ≥ 60–80 nm and the LS-1 stop leaves a small spread. Option (b) becomes necessary as sacrificial layers thin or as the spread handed from LS-1 grows.

### 12.3.3 Lateral Attack

The breakthrough is the first step that etches poly-Si chemically, and the upper poly-Si runs sideways under the stack. A chemistry that etches poly-Si isotropically can undercut it beneath the slit walls. A small undercut is harmless. A large one weakens the source contact geometry after replacement. Breakthrough chemistries are therefore kept ion-driven, with enough polymer to protect the exposed poly-Si sidewall.

---

## 12.4 ARDE Across Regions

### 12.4.1 Slit Ends

Near its end, a slit is walled on three sides. Within about one to two slit widths of the end, the geometry looks more like a hole than a slot, and neutral and ion transmission fall (Chapter 3):

```
Slit end in plan view:

  ════════════════════════╗
  slit body (slot-like)   ║ ← end wall
  ════════════════════════╝
                    ◄─ ~1–2 W ─►  end-affected zone

Effects at depth:
  - End depth lags the body (hole-like transport): the end arrives
    late at the stop
  - The end recedes along the slit with depth (line-end shortening
    at depth) because the end wall tapers
  - Asymmetric charging bends the end region (Chapter 3, Section 3.5.3)
```

```
Remedies:
  Extend slits beyond the active region     The affected end sits in a
  into dummy area                           region where its shape does
                                            not matter
  Hammerhead ends (local widening)          Restores slot-like transport
                                            at the end
  End OPC (lithographic bias)               Compensates line-end
                                            shortening at the top
```

### 12.4.2 Junctions

Where two slits meet, or a partial slit joins a main slit, the opening is locally wider:

```
T-junction in plan view:

  ══════════════╦══════════════
                ║    ← local opening wider than W
                ║

Effects:
  - Faster transport → the junction arrives early at the stop
  - Extra poly-Si loss at the junction during LS-1
  - Wider local bottom; liner and fill behave differently there
```

Layouts avoid crossings where possible. Where a junction is required, a local CD bias (narrowing the mask at the junction) restores the nominal transport.

### 12.4.3 The Staircase Region

The slit continues through the staircase at each end of the array. There it cuts through fill oxide above the remaining ON pairs (Chapter 2, Section 2.1.3). Fill oxide and ON pairs etch at different rates in the same chemistry:

```
Arrival time through a mixed column:

  t = H_fill / ER_fill + H_ON / ER_ON

Fraction of fill oxide: φ = H_fill / H_total, with H_total ≈ 11.5 µm

Relative arrival:  t(φ) / t(0) = (1 − φ) + φ · (ER_ON / ER_fill)

Example: fill oxide etches 10% faster than ON pairs (ER_fill = 1.1 ER_ON)
  φ = 0     (array):                 1.000
  φ = 0.5   (middle of staircase):   0.5 + 0.5/1.1 = 0.955   (4.5% early)
  φ ≈ 0.98  (far end of staircase):  0.02 + 0.98/1.1 = 0.911 (8.9% early)

  8.9% of 28.4 min ≈ 2.5 min earlier than the array
```

The far end of the staircase arrives at the source stack about 2.5 minutes before the array, more than the entire radial spread. If the fill oxide etches slower than ON (dense HDP oxide in some flows), the staircase arrives late instead, and the array waits.

```
Consequence for LS-1 (fill 10% faster):
  The main etch must end when the staircase slits reach poly-Si,
  2.5 min before the array does
  The array then completes its last ~0.7 µm of stack in LS-1
    (2.5 min × 0.30 µm/min ≈ 0.75 µm of main-etch-equivalent depth)
  LS-1 time grows: (0.75 + 0.345) µm / 0.25 µm/min × 1.2 ≈ 5.3 min
  Poly-Si loss in the staircase: 0.015 × 5.3 ≈ 79 nm (of 150 nm)
```

Two problems follow. First, the staircase slits lose about half the poly-Si stop. Second, the array finishes 0.75 µm of its etch in a polymerizing chemistry that was designed for stopping, not for etching, which costs taper and bottom CD. The remedies:

```
Remedy                                    Effect
──────────────────────────────────────────────────────────────────────────
Match fill-oxide etch rate to ON (fill    Removes the offset at the
deposition and densification choice)      source; best fix
Thicker poly-Si stop under the staircase  More loss allowed there
(if the layout permits)
Higher LS-1 selectivity                   Less loss per minute of wait
Separate slit mask or etch for the        Decouples the two regions;
staircase region                          costs a mask
Accept a longer LS-1 with a ramped        Array finishes in a less
chemistry                                 polymerizing condition first
```

**For most products, the staircase region, not the wafer edge, sets the LS-1 overetch.** This is easy to miss in development if test structures sample only the array.

### 12.4.4 Under the Staircase

The landing stack under the staircase must also be checked. In some CuA designs, the source plate does not extend fully under the staircase, or the layers there differ. A slit that crosses a region without the poly-Si stop will keep etching through LS-1 and can reach the oxide over the CMOS interconnect. Design rules must guarantee that every slit segment lands on a stop layer, or that segments outside the stop are terminated before the stack ends.

### 12.4.5 Array-Edge Slits

The first and last slits in an array have a neighbor slit on one side only. On the other side is unslit stack or a large dummy region. Their local loading, polymer supply, and charging differ from slits inside the array. They can arrive at a different time and bend toward or away from the array. Dummy slits outside the last active block are the standard remedy.

---

## 12.5 Building the Arrival Map

```
Arrival offsets relative to the array body at wafer center
(illustrative, fill oxide 10% faster):

Region / condition                     Offset (% of t)    Offset (min)
──────────────────────────────────────────────────────────────────────────
Array body, center                      0                   0
Array body, extreme edge (radial)      +3.0               +0.85
Narrow slit segment (−5% CD)           +1.9               +0.54
Slit end (without hammerhead)          +5 (local)         +1.4
T-junction                             −4 (local)         −1.1
Staircase, middle                      −4.5               −1.3
Staircase, far end                     −8.9               −2.5
──────────────────────────────────────────────────────────────────────────
Total span (earliest to latest)        ~14%               ~3.9 min
```

The span sets the LS-1 overetch, and the selectivity sets the poly-Si loss:

```
Span in depth equivalent: ≈ 14% × 11.5 µm ≈ 1.6 µm
  (counted at main-etch rate; finished at LS-1 rate)

Required selectivity for 75 nm allowed loss with 20% margin:
  S_min = 1.2 × 1600 / 75 ≈ 26

Available: S = 16.7 → not enough for the full span
```

With every local effect included, the stop is overloaded. The practical response is to remove the largest terms by design: hammerhead or extended slit ends, biased junctions, and matched fill oxide. With those, the span falls back to the radial and width terms (≈ 5%), and S_min ≈ 9, well within 16.7.

---

## 12.6 Failure Modes

```
Failure                      Cause                          Consequence
────────────────────────────────────────────────────────────────────────────────────
Short landing: bottom in     Arrival late beyond LS-1;      Sacrificial layer not
poly-Si or liner             LS-2 too short; local etch     exposed → not removed
                             stop (polymer, particle)       → no source contact
                                                            for that block (open
                                                            strings)
Landing too deep: through    LS-2 too long; thin poly-Si    Bottom liner lost;
sacrificial into lower       left by LS-1 (early region);   source contact shape
poly-Si                      microtrench corners            wrong; replacement
                                                            source may etch the
                                                            lower poly-Si
Punch-through to oxide       Missing stop (layout); LS-1    ACS or source shorted
over CMOS                    far too long; staircase        to, or damaging, CMOS
                             region without stop            interconnect; often a
                                                            die killer
Non-uniform bottom           Rounded bottom, partial        Partly exposed
                             corner clearing                sacrificial layer;
                                                            slow, uneven removal
```

Short landing is the most common and the hardest to see: the slit looks complete in a top-down image and even in a cross-section that misses the affected point. It appears only after replacement source, as blocks that do not read (Chapter 16).

---

## 12.7 Summary & Key Takeaways

1. **The window is smaller than the spread.** An 80 nm landing layer must absorb a 345 nm radial arrival spread and more from local effects.

2. **The stop converts spread into thickness.** At selectivity 16.7, 345 nm of arrival spread becomes 21 nm of poly-Si thickness spread for the breakthrough.

3. **Size the overetch with LS-1 rates.** The stopping chemistry etches the remaining stack more slowly than the main etch.

4. **Breakthrough precision depends on the method.** A timed non-selective breakthrough lands within about ±14 nm. A selective poly-Si etch with a liner stop lands within about ±3 nm, at the cost of complexity.

5. **The staircase usually sets the overetch.** Slits through fill oxide can arrive minutes earlier than in the array. Matching the fill etch rate is the best fix.

6. **Design out the local terms.** Slit ends, junctions, and array-edge slits add arrival spread that the stop cannot absorb. Hammerheads, biasing, dummies, and extensions remove them.

---

## Study Questions

1. A product has a 4% radial arrival spread on a 12.5 µm stack. LS-1 rates are 0.22 µm/min for ON and 0.012 µm/min for poly-Si. Compute the LS-1 time with 20% margin, the maximum poly-Si loss, and the thickness spread handed to LS-2.

2. For the product in Question 1, the breakthrough is timed and non-selective at 0.10 µm/min with ±6% rate non-uniformity. The poly-Si stop is 150 nm, the liner 10 nm, and the sacrificial layer 60 nm. Compute the breakthrough time to reach the middle of the sacrificial layer and the final position variation. Does it fit the window?

3. In a product, the staircase fill oxide etches 15% slower than the ON pairs. Compute the relative arrival at φ = 0.5 and φ = 0.98. Which region now arrives first, and how does that change the LS-1 strategy?

4. Explain why a slit end lags the slit body at depth, using the transport results of Chapter 3. Why does a hammerhead help?

5. A failure analysis finds a die where 14 blocks in one region cannot be read after replacement source, while the slits look complete in top-down inspection. List the landing-related causes you would check, in order, and the measurement that would confirm each.

6. With the arrival map of Section 12.5, which two layout fixes reduce the span most? Recompute S_min after removing the slit-end and staircase terms.

---

**Next Chapter:** [Chapter 13: Mask Budget, Loading & Uniformity](./13-mask-budget-uniformity.md)

---

**Chapter 12 Development Status:** Complete  
**Version:** 1.0
