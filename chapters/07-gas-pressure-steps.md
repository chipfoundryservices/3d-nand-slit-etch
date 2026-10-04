# Chapter 7: Gas Delivery, Pressure & Multi-Step Recipe Design

## Overview

No single set of conditions is right for a whole slit. Near the top, the priority is bow: the mask facet is forming, reflected ions are striking the upper wall, and the sidewall needs protection. In the middle, the priority is rate, because most of the etch time is spent there. Near the bottom, the priority is keeping the bottom open and the profile from tapering as neutrals and ions thin out. At the end, the priority is landing. A production slit recipe is therefore a sequence of steps, each tuned for one depth range, joined by transitions that must not disturb the etch.

This chapter covers the pressure and flow parameters that shape the chemistry, the architecture of a multi-step slit recipe, how steps are joined, how gas is tuned radially, and how a recipe is developed when the result of a change can only be seen after half an hour of etching.

**Learning Objectives:**
- Estimate sheath thickness and ion collisionality and relate them to pressure
- Explain how pressure trades directionality against polymer and neutral supply
- Lay out a multi-step slit recipe and state the purpose of each step
- Estimate gas-exchange and settling times at step transitions
- Use center/edge gas splits to tune radial rate and polymer
- Plan a partial-etch (depth-series) experiment to see how the profile evolves

---

## 7.1 Pressure

### 7.1.1 Sheath Thickness and Ion Collisions

At kilovolt bias, the sheath above the wafer is millimetres thick. Whether ions cross it without colliding depends on pressure:

```
Child-law sheath thickness:
  s = [ (4ε₀/9) · √(2e/M) · V^(3/2) / J_i ]^(1/2)

Reference: Ar⁺ (M = 40 amu), V = 3 kV, J_i = 5 mA/cm² (50 A/m²)
  √(2e/M) = 2.20 × 10³
  s² = 3.93 × 10⁻¹² × 2.20 × 10³ × 1.64 × 10⁵ / 50 = 2.84 × 10⁻⁵ m²
  s ≈ 5.3 mm

Ion mean free path for charge exchange (σ ≈ 5 × 10⁻¹⁵ cm²):
  λ_i = 1 / (n_g σ),  n_g = 3.2 × 10¹⁶ cm⁻³ per Torr (at ~300 K)

  p (mTorr)    n_g (cm⁻³)     λ_i (mm)    s/λ_i    exp(−s/λ_i)
  ──────────────────────────────────────────────────────────────────
  10           3.2 × 10¹⁴     6.2         0.85     0.43
  20           6.4 × 10¹⁴     3.1         1.7      0.18
  40           1.3 × 10¹⁵     1.6         3.4      0.03
```

At 20 mTorr, most ions undergo at least one charge-exchange collision in the sheath. A charge-exchange ion starts nearly at rest wherever it is created, so it arrives with less than the full sheath energy and with a wider angle. **Lower pressure gives a narrower ion energy and angle distribution.** The numbers above are illustrative. Real gas mixtures, molecular ions, and RF modulation of the sheath change the details, but the trend is robust.

### 7.1.2 What Pressure Trades

```
Lower pressure (≈10 mTorr)                 Higher pressure (≈30–40 mTorr)
──────────────────────────────────────────────────────────────────────────────
Narrower ion angle; better transmission    Wider ion angle; more bow and taper
Less polymer deposition (lower neutral     More polymer; better mask selectivity
flux; shorter residence at fixed flow)     and sidewall protection
Higher ion energy per watt (fewer          More collisions; lower mean ion
collisions)                                energy at the same power
Lower neutral flux to the bottom           Higher neutral flux; helps when
                                           neutral-limited
Harder to keep uniform at the edge         Usually more uniform
```

Slit main etches typically run at 10–30 mTorr. Many recipes use lower pressure early, for directionality while the facet forms, and higher pressure later, for neutral supply at depth. Because the slit stays ion-limited almost to the bottom (Chapter 3), the case for raising pressure late is weaker for slits than for holes.

