# Appendix E: Slit Geometry, Transport & Budget Calculations

Collected formulas and worked calculations used throughout the book, arranged so they can be repeated with a fab's own numbers. Each section names the chapter where the method is developed.

---

## E.1 Layout Geometry (Chapter 1)

```
Aspect ratio:                A = D / W_t
Rows of holes:               width = (n − 1) · a·√3/2 + d_h
Slit pitch:                  P_s = rows width + W_t + 2s
Slit area overhead:          f_slit = (W_t + 2s) / P_s
Lateral nitride removal:     d_lat = (P_s − W_slit) / 2
Area value of clearance:     Δf = 2 Δs / P_s

Reference: a = 160 nm, d_h = 120 nm, n = 12, W_t = 200 nm, s = 80 nm
  rows width = 11 × 138.6 + 120 = 1645 nm
  P_s = 1645 + 200 + 160 ≈ 2.0 µm
  f_slit = 360 / 2000 = 18%
  d_lat ≈ 0.90 µm (top), 0.94 µm (bottom)
```

---

## E.2 Depth-Resolved Clearance Budget (Chapter 1)

### E.2.1 Formula

```
s(z) = s_nom − ΔW_slit(z)/2 − Δr_hole(z) − z·tan θ_t − δ_rand

δ_rand = √(OL² + wiggle² + deck_OL²)     (3σ values)

Tilt limit at depth z:  tan θ_max(z) = [s(z)|_{θ=0} − s_min] / z
```

### E.2.2 Spreadsheet Layout

```
Column    Quantity                         Reference row: upper bow
──────────────────────────────────────────────────────────────────────
A         Depth z (µm)                     1.5
B         Slit CD at z (nm)                230
C         ΔW_slit/2 = (B − W_t)/2           15
D         Hole CD at z (nm)                140
E         Δr_hole = (D − d_h,top)/2         10
F         δ_rand (nm)                       16.4
G         s(z) at θ = 0 = s_nom − C − E − F 38.6
H         Margin = G − s_min                8.6
I         θ_max = atan(H / (1000·A)) (°)    0.33

Repeat rows for every depth where either profile has an extreme:
slit bow, hole bow (each deck), deck joint, bottom.
The smallest θ_max over all rows is the tilt limit.
```

### E.2.3 Reference Results

```
Depth        Slit CD   Hole CD   s(z), θ=0   Margin   θ_max
──────────────────────────────────────────────────────────────
1.5 µm       230       140       38.6 nm     8.6      0.33°
7.2 µm       174       140       66.6 nm     36.6     0.29°   ← limit
11.5 µm      132       70        122.6 nm    92.6     0.46°
```

---

## E.3 Neutral Transport (Chapter 3)

### E.3.1 Monte Carlo Method

The transmission values in Chapter 3 and Appendix B were computed with the following free-molecular Monte Carlo procedure:

```
Geometry: feature of width (or diameter) 1 and depth A; z = 0 at the
          top opening, z = A at the bottom; slot infinite along y.

For each test particle:
  1. Start at a random point on the top opening (uniform over the
     opening area).
  2. Draw a direction from a cosine distribution about the inward
     normal (−z into the feature):
        sin²θ = u₁,  φ = 2π u₂   (u₁, u₂ uniform on [0, 1))
  3. Fly in a straight line to the first surface: a sidewall, the
     bottom plane (z = A), or back out of the top (z = 0).
  4. If the bottom: count as transmitted; stop.
     If the top: count as returned; stop.
     If a sidewall: with probability s, the particle sticks (lost);
     otherwise re-emit from the hit point with a new cosine direction
     about the local wall normal; go to step 3.

K_n = (number transmitted) / (number started)

Statistics: 20 000–40 000 particles per point gives ±1–3% relative
error for K_n > 0.02. Check against Clausing values for a cylinder
(A = 1: 0.514; A = 10: 0.109) and parallel plates (A = 1: 0.685).
```

### E.3.2 Fits and Limits

```
Hole (A ≥ 5):      K_n ≈ 1 / (1 + 0.75 A)
Slot (A ≥ 5):      K_n ≈ (ln A + 0.15) / A
Line of sight:     slot ≈ √(1 + A²) − A ≈ 1/(2A); hole ≈ 1/(4A²)
```

---

## E.4 Ion Transmission and ARDE (Chapters 3 and 6)

```
Direct ion transmission (small A·σ_θ):
  Slot: K_i ≈ 1 − √(2/π) · A · σ_θ = 1 − 0.80 A σ_θ
  Hole: K_i ≈ 1 − 1.60 A σ_θ

Angular spread vs energy (collisionless sheath):
  σ_θ ∝ E^(−1/2); reference σ_θ = 4 × 10⁻³ rad at 3 keV

Synergy model:
  1/ER(A) = 1/(ER_n0 · K_n(A)) + 1/(ER_i0 · K_i(A))
  Reference: ER_n0 = 8.0 µm/min, ER_i0 = 0.75 µm/min

Time to depth (numerical):
  t(z) = Σ Δz / ER(A(z')),  A(z') = z' / W,  Δz ≤ 5 nm

Reference results: average 0.405 µm/min to 11.5 µm (28.4 min);
hole of the same width: 0.22 µm/min.
```

---

## E.5 Ion Energy Distribution (Chapter 6)

