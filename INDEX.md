# Index: Book #24 Navigation Guide

## Quick Navigation

**Total Content:** 16 chapters + 7 appendices + glossary  
**Estimated Read Time:** 22–30 hours for the complete book; 6–10 hours for a focused reading path

| Part | Chapters | Theme |
|------|----------|-------|
| I | 1–4 | Fundamentals: architecture, stack and landing layers, HAR trench physics, chemistry and mask |
| II | 5–9 | Hardware: reactor, ion energy and pulsing, gas and recipe steps, temperature and cryo, edge sheath |
| III | 10–14 | Phenomena: profile, tilt and distortion, landing, mask and uniformity, advanced schemes |
| IV | 15–16 | Production: endpoint, metrology, APC, integration, yield, cost |

---

## Part I: Fundamentals (Chapters 1–4)

### Chapter 1: [Replacement-Gate 3D NAND & the Role of the Slit](./chapters/01-slit-architecture.md)
**Estimated Time:** 60 min | **Difficulty:** Foundation | **Reading Level:** All roles  
**Focus:** Why does the array need slits, and what must they deliver?

**Key Topics:**
- Replacement-gate sequence and the access problem
- The four jobs of a slit: access, isolation, common source, source access
- Slit geometry, aspect ratio by generation, pitch and area overhead
- Depth-resolved clearance budget and the tilt limit
- Specification sheet for a modern slit

**Prerequisites:** None (foundational)  
**Cross-References:** Book #23 (staircase region); Silicon Nitride Etch companion  
**Critical Equations:** f_slit = (W_t + 2s)/P_s; s(z) clearance budget; tan θ_max = margin/z  
**Study Questions:** 5 calculations on layout, clearance, and scaling

---

### Chapter 2: [The Stack Beneath the Slit — Layers, Landing Stack & Stress](./chapters/02-stack-landing-materials.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Process/Integration roles  
**Focus:** What does the slit cut through and land on, and what happens to the stack when it is cut?

**Key Topics:**
- Reference stack, select-gate and dummy levels, staircase fill
- Harmonic-mean etch rate through ON pairs; striation from rate mismatch
- Stack-thickness variation and arrival spread at the source
- Substrate, poly-Si plate, and replacement-source landing stacks
- Stoney bow, compensation, and the post-slit saddle

**Prerequisites:** Chapter 1  
**Cross-References:** Books #6–10; Appendix A  
**Critical Equations:** ER_avg = p / (t_ox/ER_ox + t_N/ER_N); Stoney κ; f_rel ≈ 1 − w_b/h  
**Study Questions:** 5 calculations on rate, arrival, and bow

---

### Chapter 3: [High-Aspect-Ratio Trench Etch Physics](./chapters/03-har-trench-physics.md)
**Estimated Time:** 90 min | **Difficulty:** Advanced | **Reading Level:** Process/Research roles  
**Focus:** Why does a slit etch differently from a hole?

**Key Topics:**
- Ion–neutral synergy model
- Monte Carlo neutral transmission: slot vs. hole, with and without sticking
- Ion angular spread and direct transmission
- ARDE table and time-to-depth curve for the reference slit
- Charging in trenches; where symmetry breaks

**Prerequisites:** Chapters 1–2; Books #1–5  
**Cross-References:** Appendix B.6, Appendix E.3–E.4  
**Critical Equations:** K_n,slot ≈ (ln A + 0.15)/A; K_i ≈ 1 − 0.80Aσ_θ; 1/ER = 1/ER_n + 1/ER_i; θ_defl ≈ qE⊥L/(2E_i)  
**Study Questions:** 6 calculations on transport, ARDE, and charging

---

### Chapter 4: [Slit Etch Chemistries & the Hard-Mask System](./chapters/04-chemistry-hardmask.md)
**Estimated Time:** 80 min | **Difficulty:** Advanced | **Reading Level:** Process/Research roles  
**Focus:** Which gases do what, and how long does the mask last?

