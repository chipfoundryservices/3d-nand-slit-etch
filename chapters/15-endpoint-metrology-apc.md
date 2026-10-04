# Chapter 15: Endpoint, Metrology & Advanced Process Control

## Overview

A slit etch is hard to watch. Its open area is about 7% of the wafer, and its products leave through trenches 60 times deeper than they are wide. The etch front is spread over hundreds of nanometres of depth across the wafer, so the layer-by-layer signal that works in a staircase etch disappears after the first micron. When the slit finally reaches the source stack, it does so gradually, region by region, over one to four minutes. After the etch, the most important dimensions, the bottom CD, the tilt, and the landing point, are buried 11 µm down.

This chapter covers what can be sensed during the etch, what can be measured after it, and how those measurements drive advanced process control (APC): feed-forward from upstream data, edge control from ring life and tilt measurements, feedback on profile, and fault detection that catches a bad wafer before it moves on.

**Learning Objectives:**
- Explain why optical-emission layer counting fails in deep slits and what replaces it
- Describe transition-based endpoint detection for the landing stage
- Match metrology methods to slit parameters and to the sampling locations that matter
- Use voltage-contrast inspection to find slits that did not land
- Build feed-forward and EWMA feedback controllers for main-etch time and edge tilt
- Set fault-detection rules for chucking, RF, and chemistry excursions

---

## 15.1 What the Plasma Tells Us

### 15.1.1 Signal Size

```
Optical emission from slit-bottom products (illustrative estimate):

  Open area fraction:                 ≈ 7%
  Product escape from the bottom      ≈ K_n(A) ≈ 0.07 at A = 58
  (same transmission as entry)
  Bottom rate relative to open field: ≈ 0.43

  Bottom-product signal relative to an open-field etch:
    0.07 × 0.07 × 0.43 ≈ 2 × 10⁻³

Meanwhile, mask erosion over 93% of the wafer produces CO, CN (with N),
and CₓFᵧ continuously.
```

The slit bottom contributes a fraction of a percent of the optical signal, against a large and slowly drifting background from the mask. Any endpoint must look for **changes** in that small component, not its absolute level.

### 15.1.2 Why Layer Counting Fails

In a staircase or select-gate-cut etch, the etch front is shallow and nearly flat across the wafer. The CN emission (388 nm) rises each time nitride is exposed and falls when it clears, so layers can be counted. In a slit:

```
Front spread across the wafer: ≈ 3% of depth (Chapter 2)

The modulation at the pair period survives only while the spread is
less than about half a pair pitch:
  0.03 × z < p / 2 = 27.5 nm  →  z < ~0.9 µm

Below about 1 µm (the first ~16 pairs), different regions of the wafer
are in different layers at the same moment, and the modulation averages
away.
```

**Layer counting is not available for slits after the first micron.** The main etch is therefore timed, with feed-forward correction (Section 15.4), not endpointed.

### 15.1.3 Landing Transition

At the source stack, the signal changes in one useful way: once a region reaches the poly-Si stop, it stops producing nitride and oxide products. As more regions arrive, CN and other stack-product signals decline:

```
Normalized stack-product signal during LS-1 (schematic):

  1.0 ┤──────────╮
      │           ╲            transition spread over the arrival
      │            ╲           span (1–4 min, Chapter 12)
      │             ╲
  0.0 ┤              ╰──────────
      └──────────────────────── time in LS-1
             t₁₀    t₅₀   t₉₀

  t₁₀: first regions on poly-Si
  t₉₀: nearly all regions on poly-Si
```

Practical use:

```
Use                          How
──────────────────────────────────────────────────────────────────────
Verify LS-1 completeness     Require t₉₀ (or a fitted completion
                             point) before the end of LS-1; flag the
                             wafer otherwise
Adjust LS-1 length           End LS-1 at t₉₀ + fixed margin instead of
                             a fixed time (only if the signal is robust)
Detect arrival shifts        t₅₀ trending later across wafers → rate
                             drift, thicker stacks, or a narrower CD
```