---

## 7.2 Flow, Ratios, and Residence Time

Total flow and pressure set residence time (Chapter 5, Section 5.4.1). Gas ratios set chemistry. The two are separate knobs and should be changed separately:

```
Change                          What it does
──────────────────────────────────────────────────────────────────────
Scale all flows together        Changes residence time; dissociation
(same pressure)                 and fragment mix shift; ratios fixed
Change one gas at fixed total   Changes chemistry; residence time
                                fixed
Change pressure at fixed flow   Changes both residence time and
                                sheath collisionality
```

A common mistake is to change one gas flow without adjusting the diluent and then attribute a residence-time effect to the chemistry. In development, recipes are usually parameterized by total flow, ratios, and pressure rather than by raw flows.

---

## 7.3 Multi-Step Recipe Architecture

### 7.3.1 A Reference Recipe Outline

```
Step  Name               Depth range   Main aim              Typical changes
                         (µm)                                 (illustrative)
───────────────────────────────────────────────────────────────────────────────────
0     BARC/SiON open     cap           Pattern transfer      CF₄/CHF₃/Ar, low p
1     a-C open           mask          Vertical mask walls   O₂ + passivant, low T
2     ME-1 (top)         0 → 3         Bow control while     Lower bias (≈0.6–0.8 of
                                       facet forms           ME-2); higher C₄F₆
                                                             fraction; pulsed; lower p
3     ME-2 (body)        3 → 8         Rate                  Full bias; balanced
                                                             ox:N; continuous or
                                                             high duty
4     ME-3 (deep)        8 → 11.3      Open bottom; avoid    Higher bias; slightly more
                                       taper and stop        O₂ or small NF₃; ox:N
                                                             retuned for depth
5     LS-1 (land/stop)   11.3 → poly   Stop on poly-Si;      Less O₂; more C₄F₆;
                                       equalize the front    overetch time set by
                                                             arrival spread (Ch. 12)
6     LS-2 (break-       poly → sacr.  Open poly-Si and      F-rich breakthrough or
      through)                         liner; land in        poly-selective + oxide
                                       sacrificial layer     punch
7     Post-etch          —             Remove polymer;       O₂-based; sometimes in
      treatment                        reduce F              a separate chamber
```

The depth boundaries are set by time, using the time-to-depth curve (Chapter 3, Section 3.4.2) for the reference product. ME-1 ending at 3 µm, for example, is about 5 minutes into the etch.

### 7.3.2 Why Steps Rather Than One Recipe

Chapter 3 showed that the bottom environment changes steadily with depth: fewer neutrals, a different neutral mix, more ions lost to the wall, and more charging. Chapter 6 showed that ion energy is worth more at depth. Chapter 4 showed that the oxide/nitride balance and the bottom polymer drift with depth. A recipe that is right at one depth is wrong at another. Steps, and ramps within steps, follow that drift.

### 7.3.3 Ramping Within a Step

Modern controllers can ramp a parameter linearly through a step. Continuous ramps avoid the small profile discontinuities that discrete steps can leave on the sidewall:

```
Common ramps in slit etch:
  Bias power:      rising through ME-2 and ME-3 (Chapter 6, Section 6.5)
  O₂ flow:         rising slightly through ME-3 to keep the bottom open
  CH₂F₂ flow:      adjusted to keep ox:N ≈ 1 at the bottom (Ch. 4.3.3)
  ESC temperature: (where possible) adjusted to shift polymer (Ch. 8)
```

### 7.3.4 Step Marks on the Sidewall

An abrupt step change can leave a visible ring on the sidewall at the corresponding depth: a slight widening, narrowing, or change in striation. These **step marks** are a useful diagnostic, because they show exactly where each step began. A step mark that grows into a notch is not acceptable. It becomes a weak point for the liner and a place where metal recess behaves differently. Smoothing the transition (Section 7.4) usually removes it.

---

## 7.4 Step Transitions

