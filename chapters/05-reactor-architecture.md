# Chapter 5: Reactor Architecture for Deep Slit Etch

## Overview

A slit etch runs for half an hour at ion energies of several kilovolts, with a plasma chemistry that must stay balanced across 300 mm and from the first wafer after a clean to the last wafer before maintenance. The reactor has to deliver a large, well-collimated ion flux, keep heavy fluorocarbon fragments from being broken down too far, remove tens of kilowatts of heat from the wafer, and present the same sheath to the extreme edge of the wafer as to its center.

High-aspect-ratio dielectric etch, including both channel holes and slits, is done almost entirely in **capacitively coupled plasma (CCP)** reactors with a very-high-frequency source and a high-power low-frequency bias. This chapter explains why, describes the main parts of such a reactor, and works through the power, residence-time, pumping, and throughput numbers that define a slit-etch chamber.

**Learning Objectives:**
- Explain why CCP reactors dominate HAR dielectric etch over inductively coupled designs
- Describe the roles of the VHF source and LF bias and their partial coupling
- Estimate ion energy and wafer heat load from bias power and ion current
- Compute gas residence time and required pumping speed
- Estimate chamber throughput and the chamber count a fab needs for slit etch
- List the hardware parameters that must be matched between chambers

---

## 5.1 What the Reactor Must Provide

```
Requirement                           Typical (illustrative)        Why
──────────────────────────────────────────────────────────────────────────────
Ion energy                            2–6 keV peak; mean ~1.5–4 keV  Etch rate at depth;
                                                                    ion transmission
Ion angular spread                    σ_θ ≲ 0.3°                    Bow; bottom flux
Ion flux uniformity                   ≤ ±2% to 3 mm from edge       Depth uniformity
Moderate dissociation                 Preserve CₓFᵧ fragments       Polymer, mask
                                                                    selectivity
Short gas residence                   ~5–20 ms                      Limit secondary
                                                                    dissociation
Wafer heat removal                    5–20 W/cm²                    Temperature control
                                                                    (Chapter 8)
Edge sheath control                   Tilt ≤ 0.25° at edge          Clearance (Chapter 9)
Stability over long recipes           Drift ≤ 1% over 30+ min       Landing, profile
Clean, low-particle operation         Fab spec                      No blocked slits
```

---

## 5.2 Why Capacitive Coupling

### 5.2.1 CCP Versus ICP for HAR Dielectric Etch

```
Property                      CCP (VHF + LF)                ICP + RF bias
──────────────────────────────────────────────────────────────────────────────
Plasma density                10¹⁰–10¹¹ cm⁻³                10¹¹–10¹² cm⁻³
Electron temperature          Moderate                      Higher in the source
Fluorocarbon dissociation     Moderate: CF₂, C₂F₂, C₃F₃     High: F, CF, C
                              fragments survive             dominate
Polymer quality for HAR       Good mask and sidewall        Thinner, F-richer
                              protection                    unless heavily diluted
High-voltage bias             Natural: electrode gap and    Possible but RF window,
                              area ratio suit high V        coil, and bias design
                                                            limit it
Gap                           Small (2–4 cm)                Large (8–15 cm)
Use in 3D NAND                Channel holes, slits,         Staircase trim–etch,
                              contacts                      poly and metal etch
```

The deciding factor is chemistry. HAR dielectric etch depends on a polymer film that protects the mask and the sidewall while letting ions etch the bottom. That film forms best from heavier fragments of C₄F₆ and C₄F₈. The intense electron heating in an ICP source breaks those fragments down further, toward F and small radicals. That raises the etch rate of the mask and makes the sidewall harder to protect. A CCP with a small gap and short residence time produces a gentler fragment mix.

### 5.2.2 The Two Frequencies