Because the bottom signal is so small, these transitions are found with multivariate methods: principal-component or partial-least-squares models over the whole spectrum, trained on wafers whose landing was checked by cross-section, rather than single-wavelength thresholds.

### 15.1.4 RF and Other Signals

```
Signal                         What it reports
──────────────────────────────────────────────────────────────────────
Bias voltage / current         Sheath impedance; shifts with chamber
harmonics                      condition and, weakly, with the landing
Helium leak rate per zone      Wafer seating; shape change as stress is
                               released (Chapter 8)
Throttle-valve position        Pumping conductance; confinement-ring
                               condition
Reflected power, arc counters  Matching problems; arcing at high voltage
ESC current                    Chucking quality; residual charge
```

---

## 15.2 Measuring the Slit

### 15.2.1 Methods

```
Method                         Measures                      Notes
──────────────────────────────────────────────────────────────────────────────────
CD-SEM (top-down)              Top CD, wiggle (centerline    Fast, in-line; top only
                               along the slit), slit-end
                               position
High-voltage SEM (HV-SEM,      Bottom CD; top-to-bottom      In-line, in-die; shows
10–30 keV landing)             offset (tilt); some profile   the bottom through the
                               information                   dielectric; calibrate
                                                             against cross-sections
CD-SAXS (transmission          Average profile of a          Non-destructive; high
small-angle X-ray scattering)  periodic slit array: CD vs    information content;
                               depth, bow, taper, tilt       slower; needs periodic
                                                             targets
IR / Mueller-matrix OCD        Profile parameters by         Fast; model-based; deep
                               model fitting                 dielectric stacks limit
                                                             sensitivity at the bottom
Cross-section SEM / TEM        Full profile, landing,        Destructive; reference
                               striation, bottom shape       for everything else
E-beam voltage contrast (VC)   Whether a slit is open to     Finds short landings and
                               the source (electrically)     bridges across a wafer
Wafer geometry (interfero-     Bow, shape, local slope;      Feed-forward to later
metric)                        predicted in-plane            lithography
                               distortion
```

### 15.2.2 Voltage Contrast for Landing

A slit that has reached the source stack is connected, through its conductive bottom, to the source plate, which is a large conductor. A slit that stopped short is isolated. Under an electron beam, isolated features charge differently from connected ones and appear with different brightness:

```
After landing (or after a conductive fill of a test structure):

  Connected (landed) slit:     discharges to the source → normal contrast
  Isolated (short) slit:       charges → anomalous contrast

Use: scan arrays for slits or slit segments with anomalous contrast;
each one is a candidate short landing or a bridge.
```

Voltage-contrast inspection finds landing failures that a cross-section would miss, because it samples every slit in the scanned area rather than one cut. It is the main in-line defense against the "looks complete, does not work" failure of Chapter 12, Section 12.6.

### 15.2.3 Where to Measure

A slit fails at its worst point. Sampling must cover the places this book has identified as worst:

```
Location                                    Why                     Chapter
──────────────────────────────────────────────────────────────────────────────
Edge, 3–5 mm in, at the two critical        Tilt perpendicular to   9
sectors (radius ⟂ slits)                    slits is largest
Edge, all around                            Mask margin, edge       13
                                            depth
Staircase region slits, near the far end    Earliest arrival;       12
                                            largest poly-Si loss
Slit ends and partial-slit gaps             Lag, recession,         12, 14
                                            bending
Array-edge slits                            Loading and charging    12, 13
                                            asymmetry
Center                                      Reference; bow at the   1, 10
                                            critical depth
```

A sampling plan that measures five points on a cross through the wafer center, along both axes, will usually miss the critical tilt sectors at the very edge, the staircase landing, and the slit ends.

---

## 15.3 Fault Detection

