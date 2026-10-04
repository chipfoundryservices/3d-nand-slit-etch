# Chapter 6: Ion Energy, Bias Waveforms & Pulsing

## Overview

Ions do most of the work at the bottom of a slit. They supply the energy that drives fluorocarbon chemistry into the oxide and nitride, they clear the polymer that would otherwise stop the etch, and their direction decides whether the walls stay straight. Three properties of the ion flux matter: **how much energy each ion carries**, **how that energy is distributed across the ions**, and **how the flux is timed**. A slit-etch bias system controls all three.

This chapter explains why slit etch uses kilovolt ions, how the ion energy distribution depends on the bias frequency and waveform, why tailored waveforms deliver more useful energy per watt, and how pulsing the bias or source relieves charging and builds sidewall protection. It closes with how ion energy is ramped through the etch.

**Learning Objectives:**
- Relate ion energy to etch yield, angular spread, and ion transmission at depth
- Describe the ion energy distribution produced by a low-frequency sinusoidal bias
- Compute the fraction of ions below a given energy for a sinusoidal bias
- Quantify the yield advantage of a narrow, tailored ion energy distribution
- Explain how pulsing relieves charging and adds passivation, and compute peak and average powers
- Design an ion energy ramp through the depth of a slit

---

## 6.1 Why Kilovolt Ions

### 6.1.1 Yield

Ion-enhanced etch yield in fluorocarbon plasma rises with the square root of ion energy above a threshold:

```
Y(E) = A · (√E − √E_th)

For SiO₂ in fluorocarbon plasma: E_th ≈ 20–50 eV (take 40 eV)

Relative yield (to 1 keV):
  E (eV)     √E − √E_th    Relative Y
  ─────────────────────────────────────
  500        16.0          0.63
  1000       25.3          1.00
  3000       48.4          1.91
  6000       71.1          2.81
```

Yield grows more slowly than energy. Tripling the ion energy from 1 to 3 keV roughly doubles the yield. The power cost triples, so the yield per watt drops. Kilovolt energies are used anyway because of what they do to transport.

### 6.1.2 Angular Spread and Transmission

The angular spread of ions leaving a collisionless sheath falls as the inverse square root of energy (Chapter 3, Section 3.3.1). Higher energy means straighter ions, and straighter ions reach a deep slit bottom without touching the wall:

```
σ_θ scaled from 4 × 10⁻³ rad at 3 keV, σ_θ ∝ E^(−1/2)
Slot direct transmission at A = 58: K_i ≈ 1 − 0.80 · A · σ_θ

  E (keV)    σ_θ (mrad)    K_i (A = 58)
  ──────────────────────────────────────
  1.0        6.9           0.68
  3.0        4.0           0.81
  6.0        2.8           0.87
```

### 6.1.3 Bottom Ion Term

Combining yield and transmission, the ion-limited rate at depth grows faster than yield alone:

```
ER_i(A) ∝ Γ_i · Y(E) · K_i(E, A)

From 1 keV to 3 keV at A = 58:
  Yield ratio:         1.91
  Transmission ratio:  0.81 / 0.68 = 1.19
  ER_i ratio:          1.91 × 1.19 = 2.27
```

The deeper the slit, the more the transmission factor adds to the case for high energy. This is why HAR bias power has risen with every generation of layer count.

### 6.1.4 What Energy Costs

```
Cost of high ion energy               Where it shows up
──────────────────────────────────────────────────────────────────────
Mask erosion and faceting             Mask budget, bow (Chapters 10, 13)
Heat load (Chapter 5, Section 5.3.2)  Wafer temperature, polymer
                                      (Chapter 8)
High voltage near the wafer           Arcing risk; insulator design
Edge-ring and chamber-part erosion    Ring life; tilt drift (Chapter 9)
Sputtered mask and part material      Redeposition; particles
```

Mask erosion also rises with energy, roughly in proportion to yield, so open-field selectivity changes only modestly with energy in this range. The gain from high energy comes mostly at the bottom, where transmission improves, while the costs come at the top. That asymmetry is the reason for ramping energy with depth (Section 6.5).