### 7.4.1 Gas Exchange

When flows change, the new mixture does not reach the plasma instantly:

```
Delay components (illustrative):

  Gas line transport:     line volume / volumetric flow at line pressure
    e.g., 40 cm³ of line at ~10 Torr carrying 50 sccm:
    volumetric flow = 50 × 760/10 = 3800 cm³/min = 63 cm³/s
    delay ≈ 40 / 63 ≈ 0.6 s

  Showerhead plenum mixing:   ~0.2–1 s
  Chamber residence time:     ~0.01 s (negligible)
  Pressure settling (throttle valve):   ~0.5–2 s

Total effective transition: ~1–3 s
```

Small flows of minor gases (a few sccm of O₂ or NF₃) take longest to settle, because their line transit is slowest. A step that changes O₂ by a few sccm may take several seconds to reach its new chemistry. For a 30-minute etch this is negligible in time, but if the transition is abrupt in power and slow in gas, the wafer sees a few seconds of mismatched conditions. Those seconds can mark the sidewall.

### 7.4.2 Plasma-On Transitions

Slit recipes keep the plasma on between main-etch steps. Extinguishing and re-striking the plasma at full bias voltage risks arcing, particle release, and a burst of charging. Good transition practice:

```
- Keep source power on; change bias power with a short ramp (~1–2 s)
- Change gases first, then power, so the chemistry is ready before the
  ions arrive at the new energy
- Avoid pressure steps larger than ~30% in one transition
- Hold the matching network in a known position or use fast
  frequency tuning to avoid reflected-power spikes
```

### 7.4.3 Transition Into Landing

The transition from ME-3 to LS-1 is the most sensitive. It changes the polymer balance sharply so that poly-Si stops etching. If it happens too early, before most of the wafer has cleared the stack, the more polymerizing chemistry slows the etch through the last oxide and nitride layers and lengthens the step. If it happens too late, the early regions etch into the poly-Si at main-etch selectivity. The transition is usually timed from the product's time-to-depth curve, with APC feed-forward on stack thickness (Chapter 15), rather than triggered by endpoint.

---

## 7.5 Center/Edge Gas Tuning

### 7.5.1 Radial Profiles

Gas fed through the showerhead flows radially outward to the pump. Reactive species are consumed along the way and products build up. The edge of the wafer therefore sees a different mixture from the center. Plasma density is not uniform either (Chapter 5, Section 5.5). The result is radial variation in rate, polymer, and CD.

### 7.5.2 Tuning Knobs

```
Knob                            Typical effect (illustrative)
──────────────────────────────────────────────────────────────────────
Center:edge flow split          Shifts rate radially by a few %
(same mixture)
Separate edge mixture           Adds polymer or etchant at the edge;
(e.g., extra O₂ or C₄F₆ at      adjusts edge CD and bow
the edge)
Edge tuning gas near the ring   Fine-tunes the outer ~10 mm
```

Gas tuning adjusts **rate, CD, and bow** across the wafer. It does not fix **tilt**, which is caused by ion direction, not chemistry. Tilt is fixed with the edge sheath (Chapter 9). Confusing the two wastes development time: an edge gas change can make the edge profile look different in cross-section without moving the slit axis at all.

### 7.5.3 Interaction With Landing

Radial rate differences determine the arrival spread at the poly-Si stop, which sets the overetch needed in LS-1 (Chapter 12). A gas split that flattens the main-etch rate profile shortens LS-1 and reduces poly-Si loss at the early-arriving radius. Some recipes use a different gas split in ME-3 than in ME-2, aimed specifically at equalizing arrival at the stop.

---

## 7.6 Developing a Slit Recipe

### 7.6.1 The Problem

A full slit takes about 30 minutes to etch, and its profile can only be seen by cross-section or by advanced metrology (Chapter 15). Each experiment is expensive and slow. Moreover, a change made in ME-1 affects the profile seen at the bottom, because everything below the top is etched through the opening that ME-1 created.

### 7.6.2 Depth-Series Experiments

