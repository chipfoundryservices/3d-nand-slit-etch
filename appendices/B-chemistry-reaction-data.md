# Appendix B: Chemistry & Reaction Data

Reference data for slit-etch chemistry: feed gases, their main fragments, surface reactions, products, optical emission lines, and transport parameters. Values are **representative** and should be treated as order-of-magnitude guidance for recipe reasoning, not as measured constants for a specific tool.

---

## B.1 Feed Gases

```
Gas      MW (g/mol)  F/C    Boiling pt   GWP-100 (approx.)  Role in slit etch
───────────────────────────────────────────────────────────────────────────────────────
C₄F₆     162         1.5    6 °C         < 1                Polymer backbone; mask
                                                            selectivity
C₄F₈     200         2.0    −6 °C        ~10 000            Balanced polymer
C₅F₈     212         1.6    27 °C        < 1                Alternative to C₄F₆
CF₄      88          4.0    −128 °C      ~7 000             F-rich etchant (mask
                                                            open, breakthrough)
CHF₃     70          3.0    −82 °C       ~12 000            Polymer, mask open
CH₂F₂    52          2.0    −52 °C       ~700               H source; nitride rate
CH₃F     34          1.0    −78 °C       ~100               Strong H source
                                                            (nitride-selective use)
NF₃      71          —      −129 °C      ~16 000            F source; bottom
                                                            clean; WAC
SF₆      146         —      −64 °C       ~24 000            F source (small)
O₂       32          —      −183 °C      0                  Polymer control
Ar       40          —      −186 °C      0                  Diluent; ion source
COS      60          —      −50 °C       low                Passivating additive
HBr      81          —      −67 °C       0                  Passivation; poly-Si etch
Cl₂      71          —      −34 °C       0                  Poly-Si etch (LS-2b)

(GWP values are approximate and vary by assessment; use current
 regulatory values for emissions accounting.)
```

Low-GWP gases such as C₄F₆ and C₅F₈ are preferred for emissions, but their fragments and some byproducts (e.g., CF₄, C₂F₆ formed in the plasma) still need abatement.

---

## B.2 Main Fragments and Their Roles

```
Fragment / species      Origin                 Sticking (illustrative)   Role
──────────────────────────────────────────────────────────────────────────────────────
F                       All F-containing gases  Low on polymer (~0.01);  Etchant
                                                reacts with Si surfaces
CF₃                     CF₄, CHF₃, C₄F₈         Low                      Etchant/ion
                                                                          precursor
CF₂                     C₄F₆, C₄F₈              0.01–0.1                 Polymer
                                                                          precursor
CF                      All fluorocarbons       Higher; ion-assisted     Polymer
C₂F₂, C₃F₃, C₂F₄ etc.   C₄F₆, C₄F₈              0.1–0.5 (large           Dense polymer
                                                fragments)               on mask, top
                                                                          sidewall
H                       CH₂F₂, CHF₃, CH₃F       Low                      F scavenger
                                                                          (HF); nitride
                                                                          etch (HCN)
O                       O₂                      Moderate; consumed by    Polymer
                                                polymer and mask         removal
CₓFᵧ⁺, Ar⁺              Ionization              —                        Energy delivery
```

---

## B.3 Surface Reactions (Simplified)

```
SiO₂ (ion-enhanced, under CₓFᵧ polymer):
  SiO₂ + CₓFᵧ (polymer) + ion → SiF₄↑ + CO↑ / CO₂↑ / COF₂↑

Si₃N₄:
  Si₃N₄ + CₓFᵧ + ion → SiF₄↑ + FCN↑ / (CN)₂↑ + N₂↑
  With H:  → HCN↑, NH₃-type species; raises nitride rate

Poly-Si (under thick polymer, LS-1):
  Si + F (through polymer) → SiF₄↑   (slow: no O or N to clear polymer)

Amorphous carbon mask:
  C + O → CO↑, CO₂↑
  C + F + ion → CₓFᵧ↑ (adds polymer precursors near the top)
  C + N → CN (with N-containing gases)

Polymer removal:
  CₓFᵧ (film) + O → CO↑ / COF₂↑
  CₓFᵧ (film) + ion → sputtered fragments

Cryogenic regime (schematic, Chapter 8):
  HF(ads) + SiO₂ + ion → SiF₄↑ + H₂O
  Nitride products + HF → NH₄F / (NH₄)₂SiF₆-type surface species
  (condensed passivation that desorbs on warming)
```