---

## 6.2 The Ion Energy Distribution

### 6.2.1 Low-Frequency Sinusoidal Bias

At bias frequencies of a few hundred kHz, an ion crosses the sheath in much less than one RF period. Each ion's energy is set by the sheath voltage at the moment it enters. For a sinusoidal sheath voltage:

```
V_sh(t) = V̄ · (1 + sin ωt)     (ranging from ~0 to 2V̄)

Ion energy E(t) = e · V_sh(t); ion flux roughly uniform in time

Ion energy distribution (IED):
  f(E) ∝ 1 / √(V̄² − (E/e − V̄)²)      for 0 < E < 2eV̄

  f(E)
   │█                                     █
   │█                                     █
   │ █                                   █
   │  ██                               ██
   │    ████                       ████
   │        ███████████████████████
   └──────────────────────────────────────── E
   0                 eV̄                   2eV̄
   (bimodal: most ions near the minimum and maximum)
```

### 6.2.2 How Many Ions Are Slow?

```
Fraction of ions with energy below E_c:

  P(E < E_c) = 1/2 + (1/π) · arcsin(E_c / (eV̄) − 1)

Examples:
  E_c = 0.25 eV̄:  1/2 + arcsin(−0.75)/π = 0.5 − 0.270 = 0.23
  E_c = 0.50 eV̄:  1/2 + arcsin(−0.50)/π = 0.5 − 0.167 = 0.33

For V̄ = 3 kV: a third of all ions arrive with less than 1.5 keV,
and nearly a quarter with less than 750 eV.
```

Slow ions are the ones with the widest angular spread, so they are the ones most likely to strike the upper sidewall or the mask facet. They contribute little at the bottom of a deep slit and a good deal to bow and mask erosion.

### 6.2.3 Effect of Frequency

```
Bias frequency     Regime                      IED shape
──────────────────────────────────────────────────────────────────────
100–400 kHz        Ions follow the sheath      Broad, bimodal; highest
                   instantaneously             peak energy per watt
2 MHz              Partial averaging           Narrower bimodal
13.56 MHz          Ions average many cycles    Narrow peak near the mean;
                                               lower peak energy per watt
```

Lower frequency gives the highest peak energies for a given power and voltage rating, which is why HAR systems use it. The broad distribution is the price. Tailored waveforms aim to keep the low-frequency advantage without paying that price.

---

## 6.3 Tailored Bias Waveforms

### 6.3.1 The Idea

If the sheath voltage were held at a constant high value for most of the cycle, nearly all ions would arrive at the same high energy. A sinusoid cannot do this, but a shaped voltage waveform can. A typical tailored waveform holds the wafer at a steady negative voltage for most of the period and then briefly returns it toward the plasma potential, so electrons can neutralize the charge on the wafer surface:

```
Wafer voltage (schematic)

  0 ┤   ┌┐            ┌┐            ┌┐
    │   ││            ││            ││     ← short positive excursion
    │   ││            ││            ││       (electron collection)
 −V ┤───┘└────────────┘└────────────┘└───  ← long flat negative phase
    │      (ions accelerated at nearly constant energy)
    └────────────────────────────────────── t

IED: one narrow peak near eV, instead of a broad bimodal spread
```

During the long flat phase, ions charge the wafer surface and the dielectric under it, so the surface voltage slowly drifts. Practical waveforms add a small ramp during the flat phase to compensate and keep the ion energy constant.

### 6.3.2 Yield Advantage at Equal Mean Energy

For the same mean ion energy, a narrow distribution produces more yield than a broad one, because yield grows as the square root of energy:

```
Sinusoidal IED, mean eV̄:
  ⟨√E⟩ = √(eV̄) · ⟨√(1 + sin φ)⟩ = √(eV̄) × 2√2/π = 0.900 √(eV̄)

With threshold, E_th = 40 eV, V̄ = 3 kV:
  Sinusoidal:      ⟨√E − √E_th⟩ ≈ 43.2  (ions below E_th contribute 0)
  Monoenergetic:   √3000 − √40 = 48.4
  Ratio: 48.4 / 43.2 = 1.12
```

