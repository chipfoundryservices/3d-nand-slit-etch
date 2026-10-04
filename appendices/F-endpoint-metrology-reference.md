# Appendix F: Endpoint & Metrology Reference

Quick reference for in-situ sensing, post-etch metrology, and sampling in a slit-etch module. Chapter 15 develops the methods; this appendix collects their capabilities, limits, and recommended use.

---

## F.1 In-Situ Signals

```
Signal                    Sensitivity to slit bottom    Best use
────────────────────────────────────────────────────────────────────────────────
OES, single line          Very low (≈0.2% of open-      Chamber fingerprint;
(CN 388, CO 483/520,      field signal from the         gross faults
SiF 440, F 704)           bottom)
OES, full spectrum +      Low but usable for            Landing transition
multivariate (PCA/PLS)    transitions                   (t₁₀, t₅₀, t₉₀);
                                                        virtual metrology
OES layer modulation      Lost below ~1 µm depth        Only for the first
                          (front spread > p/2)          ~16 pairs; select-gate
                                                        cuts (shallow)
RF V/I and harmonics      Weak; chamber-state           Matching, arcing,
                          sensitive                     wall-state drift
He leak per zone          Wafer seating and shape       Chucking faults; stress-
                                                        release trend
Throttle position         Conductance                   Confinement-ring and
                                                        pump health
Arc counters              Discrete events               Wafer/chuck damage
                                                        detection
```

### F.1.1 Landing-Transition Parameters

```
t₁₀   First regions reach poly-Si (10% decline in stack-product
      component)
t₅₀   Median arrival; track for drift (rate, stack thickness, CD)
t₉₀   Nearly complete; must occur before LS-1 ends
Span  t₉₀ − t₁₀; tracks within-wafer arrival spread
      Growing span → uniformity degradation (edge ring, gas, ESC)
      Shifting t₅₀ with stable span → global rate or thickness change
```

---

## F.2 Post-Etch Metrology

```
Method          Parameters                 Resolution /     Throughput   Destructive
                                           precision
                                           (illustrative)
──────────────────────────────────────────────────────────────────────────────────────────
CD-SEM          Top CD; wiggle; slit-end   ±1 nm (top CD)   High         No
                position
HV-SEM          Bottom CD; top–bottom      ±2–3 nm (bottom  Medium       No
(10–30 keV)     offset (tilt); bottom      CD); ±0.02°
                shape (qualitative)        (tilt, at 11 µm)
CD-SAXS         CD(z) profile; bow;        ±1 nm (CD);      Low–medium   No
                taper; tilt; depth         ±0.01° (tilt)
                (array average)
IR / Mueller    Depth; selected profile    Model-dependent  High         No
OCD             parameters
X-SEM           Full profile; landing;     ±2–5 nm          Low          Yes
                striation; mask
TEM / STEM      Bottom detail; liners;     < 1 nm           Very low     Yes
                landing interfaces
E-beam VC       Electrical continuity to   Detects each     Medium       No
                source (landed or not);    failing slit
                bridges                    segment
Wafer geometry  Bow, shape, local slope;   ~0.1 µm height   High         No
(interferometric) predicted distortion
Overlay (later  Distortion impact          ~1 nm            High         No
layers)
```

### F.2.1 Choosing a Method

```
Question                                         Method
──────────────────────────────────────────────────────────────────────
Is the top CD on target?                         CD-SEM
Is the bottom wide enough?                       HV-SEM; SAXS
Is the slit tilted at the edge?                  HV-SEM at critical sectors;
                                                 SAXS (array average)
Where is the bow, and how big?                   SAXS; X-SEM (depth series)
Did every slit land?                             VC (all slits in area);
                                                 X-SEM / TEM (where)
Is there striation?                              X-SEM / TEM
What did the slit do to the wafer?               Wafer geometry pre/post
```

---

## F.3 Sampling Plan (Reference)

```
Site   Location                                        Measurements
─────────────────────────────────────────────────────────────────────────────
1      Center                                          Top CD, bottom CD, bow
                                                       (SAXS), tilt
2–3    Mid-radius (two azimuths)                       Top CD, bottom CD
4–5    3 mm from edge, critical sectors (radius ⟂      Tilt, bottom CD,
       slits; e.g., 12 and 6 o'clock for slits along   remaining mask
       3–9 o'clock)
6–7    5 mm from edge, critical sectors                Tilt (profile of
                                                       tilt vs. x)
8–9    3 mm from edge, non-critical sectors (3 and 9   Edge mask, edge depth,
       o'clock)                                        bottom CD
10     Staircase slit, far end (array edge die)        Landing (VC + periodic
                                                       X-SEM), bottom CD
11     Slit end / partial-slit gap                     End position, end depth,
                                                       bending
12     Array-edge (first/last) slit                    CD, bending
13     Select-gate-cut crossing (if applicable)        Junction depth
```

VC inspection: at least one full plane per sampled wafer, plus a staircase region at each end.

---

## F.4 Control Limits (Illustrative)

```
Parameter                     Target     Control limit      Spec limit
─────────────────────────────────────────────────────────────────────────
Top CD (nm)                   200        ±4                 ±6
Bow (max CD − top CD, nm)     22         +5                 ≤ 30
Bottom CD (nm)                140        ±6                 ≥ 130
Tilt, critical sector (°)     0.00       ±0.12              ±0.25
Remaining mask, edge (µm)     0.65       −0.08              ≥ 0.5
Landing (nm into sacrificial) 40         ±15                within layer,
                                                            ≥ 20 from edges
VC anomalies (per plane)      0          > 0 → review       per bad-block
                                                            allowance
```

---

## F.5 Virtual Metrology Inputs

```
Category        Inputs
──────────────────────────────────────────────────────────────────────
Upstream        Stack thickness (measured), nitride deposition chamber,
                a-C thickness and density, litho CD
Chamber state   Ring RF hours, electrode RF hours, time since WAC/PM,
                chamber ID
In-situ         OES PCA scores per step, landing t₁₀/t₅₀/t₉₀, RF
                harmonics, He leak trend, throttle position
Outputs         Predicted depth/arrival, edge tilt, bottom CD,
                landing completeness (probability)
```

---

**Appendix F Version:** 1.0  
**Last Updated:** 2026-10-04