---

## B.4 Product Volatility

```
Product        Boiling / sublimation point    Volatile at process conditions?
────────────────────────────────────────────────────────────────────────────────
SiF₄           −86 °C (sublimes)              Yes
CO             −191 °C                        Yes
CO₂            −78 °C (sublimes)              Yes
COF₂           −85 °C                         Yes
FCN            −46 °C                         Yes
HCN            26 °C                          Yes (at low pressure)
N₂             −196 °C                        Yes
SiBr₄          153 °C                         Marginal; redeposition risk
SiCl₄          58 °C                          Yes at low pressure
(NH₄)₂SiF₆     Sublimes ~100 °C+              No at cryogenic temperature;
                                              desorbs on warming
```

---

## B.5 Optical Emission Lines Used for Monitoring

```
Species     Wavelength (nm)      Tracks                         Use in slit etch
──────────────────────────────────────────────────────────────────────────────────
CN          388.3 (also 386–388  Nitride etching; also mask     Landing transition
            band)                with N-containing gases        (decline as regions
                                                                reach poly-Si)
CO          483.5, 519.8         Oxide etching; mask erosion    Background; mask
                                                                fingerprint
SiF         440.0, 436.8         Si-containing film etching     Weak; landing
F           703.7, 685.6         Free fluorine                  Chemistry balance;
                                                                actinometry with Ar
Ar          750.4, 811.5         Actinometer                    Normalization
O           777.4, 844.6         Free oxygen                    Polymer balance
CF₂         Band 240–320         Polymer precursor              Chemistry fingerprint
H           656.3 (Hα)           Hydrogen                       H-source balance
```

### B.5.1 Actinometry

```
Relative ground-state density of species X:
  n_X / n_Ar ∝ (I_X / I_Ar) × (constant for the line pair)

Valid when both lines are excited by direct electron impact from the
ground state with similar thresholds (e.g., F 703.7 with Ar 750.4).
Use for trends (e.g., F/Ar rising through the etch = wall release),
not absolute densities.
```

---

## B.6 Transport Data

### B.6.1 Neutral Transmission (Monte Carlo, Diffuse Re-emission, s = 0)

```
A        Hole K_n     Slot K_n     Slot/hole
──────────────────────────────────────────────
1        0.514        0.681        1.32
2        0.359        0.541        1.51
5        0.191        0.357        1.86
10       0.109        0.240        2.20
20       0.060        0.155        2.60
40       0.031        0.095        3.04
60       0.021        0.071        3.37

Fits (A ≥ 5): hole K ≈ 1/(1 + 0.75A); slot K ≈ (ln A + 0.15)/A
```

### B.6.2 With Sticking

```
          A = 10                A = 40
s         Hole     Slot         Hole       Slot
────────────────────────────────────────────────
0         0.109    0.240        0.031      0.095
0.05      0.015    0.132        < 10⁻⁴     0.016
0.2       0.004    0.073        < 10⁻³     0.015

Line-of-sight limit: slot ≈ 1/(2A), hole ≈ 1/(4A²)
```

### B.6.3 Thermal Speeds and Fluxes

```
Mean speed: v̄ = √(8 k_B T / (π m))

Species   m (amu)   v̄ at 400 K (m/s)
──────────────────────────────────────
H         1         2900
F         19        670
O         16        730
CF₂       50        410
C₄F₆      162       230

Flux to a surface: Γ = n v̄ / 4
```

---

## B.7 Ion-Enhanced Yield Parameters (Illustrative)

```
Y(E) = A (√E − √E_th)

Material          E_th (eV)     Relative A (fluorocarbon, ion-enhanced)
────────────────────────────────────────────────────────────────────────
SiO₂              20–50         1.0
Si₃N₄             20–50         0.9–1.1 (depends on H)
Poly-Si (under    —             ≪ 1 (polymer-limited)
thick polymer)
a-C mask          30–70         0.08–0.15 (sets S₀ ≈ 7–12)

Sputter yield at oblique incidence peaks near 60–70° from normal,
which drives mask faceting.
```

---

**Appendix B Version:** 1.0  
**Last Updated:** 2026-10-04