**Key Topics:**
- C₄F₆, CH₂F₂, O₂, Ar, and additives
- Oxide/nitride balance and its drift with depth
- Sidewall passivation and polymer transport
- Amorphous-carbon mask, opening sequence, effective selectivity
- Two-stage landing chemistry; post-etch cleanup

**Prerequisites:** Chapter 3; Books #6–10, #19  
**Cross-References:** Book #20 (ashing); Appendix B  
**Critical Equations:** r_m = ER_open/S₀; S_eff = S₀ · ER_avg/ER_open  
**Study Questions:** 5 calculations on chemistry balance and mask budget

---

## Part II: Hardware Design (Chapters 5–9)

### Chapter 5: [Reactor Architecture for Deep Slit Etch](./chapters/05-reactor-architecture.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Equipment/Process roles  
**Focus:** What kind of chamber etches a 60:1 trench for half an hour?

**Key Topics:**
- CCP vs. ICP for HAR dielectric etch
- VHF source and LF bias; ion energy from bias power
- Heat load, residence time, pumping
- Throughput and fab chamber count; matching

**Prerequisites:** Chapters 1–4  
**Cross-References:** Books #11–15  
**Critical Equations:** ⟨V_sh⟩ ≈ ηP_LF/I_i; τ = pV/Q; chambers = demand / effective WPH  
**Study Questions:** 5 calculations on energy, residence, and throughput

---

### Chapter 6: [Ion Energy, Bias Waveforms & Pulsing](./chapters/06-ion-energy-pulsing.md)
**Estimated Time:** 80 min | **Difficulty:** Advanced | **Reading Level:** Equipment/Research roles  
**Focus:** How much energy, in what distribution, and when?

**Key Topics:**
- Yield and transmission vs. ion energy
- Low-frequency IED and the slow-ion fraction
- Tailored waveforms: +12% yield at equal mean energy
- Pulsing for passivation and charge relief
- Ramping ion energy with depth

**Prerequisites:** Chapters 3, 5  
**Cross-References:** Books #11–15 (RF and pulsing)  
**Critical Equations:** Y = A(√E − √E_th); P(E < E_c) = ½ + arcsin(E_c/eV̄ − 1)/π; P_peak = P_avg/D  
**Study Questions:** 5 calculations on IED and pulsing

---

### Chapter 7: [Gas Delivery, Pressure & Multi-Step Recipe Design](./chapters/07-gas-pressure-steps.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Process/Equipment roles  
**Focus:** How is a slit recipe structured and developed?

**Key Topics:**
- Sheath thickness and ion collisionality vs. pressure
- Flow, ratios, and residence time as separate knobs
- ME-1/ME-2/ME-3/LS-1/LS-2 architecture; ramps; step marks
- Step transitions and gas-arrival delays
- Center/edge gas tuning; depth-series development

**Prerequisites:** Chapters 4–6  
**Cross-References:** Appendix C.1, Appendix D  
**Critical Equations:** Child-law sheath s; λ_i = 1/(n_gσ); line delay = V/Q_vol  
**Study Questions:** 6 calculations and planning exercises

---

### Chapter 8: [Wafer Temperature, Cryogenic Etch & Electrostatic Chucks](./chapters/08-temperature-cryo-esc.md)
**Estimated Time:** 75 min | **Difficulty:** Intermediate | **Reading Level:** Equipment/Process roles  
**Focus:** How hot is the wafer, how flat is it, and what changes when it is very cold?

**Key Topics:**
- Temperature as a polymer knob
- Heat balance through the helium gap; thermal time constant
- Bias ramps as temperature ramps
- Chucking bowed and saddle-shaped wafers; staged chucking
- Cryogenic HAR etch: mechanisms, benefits, sensitivity, hardware

**Prerequisites:** Chapters 4–5  
**Cross-References:** Chapter 14 (300+ layers)  
**Critical Equations:** ΔT = qΣR; τ = ρc_ph ΣR; P_e at gap; d ln θ/dT = −E_d/(k_BT²)  
**Study Questions:** 5 calculations on thermal and chucking design

