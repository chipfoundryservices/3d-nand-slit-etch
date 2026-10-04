# Chapter 8: Wafer Temperature, Cryogenic Etch & Electrostatic Chucks

## Overview

Every reaction in a slit etch depends on temperature. Polymer precursors stick less and desorb more from a warm surface. Etchant species adsorb more strongly on a cold one. The mask erodes differently. And the wafer is under a heat load of about 16 W/cm², which would raise its temperature by hundreds of degrees if it were not pressed against a cooled chuck with helium behind it. The electrostatic chuck (ESC) has to remove that heat, hold the wafer flat while the stack inside it releases stress, and keep the temperature uniform across 300 mm to within a degree or two.

Temperature is also the basis of the most significant recent change in HAR etch: **cryogenic etching**, where the wafer is held well below 0 °C and the chemistry relies on adsorbed etchants instead of fluorocarbon polymer. This chapter covers temperature effects in conventional slit etch, the chuck's heat balance, chucking of bowed wafers, and the mechanisms, benefits, and demands of cryogenic slit etch.

**Learning Objectives:**
- Describe how wafer temperature affects polymer, bow, taper, and mask selectivity
- Compute the wafer temperature rise above the chuck from heat flux and thermal resistances
- Estimate the wafer's thermal time constant and how a bias ramp changes wafer temperature
- Explain why bowed and saddle-shaped wafers are hard to chuck and how staged chucking helps
- Describe the mechanisms of cryogenic HAR etch and its temperature sensitivity
- List the hardware requirements of a cryogenic slit-etch chamber

---

## 8.1 Temperature Effects in Conventional Slit Etch

### 8.1.1 Why Temperature Matters

Fluorocarbon polymer forms from precursors that stick to the surface and cross-link there. The sticking probability and residence time of those precursors fall as temperature rises. A colder wafer therefore grows thicker polymer on the mask and upper sidewall, and a warmer wafer grows thinner polymer.

```
Wafer temperature effect (conventional chemistry, illustrative
sensitivities near 20–40 °C):

Response               Colder wafer                 Sensitivity
──────────────────────────────────────────────────────────────────────
Mask selectivity       Higher (thicker mask         ~+1% per °C colder
                       polymer)
Bow                    Smaller (more sidewall       ~−0.5 nm CD per °C
                       protection)                  colder
Bottom CD / taper      Smaller bottom, more         ~−0.4 nm per °C colder
                       taper
Etch rate at depth     Slightly lower               ~−0.2% per °C colder
Striation              Can change if oxide and      Recipe-specific
                       nitride polymer differ
```

The useful conclusion is not the exact numbers but the direction: **temperature is a polymer knob with the same trade-off as O₂**. Colder protects the top and threatens the bottom. Temperature non-uniformity across the wafer therefore becomes CD, bow, and taper non-uniformity.

### 8.1.2 Radial Temperature and CD

```
Example: a wafer 3 °C warmer at the edge than at the center
  Bow at the edge:    +1.5 nm CD (less protection)
  Bottom CD at edge:  +1.2 nm
  Mask selectivity:   −3% at the edge (adds to edge mask loss, Ch. 13)
```

Each effect is small on its own, but the clearance budget in Chapter 1 has only a few nanometres of margin at the critical depth. A degree or two of edge temperature matters.

---

## 8.2 The Heat Balance

### 8.2.1 Thermal Path

```
Heat path from plasma to coolant:

  plasma → wafer (775 µm Si)
         → helium backside gap (≈5–15 µm, 10–60 Torr)
         → ESC dielectric (ceramic, ≈0.3–1 mm)
         → bond layer
         → cooled baseplate (coolant channels)

  ΔT_total = q · (R_He + R_ceramic + R_bond + R_coolant)
```

### 8.2.2 Worked Example

