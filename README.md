# Book #24: 3D NAND Slit Etch — Gate-Line Slit Formation for Replacement-Gate 3D NAND

## Overview

**Book #24** is a technical reference on **3D NAND slit etch**: the deep plasma etch that cuts long, narrow trenches through the full height of a 3D NAND stack and divides the memory array into blocks. These trenches are called slits, gate-line slits (GLS), or word-line cuts. A modern slit is 150–250 nm wide at the top, 8–14 µm deep, and runs uninterrupted for millimetres across the array and through the staircase. Its aspect ratio is 40:1 to 80:1. It is one of the deepest trenches made anywhere in semiconductor manufacturing.

The slit has several jobs at once. It is the **access path** through which the sacrificial nitride is removed in hot phosphoric acid and replaced with tungsten or molybdenum word lines. It is the **isolation** that separates one block's word lines from the next. In many designs it later becomes the **common-source line**, a buried conductor that carries current from every string in the block. In flows with a replacement source under the array, it is also the access path for building the source contact. Each job places a requirement on the etch. The slit must be deep enough to reach the source layer. It must be wide enough at the bottom for liquid and gas to move through it. It must be straight enough to stay clear of the channel holes beside it, and continuous enough that no two blocks remain bridged.

The basic method is easy to state. Pattern a thick amorphous-carbon hard mask with long line openings. Etch straight down through hundreds of alternating oxide and nitride layers with a fluorocarbon plasma driven by kilovolt ion energies. Stop on a landing layer in the source stack. **The slit must go all the way down, stay straight the whole way, and stop in the right place.**

Doing it in production is hard. Neutral radicals have to reach the bottom of a trench 60 times deeper than it is wide. Ions arriving a fraction of a degree off normal hit the sidewall and bow the profile. At the wafer edge, a curved sheath tilts the whole slit toward or away from the channel holes. Stack stress makes the blocks lean and the wafer warp once the slits are cut. The mask has to survive half an hour of keV ion bombardment. A single chamber spends 25–40 minutes on one wafer. This book covers the physics, chemistry, equipment, and production engineering that make slit etch work.

---

## Intended Audience

This book is written for **semiconductor industry professionals** with working knowledge of plasma processing:

- **Process Engineers**: developing high-aspect-ratio slit recipes; controlling bow, taper, bottom CD, tilt, and landing; balancing etch rate against mask budget
- **Equipment Engineers**: specifying reactors with high-power low-frequency bias, multi-zone temperature control, tunable edge sheaths, and cryogenic options; managing edge-ring wear and chamber drift over long recipes
- **Integration Engineers**: setting slit width, pitch, and clearance to channel holes; managing replacement gate, word-line separation, source formation, and slit fill
- **Device Engineers**: understanding how slit errors become word-line-to-source shorts, block-to-block leakage, word-line resistance shifts, and dead blocks
- **Researchers**: studying transport in deep trenches, charging, sidewall passivation, cryogenic and hydrogen-fluoride-based chemistries, and stress-driven deformation