---

### Chapter 9: [Edge Ring, Sheath Control & Chamber Conditioning](./chapters/09-edge-sheath-conditioning.md)
**Estimated Time:** 75 min | **Difficulty:** Intermediate | **Reading Level:** Equipment/Process roles  
**Focus:** Why do slits tilt at the edge, and how is the chamber kept stable?

**Key Topics:**
- Sheath mismatch and the tilt profile
- Only perpendicular tilt matters: the two critical sectors
- Ring materials, wear, and life; compensation by lift or voltage
- Step-dependent mismatch; WAC, electrode aging, seasoning
- Particles and blocked slits; bad-block allowance

**Prerequisites:** Chapters 1, 5  
**Cross-References:** Chapter 11 (tilt budget), Chapter 15 (edge APC)  
**Critical Equations:** θ(x) ≈ (Δ/2s)e^(−x/s); θ_⊥ = θ_r|sin φ|; Δs/s ≈ ¾ ΔV/V  
**Study Questions:** 5 calculations on tilt and ring life

---

## Part III: Process Phenomena (Chapters 10–14)

### Chapter 10: [Profile Control — Bowing, Taper, Striation & Bottom CD](./chapters/10-profile-bow-taper.md)
**Estimated Time:** 80 min | **Difficulty:** Advanced | **Reading Level:** Process roles  
**Focus:** What shapes the slit at each depth, and how is each feature fixed?

**Key Topics:**
- Facet reflection and bow depth
- Taper, bottom-CD sensitivity, taper runaway and closure
- Horizontal and vertical striation
- Bottom shape: microtrenching and rounding
- Lever-response matrix; fix bow early, bottom CD late

**Prerequisites:** Chapters 3, 4, 6, 7  
**Cross-References:** Appendix D.2  
**Critical Equations:** z_hit ≈ W/tan 2β; dW_b/dα ≈ −356 nm/°; z_stop = z_bow + W_bow/(2 tan α)  
**Study Questions:** 6 calculations on profile

---

### Chapter 11: [Tilt, Wiggling & Stress-Induced Distortion](./chapters/11-tilt-wiggling-distortion.md)
**Estimated Time:** 75 min | **Difficulty:** Advanced | **Reading Level:** Process/Integration roles  
**Focus:** Where is the slit, and where does the wafer put it afterward?

**Key Topics:**
- Tilt sources and budget; apparent tilt from wafer slope; dog-leg tilt
- Wiggle and mask-line buckling
- Why as-etched blocks do not buckle or collapse
- Anisotropic magnification and die-level distortion; who pays

**Prerequisites:** Chapters 1, 2, 9  
**Cross-References:** Contact-Hole Etch companion (later overlay)  
**Critical Equations:** σ_cr = kπ²E/(12(1−ν²))(t/h)²; m = (h_s/2)Δκ; ε ≈ 4Δ(σh_f)/(M_sh_s)  
**Study Questions:** 6 calculations on position and distortion

---

### Chapter 12: [Landing, Etch Stop & ARDE Across Regions](./chapters/12-landing-arde-regions.md)
**Estimated Time:** 80 min | **Difficulty:** Advanced | **Reading Level:** Process/Integration roles  
**Focus:** How does every slit end inside an 80 nm layer?

**Key Topics:**
- Window vs. spread; sources of arrival spread
- LS-1 overetch, poly-Si loss, required selectivity
- LS-2 breakthrough options and precision
- Slit ends, junctions, staircase region, array-edge slits
- Arrival map; failure modes

**Prerequisites:** Chapters 2–4  
**Cross-References:** Book #23 (staircase fill); Chapter 16 (replacement source)  
**Critical Equations:** T₁ = (1+m)δ/R_ON; S_min = (1+m)δ/L_allow; t(φ)/t(0) = (1−φ) + φER_ON/ER_fill  
**Study Questions:** 6 calculations and diagnosis exercises

