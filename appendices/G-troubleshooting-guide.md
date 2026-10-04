# Appendix G: Troubleshooting Guide

Symptom-driven guide for slit-etch excursions. For each symptom: likely causes ranked from most to least common, checks to separate them, and corrective actions. Chapter references point to the underlying physics.

---

## G.1 Edge Tilt Out of Specification

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Ring wear beyond the compensation       Ring RF hours vs. curve; tilt       Update edge setting;
   curve (Ch. 9.3)                         trend vs. RF hours                  recalibrate curve;
                                                                               replace ring
2. Edge APC sign or gain error             Offset history; tilt moving away    Fix sign; verify with
   (Ch. 15.5.1)                            from target after corrections       deliberate offset
3. Wafer edge not seated (bow, particle    He leak per zone; tilt correlated   Staged chucking; clean
   under wafer) (Ch. 8.4, 11.1.2)          with leak; random wafer-to-wafer    ESC; bow-class handling
4. Step-dependent mismatch (tilt only      Depth series at edge: where does    Per-step edge setting
   in the deep part) (Ch. 9.4.3)           tilt start?                         (tunable edge)
5. Wrong ring part or mis-seated ring      Part number; height gauge           Reinstall; verify
   after PM
6. Coupling-ring or insulator wear         PM history; edge rate change        Replace per schedule
```

## G.2 Bow Above Specification

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Mask facet grown (low mask              Remaining mask; facet height;       Restore ME-1 bias /
   selectivity; new a-C lot) (Ch. 10.2)    a-C density                         passivation; a-C
                                                                               incoming check
2. Polymer thinner: O₂ MFC high, wafer     MFC check; ESC temps; He pressure   Recalibrate; restore
   warmer (Ch. 8.1)
3. Wall state: incomplete WAC or new       F/Ar actinometry trend; time since  Extend WAC; re-season
   parts (Ch. 9.5)                         PM
4. Pulsing duty or bias waveform changed   Recipe audit; generator logs        Restore
5. Pressure higher (collisional sheath)    Throttle position; gauge            Pressure gauge cal;
   (Ch. 7.1)                               calibration                         confinement rings
```

## G.3 Bottom CD Too Small / Taper Too Large

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Excess bottom polymer (C₄F₆ high,       MFC; depth series: where does       ME-3 O₂ +; small NF₃;
   O₂ low, wafer cold) (Ch. 10.3)          taper start?                        ME-3 bias +
2. Top CD narrow → higher AR (litho or     CD-SEM top CD; litho lot            Feed-forward a-C trim;
   a-C open) (Ch. 3.4.3)                                                       litho correction
3. ME-3 bias delivered low                 Delivered-power calibration         RF calibration
4. Chamber or ring drift raising           Rate at depth trend; OES t₅₀ later  Address drift source
   deposition at depth
5. Nitride composition change (ox:N        Striation change; deposition        Retune CH₂F₂ ramp
   imbalance at depth) (Ch. 4.3.3)         chamber ID
```

## G.4 Short Landing (VC Anomalies, Unread Blocks)

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. LS-1 too short for arrival span         OES t₉₀ vs. LS-1 end; where are     Lengthen LS-1; fix
   (staircase or edge) (Ch. 12.2, 12.4.3)  failures? (staircase ends, edge)    arrival map terms
2. Feed-forward error: stack thicker than  Stack thickness data; f_N table     Correct feed-forward
   assumed; nitride slower
3. LS-2 breakthrough too short / slow      Remaining poly-Si on cross-section  Adjust LS-2 time
4. Local etch stop: particle, polymer      Clustered VC anomalies; defect      Particle source; wall
   flake (Ch. 9.6)                         inspection                          management
5. Slit ends / narrow segments lag         Failures at ends and gaps           Hammerhead; end OPC
   (Ch. 12.4.1)
```

## G.5 Punch-Through or Lower Poly-Si Damage

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. LS-1 selectivity low (O₂ high, poly     Poly-Si loss in early regions       Restore LS-1 chemistry
   doping change)                          (cross-section)
2. LS-1 too long (staircase-driven)        Poly-Si loss in staircase slits     Match fill etch rate;
   (Ch. 12.4.3)                                                                stop thickness
3. Microtrenched bottom corners            Bottom shape on TEM                 More polymer / less
   (Ch. 10.5.1)                                                                energy in ME-3 end
4. LS-2 overrun                            Landing position distribution       Shorten LS-2;
                                                                               consider LS-2b
5. Missing stop in layout region           Location of punch-through vs.       Layout rule fix
   (Ch. 12.4.4)                            source-plate layout
```

## G.6 Depth / Arrival Drift (OES t₅₀ Moving)

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Upper-electrode aging                   Electrode RF hours; center rate     Electrode-age APC term;
   (Ch. 9.5.3)                             trend                               replace
2. Incoming stack thickness shift          Upstream metrology                  Feed-forward
3. Bias delivery drift                     Delivered-power check               Calibrate
4. Confinement-ring deposits (pressure     Throttle position trend             Clean / replace rings
   at fixed throttle)
5. Product mix change (loading)            Product ID                          Product offsets
   (Ch. 13.2)
```

## G.7 Striation Increase

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Ox:N sidewall balance shifted (CH₂F₂,   Which film recesses? at which       Adjust CH₂F₂ / O₂
   O₂ MFC; nitride composition)            depth?                              (ramp if depth-
   (Ch. 10.4.2)                                                                dependent)
2. Wafer temperature change                ESC temps; He                       Restore
3. New nitride deposition recipe or        Deposition chamber ID               Retune; feed-forward
   chamber
```

## G.8 Wiggle in Specific Regions

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Narrow mask lines buckling              Location (partial slits, SG cuts,   Layout rule; lower-
   (Ch. 11.2.3)                            slit pairs); a-C stress             stress a-C; limit
                                                                               fluorination
2. Litho LER / a-C open roughness          Top-down LER after a-C open         a-C open passivation
3. Charging at ends and junctions          Wiggle near ends only               Pulsing; end geometry
4. Local loading at array edge             First/last slits only               Dummy slits
```

## G.9 Remaining Mask Low at the Edge

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Edge ion flux high (ring voltage        Edge rate; ring setting history     Rebalance edge; may
   raised for tilt)                                                            trade tilt vs. mask
2. Edge zone warm                          ESC edge zone temp                  Zone offset
3. a-C thinner at edge (deposition         Incoming a-C thickness map          Deposition fix
   profile)
4. Recipe lengthened (feed-forward on      Main-etch time trend                Thicker a-C; selectivity
   thick stacks)
```

## G.10 Paired Bad Blocks Increase

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Particles from walls or electrode       Defect inspection adders; time      WAC; PM; part life
   (Ch. 9.6)                               since PM; clustering
2. Bridges at slit ends / junctions        Failure location vs. layout         Layout / OPC
3. Incomplete fill or recess bridging      Failure WL level (lower deck?)      Bottom CD; recess
   (downstream, Ch. 16.1)                                                      process
```

## G.11 Overlay Signature at Later Layers After Slit

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Anisotropic magnification from stress   Wafer geometry pre/post slit;       Scanner linear terms;
   release (Ch. 11.4.1)                    overlay x vs. y mag                 feed-forward
2. Die-level array/periphery distortion    Intrafield overlay pattern          Intrafield corrections;
   (Ch. 11.4.2)                            repeating per die                   mark placement
3. Stack stress change upstream            Deposition stress monitors          Upstream fix
```

---

**Appendix G Version:** 1.0  
**Last Updated:** 2026-10-04