The material assumes a working knowledge of plasma physics (Books #1–5) and fluorocarbon dielectric etch (Books #6–10). Book #19 (Carbon Hard Mask Etch) is especially helpful background for the mask chapters, and Book #23 (Staircase Etch) describes the stack and the staircase region the slit must cut through.

---

## Technical Scope

### Core Concepts Covered

**Geometry & Physics:**
- Slit geometry: width, depth, pitch, aspect ratio, bottom CD, clearance to channel holes
- Neutral transport in deep trenches: Knudsen flow, slot versus hole transmission, sticking
- Ion transport: angular distributions, sidewall scattering, and why trenches differ from holes
- Aspect-ratio-dependent etching (ARDE) and the etch-rate decline with depth
- Differential charging at high aspect ratio and its effect on the trench bottom

**Materials & Chemistry:**
- Alternating SiO₂/Si₃N₄ (ON) stacks and the inter-deck, cap, and source layers
- Fluorocarbon chemistries (C₄F₆, C₄F₈, CH₂F₂, CHF₃) with O₂, Ar, NF₃ and other additives
- Balanced oxide and nitride etch rates for smooth sidewalls
- Amorphous-carbon hard masks: selectivity, faceting, stress, and doped variants
- Landing-layer chemistry: stopping on polysilicon and punching into the source stack

**Equipment Design:**
- Capacitively coupled reactors with very-high-frequency source and high-power low-frequency bias
- Ion energy control, tailored bias waveforms, and pulsing for charge relief
- Gas delivery, pressure, and multi-step recipes for deep etches
- Wafer temperature control, multi-zone chucks, and cryogenic etch
- Edge-ring design, tunable edge sheath, and chamber conditioning over long recipes

**Process Phenomena:**
- Bowing, taper, necking, sidewall striation, and bottom-CD control
- Tilt at the wafer edge, slit wiggling, block leaning, and stress-induced distortion
- Landing in the source stack and etch-depth variation across the die and wafer
- Mask budget, loading, and within-wafer uniformity
- Advanced schemes: multi-deck slits, partial slits, select-gate cuts, cryogenic slit etch

**Production Integration:**
- Endpoint detection at extreme aspect ratio
- Depth, bottom-CD, tilt, and overlay metrology
- Feed-forward and feedback APC on etch time and edge tuning
- Replacement gate, word-line separation, source formation, and slit fill
- Yield signatures, throughput, and cost of ownership

### Technology Context

- **Device architectures:** Replacement-gate charge-trap 3D NAND from 64 to 300+ word-line layers, single- and multi-deck; CMOS-under-array (CuA) and wafer-bonded (array-on-CMOS) configurations
- **Stack types:** SiO₂/Si₃N₄ replacement-gate stacks (primary focus). Gate-first SiO₂/poly-Si stacks are covered where they differ
- **Process sequence:** Slit etch follows channel-hole formation, staircase etch, staircase fill, and CMP. It comes before nitride removal, word-line metal fill, word-line separation, and slit fill
- **Manufacturing scale:** 300 mm wafers, one slit mask per wafer (or one per deck), 25–45 minutes of etch per wafer, many chambers per fab dedicated to high-aspect-ratio dielectric etch

---

## Book Organization

### Part I: Fundamentals (4 Chapters)

**Chapter 1: Replacement-Gate 3D NAND & the Role of the Slit**
- Why a vertical NAND array needs slits
- The four jobs of a slit: access, isolation, source line, source access
- Slit geometry, aspect ratio, and the block-size trade-off
- Where slit etch sits in the process flow and the specification sheet

**Chapter 2: The Stack Beneath the Slit — Layers, Landing Stack & Stress**
- ON pairs, cap and inter-deck layers, and the staircase fill
- Source stacks: substrate landing, poly-Si source plates, replacement source
- Film stress, wafer bow, and how slits change both
- How stack properties set etch rate, sidewall smoothness, and landing

**Chapter 3: High-Aspect-Ratio Trench Etch Physics**
- Neutral transport: Knudsen flow and the slot-versus-hole advantage
- Ion transport: angular spread, sidewall reflection, and bottom flux
- ARDE models and the etch-rate decline with depth
- Charging in deep trenches

**Chapter 4: Slit Etch Chemistries & the Hard-Mask System**
- Fluorocarbon chemistry for non-selective ON etch
- Balanced oxide and nitride rates, sidewall passivation, and polymer transport
- The amorphous-carbon mask: selectivity, faceting, and alternatives
- Landing chemistry: stopping on poly-Si and punching into the source stack

### Part II: Hardware Design (5 Chapters)

**Chapter 5: Reactor Architecture for Deep Slit Etch**
- Why capacitively coupled plasma dominates high-aspect-ratio dielectric etch
- VHF source and high-power LF bias
- Gap, pumping, and residence time
- Platform configuration, throughput, and chamber matching

**Chapter 6: Ion Energy, Bias Waveforms & Pulsing**
- Kilovolt ion energies and narrow angular distributions
- Bias frequency, power, and the ion energy distribution
- Tailored waveforms and pulsed operation
- Pulsing for charge relief and polymer control

**Chapter 7: Gas Delivery, Pressure & Multi-Step Recipe Design**
- Pressure, flow, residence time, and radical balance
- Multi-step recipes: mask open, main etch stages, landing, overetch
- Ramped parameters with depth
- Center/edge gas tuning

**Chapter 8: Wafer Temperature, Cryogenic Etch & Electrostatic Chucks**
- Temperature dependence of polymer deposition and sidewall protection
- Multi-zone ESCs and radial tuning
- Cryogenic slit etch: mechanisms, rates, and hardware
- Chucking bowed wafers and thermal stability over long recipes

**Chapter 9: Edge Ring, Sheath Control & Chamber Conditioning**
- The edge sheath and why slits tilt at the wafer edge
- Edge-ring geometry, materials, wear, and tunable edge control
- Chamber walls, seasoning, and first-wafer effects
- Drift over long recipes and long ring life

### Part III: Process Phenomena (5 Chapters)

**Chapter 10: Profile Control — Bowing, Taper, Striation & Bottom CD**
- Bow formation and its location in depth
- Taper, necking, and bottom-CD collapse
- Sidewall striation at oxide/nitride interfaces
- Profile trade-offs and recipe levers

**Chapter 11: Tilt, Wiggling & Stress-Induced Distortion**
- Tilt budget and clearance to channel holes
- Wiggling of long slits and its causes
- Block leaning and bending after slit etch
- Anisotropic bow, in-plane distortion, and overlay of later layers

**Chapter 12: Landing, Etch Stop & ARDE Across Regions**
- Landing windows in the source stack
- Overetch, etch-stop selectivity, and punch-through
- Slits in the array, the staircase, and the periphery
- Depth loading at slit ends, junctions, and partial slits

**Chapter 13: Mask Budget, Loading & Uniformity**
- Mask consumption, faceting, and remaining mask
- Pattern density and macroloading
- Within-wafer depth, CD, and profile uniformity
- Compensation strategies

**Chapter 14: Advanced Slits — Multi-Deck, Partial Slits, Select-Gate Cuts & Cryo**
- Multi-deck slits: single-pass and two-step schemes
- Partial slits (H-cuts) and block layouts
- Shallow select-gate cuts
- Cryogenic and next-generation slit etch at 300+ layers

### Part IV: Production Scale (2 Chapters)

**Chapter 15: Endpoint, Metrology & Advanced Process Control**
- Endpoint detection at extreme aspect ratio
- Depth, bottom-CD, profile, and tilt metrology
- Slit-to-hole overlay and in-plane distortion measurement
- Feed-forward and feedback APC

**Chapter 16: Post-Slit Integration, Yield & Cost of Ownership**
- Nitride removal and word-line metal fill through the slit
- Word-line separation, source formation, and slit fill
- Defect modes and yield signatures
- Throughput, consumables, and cost-of-ownership modeling

---

## Key Technical Themes

1. **The slit is a trench, not a hole.** A long slot transmits about three times more neutral flux than a round hole of the same aspect ratio, and its ions spread in one dimension instead of two. Slit etch is easier than channel-hole etch in transport and harder in straightness over millimetres.
2. **Clearance is the master budget.** The slit sits tens of nanometres from the nearest channel hole. Top CD, bow, tilt, wiggle, and overlay all spend the same clearance.
3. **The bottom matters as much as the top.** The slit bottom must be wide enough for nitride removal, metal fill, word-line separation, and source formation. A slit that is deep but pinched is a failed slit.
4. **Landing is a selectivity problem.** Depth varies by several percent across the wafer. Only an etch stop with enough selectivity can turn that variation into a uniform landing.
5. **The wafer edge sets the yield.** Tilt from the edge sheath and ring wear, not center behavior, usually decides how many die at the edge are good.
6. **Cutting the stack releases its stress.** Slits relax stress in one direction only. Blocks lean, the wafer warps into a saddle, and every later overlay step feels it.

---

## Cross-References to Prior Books

**Related Books in the Series:**

- **Books #1–5** (Plasma Physics & Chemistry Fundamentals): sheath physics, ion energy and angular distributions, radical generation and transport
- **Books #6–10** (Dielectric Etch & Fluorocarbon Chemistry): fluorocarbon polymer, F/C ratio, oxide and nitride etch mechanisms
- **Books #11–15** (Advanced Plasma Engineering): RF delivery, pulsing, gas delivery, endpoint detection
- **Book #19** (Carbon Hard Mask Etch): amorphous-carbon mask deposition, opening, and selectivity
- **Book #20** (Photoresist Ashing): oxygen-plasma removal of the remaining carbon mask
- **Book #23** (Staircase Etch): the stack, the staircase region, and the staircase fill the slit cuts through
- **Companion volumes:** *Silicon Nitride Etch: Chemistry, Selectivity and Integration*, which covers the hot-phosphoric-acid nitride removal through the slit, and *Contact-Hole Etch*, which covers the word-line and source contacts that follow

Slit etch takes the high-aspect-ratio dielectric etch that also forms channel holes and applies it to a trench that must stay straight and continuous across the whole array.

---

## File Organization

```
3d-nand-slit-etch/
├── README.md            ← You are here
├── PREFACE.md
├── INDEX.md
├── GLOSSARY.md
│
├── chapters/
│   ├── 01-slit-architecture.md
│   ├── 02-stack-landing-materials.md
│   ├── 03-har-trench-physics.md
│   ├── 04-chemistry-hardmask.md
│   ├── 05-reactor-architecture.md
│   ├── 06-ion-energy-pulsing.md
│   ├── 07-gas-pressure-steps.md
│   ├── 08-temperature-cryo-esc.md
│   ├── 09-edge-sheath-conditioning.md
│   ├── 10-profile-bow-taper.md
│   ├── 11-tilt-wiggling-distortion.md
│   ├── 12-landing-arde-regions.md
│   ├── 13-mask-budget-uniformity.md
│   ├── 14-advanced-slit-schemes.md
│   ├── 15-endpoint-metrology-apc.md
│   └── 16-integration-yield-coo.md
│
└── appendices/
    ├── A-material-properties.md
    ├── B-chemistry-reaction-data.md
    ├── C-standard-procedures.md
    ├── D-process-windows.md
    ├── E-slit-geometry-transport-calculations.md
    ├── F-endpoint-metrology-reference.md
    └── G-troubleshooting-guide.md
```

---

## Constraints & Scope

### What This Book Covers
✅ High-aspect-ratio slit etch through ON stacks (primary focus)  
✅ Landing in substrate, poly-Si source plates, and replacement-source stacks  
✅ Multi-deck slits, partial slits, select-gate cuts, and cryogenic slit etch  
✅ Equipment design, chamber control, and production integration  
✅ The processes that use the slit (replacement gate, word-line separation, source, slit fill) as customers of the etch  
✅ Yield impact and cost of ownership  

### What This Book Does NOT Cover
❌ Channel-hole etch in depth, beyond the physics it shares with slit etch  
❌ Wet-process chemistry of hot phosphoric acid and metal ALD, beyond what the slit must provide  
❌ Lithography of the slit layer in detail  
❌ Detailed memory-cell physics and NAND circuit design  
❌ Vendor-specific recipes or proprietary tool parameters  

### A Note on Numbers
Numbers in this book come from established plasma physics, published literature trends, and representative production practice. Worked examples use **illustrative values** chosen to show the method, and the arithmetic is written out so readers can substitute their own data. A single **reference process** (a two-deck, 200-pair stack, a 200 nm slit 11.7 µm deep, and a 3.0 µm carbon mask) is used across chapters so that examples connect. The neutral-transmission values in Chapter 3 and Appendix E come from a Monte Carlo calculation of free-molecular flow, cross-checked against classical Clausing values. Treat recipe values as starting points for a design of experiments, never as qualified process conditions.

---

## Development Status

**Book #24 Foundation:** Complete  
**Part I (Chapters 1–4):** Complete  
**Part II (Chapters 5–9):** Complete  
**Part III (Chapters 10–14):** Complete  
**Part IV (Chapters 15–16):** Complete  
**Back Matter (Appendices A–G, Glossary):** Complete  

---

## Next Steps

1. **Read [PREFACE.md](./PREFACE.md)** for the motivation and reading guidance
2. **Read [INDEX.md](./INDEX.md)** for the detailed chapter outline and reading paths by role
3. **Begin [Chapter 1](./chapters/01-slit-architecture.md)**: Replacement-Gate 3D NAND & the Role of the Slit

---

**Book #24 Version:** 1.0  
**Last Updated:** 2026-10-04  
**Series:** ChipFoundryServices Technical Series