---

### Chapter 13: [Mask Budget, Loading & Uniformity](./chapters/13-mask-budget-uniformity.md)
**Estimated Time:** 65 min | **Difficulty:** Intermediate | **Reading Level:** Process roles  
**Focus:** Will the mask last everywhere, and is every slit the same?

**Key Topics:**
- Planar loss, facet, edge erosion; mask run-out
- Mask need vs. stack depth
- Low-open-area loading by the mask; microloading; edge region
- Radial knobs and conflicting goals; compensation hierarchy

**Prerequisites:** Chapters 4, 9, 10  
**Cross-References:** Book #19 (carbon mask)  
**Critical Equations:** Remaining = T₀ − loss × f_edge; h_f ≈ k_f × loss  
**Study Questions:** 5 calculations and strategy questions

---

### Chapter 14: [Advanced Slits — Multi-Deck, Partial Slits, Select-Gate Cuts & Cryo](./chapters/14-advanced-slit-schemes.md)
**Estimated Time:** 70 min | **Difficulty:** Advanced | **Reading Level:** Integration/Research roles  
**Focus:** How do slit schemes change for complex blocks and 300+ layers?

**Key Topics:**
- Single-pass vs. two-step slits; the joint and its ledges
- Partial slits (H-cuts) and gap integrity
- Select-gate cuts as layer-counting etches
- Budgets at ~17 µm; routes forward; Mo word lines; bonded designs

**Prerequisites:** Chapters 1, 8, 10–13  
**Cross-References:** Book #23 (layer counting)  
**Critical Equations:** W_upper,b + 2·OL ≤ W_lower,t; θ_lim ∝ 1/D  
**Study Questions:** 5 calculations on scheme trade-offs

---

## Part IV: Production Scale (Chapters 15–16)

### Chapter 15: [Endpoint, Metrology & Advanced Process Control](./chapters/15-endpoint-metrology-apc.md)
**Estimated Time:** 75 min | **Difficulty:** Intermediate | **Reading Level:** Process/Equipment roles  
**Focus:** How do we see the slit, and how do we steer it?

**Key Topics:**
- Signal size; why OES layer counting fails below ~1 µm
- Landing transition (t₁₀, t₅₀, t₉₀)
- HV-SEM, CD-SAXS, VC, and sampling at the critical locations
- Fault detection; feed-forward; EWMA feedback; virtual metrology

**Prerequisites:** Chapters 9, 12, 13  
**Cross-References:** Books #11–15 (endpoint); Appendix F  
**Critical Equations:** z_max ≈ p/(2 × spread); t_ME feed-forward; EWMA o_{n+1} = λo* + (1−λ)o_n  
**Study Questions:** 6 calculations and design exercises

---

### Chapter 16: [Post-Slit Integration, Yield & Cost of Ownership](./chapters/16-integration-yield-coo.md)
**Estimated Time:** 75 min | **Difficulty:** Intermediate | **Reading Level:** All roles  
**Focus:** What do later steps need from the slit, and what is it worth?

**Key Topics:**
- Nitride removal; fill stack and the bottom-CD requirement
- Metal recess ARDE and lower-deck shorts
- Replacement source; slit fill and ACS spacer punch
- Defect modes and yield signatures; edge-tilt yield estimate
- Cost of ownership; conventional vs. cryogenic; yield dominates

**Prerequisites:** Chapters 1, 10–12  
**Cross-References:** Silicon Nitride Etch and Contact-Hole Etch companions  
**Critical Equations:** W_b ≥ 2(t_blk + t_bar + t_W) + w_open; cost per wafer model  
**Study Questions:** 6 calculations on integration and cost

---

## Appendices