The standard method is to stop the etch partway, at several depths, and look at the profile at each:

```
Depth-series plan (illustrative):

  Wafer   Etch stopped after       Depth reached    Purpose
  ─────────────────────────────────────────────────────────────────
  1       ME-1 (5 min)             ~3 µm            Facet, top CD,
                                                    bow onset
  2       + 5 min of ME-2          ~5.3 µm          Bow maximum, ox:N
                                                    balance
  3       + ME-2 complete          ~8 µm            Mid-depth CD
  4       + ME-3 complete          ~11.3 µm         Bottom CD, taper
  5       Full recipe              landing          Landing, poly loss
```

Plotting CD against depth from each wafer shows how the profile evolves: where bow starts, whether it grows after ME-1, and where taper begins. A change in one step can then be judged on the wafer that ends just after that step.

### 7.6.3 Design of Experiments

```
Typical DOE practice for slit etch:
  - Screen 5–8 factors (bias, source, pressure, C₄F₆, O₂, CH₂F₂,
    ESC temperature, pulsing duty) per step with fractional designs
  - Responses: rate, ox:N, bow, top CD, bottom CD, striation, mask
    remaining, tilt at edge (separately)
  - Use partial etches so each run tests one step's effect
  - Hold upstream steps fixed while optimizing a downstream step
  - Confirm on full etches across the whole wafer, including the
    extreme edge
```

Appendix D lists starting windows and sensitivity tables, and Appendix C gives the depth-series procedure.

---

## 7.7 Summary & Key Takeaways

1. **The sheath is millimetres thick.** At 20 mTorr, most ions collide in it. Lower pressure narrows the ion energy and angle distribution, and higher pressure adds polymer and neutral supply.

2. **Change flows, ratios, and pressure separately.** Residence time and chemistry are different knobs.

3. **A slit recipe is a sequence of depth-targeted steps.** ME-1 controls bow, ME-2 delivers rate, ME-3 keeps the bottom open, LS-1 stops on poly-Si, and LS-2 lands in the sacrificial layer.

4. **Transitions must be smooth.** Minor-gas changes take seconds to arrive. Change gases before power and keep the plasma on.

5. **Gas tuning fixes rate, CD, and bow radially, not tilt.** Tilt belongs to the edge sheath.

6. **Develop with depth series.** Partial etches show how the profile evolves, so each step can be judged on its own.

---

## Study Questions

1. Compute the Child-law sheath thickness for V = 4 kV and J_i = 6 mA/cm² with Ar⁺. At 15 mTorr, what fraction of ions cross the sheath without a charge-exchange collision (σ = 5 × 10⁻¹⁵ cm²)?

2. A recipe raises O₂ from 20 to 26 sccm while keeping Ar fixed at 300 sccm. Total flow changes by how much? If the goal was only to change the chemistry, how should the Ar flow be adjusted to keep residence time constant at the same pressure?

3. A step change adds 3 sccm of NF₃ through a 30 cm³ line at 8 Torr. Estimate the line transit delay. If the bias power changes instantly at the step boundary, for how long does the wafer see the new bias with the old chemistry?

4. Using the time-to-depth values in Chapter 3, Section 3.4.2, find the step times for ME-1 (0–3 µm), ME-2 (3–8 µm), and ME-3 (8–11.3 µm). Which step contributes most to total time?

5. An edge gas change makes the extreme-edge slits look less tilted in a cross-section taken at 1 µm depth, but a full-depth cross-section shows the same bottom displacement as before. Explain what the gas change probably did and why it did not fix tilt.

6. Plan a depth series to find out whether a sidewall step mark at 3 µm comes from the ME-1/ME-2 transition. Which wafers would you run, and what would you change between them?

---

**Next Chapter:** [Chapter 8: Wafer Temperature, Cryogenic Etch & Electrostatic Chucks](./08-temperature-cryo-esc.md)

---

**Chapter 7 Development Status:** Complete  
**Version:** 1.0
