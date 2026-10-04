# Appendix A: Stack, Mask & Landing-Layer Material Properties

Reference properties for the films a slit etch passes through, the mask that defines it, and the layers it lands on. Values are **representative ranges** for PECVD, LPCVD, and similar production films. They vary with deposition conditions and should be replaced by measured values for any specific process.

---

## A.1 Stack Dielectrics

```
Property                         SiO₂ (PECVD TEOS)     Si₃N₄ (PECVD SiH₄/NH₃)
────────────────────────────────────────────────────────────────────────────────
Density (g/cm³)                  2.15–2.25             2.5–2.8
Refractive index (633 nm)        1.45–1.47             1.85–2.05
Hydrogen (at.%)                  1–4 (Si–OH, H₂O)      12–25 (Si–H, N–H)
Young's modulus (GPa)            60–75                 150–220
Poisson's ratio                  0.17–0.20             0.22–0.27
Intrinsic stress (MPa)           −100 to −350          −200 to +400 (tunable)
CTE (10⁻⁶ /K)                    0.5–1.0               2.5–3.5
Thermal conductivity (W/m·K)     1.1–1.4               2–15 (density-dependent)
Dielectric constant              3.9–4.2               6.5–7.5
Bond energy (eV)                 Si–O ≈ 8.3            Si–N ≈ 4.6
Typical thickness in stack       20–30 nm              25–35 nm
(reference)                      (25 nm)               (30 nm)
```

### A.1.1 Effective ON-Stack Properties (Reference Pair: 25 nm SiO₂ / 30 nm Si₃N₄)

```
Property                         Value (illustrative)      Method
──────────────────────────────────────────────────────────────────────────
Pair pitch p                     55 nm
Average stress                   −82 MPa                   Thickness-weighted
                                                           (σ_ox = −300, σ_N = +100)
In-plane modulus (approx.)       ~100–120 GPa              Thickness-weighted
Average density                  ≈ 2.45 g/cm³              Thickness-weighted
Average etch rate (reference     ≈ 0.40 µm/min (0.69 open  Chapter 3 model
slit)                            field, 0.30 at A ≈ 58)
```

---

## A.2 Other Stack Layers

```
Layer                         Typical material          Thickness       Notes
────────────────────────────────────────────────────────────────────────────────────
Cap oxide                     PECVD TEOS                200–500 nm      Above top
                                                                        select gates
Inter-deck layer              Oxide (sometimes with     100–300 nm      Hole joint;
                              poly-Si plugs at holes)                   slit sees oxide
Select-gate / dummy levels    Same as pairs, sometimes  1–2× pair       Local rate and
                              thicker nitride or oxide  thickness       OES changes
Staircase fill                TEOS, HDP oxide, or       Up to full      Rate differs
                              flowable oxide (densified) stack height   from ON
                                                                        (Chapter 12)
```

### A.2.1 Staircase Fill Oxide Variants

```
Fill type               Density       Relative etch rate    Notes
                        (g/cm³)       vs ON (fluorocarbon,
                                      illustrative)
──────────────────────────────────────────────────────────────────────
PECVD TEOS              2.15–2.25     1.05–1.15             Common; may need
                                                            densification
HDP oxide               2.2–2.3       0.95–1.05             Denser; closer
                                                            to ON
Flowable / spin-on,     2.0–2.2       1.10–1.30             Fast, depends on
densified                                                   cure and anneal
```

---

## A.3 Source and Landing Layers

```
Layer                         Thickness      Role                Rate in LS-1
                              (reference)                        (µm/min, illustrative)
───────────────────────────────────────────────────────────────────────────────────────
n⁺ poly-Si (upper)            150 nm         Etch stop           0.015
SiO₂ liner                    10 nm          Second stop (LS-2b) ≈ ON rate
Sacrificial poly-Si           80 nm          Landing target      0.015 (LS-1);
                                                                 removed later
SiO₂ liner                    10 nm          Protects lower      —
                                             poly-Si
n⁺ poly-Si (lower)            200 nm         Source plate        Must not be reached
Si substrate (non-CuA)        —              Landing (arch. a)   0.01–0.03
```

### A.3.1 Polysilicon Properties