| Appendix | Title | Use |
|----------|-------|-----|
| [A](./appendices/A-material-properties.md) | Stack, Mask & Landing-Layer Material Properties | Film data, fill oxides, masks, chamber parts, mechanics |
| [B](./appendices/B-chemistry-reaction-data.md) | Chemistry & Reaction Data | Gases, fragments, reactions, OES lines, transport tables |
| [C](./appendices/C-standard-procedures.md) | Standard Operating Procedures | Depth series, qualification, tilt calibration, seasoning, landing checks, matching |
| [D](./appendices/D-process-windows.md) | Process Windows & Lookup Tables | Starting recipes, sensitivities, time-to-depth, tilt and taper tables |
| [E](./appendices/E-slit-geometry-transport-calculations.md) | Slit Geometry, Transport & Budget Calculations | All formulas and the Monte Carlo method |
| [F](./appendices/F-endpoint-metrology-reference.md) | Endpoint & Metrology Reference | Signals, methods, sampling plan, control limits |
| [G](./appendices/G-troubleshooting-guide.md) | Troubleshooting Guide | Symptom → cause → check → action |

Also: [GLOSSARY.md](./GLOSSARY.md)

---

## Reading Paths by Role

### Process Engineer (≈10 hours)
1 → 3 → 4 → 7 → 10 → 12 → 13 → Appendix D, E, G

### Equipment Engineer (≈9 hours)
1 → 5 → 6 → 7 → 8 → 9 → 15 → Appendix A, C, F

### Integration Engineer (≈8 hours)
1 → 2 → 11 → 12 → 14 → 16 → Appendix A, E, G

### Device Engineer (≈5 hours)
1 → 2 → 11 → 16

### Researcher (≈10 hours)
3 → 4 → 6 → 8 → 10 → 14 → Appendix B, E

---

## Cross-Reference Map to Other Books

| Book | Topic | Relevant Chapters |
|------|-------|-------------------|
| Books #1–5 | Plasma Physics Fundamentals | Ch. 3, 5, 6, 7 |
| Books #6–10 | Dielectric & Fluorocarbon Etch | Ch. 2, 4, 10 |
| Books #11–15 | Advanced Plasma Engineering | Ch. 5, 6, 7, 15 |
| Book #19 | Carbon Hard Mask Etch | Ch. 4, 13 |
| Book #20 | Photoresist Ashing | Ch. 4 (post-etch strip) |
| Book #23 | Staircase Etch | Ch. 1, 2, 12, 14 |
| Companion | Silicon Nitride Etch | Ch. 1, 16 |
| Companion | Contact-Hole Etch | Ch. 11, 16 |

---

## Study Questions Summary

**Total Study Questions:** 87 (5–6 per chapter × 16 chapters)  
**Nature:** Mostly calculation-based  
**Topics:** Slit layout and clearance, transport and ARDE, ion energy and pulsing, thermal and chucking design, edge tilt and ring life, profile control, landing and selectivity, mask budget, multi-deck schemes, APC, integration requirements, cost

Examples:
- Build a depth-resolved clearance budget and derive the tilt limit
- Compare neutral transmission in a slot and a hole with and without sticking
- Compute the yield advantage of a tailored bias waveform at equal power
- Estimate edge tilt from ring wear and the ring-voltage change that cancels it
- Size the LS-1 overetch and the selectivity needed for a given arrival map
- Compute the a-C thickness needed for a deeper stack
- Derive the minimum bottom CD from a word-line fill stack
- Compare cost per wafer for conventional and cryogenic slit etch

---

## How to Use This Index

1. **First time?** Read PREFACE.md, then this INDEX, then Chapter 1.
2. **Focused reading?** Pick your role from the reading paths above.
3. **Reference mode?** Jump to the chapter. Use Appendix G for symptoms and Appendix E for formulas.
4. **Deep dive?** Read Chapters 1–16 in order and work the study questions.

---

**Index Version:** 1.0  
**Last Updated:** 2026-10-04  
**Next:** Begin [Chapter 1: Replacement-Gate 3D NAND & the Role of the Slit](./chapters/01-slit-architecture.md)
