# Chapter 16: Post-Slit Integration, Yield & Cost of Ownership

## Overview

The slit etch ends when the plasma turns off, but the slit's work has only begun. Through it, the next several modules remove the nitride, deposit the word-line metal, separate the word lines, build the source contact, and finally fill the slit. Each of these steps depends on the shape the etch left behind, and most of the yield consequences of a slit-etch problem only appear after them. Equally, the slit etch is one of the most expensive single steps in a 3D NAND flow, measured in chamber hours, consumables, and floor space.

This chapter follows the slit through its downstream customers to derive the requirements they place on the etch, maps slit-etch defects to their electrical and yield signatures, and builds a cost-of-ownership model that puts etch rate, consumables, and yield in the same units.

**Learning Objectives:**
- Derive the bottom-CD requirement from the replacement-gate fill stack
- Explain metal-recess ARDE and its yield consequences in the lower deck
- Describe the replacement-source sequence and what it needs from the slit
- Map slit-etch defects to electrical failures and yield signatures
- Estimate yield loss from edge tilt in the critical sectors
- Build a cost-of-ownership model and compare conventional and cryogenic slit etch

---

## 16.1 Replacement Gate Through the Slit

### 16.1.1 Nitride Removal

```
Hot phosphoric acid (≈ 160 °C), through the slit:
  Lateral distance from each slit: d_lat ≈ 0.90–0.94 µm (Chapter 1)
  PECVD nitride rate (illustrative): 5–8 nm/min
  Time: ≈ 0.92 µm / 6 nm/min ≈ 150 min

Selectivity to oxide must be very high (≫ 100) so that the oxide
shelves survive; dissolved silica builds up in the acid and in the
cavities and can redeposit on the shelves.
```

The etch must deliver fresh acid to every nitride level and carry silica away. Transport is slowest at the slit bottom, where the slit is narrowest and farthest from the bath. A narrow bottom leads to slower lateral etching in the lowest levels, leftover nitride near the block midline, and silica redeposition. All of these show up as high resistance or opens in the lowest word lines.

### 16.1.2 After Removal: The Fragile Stage

Once the nitride is gone, each block is a stack of thin oxide shelves held apart only by the channel holes. Chapter 11 showed that the as-etched blocks are far too stiff to lean. The shelves are not. Drying, rinsing, and handling between nitride removal and metal fill are the period of highest mechanical risk. The slit etch contributes indirectly: straight, uniform slits wet and dry evenly, while slits with large wiggle or variable width create uneven capillary loads.

### 16.1.3 Metal Fill and the Bottom-CD Requirement

Metal is deposited by ALD or CVD through the slit into every cavity. It coats the slit walls with the same thickness:

```
Fill stack on each slit wall (illustrative, tungsten):
  Blocking layer (Al₂O₃):         t_blk ≈ 3 nm
  Barrier (TiN):                  t_bar ≈ 3 nm
  Tungsten to fill a 30 nm cavity from both faces, with overburden:
                                  t_W   ≈ 25 nm
  Total per wall:                 ≈ 31 nm

The slit must stay open at the bottom after the fill, so precursors
keep reaching the lowest cavities and the recess etchant can follow:
  W_b ≥ 2 × (t_blk + t_bar + t_W) + w_open
  w_open ≈ 40 nm (illustrative minimum for transport)
  W_b ≥ 2 × 31 + 40 = 102 nm

Reference spec: W_b ≥ 130 nm → 28 nm margin
```

**This is where the bottom-CD specification comes from.** If the slit pinches below about 100 nm at the bottom, the fill closes the slit there before the deepest cavities are complete, leaving voids and blocking the recess. With molybdenum (thinner barrier, sometimes none), the fill stack per wall changes, and the bottom-CD requirement should be recalculated (Chapter 14, Section 14.4.3).

### 16.1.4 Metal Recess: Word-Line Separation

After fill, metal on the slit walls connects every word line to every other. A recess etch removes it and pulls the metal back into each cavity:

```
Target: metal removed from slit walls; recessed ~20 nm into each
cavity, uniformly from top to bottom

Recess ARDE: the etchant reaches the bottom of the narrowed slit
(≈ 68 nm wide after fill, for W_b = 130 nm) less readily than the top

  If the recess is timed for the top:  bottom under-recessed
                                       → residual metal bridges word
                                         lines in the lower deck
  If timed for the bottom:             top over-recessed
                                       → word lines lose cross-section
                                         near the slit; higher R; less
                                         gate metal at the outer holes
                                         (clearance budget, Chapter 1)
```

The wider and straighter the slit bottom, the smaller the top-to-bottom recess difference. Striation adds a level-by-level variation: word-line levels whose nitride was laterally recessed in the slit etch (Chapter 10, Section 10.4) start with metal closer to the slit and need more recess. **Lower-deck word-line shorts after recess are often a slit-etch bottom-CD problem in disguise.**

---

## 16.2 Replacement Source Through the Slit (CuA Flows)

```
Replacement-source sequence (reference stack, simplified):

  1. Slit liner: thin protective film (e.g., nitride/poly or oxide
     combination) on the slit walls to protect the ON stack
  2. Liner opening at the slit bottom (anisotropic punch at high AR)
  3. Sacrificial poly-Si removal through the slit (selective wet or
     vapor etch); the cavity extends under the whole block
  4. Removal of the channel-hole films (blocking oxide, charge trap,
     tunnel oxide) where they are now exposed at the source level,
     uncovering the poly-Si channel sidewall
  5. Doped poly-Si deposition to fill the cavity and contact the
     channel sidewall
  6. Poly-Si recess from the slit; liner removal
  7. Continue with nitride removal (Section 16.1)
```

```
What each step needs from the slit etch:
  Step 2: a flat bottom inside the sacrificial layer (Chapter 12);
          a short landing leaves the liner punch nothing to open into
  Step 3: the sacrificial layer exposed across the full slit width
  Step 4: no punch-through to the lower poly-Si; the bottom liner
          between sacrificial and lower poly-Si intact
  Step 5: bottom CD wide enough for the doped poly to reach the
          cavity without pinching off the slit first
```

A short landing defeats the whole sequence for that slit: the sacrificial layer under its blocks is never removed, the channels there are never contacted, and the blocks cannot be read.

---

## 16.3 Slit Fill

```
Fill option                     Used when                    Slit-etch implication
──────────────────────────────────────────────────────────────────────────────────────
Dielectric only (oxide)         Source is a plate under the  Slit width just needs to
                                array (CuA)                  fill without voids
Spacer + conductor (array       Source in the substrate or   Spacer bottom punch at
common source, ACS)             reached through the slit     very high AR; conductor
                                                             cross-section sets source
                                                             resistance
```

For ACS designs, the spacer narrows the slit before its bottom is opened:

```
Example: W_b = 130 nm, oxide spacer 35 nm per wall
  Opening at the bottom: 130 − 70 = 60 nm
  Aspect ratio of the spacer punch: 11.7 µm / 0.060 µm ≈ 195
```

A spacer punch at AR ≈ 200 is one of the hardest anisotropic etches in the flow. It is another reason ACS designs push for wider slit bottoms.

---

## 16.4 Defect Modes and Yield Signatures

```
Slit-etch defect                 Electrical failure                Signature
────────────────────────────────────────────────────────────────────────────────────────────
Incomplete slit / bridge          Word-line short between two       Bad blocks in adjacent
(particle, local etch stop)       adjacent blocks                   pairs; random or
                                                                    clustered (flakes)
Short landing (sacrificial not    No source contact for the         Whole blocks fail read;
exposed)                          block's strings                   regional pattern
                                                                    (e.g., staircase end,
                                                                    late-arriving radius)
Punch-through to CMOS             Source or ACS shorted to CMOS     Die fail; often near
                                  interconnect                      layout regions without
                                                                    a stop (Ch. 12.4.4)
Tilt or bow into the hole row     Gate metal thinned at outer       Outer-string failures;
                                  holes; liner/fill reaches the     wafer edge, in the two
                                  channel; WL-to-source leakage     critical sectors
Narrow bottom                     Incomplete nitride removal,       Lower-deck word lines:
                                  voids, under-recess               high R, opens, WL–WL
                                                                    shorts
Striation                         Level-dependent recess            Specific word-line
                                                                    levels leak or short
Wiggle                            Local clearance and recess        Local, along specific
                                  variation                         slits (narrow-mask
                                                                    regions)
Die-level distortion              Contact misalignment at later     Word-line contact shorts
                                  layers                            near the array/staircase
                                                                    boundary; die-position
                                                                    repeating pattern
```