At equal power (equal mean energy and flux), a monoenergetic distribution gives about **12% more yield**. It also removes the low-energy tail with its wide angular spread, and it reaches the same useful energy at about **half the peak voltage** of a sinusoid, which relieves insulation and arcing limits. These are the reasons tailored-waveform bias supplies have entered HAR etch.

### 6.3.3 Limits

```
Limitation                           Consequence
──────────────────────────────────────────────────────────────────────
Fast, high-voltage switching          Power-supply complexity; matching
                                     and filtering at the electrode
Surface charging during the flat      Requires ramp compensation; limits
phase (thicker dielectric = faster    flat-phase length
drift)
Interaction with VHF source           Sheath dynamics differ; recipe
                                     transfer from sinusoidal is not 1:1
```

---

## 6.4 Pulsing

### 6.4.1 Pulsing Modes

```
Mode                       What is pulsed            Typical (illustrative)
──────────────────────────────────────────────────────────────────────────────
Bias pulsing               LF bias on/off            1–10 kHz, duty 20–80%
Source pulsing             VHF on/off                1–20 kHz
Synchronized pulsing       Both, with set phase      Common in HAR tools
Multi-level pulsing        Bias switches between     High / low levels
                           high and low levels       rather than on / off
```

### 6.4.2 What Happens in Each Phase

```
On phase (bias high):
  Ions at high energy etch the bottom and remove polymer
  Bottom charges positive; upper walls charge negative

Off phase (bias off or low):
  Ion energy drops to tens of eV; little etching
  Neutral fluorocarbon flux continues → polymer deposits on the
  sidewall and the mask without ion removal (passivation)
  Electron temperature falls within ~10 µs; if the source is also
  off, the plasma decays toward an ion–ion plasma with negative ions
  Low-energy electrons and negative ions can reduce the positive
  bottom charge and the lateral field asymmetries (charge relief)
```

Pulsing turns a continuous etch into a fast alternation of etch and deposition. The off phase is a passivation step that strengthens sidewall protection and a charge-relief step that reduces bending at asymmetric features (Chapter 3, Section 3.5.3).

### 6.4.3 Peak and Average Power

```
P_avg = D · P_peak      (D = duty cycle)

Example: same average bias power as the continuous reference (15 kW)
  D = 50% → P_peak = 30 kW during the on phase

During the on phase, at the same ion current, the mean ion energy
roughly doubles (≈6 keV instead of 3 keV).
Heat load follows the average power: still ≈15 W/cm².
```

At the same average power and heat load, pulsing delivers fewer, more energetic ions. From Section 6.1.3, more energetic ions transmit better and etch more per ion at depth. The off phase adds passivation. The net effect on rate depends on whether the gain at depth outweighs the off-time:

```
Illustrative comparison at A = 58 (relative to continuous 3 keV):

                         Continuous 3 keV    50% pulsed, 6 keV on
──────────────────────────────────────────────────────────────────────
Ion energy per ion        1.00                2.00
Yield per ion             1.00                71.1 / 48.4 = 1.47
Ion transmission          0.81                0.87
Ions delivered (time-     1.00                0.50
averaged)
Bottom ion term           1.00                0.50 × 1.47 × 0.87/0.81
                                              = 0.79
```

At equal average power, pulsing lowers the ion term at the bottom in this example. It is used for profile and charging control, not for rate. Recipes often reserve heavy pulsing for the stages where bow and bending form, and run continuous or high-duty conditions where rate matters most (Chapter 7).

### 6.4.4 Choosing Off Time

```
Off time            Effect
──────────────────────────────────────────────────────────────────────
< 10 µs             Electrons still hot; little charge relief; mainly
                    a deposition pause
10–100 µs           Electron cooling; ion–ion plasma if the source is
                    also off; charge relief begins
> 100 µs            Strong passivation; risk of re-ignition transients
                    and arcing at each pulse; plasma may not restrike
                    uniformly
```