```
                 ┌───────────────────────────────┐
  Gas in ──────► │ upper electrode / showerhead  │ ← VHF (or grounded)
                 │  (Si, multi-zone gas)         │
                 ├───────────────────────────────┤
                 │   plasma (gap 2–4 cm)         │
                 ├───────────────────────────────┤
                 │ wafer on ESC  │ edge ring     │ ← LF bias + VHF source
                 └───────────────────────────────┘     (on the lower electrode
                         │ confinement rings │          in many designs)
                         ▼ pump               ▼

VHF source (27–100 MHz, 1–5 kW): sets plasma density and ion flux.
  At high frequency, most power goes into electron heating, and the
  sheath voltage it creates is modest.

LF bias (100 kHz–2 MHz, 5–30 kW): sets ion energy.
  At low frequency, most power goes into accelerating ions through
  a large sheath voltage.
```

The decoupling is not perfect. A high LF voltage widens the sheath and changes how the VHF power is absorbed, so raising bias power usually changes density somewhat. The VHF source also adds a small component to the ion energy. Process engineers treat the two powers as two knobs with a known interaction matrix (Appendix D).

### 5.2.3 Bias Frequency Choice

At low bias frequency, the RF period is long compared with the time an ion takes to cross the sheath. Each ion sees nearly the instantaneous sheath voltage, so the ion energy distribution is broad, spanning from near zero to nearly the peak voltage, with peaks at both ends. At higher bias frequency, ions average over many cycles and the distribution narrows around the mean. HAR tools have moved toward **lower** bias frequencies (hundreds of kHz) despite the broad distribution, because they give the highest peak energies for a given power and because the high-energy part of the distribution does most of the etching at depth. Chapter 6 covers ion energy distributions and how tailored waveforms reshape them.

---

## 5.3 Power, Ion Energy, and Heat Load

### 5.3.1 Ion Energy From Bias Power

Most of the LF bias power goes into accelerating ions through the sheath at the wafer:

```
P_ions ≈ η · P_LF ≈ I_i · ⟨V_sh⟩

where η     = fraction of bias power delivered to ions (~0.6–0.8)
      I_i   = total ion current to the wafer
      ⟨V_sh⟩ = time-averaged sheath voltage (≈ mean ion energy / e)

Reference (illustrative):
  P_LF = 15 kW, η = 0.7 → P_ions = 10.5 kW
  Ion current density J_i = 5 mA/cm² over 707 cm² → I_i = 3.5 A
  ⟨V_sh⟩ ≈ 10 500 / 3.5 = 3.0 kV  → mean ion energy ≈ 3 keV
```

Raising bias power raises ion energy roughly in proportion, as long as the ion current stays the same. Raising source power raises ion current and therefore **lowers** the ion energy at fixed bias power. That interaction matters when a recipe raises source power to increase rate and gets less energy per ion as a result.

### 5.3.2 Heat Load on the Wafer

Nearly all the power delivered to ions ends up as heat in the wafer:

```
Heat flux = P_ions / A_wafer = 10 500 W / 707 cm² ≈ 15 W/cm²

Add surface recombination and plasma radiation (illustrative +1–2 W/cm²):
  Total ≈ 16–17 W/cm²
```

That is several times the heat flux of a typical oxide etch and far above what wafer-backside helium cooling handles easily. Chapter 8 covers the chuck design that keeps the wafer within a few degrees of its setpoint under this load.

### 5.3.3 Voltage Limits

Peak sheath voltages of 5–10 kV stress every insulating part near the wafer. The chuck dielectric, the edge ring and its insulators, the RF feed, and the helium passages must all stand off these voltages without arcing. Arcing at the wafer edge or through a helium hole damages the wafer and the chuck. High-voltage bias design is as much an insulation problem as a plasma problem.

---

## 5.4 Gap, Gas Flow, and Pumping

### 5.4.1 Residence Time