```
Sinusoidal low-frequency bias, ions following the sheath:
  E = eV̄ (1 + sin φ),  φ uniform

  P(E < E_c) = 1/2 + (1/π) arcsin(E_c/(eV̄) − 1)
  ⟨√E⟩ = (2√2/π) √(eV̄) = 0.900 √(eV̄)

Yield ratio, monoenergetic vs sinusoidal at equal mean energy
(E_th = 40 eV, V̄ = 3 kV): 48.4 / 43.2 = 1.12

Pulsing at duty D, equal average power:
  P_peak = P_avg / D; on-phase energy ≈ E_cont / D (fixed J_i)
```

---

## E.6 Sheath and Collisions (Chapter 7)

```
Child-law sheath:  s = [(4ε₀/9) √(2e/M) V^(3/2) / J_i]^(1/2)
  Reference (Ar⁺, 3 kV, 5 mA/cm²): s ≈ 5.3 mm

Charge-exchange mean free path: λ_i = 1/(n_g σ_cx)
  n_g ≈ 3.2 × 10¹⁶ cm⁻³ per Torr; σ_cx ≈ 5 × 10⁻¹⁵ cm²
Collisionless fraction: exp(−s/λ_i)

Residence time:  τ = p V / Q;  Q (Torr·L/s) = sccm × 0.01267
Pumping speed:   S_eff = Q / p
```

---

## E.7 Edge Sheath and Tilt (Chapter 9)

```
Boundary mismatch: Δ = (h_r − h_w) + (s_r − s_w)
Tilt profile:      θ(x) ≈ (Δ / (2s)) · exp(−x / s)
Perpendicular tilt for slits along x: θ_⊥ = θ_r |sin φ|
Ring-voltage compensation: Δs/s ≈ (3/4) ΔV/V

Allowed mismatch for tilt limit θ_lim at x:
  |Δ|_max = 2s · θ_lim · exp(x/s)
  Reference (θ_lim = 0.25° = 4.36 mrad, x = 3 mm, s = 5.3 mm):
  |Δ|_max = 10.6 × 4.36 × 10⁻³ × e^0.566 mm = 0.081 mm
```

---

## E.8 Mask Budget (Chapters 4 and 13)

```
r_m = ER_open / S₀
Mask loss (main etch) = r_m × t_ME
Effective selectivity = S₀ × ER_avg / ER_open
Facet height h_f ≈ k_f × planar loss (k_f ≈ 0.10–0.20)
Remaining = T₀ − (open loss) − f_edge × (main + landing loss)
Condition: remaining > h_f + reserve

Reference: T₀ = 3.0 µm, r_m = 0.069 µm/min, t_ME = 28.4 min
  center remaining 0.88 µm; edge (f = 1.12) 0.63 µm
```

---

## E.9 Profile (Chapter 10)

```
Facet reflection depth:   z_hit ≈ W / tan(2β)
Bow growth:               ΔW = 2 ∫ max(0, LER) dt
Taper:                    W(z) = W_bow − 2 (z − z_bow) tan α
Bottom-CD sensitivity:    dW_b/dα = −2 (D − z_bow) × π/180 per degree
Closure depth:            z_stop = z_bow + W_bow / (2 tan α)
Striation amplitude:      δ_s ≈ |LER_ox − LER_N| × t_exposed
```

---

## E.10 Landing (Chapters 2 and 12)

```
Arrival spread (fractional):   δt/t ≈ δH/H − δER/ER
Staircase arrival:             t(φ)/t(0) = (1 − φ) + φ · ER_ON / ER_fill
LS-1 time:                     T₁ = (1 + m) × δ_spread / R_ON,LS1
Poly-Si loss (earliest):       L_max = R_poly × T₁
Thickness spread to LS-2:      ≈ δ_spread / S
Required selectivity:          S_min = (1 + m) δ_spread / L_allow

Reference: δ_spread = 345 nm, R_ON = 0.25, R_poly = 0.015 µm/min, m = 0.2
  T₁ = 100 s; L_max = 25 nm; spread to LS-2 = 21 nm
```

---

## E.11 Stress, Bow, and Distortion (Chapters 2 and 11)

```
Stack stress:              σ = (t_ox σ_ox + t_N σ_N) / p
Stoney curvature:          κ = 6 σ_f h_f / (M_s h_s²)
Bow:                       δ = κ r² / 2
Cross-slit release:        f_rel ≈ 1 − w_b / h; wafer-level ≈ f_array × f_rel
Plate buckling (wall):     σ_cr = k π² E / (12(1 − ν²)) · (t/h)², k ≈ 1.28
Magnification from Δκ:     m = (h_s/2) Δκ
Local surface strain:      ε ≈ 4 Δ(σ_f h_f) / (M_s h_s)

Reference: σ = −82 MPa; uncompensated bow ≈ 560 µm; m_⊥ ≈ 10.6 ppm
```

---

## E.12 Thermal (Chapter 8)

```
ΔT = q × Σ R_i
τ_wafer = ρ c_p h × Σ R_i  (≈ 0.29 s, reference)
Coverage sensitivity (adsorption): d ln θ / dT ≈ −E_d / (k_B T²)
ESC force at gap g: P_e ∝ [ε_r V / (d + ε_r g)]²
Plate flattening pressure: P ≈ 64 D δ / R⁴
```

---

## E.13 Throughput and Cost (Chapters 5 and 16)

```
Chamber WPH = 60 / cycle time (min)
Effective WPH = WPH × availability × utilization
Chambers needed = (WSPM / 720) / effective WPH
Depreciation per wafer = (tool cost / years) / (effective WPH × 8760)

Reference: cycle 37.6 min → 1.60 WPH → 1.22 effective
  100k WSPM → 114 chambers; depreciation ≈ $84/wafer; total ≈ $122/wafer
```

---

**Appendix E Version:** 1.0  
**Last Updated:** 2026-10-04