### 16.4.1 Reading the Signature

The useful diagnostic question is **where** failures fall:

```
Pattern                                    Points to
──────────────────────────────────────────────────────────────────────
Edge die, at 12 and 6 o'clock (for slits   Edge tilt (Chapter 9)
running 3–9 o'clock)
Edge die, all around                       Edge mask, edge depth, or
                                           edge bottom CD (Chapter 13)
Blocks at the staircase ends of each       Landing in the staircase
plane                                      region (Chapter 12)
Lowest word lines, all die                 Bottom CD / recess ARDE
Paired bad blocks, random                  Particles, bridges (Chapter 9)
Paired bad blocks, clustered               Wall flake event
Same word-line level, all die              Striation / chemistry at that
                                           depth
```

### 16.4.2 Yield From Edge Tilt

```
Illustrative estimate:
  Die size 1 cm × 1 cm; ~650 die per wafer
  Die touching the outer 3 mm band (r = 144–147 mm):
    circumference ≈ 2π × 145.5 mm ≈ 914 mm → ~90 die
  Critical sectors: two sectors of ±30° around 12 and 6 o'clock
    → 120° / 360° = 1/3 of the band → ~30 die

If edge tilt exceeds the limit in the critical sectors (e.g., a ring
past its compensation range):
  Yield loss ≈ 30 / 650 ≈ 4.6%
```

A few percent of die is a large loss in a mature product. It is also entirely concentrated in a pattern that a correctly designed sampling plan (Chapter 15) will catch early.

---

## 16.5 Cost of Ownership

### 16.5.1 Model

```
Cost per wafer pass = depreciation + consumables + gases + power
                      + maintenance labor + metrology share

Reference conventional slit etch (illustrative):

Depreciation
  Chamber cost incl. platform share:   $4.5 M
  Depreciation period:                 5 years → $0.90 M / year
  Effective throughput:                1.22 WPH (Chapter 5)
  Wafers per year:                     1.22 × 8760 ≈ 10 700
  Depreciation per wafer:              ≈ $84

Consumables
  Edge ring ($15 k / 9 000 wafers):             $1.7
  Upper electrode ($40 k / ~5 500 wafers):      $7.3
  ESC refurbishment ($100 k / 30 000 wafers):   $3.3
  Other kit parts (confinement rings, liners):  $5.0
                                                ─────
                                                $17.3

Gases (fluorocarbons, Ar, O₂, others):          $4.0
Power (≈ 25 kWh incl. chiller and pumps,
  $0.10/kWh):                                   $2.5
Maintenance labor:                              $8.0
Metrology share:                                $6.0
──────────────────────────────────────────────────────
Total                                           ≈ $122 per wafer
```

Depreciation is about 70% of the cost. **Etch rate is the dominant cost lever**, because it sets how many chambers the fab must buy.

### 16.5.2 Sensitivities

```
Change                                      Cost per wafer (approx.)
──────────────────────────────────────────────────────────────────────
Average etch rate +10% (Chapter 5:          Depreciation −7% → −$6
cycle 37.6 → 35.0 min)
Ring life doubled (SiC or better            −$0.9
compensation)
Upper electrode life +50%                   −$2.4
Availability 90% → 93%                      Depreciation −3% → −$3
```

### 16.5.3 Conventional Versus Cryogenic

```
                                Conventional     Cryogenic (illustrative)
──────────────────────────────────────────────────────────────────────────
Main etch                       28.4 min         14.2 min (2× rate)
Wafer cycle                     37.6 min         23.4 min
Effective WPH                   1.22             1.96
Chamber cost                    $4.5 M           $5.85 M (+30%)
Depreciation per wafer          $84              $68
Consumables, gases, power,      ~$38             ~$40 (chiller power
labor, metrology                                 up; fluorocarbon down)
──────────────────────────────────────────────────────────────────────────
Total per wafer                 ≈ $122           ≈ $108
Chambers for 100k WSPM          ~114             ~71
```