```
τ = p · V / Q

where p = pressure, V = plasma volume, Q = throughput (Torr·L/s)
      Q (Torr·L/s) = flow (sccm) × 760 / 60 000

Reference:
  Electrode radius 0.17 m, gap 3 cm → V = π × 0.17² × 0.03 = 2.7 L
  p = 20 mTorr, total flow 400 sccm → Q = 400 × 0.01267 = 5.07 Torr·L/s
  τ = 0.020 × 2.7 / 5.07 = 10.7 ms
```

A residence time near 10 ms means each molecule spends only a short time in the plasma before being pumped. Fewer heavy fragments are broken down a second time. Lower flow or a larger volume increases τ and shifts the fragment mix toward smaller, more fluorine-rich species. Residence time is therefore a chemistry parameter, not only a flow parameter.

### 5.4.2 Pumping Speed

```
Required effective pumping speed at the chamber:

  S_eff = Q / p = 5.07 / 0.020 = 253 L/s

High-flow, low-pressure steps need more. At 600 sccm and 15 mTorr:
  S_eff = 7.6 / 0.015 = 507 L/s
```

The turbopump is usually rated for several thousand litres per second, but the conductance of the confinement rings and the pumping port limits what the chamber actually achieves. Confinement rings keep the plasma off the chamber walls and out of the pumping path. Their gaps also set conductance. Rings that erode or collect deposits change the pressure for a given throttle position, and so they change the process.

### 5.4.3 Gas Injection

The showerhead upper electrode distributes gas through hundreds of holes. Most HAR chambers divide the showerhead into at least two radial zones (center and edge), and some have three or more, with independent flow splits or separate gas mixtures. A separate **edge gas injection** near the edge ring can add or tune gases at the wafer edge. Gas tuning is the main way to adjust radial etch-rate and polymer profiles once the hardware is fixed (Chapter 7).

---

## 5.5 Uniformity at VHF

At 60–100 MHz, the free-space wavelength is 3–5 m, but inside the reactor the effective wavelength is reduced by the plasma and the sheath. When it approaches the electrode size, standing waves form, and power deposition becomes center-high. The edge, meanwhile, is affected by the electrode boundary. Countermeasures include:

```
Countermeasure                       Effect
──────────────────────────────────────────────────────────────────────
Shaped (lens-like) electrode         Compensates the center-high profile
Lower VHF frequency                  Longer wavelength; weaker standing
                                     wave; less dissociation control
Multi-zone or segmented feeds        Tune radial power
Magnetic or phase control (some      Reshape density
designs)
Edge-ring and edge electrode tuning  Correct the outer 10–15 mm
                                     (Chapter 9)
```

For slit etch, radial uniformity of ion flux and ion energy sets depth uniformity and the landing overetch (Chapter 13). Ion direction at the edge sets tilt (Chapter 9).

---

## 5.6 Throughput and Chamber Count

### 5.6.1 Wafer Cycle Time

```
Reference wafer cycle (single chamber, illustrative):

Step                                    Time (min)
────────────────────────────────────────────────────
Transfer in, chuck, stabilize           1.0
SiON/a-C mask open (in situ)            3.0
Main etch to source stack               28.4
Landing stage 1 (stop on poly-Si)       1.5
Landing stage 2 (breakthrough)          1.5
Dechuck, transfer out                   0.7
Waferless clean (WAC) per wafer         1.5
────────────────────────────────────────────────────
Total                                   37.6 min

Chamber throughput: 60 / 37.6 = 1.60 wafers per hour (WPH)
```

The main etch is 75% of the cycle. Any gain in average etch rate goes almost directly to throughput.

### 5.6.2 Chamber Count for a Fab

```
Fab output: 100 000 wafer starts per month (WSPM) through the slit layer
  Required: 100 000 / (30 × 24) = 139 WPH

Effective chamber output = 1.60 WPH × availability × utilization
  Availability 90%, utilization 85% → 1.22 WPH per chamber

Chambers needed = 139 / 1.22 ≈ 114 chambers
  On 6-chamber platforms: ~19 platforms for slits alone
```