```
Signal                         Rule (illustrative)                   Action
──────────────────────────────────────────────────────────────────────────────────
He leak at chuck start         > limit after staged chucking          Abort before
                                                                      plasma; re-chuck
He leak during etch            Step rise > X% in < 10 s               Flag; check edge
                                                                      tilt and profile
Arc counter                    Any hard arc                           Flag; inspect
                                                                      wafer and chuck
Reflected bias power           > limit for > 2 s                      Flag; matching
OES landing transition         t₉₀ not reached before end of LS-1     Flag; VC inspect
OES main-etch fingerprint      PCA residual > limit                   Flag; chemistry or
                                                                      wall excursion
Throttle valve position        Drift > X% from chamber baseline       Check confinement
                                                                      rings, pump
Ring RF hours                  > compensation range                   Schedule ring
                                                                      change
```

Fault detection is cheap compared with metrology, and it sees every wafer. Its job is to separate wafers that need extra metrology from those that do not.

---

## 15.4 Feed-Forward Control

### 15.4.1 Main-Etch Time

```
t_ME = t_ref × (H / H_ref) × f_N × f_CD × f_chamber × f_product

where H          = measured stack thickness for this wafer (or lot)
      f_N        = nitride-composition factor (by deposition chamber)
      f_CD       = aspect-ratio factor from measured litho / a-C CD
                   (≈ 1 + 0.4 × fractional CD shortfall, Chapter 3)
      f_chamber  = chamber offset (from matching)
      f_product  = product loading offset

Example:
  t_ref = 28.4 min, H = 11.62 µm (H_ref = 11.50 µm) → × 1.0104
  CD 3% narrow → f_CD = 1.012
  Other factors = 1
  t_ME = 28.4 × 1.0104 × 1.012 = 29.04 min (+38 s)
```

Feed-forward removes wafer-to-wafer arrival variation before it reaches the stop, so the LS-1 overetch only has to absorb within-wafer and within-die spread.

### 15.4.2 Edge Settings From Ring Life

```
Edge setting (ring height or voltage) = g(ring RF hours) + feedback offset

g(): calibrated wear curve, e.g., 0.11 µm of ring wear per wafer
     (Chapter 9) → equivalent voltage or height step per N wafers
```

### 15.4.3 Downstream Feed-Forward

Slit metrology feeds later steps as well:

```
Slit data                          Used by
──────────────────────────────────────────────────────────────────────
Bottom CD                          Nitride-removal time; metal recess
                                   time (Chapter 16)
Post-slit wafer shape and          Lithography corrections for word-line
predicted distortion               contacts and bit-line contacts
                                   (Chapter 11)
Landing depth (sampled)            Replacement-source etch timing
```

---

## 15.5 Feedback Control

### 15.5.1 EWMA Controller

An exponentially weighted moving average (EWMA) controller moves the recipe offset a fraction λ of the way toward the offset that would have hit the target on the last run:

```
o*      = o_n + (y_target − y_n) / b      (offset that would have been right)
o_{n+1} = λ · o* + (1 − λ) · o_n

where y_n = measured response for run n (made with offset o_n)
      b   = process gain (response per unit of offset), with its sign
      λ   = weight, typically 0.2–0.5
```

This form is equivalent to the textbook EWMA and is easier to check by hand.

```
Example: edge tilt control with ring voltage

Gain (from Chapter 9): 2.5% of ring voltage offsets 0.1 mm of mismatch,
which is worth 0.31° at 3 mm from the edge → |b| ≈ 0.124° per %.
Convention for this chamber: raising ring voltage moves tilt inward
(negative), so b = −0.124 °/%.

Measured y_n = +0.10° (outward) with current offset o_n = +1.0%
Target y_target = 0.00°, λ = 0.3

  o*      = 1.0 + (0 − 0.10) / (−0.124) = 1.0 + 0.81 = 1.81%
  o_{n+1} = 0.3 × 1.81 + 0.7 × 1.0 = 1.24%
```

The controller adds 0.24% of ring voltage. That removes about 0.03° of the 0.10° error on the next run and the rest over the following runs, while filtering measurement noise. **The most common error in such loops is the sign of the gain.** Getting it wrong drives the tilt away from target at a rate set by λ. Every new loop should be checked with a deliberate small offset before it is closed.