```
Property                          Value (illustrative)
──────────────────────────────────────────────────────
Density                           2.33 g/cm³
Doping (n⁺)                       10²⁰–10²¹ cm⁻³ (P or As)
Grain size                        20–100 nm
Resistivity (n⁺, annealed)        1–5 mΩ·cm
Selectivity ON : poly (LS-1)      10–30
Selectivity poly : oxide          ≥ 20 (halogen-based LS-2b)
```

---

## A.4 Hard-Mask Materials

```
Property                    Standard a-C       High-density a-C    B-doped carbon      SiON cap
──────────────────────────────────────────────────────────────────────────────────────────────────
Density (g/cm³)             1.5–1.8            1.9–2.2             2.0–2.3             2.2–2.6
Hydrogen (at.%)             15–30              5–15                5–15                —
Stress (MPa)                −100 to −500       −500 to −1500       −300 to −1200       −100 to −400
Optical k (633 nm)          0.1–0.4            0.4–0.8             0.4–0.8             low
Selectivity ON : mask       6–10               10–20               12–25               —
(open field)
Strip                       O₂ ash             O₂ ash              O₂ ash + additional  F-based etch
                                                                    clean               or with mask
Typical thickness           2–4 µm             1.5–3 µm            1.5–3 µm            30–60 nm
(reference: 3.0 µm a-C, 40 nm SiON)
```

### A.4.1 Mask Erosion Rate (Reference Conditions)

```
Open-field mask erosion rate r_m ≈ ER_open / S₀
  ER_open = 0.686 µm/min, S₀ = 10 → r_m ≈ 0.069 µm/min
Effective selectivity over the etch = S₀ × (ER_avg / ER_open)
  = 10 × 0.405 / 0.686 ≈ 5.9
Facet height ≈ 0.10–0.20 × planar mask loss
```

---

## A.5 Word-Line Fill Materials (Downstream Reference)

```
Material          Barrier / liner          Typical per-wall      Notes
                                           thickness on slit
──────────────────────────────────────────────────────────────────────────────
W (CVD/ALD)       Al₂O₃ 2–4 nm + TiN       ~28–35 nm total       Strong tensile stress;
                  2–4 nm                                         F from WF₆ precursor
Mo (ALD/CVD)      Al₂O₃ 2–4 nm; thin or    ~20–28 nm total       Lower resistivity in
                  no barrier                                     thin cavities; different
                                                                 recess chemistry
```

These set the bottom-CD requirement (Chapter 16, Section 16.1.3).

---

## A.6 Chamber and Edge-Ring Materials

```
Part                    Material          Erosion behavior               Notes
───────────────────────────────────────────────────────────────────────────────────
Upper electrode         Si (single or     Erodes under ion bombardment;  Si release scavenges
(showerhead)            poly crystal)     holes widen                    F; life ~ thousands
                                                                         of RF hours
Edge (focus) ring       Si                ~0.2 µm / RF h (illustrative)  Sets edge sheath;
                                                                         tilt (Chapter 9)
Edge ring (alt.)        CVD SiC           ~2–3× slower than Si           C release at edge
Covers, insulators      Quartz, Al₂O₃,    Quartz erodes fast in F        O release near edge
                        Y₂O₃-coated parts plasma; Y₂O₃ resists
Chamber walls / liners  Anodized Al,      Collect polymer; cleaned by    Wall state drives
                        Y₂O₃ coatings     WAC                            drift (Chapter 9)
ESC dielectric          Al₂O₃ or AlN      Wears slowly; surface          He conductance,
                        ceramic           roughness changes              clamping
```

---

## A.7 Mechanical Constants for Stress Calculations

```
Si(100) substrate:
  Biaxial modulus M_s = E/(1 − ν)         ≈ 180 GPa
  Young's modulus E (in-plane, approx.)   ≈ 130 GPa
  Poisson's ratio ν                       ≈ 0.28 (biaxial), 0.06–0.36
                                          (direction-dependent)
  Thickness (300 mm)                      775 µm
  Flexural rigidity D = E h³ / (12(1−ν²)) ≈ 5.4 N·m

Stoney:      κ = 6 σ_f h_f / (M_s h_s²)
Bow:         δ = κ r² / 2
Surface strain from film force change:
             ε ≈ 4 Δ(σ_f h_f) / (M_s h_s)
```

---

**Appendix A Version:** 1.0  
**Last Updated:** 2026-10-04