```
Heat flux q = 16 W/cm² (Chapter 5, Section 5.3.2)

Thermal resistances (illustrative):
  Helium gap at 40 Torr:   h_He ≈ 0.6 W/(cm²·K) → R_He = 1.67 cm²·K/W
  Ceramic (Al₂O₃, 1 mm, k = 30 W/m·K): R = 0.33 cm²·K/W
  Bond layer:              R ≈ 0.07 cm²·K/W
  Coolant film:            R ≈ 0.19 cm²·K/W
  ──────────────────────────────────────────────
  Total:                   R ≈ 2.26 cm²·K/W

Temperature rise of wafer over coolant:
  ΔT = 16 × 2.26 ≈ 36 K
    He gap:  16 × 1.67 = 27 K   (dominant)
    Ceramic: 16 × 0.33 =  5 K
    Others:  16 × 0.26 =  4 K

With coolant at −10 °C, the wafer runs at about +26 °C.
```

The helium gap is the largest resistance. Its conductance depends on helium pressure, gap size, and the surface finish of the wafer and chuck. Anything that changes any of these changes wafer temperature, and so changes polymer.

### 8.2.3 Sensitivities

```
Change                                       Wafer ΔT change (reference)
──────────────────────────────────────────────────────────────────────────
He pressure 40 → 30 Torr                     h_He 0.6 → ~0.5;
                                             ΔT_He 27 → 32 K (+5 K)
Local gap +3 µm (bow, particle, wear)        Local h_He −15–25%;
                                             +4 to +7 K locally
Bias power +10%                              +3.6 K
Coolant temperature +1 °C                    +1 K (1:1)
```

### 8.2.4 Thermal Time Constant

```
Wafer heat capacity per area:
  C = ρ · c_p · h = 2.33 g/cm³ × 0.70 J/(g·K) × 0.0775 cm
    = 0.126 J/(cm²·K)

Time constant: τ = C · R_total = 0.126 × 2.26 ≈ 0.29 s
```

The wafer reaches thermal steady state within about a second of any change in power. **Wafer temperature follows the bias power through the recipe.** A bias ramp is also a temperature ramp:

```
Ion power ramp 0.60 → 0.90 of reference (Chapter 6, Section 6.5):
  Heat flux 9.6 → 14.4 W/cm² (ion part)
  Wafer ΔT (scaling the ion part of the 36 K rise): ≈ 21 → 32 K
  The wafer warms by ~11 K from ME-1 to the end of ME-3
```

An 11 K rise, at the sensitivities in Section 8.1.1, thins the polymer late in the etch, which tends to open the bottom. This may be useful. If not, it can be offset by stepping the ESC setpoint or the helium pressure down as the bias rises. Either way, a recipe that ramps bias without accounting for temperature has a hidden second variable.

---

## 8.3 Multi-Zone Chucks

### 8.3.1 Zone Layouts

```
Layout                         Zones        Use
──────────────────────────────────────────────────────────────────────
Radial (center / mid / edge)   2–4          Radial CD, bow, mask
                                            uniformity
Radial + edge band             4–6          Extreme-edge tuning
Fine-grid (many heaters)       tens–100+    Local, non-radial
                                            compensation (e.g., a known
                                            azimuthal pattern)
```

Zone heaters sit in or under the ceramic and add heat locally against the common coolant. They can only raise temperature above the coolant baseline, so the coolant is set colder than the coldest zone needs to be.

### 8.3.2 Using Zones

Zones are the tool for **radial and azimuthal polymer and CD control**. Because the ESC temperature changes polymer everywhere along the profile, a zone offset that fixes edge bow also changes edge bottom CD and edge mask erosion. As with gas tuning (Chapter 7, Section 7.5), zones do not correct tilt.

### 8.3.3 Helium Zones

Separate helium zones (typically inner and outer) allow different backside pressures. A higher outer-zone pressure compensates the weaker contact at the edge of a bowed wafer. Helium leak rate per zone is a valuable sensor: it reports how well the wafer is seated.

---

## 8.4 Chucking Bowed and Saddle-Shaped Wafers

### 8.4.1 The Problem

Wafers reaching the slit etch have been through stack deposition, channel-hole etch, staircase etch, and fill. Their bow can be 50–150 µm, and it may not be rotationally symmetric. During the slit etch, the stack releases stress across the slits, and the wafer moves toward a saddle shape (Chapter 2, Section 2.5.4). The ESC must clamp it at the start and keep it clamped as it changes shape.

### 8.4.2 Clamping Pressure and Gaps