### 15.5.2 Feedback Loops in a Slit Module

```
Loop                  Measured           Adjusted               Rate
──────────────────────────────────────────────────────────────────────────────
Top CD                CD-SEM after etch  a-C open trim time     Per lot
Edge tilt             HV-SEM at critical Ring voltage / height  Per lot or
                      sectors                                   per day
Bottom CD             HV-SEM / SAXS      ME-3 O₂ or bias offset Daily–weekly
                                                                (slow loop)
Bow                   SAXS / X-section   ME-1 bias offset       Weekly (slow;
                                                                small gain)
Landing               VC; sampled X-sec  LS-1 / LS-2 time       Per lot
Depth arrival         OES t₅₀ trend      Main-etch time         Per wafer
                                         (virtual metrology)
```

Profile loops (bow, bottom CD) run slowly, because their measurements are slow and their gains interact (Chapter 10, Section 10.6). Fast loops are reserved for parameters with single, well-understood knobs: top CD, tilt, and time.

### 15.5.3 Virtual Metrology

Physical metrology samples a few wafers. Virtual metrology predicts slit parameters for every wafer from data that are always available: OES fingerprints, RF signals, helium leak, ring and electrode life, upstream thickness and CD. A regression or machine-learning model trained on measured wafers predicts, for example, landing completeness or edge tilt. It is used to choose which wafers to measure and to fill gaps between measurements, not to replace measurement entirely.

---

## 15.6 Summary & Key Takeaways

1. **The slit is a small signal under a big background.** Bottom products are about 0.2% of an open-field signal, against continuous mask-erosion emission.

2. **Layer counting stops after about 1 µm.** Front spread across the wafer exceeds half a pair pitch, so the main etch is timed with feed-forward correction.

3. **Landing appears as a transition.** Stack-product emission declines as regions reach the poly-Si stop. Its completion verifies LS-1, and its timing tracks drift.

4. **Measure where slits fail.** HV-SEM and CD-SAXS see the bottom and the tilt. Voltage contrast finds unlanded slits. Sampling must cover the critical edge sectors, staircase slits, and slit ends.

5. **Feed-forward removes wafer-to-wafer spread.** Stack thickness, nitride composition, CD, chamber, and product factors set the main-etch time for each wafer.

6. **Feedback is fast for simple knobs and slow for profile.** EWMA loops on tilt, top CD, and time run often. Bow and bottom-CD loops run slowly. Always check the sign of the gain.

---

## Study Questions

1. Estimate the depth at which OES layer modulation disappears for a stack with 50 nm pair pitch and 2% front spread. How many pairs can be counted?

2. A wafer's measured stack thickness is 11.38 µm, its nitride came from a deposition chamber with f_N = 0.985, and its slit CD is 2% wide. Compute the feed-forward main-etch time, starting from t_ref = 28.4 min.

3. The OES landing transition on a series of wafers shows t₅₀ moving 6 s later per day, while t₉₀ − t₁₀ stays constant. What does this suggest, and what would you check first? What if t₉₀ − t₁₀ were growing instead?

4. Edge tilt gain is −0.12° per % of ring voltage. Measured tilt is −0.06° (inward) with an offset of +1.5%. Using the "fraction toward the right offset" form of EWMA with λ = 0.4, compute the next offset.

5. Design a metrology sampling plan of no more than 13 sites per wafer for post-slit HV-SEM that covers tilt, edge mask, staircase landing, and slit ends. Justify each site.

6. Explain why a slit can pass CD-SEM, HV-SEM, and a cross-section and still fail voltage-contrast inspection. What would the failure most likely be?

---

**Next Chapter:** [Chapter 16: Post-Slit Integration, Yield & Cost of Ownership](./16-integration-yield-coo.md)

---

**Chapter 15 Development Status:** Complete  
**Version:** 1.0
