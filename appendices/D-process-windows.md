# Appendix D: Process Windows & Lookup Tables

Starting-point recipes and sensitivity tables for a 300 mm CCP slit-etch chamber with a VHF source and high-power LF bias. All values are **illustrative starting points for a design of experiments**, not qualified conditions. They are scaled to the reference process of this book (11.5 µm stack above the source, 200 nm slit, 3.0 µm a-C mask).

---

## D.1 Starting Recipes

### D.1.1 Mask Open

```
Step              Gas (sccm)                 p (mTorr)  Source / bias      Time
──────────────────────────────────────────────────────────────────────────────────
BARC/SiON open    CF₄ 100, CHF₃ 30, Ar 100   15         600 W / 300 W      40–60 s
a-C open          O₂ 150, N₂ 50 (or COS 5)   10         1000 W / 500 W     2–4 min
                  Wafer 0–20 °C (cold for vertical walls)
```

### D.1.2 Main Etch Steps

```
Parameter            ME-1 (0–3 µm)     ME-2 (3–8 µm)      ME-3 (8–11.3 µm)
───────────────────────────────────────────────────────────────────────────────
C₄F₆ (sccm)          40 (30–50)        35 (25–45)         32 (25–40)
CH₂F₂ (sccm)         15 (5–25)         20 (10–30)         22 (10–35)
O₂ (sccm)            25 (15–35)        30 (20–40)         34 (25–45) ramp
NF₃ (sccm)           0                 0                  0–5
Ar (sccm)            300 (200–400)     300                300
Pressure (mTorr)     15 (10–20)        20 (15–25)         20 (15–30)
VHF source (W)       2500              2500               2500
LF bias (kW)         10 (8–12)         15 (12–18)         15→18 ramp
Bias mode            Pulsed 50–70%     Continuous or      Continuous
                     duty               > 80% duty
ESC (°C, wafer est.) 20               25                  30 (rises with
                                                          bias; Ch. 8)
Time (reference)     ≈ 5.4 min         ≈ 12.2 min         ≈ 10.1 min
Expected             Bow onset         Rate ≈ 0.40–0.45   Bottom CD ≥ 130 nm
                     limited           µm/min at depth    at end
```

### D.1.3 Landing

```
Parameter            LS-1 (stop on poly-Si)   LS-2a (breakthrough)   LS-2b-1 (poly, sel.)
──────────────────────────────────────────────────────────────────────────────────────────
Main gases           C₄F₆ 45, Ar 300,         CF₄ 60, Ar 200,        HBr 150, O₂ 3–5,
                     O₂ 10–15                  O₂ 5                   (Cl₂ 0–20)
Pressure (mTorr)     20                        15                     20
Bias (kW)            12–15                     8                      4–6
Rates at bottom      ON 0.25; poly 0.015       poly ≈ ox ≈ 0.12       poly 0.05–0.08;
(µm/min)             (S ≈ 17)                                         ox < 0.004
Time                 ≈ 100 s (array only);     ≈ 1.5 min              set by remaining
                     longer with staircase                            poly-Si
                     offset (Ch. 12)
```

---

## D.2 Sensitivity Tables

### D.2.1 Main Etch (ME-2), Per Unit Change (Illustrative)

```
Change                 Rate at depth   Ox:N ratio   Mask sel.   Bow     Bottom CD
───────────────────────────────────────────────────────────────────────────────────
+1 kW bias             +4%             ~0           −2%         +1 nm   +2 nm
+500 W source          +3%             ~0           −3%         +1 nm   +1 nm
                       (energy per ion falls)
+5 mTorr               −2%             +0.02        +3%         +2 nm   −3 nm
+5 sccm C₄F₆           −2%             +0.03        +6%         −2 nm   −4 nm
+5 sccm CH₂F₂          +1%             −0.08        +2%         −1 nm   −1 nm
+5 sccm O₂             +3%             −0.02        −8%         +2 nm   +5 nm
+5 °C wafer            +1%             ±            −5%         +2.5 nm +2 nm
```

### D.2.2 Interaction of Source and Bias

```
                       Ion current J_i    Mean ion energy    Rate at depth
──────────────────────────────────────────────────────────────────────────
Bias +10%, source 0    ~+2%               ~+8%               +4–5%
Source +10%, bias 0    ~+8%               ~−7%               +1–3%
Both +10%              ~+10%              ~0%                +5–6%
```

### D.2.3 Edge Controls (Outer 10 mm)

```
Change                          Tilt at 3 mm   Edge rate   Edge mask loss   Edge bottom CD
──────────────────────────────────────────────────────────────────────────────────────────
Ring voltage +1%                −0.12°         +0.5%       +0.5%            +0.5 nm
Ring height +20 µm              −0.06°         −0.2%       ~0               ~0
Edge ESC zone +2 °C             ~0             +0.2%       +2%              +0.8 nm
Edge gas: +3 sccm O₂            ~0             +1%         +3%              +2 nm
```

---

## D.3 Lookup Tables

### D.3.1 Time to Depth (Reference Slit, Chapter 3 Model)

```
Depth (µm)   1     2     3     4     5     6      8      10     11.5
Time (min)   1.6   3.4   5.4   7.5   9.8   12.2   17.6   23.6   28.4
Rate at      0.59  0.53  0.49  0.45  0.42  0.40   0.35   0.32   0.30
depth (µm/min)
```

### D.3.2 Tilt Displacement

```
Lateral offset (nm) = depth × tan θ

             Tilt θ
Depth (µm)   0.05°   0.10°   0.15°   0.20°   0.25°   0.30°
──────────────────────────────────────────────────────────────
1.5          1.3     2.6     3.9     5.2     6.5     7.9
5.0          4.4     8.7     13.1    17.5    21.8    26.2
7.2          6.3     12.6    18.8    25.1    31.4    37.7
11.5         10.0    20.1    30.1    40.1    50.2    60.2
17.3         15.1    30.2    45.3    60.4    75.5    90.6
```

### D.3.3 Bottom CD vs. Taper (Bow 230 nm at 1.5 µm, Depth 11.7 µm)

```
Taper α (°)       0.20    0.24    0.28    0.32    0.36    0.40
Bottom CD (nm)    159     145     130     116     102     88
```

### D.3.4 Required LS-1 Selectivity

```
S_min = 1.2 × δ_spread / L_allow     (L_allow = allowed poly-Si loss)

                    L_allow (nm)
δ_spread (nm)       50      75      100
──────────────────────────────────────────
300                 7.2     4.8     3.6
500                 12      8.0     6.0
800                 19      13      9.6
1600                38      26      19
```

---

**Appendix D Version:** 1.0  
**Last Updated:** 2026-10-04
