# Appendix C: Standard Operating Procedures

Representative procedures for developing, qualifying, and maintaining a slit-etch process. They are templates: adapt the limits, sample sizes, and tools to the fab's own specifications and equipment.

---

## C.1 Depth-Series Profile Development

**Purpose:** See how the slit profile evolves through the recipe, so each step can be judged on its own (Chapter 7, Section 7.6.2).

```
Prerequisites
  - Product or short-loop wafers with the full stack and a-C mask
  - Time-to-depth curve for the current recipe (Chapter 3, Section 3.4.2)

Procedure
  1. Choose stop points at the end of each step and at least one point
     inside the longest step (reference: after ME-1, mid ME-2, end ME-2,
     end ME-3, full recipe).
  2. Run one wafer per stop point in the same chamber, consecutively,
     with standard WAC between wafers.
  3. Strip the remaining mask on half of each wafer (ash) and keep the
     other half with mask, so facet and remaining mask can be measured.
  4. Cross-section (or SAXS on a periodic array) at: center; mid-radius;
     3 mm from the edge at a critical tilt sector; 3 mm from the edge at a
     non-critical sector; one staircase slit near its far end.
  5. Measure at each site: depth; CD at 0.1 µm intervals for the top 3 µm
     and 0.5 µm intervals below; remaining mask; facet height; striation
     at three depths; top/bottom offset (tilt).
  6. Plot CD(z) for all stop points on one chart per site.

Interpretation
  - Bow growing after ME-1 → facet-driven; act on ME-1/ME-2 bias, mask
    selectivity, or passivation (Chapter 10)
  - Step marks at stop depths → transition problem (Chapter 7, 7.4)
  - Taper starting at a specific depth → chemistry drift with depth;
    act on ME-3
  - Tilt appearing only below a given depth → step-dependent edge
    mismatch (Chapter 9, 9.4.3)
```

---

## C.2 New-Chamber Qualification

```
1. Hardware checks
   - RF delivered-power calibration at the electrode (source and bias)
   - Electrode gap, edge-ring height, coupling-ring part numbers
   - ESC zone temperature calibration (sensor wafer)
   - He leak baseline per zone on a bare wafer
   - MFC calibration (rate-of-rise) for all gases
   - Base pressure, leak-up rate, throttle position at reference flow
2. Seasoning (C.4)
3. Blanket-film rates: SiO₂, Si₃N₄, a-C, poly-Si; within-wafer maps
4. Patterned monitors: full-recipe slit wafers (3 minimum)
   - Depth / landing (cross-section at 5 sites + staircase)
   - Top CD, bow, bottom CD, striation
   - Edge tilt at both critical sectors, 3 and 5 mm from the edge
   - Remaining mask at center and edge
   - VC inspection of a full array region
5. Matching to the reference chamber (C.8)
6. Release with chamber-specific APC offsets
```

---

## C.3 Edge-Tilt Calibration and Compensation Curve

**Purpose:** Measure tilt as a function of edge setting and ring life, to build the feed-forward curve used by edge APC (Chapter 15, Section 15.4.2).

```
Procedure
  1. With a new ring, run a full-recipe slit wafer at the nominal edge
     setting.
  2. Repeat at ±2 and ±4 steps of edge setting (ring height or voltage).
  3. Measure top-to-bottom offset by HV-SEM or cross-section at
     x = 2, 3, 5, 8 mm from the edge, at both critical sectors.
  4. Fit tilt(x, setting); extract the gain b (° per step) at x = 3 mm.
  5. Repeat steps 1–4 at roughly 25%, 50%, and 75% of expected ring life
     (or use monitor wafers run through life).
  6. Fit the setting that gives zero tilt at x = 3 mm vs. ring RF hours:
     this is the feed-forward curve g(RF hours).

Checks
  - Tilt profile shape should match exp(−x/s) roughly; strong deviation
    suggests wafer-seating or step-dependent problems
  - Gain sign verified by a deliberate offset before closing the loop
```

---

## C.4 Seasoning After Wet Clean or Part Replacement

```
1. Pump down; leak-up check; RF and ESC checks
2. Waferless conditioning plasma: main-etch chemistry, 30–60 min total
   in 5–10 min segments, with WAC between segments
3. Dummy wafers (a-C coated or patterned dummies): 5–15 wafers of the
   full recipe, with standard WAC
4. Monitor: blanket rate check, then one patterned slit wafer
5. Accept when: rate within ±1.5% of chamber baseline; top CD and
   edge tilt within control limits; OES main-etch fingerprint within
   PCA limits
```

The a-C-coated dummies matter: a slit wafer is mostly carbon mask (Chapter 13, Section 13.2.1), and seasoning on bare silicon or oxide dummies leaves the walls in a different state from production.

---

## C.5 Edge-Ring Replacement

```
1. Record ring RF hours, final edge setting, last tilt measurements
2. Vent, replace edge ring (and coupling/cover rings per PM schedule);
   verify ring seating and height with a gauge
3. Reset the edge-setting curve to the new-ring origin; reset RF hours
4. Season (C.4, shortened if only the ring was replaced)
5. Tilt verification wafer (C.3 steps 1 and 3 at nominal setting)
6. Release when edge tilt at critical sectors is within ±0.05° of target
```

---

## C.6 Staged Chucking Verification

```
1. Load a wafer of known high bow (e.g., ≥ 120 µm), representative of
   the product after staircase and fill
2. Apply chucking voltage with helium off; wait 2 s
3. Ramp helium to 50% of process pressure; record leak per zone
4. Ramp to process pressure; record leak per zone
5. Run a 5-minute plasma at main-etch power; record leak trend
6. Pass if: leak below limit at each stage; no step changes > X% during
   plasma; dechuck clean with no wafer movement
7. Repeat with a saddle-shaped post-slit wafer (for re-chucking in later
   steps or rework)
```

---

## C.7 Landing Verification

```
1. Cross-section at: wafer center; extreme edge (3 mm) at a critical
   sector; staircase slit near its far end; a slit end; a partial-slit
   gap end (if present)
2. Measure at each: bottom position relative to the sacrificial layer
   (target: inside, ≥ 20 nm from both boundaries); remaining upper
   poly-Si thickness beside the slit; any lower-liner damage; bottom
   shape (flat / rounded / microtrenched)
3. VC inspection over at least one full plane per sampled wafer;
   classify anomalous-contrast slits by location
4. Correlate VC anomalies with OES landing-transition data (t₉₀) for the
   same wafers
5. Accept when: all cross-sections in window; VC anomaly density below
   limit; no regional clustering
```

---

## C.8 Chamber Matching

```
1. Run the same 3–5 wafer monitor set (from one stack lot and one
   lithography lot) in the reference chamber and the candidate chamber
2. Compare, site by site:
     Depth / arrival (OES t₅₀)       target |Δ| ≤ 1%
     Top CD                          |Δ| ≤ 2 nm
     Bow                             |Δ| ≤ 4 nm
     Bottom CD                       |Δ| ≤ 5 nm
     Edge tilt (critical sectors)    |Δ| ≤ 0.05°
     Remaining mask                  |Δ| ≤ 0.05 µm
3. If mismatched, check hardware first (Chapter 5, Section 5.7):
   delivered power, gap, ring state, electrode age, ESC temps, MFCs
4. Only then apply chamber-specific recipe offsets (time, edge setting,
   zone offsets)
5. Re-verify after offsets; record offsets in APC
```

---

**Appendix C Version:** 1.0  
**Last Updated:** 2026-10-04