```
Electrostatic pressure (Coulomb chuck, simplified):

  P_e = (ε₀/2) · [ε_r V / (d + ε_r g)]²

where d = dielectric thickness above the electrode, ε_r = its
relative permittivity, g = air gap between wafer and chuck surface

At contact (g ≈ few µm): P_e ≈ 10–30 kPa (illustrative)

With a local air gap, the force falls sharply:
  d = 0.3 mm, ε_r = 9, g = 100 µm:
  ratio = [d / (d + ε_r g)]² = [0.3 / (0.3 + 0.9)]² = 1/16

  20 kPa at contact → 1.25 kPa at a 100 µm gap
```

The force needed to flatten a bowed wafer is small. Treating the wafer as a clamped plate, flattening 150 µm of bow needs only about 0.1 kPa:

```
Plate bending: P ≈ 64 · D · δ / R⁴
  D = E h³ / (12 (1 − ν²)) ≈ 130 GPa × (775 µm)³ / 11.2 ≈ 5.4 N·m
  δ = 150 µm, R = 0.15 m
  P ≈ 64 × 5.4 × 1.5 × 10⁻⁴ / 5.06 × 10⁻⁴ ≈ 100 Pa
```

The difficulty is not the flattening force but the **helium pressure**. At 40 Torr (5.3 kPa), the helium pushes up harder than a lifted edge can be pulled down (1.25 kPa at 100 µm gap). If helium is applied before the wafer is seated, it lifts the edge further, the leak rate rises, and the chuck may fault.

### 8.4.3 Staged Chucking

```
Staged chucking sequence (illustrative):

  1. Apply chucking voltage with helium off; allow ~1–2 s to seat
  2. Optionally apply a short, low-power plasma to help discharge
     and seat the wafer (some systems)
  3. Ramp helium to an intermediate pressure; check leak rate
  4. Ramp helium to the process pressure; check leak rate per zone
  5. Start the process only if leak rates are within limits
```

During the etch, the helium leak rate is monitored. A slow drift through the etch is expected as the wafer changes shape. A sudden rise indicates loss of contact, which will raise local temperature (Section 8.2.3) and is a reason to abort or flag the wafer.

### 8.4.4 Dechucking

After the etch, residual charge in the dielectric can hold the wafer. A saddle-shaped wafer can spring away unevenly when released, which risks sliding or particles. Dechuck sequences reverse the voltage, use a short plasma to neutralize charge, and lift the wafer slowly.

---

## 8.5 Cryogenic Slit Etch

### 8.5.1 What Changes at Low Temperature

In cryogenic HAR etch, the wafer is held at roughly −70 to −20 °C, and the chemistry shifts away from fluorocarbon polymer toward hydrogen- and fluorine-containing gases whose products adsorb strongly on a cold surface. The mechanisms reported in the literature include:

```
Mechanism                                     Effect
──────────────────────────────────────────────────────────────────────────
Enhanced adsorption of HF and related         More etchant on the bottom
species on cold surfaces                      surface per ion impact;
                                              higher yield
Ion-assisted reaction of an adsorbed          SiO₂ and Si₃N₄ etch faster
HF-rich layer (similar in chemistry to        than in conventional plasmas
vapor-HF oxide etch)
Condensed or adsorbed byproducts on the       Sidewall passivation that does
sidewall (e.g., ammonium fluorosilicate-      not rely on fluorocarbon
type salts from nitride etching)              polymer
Passivation that desorbs when the wafer       Less residue; easier cleanup
warms
Less fluorocarbon in the feed                 Lower greenhouse-gas
                                              emissions per wafer
```

Specific cryogenic chemistries are proprietary, and published descriptions vary. The common feature is that **temperature, rather than polymer, controls the surface coverage of reactants and passivants**.

### 8.5.2 Benefits for Slits

```
Benefit (illustrative)                  Slit consequence
──────────────────────────────────────────────────────────────────────
Average rate ~1.5–2.5× conventional     Main etch 11–19 min instead of
                                        ~28 min; fewer chambers
Higher mask selectivity reported         Thinner mask or deeper slit
                                        per mask
Less polymer at the bottom               Less taper, wider bottom CD
Reduced fluorocarbon use                 Lower emissions
```

```
Throughput example (Chapter 5 model):
  Main etch at 2× rate: 28.4 → 14.2 min
  Wafer cycle: 37.6 → 23.4 min → 2.56 WPH per chamber
  Fab model (139 WPH, 90% × 85%): 114 → 71 chambers
```