Under these assumptions, cryogenic etch saves about 11% per wafer and about 40% of the chamber count and floor space. The result is sensitive to the actual rate gain and tool premium, and to any yield difference, which brings the analysis back to yield.

### 16.5.4 Yield Dominates

```
Value of 1% die yield (illustrative): a 3D NAND wafer worth $3 000–5 000
  1% yield ≈ $30–50 per wafer

Compare: the entire slit-etch cost ≈ $122 per wafer
```

**One percent of yield is worth roughly a third of the whole etch cost.** The edge-tilt loss estimated in Section 16.4.2 (4.6%) would be worth more than the entire slit etch. This is why fabs spend freely on edge control, metrology at the critical sectors, and ring-life management, and why recipe changes that save a minute of etch time are adopted only if they cost no yield.

---

## 16.6 Summary & Key Takeaways

1. **The slit's customers set its bottom CD.** Fill stacks of about 31 nm per wall plus a transport opening require about 100 nm at the bottom. The reference 130 nm specification leaves 28 nm of margin.

2. **Metal recess inherits slit ARDE.** A narrow bottom leaves metal in the lower deck and shorts word lines. Striation makes recess level-dependent.

3. **Replacement source depends on the landing.** A short landing means no source contact for the block. A punch-through can destroy the bottom liner or worse.

4. **Failure location identifies the cause.** Edge sectors indicate tilt. Staircase-end blocks indicate landing. Lowest word lines indicate bottom CD. Paired blocks indicate bridges.

5. **Depreciation dominates cost.** At about $122 per wafer, roughly 70% is chamber capital, so etch rate is the main cost lever. Cryogenic etch can cut cost by about a tenth and chamber count by about 40%.

6. **Yield outweighs cost.** One percent of yield is worth about a third of the slit-etch cost per wafer. Edge control pays for itself many times over.

---

## Study Questions

1. A molybdenum word-line process uses a 2 nm blocking layer, no barrier, and 22 nm of Mo per wall. With w_open = 40 nm, compute the minimum bottom CD. How much could the slit's taper increase before this limit is reached, for a bow CD of 230 nm at 1.5 µm and a depth of 11.7 µm?

2. After metal fill, the reference slit is 68 nm wide at the bottom and 168 nm at the bow depth. If the recess etch rate at the bottom is 70% of that at the top, and the recess is timed to achieve 20 nm at the bottom, what is the recess at the top? What are the consequences for word-line resistance and the outer channel holes?

3. An ACS design needs a 40 nm spacer per wall and a 60 nm minimum opening for the spacer punch. What bottom CD does the slit need? What is the aspect ratio of the punch at 11.7 µm depth?

4. A wafer map shows failed blocks concentrated at the two ends of each plane, at all radii. Which slit-etch problem does this suggest, and which measurement from Chapter 15 would confirm it?

5. Using the cost model, compute the cost per wafer if the chamber cost rises to $5.0 M and the average etch rate improves by 15%. Is the trade worthwhile?

6. A recipe change saves 2 minutes of etch per wafer but increases edge-tilt yield loss by 0.5% at the end of ring life, which is a quarter of the ring's life. Using the numbers in Section 16.5, estimate the net value per wafer of the change, averaged over the ring life.

---

## Closing Note

A slit is defined by one line in a layout and made by one step in the flow. It nevertheless sets how cleanly the word lines are formed, separated, and connected to the source, and its errors show up at the wafer edge, at the ends of the array, and in the lowest word lines. Mastering it means controlling the bottom as well as the top, the edge as well as the center, and what the stack does after the plasma is off as well as what the plasma does during the etch.

---

**Back to:** [README](../README.md) · [INDEX](../INDEX.md) · [Appendices](../appendices/)

---

**Chapter 16 Development Status:** Complete  
**Version:** 1.0