---

## 6.5 Ramping Ion Energy Through the Etch

### 6.5.1 Why Ramp

The benefits of high ion energy grow with depth, through ion transmission. The costs, mask faceting and bow, are concentrated near the top, early in the etch, when the facet forms and reflected ions strike the upper wall. A ramp spends energy where it pays.

### 6.5.2 Worked Example

Using the ARDE model of Chapter 3, let the ion-limited open-field rate ER_i0 follow the bias power, and compare a constant bias with a linear ramp:

```
Case                          ER_i0 vs depth              Time to     Time-avg
                                                          11.5 µm     ER_i0
──────────────────────────────────────────────────────────────────────────────
Constant (reference)          0.75 µm/min throughout      28.4 min    0.750
Ramp A                        0.60 → 0.90 linearly        28.5 min    0.762
Ramp B                        0.65 → 0.90 linearly        27.9 min    0.786

(ER_i0 is proportional to delivered ion power at fixed flux.)
```

Ramp A reaches the source stack in the same time as the constant recipe, with about 1.6% more time-averaged ion power, while running the top of the etch at **20% lower** ion power, where bow and facets form. Ramp B uses about 5% more power to save half a minute. In practice, the ramp is usually implemented as three to five discrete steps rather than a continuous ramp (Chapter 7).

### 6.5.3 Ramping Other Parameters With Energy

Raising ion energy at depth increases mask erosion late in the etch, when the mask is already thin. Recipes usually raise the polymerizing gas fraction a little at the same time, to keep mask erosion steady. Ion energy, O₂ flow, and C₄F₆ fraction therefore move together through the etch, not independently.

---

## 6.6 Summary & Key Takeaways

1. **High energy pays at the bottom.** From 1 to 3 keV, yield roughly doubles and direct transmission at A = 58 rises from 0.68 to 0.81. The ion term at depth rises 2.3-fold.

2. **Low-frequency sinusoidal bias gives a broad distribution.** A third of ions arrive with less than half the mean energy. Those ions etch little at depth and contribute to bow and mask erosion.

3. **Tailored waveforms concentrate energy.** At equal mean energy, a narrow distribution gives about 12% more yield, removes the slow tail, and reaches the same useful energy at about half the peak voltage.

4. **Pulsing alternates etching and passivation.** Off phases add sidewall polymer and relieve charging. At equal average power, pulsing reduces the bottom ion term, so it is used for profile and charging control rather than for rate.

5. **Ramp ion energy with depth.** A 0.60→0.90 ramp matches the constant-power etch time while using 20% less ion power at the top, where bow forms.

---

## Study Questions

1. Using Y(E) = A(√E − √E_th) with E_th = 40 eV and σ_θ ∝ E^(−1/2) (4 mrad at 3 keV), compute the relative bottom ion term at A = 58 for 2 keV and 4 keV, relative to 3 keV.

2. For a sinusoidal low-frequency bias with V̄ = 2.5 kV, what fraction of ions arrive with energy below 500 eV? Below 1.25 keV?

3. A tailored-waveform supply delivers a monoenergetic IED at 2.7 keV. What sinusoidal mean energy V̄ would give the same ⟨√E − √E_th⟩? Compare the peak voltages of the two cases.

4. A recipe pulses the bias at 30% duty with the same average power as a continuous 3 keV recipe. Estimate the on-phase ion energy, the yield per ion, the ion transmission at A = 58, and the relative bottom ion term. Is this stage suitable for the deep part of the etch?

5. Design a three-step ion power schedule (fractions of reference ER_i0 for depths 0–3, 3–8, and 8–11.5 µm) that keeps the top 3 µm at 80% power and reaches the source stack in no more than 28.4 minutes. Use the Chapter 3 model or reason from the ramp results in Section 6.5.2.

---

**Next Chapter:** [Chapter 7: Gas Delivery, Pressure & Multi-Step Recipe Design](./07-gas-pressure-steps.md)

---

**Chapter 6 Development Status:** Complete  
**Version:** 1.0