### 8.5.3 Temperature Sensitivity

Adsorption equilibria depend exponentially on temperature. If surface coverage follows a desorption energy E_d:

```
d ln θ / dT ≈ −E_d / (k_B T²)

E_d = 0.5 eV, T = 233 K (−40 °C):
  k_B T² = 8.617 × 10⁻⁵ eV/K × (233 K)² = 4.68 eV·K
  E_d / (k_B T²) = 0.5 / 4.68 = 0.107 K⁻¹

  ≈ 11% change in coverage per kelvin
```

Compared with about 1% per degree for conventional polymer effects (Section 8.1.1), this is an order of magnitude more sensitive. **Cryogenic etch turns wafer temperature uniformity from a tuning parameter into a primary specification.** Sub-degree uniformity across the wafer and wafer-to-wafer stability are required.

### 8.5.4 Hardware Demands

```
Requirement                         Why
──────────────────────────────────────────────────────────────────────
Chiller to ≈ −70 °C with high       Hold the setpoint against
capacity                            ~15 W/cm² (higher h needed)
ESC materials and bonds rated for   Thermal cycling between transfer
low temperature                     and process
Low-temperature helium cooling      Lower wafer-to-chuck ΔT so the
with high conductance               wafer stays cold under full bias
Condensation control in transfer    A cold wafer in a warmer, humid
                                    environment collects water;
                                    warm-up before exit
Wall and part temperatures          Prevent byproduct condensation
managed separately                  on chamber parts
Very tight temperature uniformity   Coverage sensitivity ~10%/K
```

Chapter 14 returns to cryogenic etch as one of the routes to slits at 300+ layers.

---

## 8.6 Summary & Key Takeaways

1. **Temperature is a polymer knob.** Colder wafers protect the mask and upper sidewall and narrow the bottom, much like lower O₂.

2. **The helium gap dominates the thermal path.** At 16 W/cm², the wafer runs about 36 K above the coolant in the reference case, 27 K of it across the helium gap.

3. **The wafer follows the bias within a second.** A bias ramp from 0.60 to 0.90 of reference warms the wafer by about 11 K through the etch. That must be either used or compensated.

4. **Helium, not bending stiffness, defeats chucking.** Bowed edges are easy to flatten but are pushed up by helium if it is applied too early. Staged chucking and helium-leak monitoring are essential.

5. **Cryogenic etch can double the rate.** It relies on adsorbed etchants and condensed passivants instead of fluorocarbon polymer, and it reduces fluorocarbon use.

6. **Cryogenic etch makes temperature a primary specification.** Coverage can change by about 10% per kelvin, so uniformity and stability requirements tighten by an order of magnitude.

---

## Study Questions

1. A chamber runs 20 W/cm² of heat flux. The helium gap conductance is 0.8 W/(cm²·K), and the other resistances total 0.6 cm²·K/W. Compute the wafer temperature rise above the coolant. What coolant temperature gives a wafer temperature of 20 °C?

2. A bowed wafer has a 6 µm larger helium gap at the outer 10 mm, reducing h_He there by 20%. Using the reference heat flux and resistances, estimate the edge temperature rise relative to the center. Using the sensitivities in Section 8.1.1, estimate the change in bow and bottom CD at the edge.

3. A recipe ramps bias from 0.70 to 1.00 of the reference ion power. Estimate the wafer temperature change through the etch. What change in ESC setpoint would hold the wafer temperature constant?

4. Using the Coulomb chuck formula with d = 0.25 mm and ε_r = 10, compute the ratio of clamping pressure at a 60 µm gap to that at contact. If the contact pressure is 25 kPa, can the chuck hold the edge against 40 Torr of helium at that gap?

5. A cryogenic process has a reactant coverage sensitivity of 10%/K. A wafer has a 0.8 K center-to-edge temperature difference. Estimate the coverage difference. If the etch rate is proportional to coverage, how much depth difference does that produce over a 14-minute main etch at 0.8 µm/min?

---

**Next Chapter:** [Chapter 9: Edge Ring, Sheath Control & Chamber Conditioning](./09-edge-sheath-conditioning.md)

---

**Chapter 8 Development Status:** Complete  
**Version:** 1.0