These numbers are illustrative, but the scale is real. HAR dielectric etch is one of the largest tool populations in a 3D NAND fab, and slit etch is a substantial share of it. A 10% gain in average etch rate saves about 8–9 chambers in this example.

### 5.6.3 In-Situ Mask Open Versus Separate Chamber

Opening the a-C mask in the same chamber saves a transfer but adds oxygen-chemistry steps that change the wall state before the main etch. Opening it in a dedicated chamber keeps the main-etch chamber in a single chemistry regime and frees about 3 minutes per wafer, at the cost of an extra transfer and an extra chamber type. Both configurations are used.

---

## 5.7 Chamber Matching

A fab runs the same slit recipe in many chambers. They must produce the same slit, because a wafer's later steps and APC do not know which chamber etched it. The parameters that most often cause mismatch:

```
Hardware parameter                    Slit parameter affected
──────────────────────────────────────────────────────────────────────
Delivered LF power and voltage        Rate, bow, mask selectivity
(calibration at the electrode)
Electrode gap                         Density, rate, radial profile
Edge-ring height and wear state       Edge tilt, edge rate (Chapter 9)
Upper-electrode (showerhead) age      Gas distribution, rate profile;
and hole erosion                      Si release into the plasma
Confinement-ring condition            Pressure, residence time
ESC zone temperatures and He          Polymer, bow, radial CD
pressures
Chiller and wall temperatures         Wall deposition, drift
Gas MFC calibration                   Polymer balance
```

Matching starts with hardware calibration and is completed with per-chamber recipe offsets, usually a small time or power trim, maintained by APC (Chapter 15).

---

## 5.8 Summary & Key Takeaways

1. **CCP reactors dominate HAR dielectric etch.** Their moderate dissociation preserves the heavy fluorocarbon fragments that protect the mask and the sidewall.

2. **VHF sets the flux; LF sets the energy.** At 15 kW of bias and 3.5 A of ion current, the mean ion energy is about 3 keV. Raising source power at fixed bias lowers the energy per ion.

3. **Heat load is extreme.** About 15–17 W/cm² reaches the wafer, which makes the chuck a central part of the design.

4. **Residence time is a chemistry knob.** Around 10 ms keeps fragments from breaking down further. Flow, pressure, and volume all set it.

5. **The main etch dominates the cycle.** At about 1.6 WPH per chamber, a high-volume fab needs on the order of a hundred chambers for slits alone.

6. **Matching is a hardware problem first.** Delivered power, gap, edge-ring state, electrode age, and temperatures must match before recipe offsets can close the gap.

---

## Study Questions

1. A chamber runs 18 kW of LF bias with 70% delivered to ions. The ion current density is 6 mA/cm² over a 300 mm wafer. Compute the mean ion energy and the ion heat flux. If source power is raised so that J_i increases to 7 mA/cm² at the same bias power, what is the new mean ion energy?

2. For a plasma volume of 2.4 L, compute the residence time at 25 mTorr with 300 sccm total flow, and at 15 mTorr with 600 sccm. Which condition would you expect to preserve more C₄F₆ fragments, and why?

3. A recipe change raises the average main-etch rate from 0.405 to 0.45 µm/min for the 11.5 µm stack. Recompute the wafer cycle time and the chamber throughput. Using the fab model in Section 5.6.2, how many chambers are saved?

4. Explain why HAR tools have moved to lower bias frequencies even though the ion energy distribution becomes broader. What part of the distribution matters most at the bottom of a deep slit?

5. List three hardware differences that could make one chamber produce slits with more edge tilt than another chamber running the same recipe. For each, name a measurement that would detect it.

---

**Next Chapter:** [Chapter 6: Ion Energy, Bias Waveforms & Pulsing](./06-ion-energy-pulsing.md)

---

**Chapter 5 Development Status:** Complete  
**Version:** 1.0
