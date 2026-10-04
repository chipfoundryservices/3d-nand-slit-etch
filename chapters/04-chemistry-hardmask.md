# Chapter 4: Slit Etch Chemistries & the Hard-Mask System

## Overview

Slit chemistry has to do four things at once. It must etch oxide and nitride at nearly the same rate, so the slit goes down evenly and the sidewall stays smooth. It must protect the sidewall enough to stop bowing without leaving so much polymer at the bottom that the slit tapers shut. It must etch the stack much faster than the carbon mask, for half an hour. And near the end, it must change character so the etch stops on polysilicon and then opens into the landing layer.

No single gas does all of this. Production slit recipes use a heavy fluorocarbon for polymer and mask selectivity, a hydrofluorocarbon for nitride rate, oxygen to trim polymer, argon to carry the ions, and sometimes a fluorine source or a sulfur- or other passivating additive. The mask is usually a thick film of amorphous carbon. This chapter covers how each ingredient works, how the oxide/nitride balance is set, what the mask contributes, and how the landing chemistry differs from the main etch.

**Learning Objectives:**
- Explain the role of each gas in a slit main-etch recipe
- Describe how hydrogen and oxygen shift the oxide/nitride rate ratio
- Relate polymer precursor sticking to where sidewall protection forms
- Compute mask consumption and effective selectivity over an ARDE-limited etch
- Describe the amorphous-carbon mask stack and its opening sequence
- Design a two-stage landing on a poly-Si stop and into a sacrificial layer

---

## 4.1 What the Main-Etch Chemistry Must Deliver

```
Requirement                         Target (illustrative)     Why
──────────────────────────────────────────────────────────────────────────────
Oxide : nitride rate ratio          0.9–1.2 at all depths     Even etch front;
                                                              smooth sidewall
Stack : mask selectivity            ≥ 8 open-field;           Mask survives the
(open field)                        ≥ 5 effective             whole etch
Sidewall protection                 Bow ≤ 30 nm               Clearance budget
Bottom cleanliness                  No polymer etch stop      Full depth
                                    to A ≈ 60–80
Stack : poly-Si selectivity         ≥ 10 (landing stage)      Landing (Ch. 12)
Byproduct volatility                SiF₄, CO, CO₂, COF₂,      No redeposition in
                                    FCN, HCN, N₂              the slit
```

These requirements conflict. More polymer protects the sidewall and the mask but threatens the bottom. Less polymer opens the bottom but bows the top and erodes the mask. The recipe balances them, and the balance point moves with depth (Chapter 7).

---

## 4.2 The Ingredients

### 4.2.1 Fluorocarbons and the F/C Ratio

```
Gas      F/C ratio   Character in a dense plasma
──────────────────────────────────────────────────────────────────────────
CF₄      4.0         Fluorine-rich etchant; little polymer
C₄F₈     2.0         Balanced; CF₂-rich polymer
C₄F₆     1.5         Polymer-rich; carbon-rich film; high mask
                     selectivity; main gas in many HAR recipes
C₅F₈     1.6         Similar to C₄F₆
```

Lower F/C ratio means more carbon-rich, more ion-resistant polymer. That protects the mask and the upper sidewall. It also threatens the bottom, where a thick film can stop the etch. C₄F₆ is the usual backbone of HAR dielectric recipes because its fragments (C₂F₂, C₃F₃, CF₂, CF) deposit a dense film on carbon mask surfaces while still letting keV ions etch oxide through a thin steady-state film.

### 4.2.2 Hydrofluorocarbons

```
Gas      Role
──────────────────────────────────────────────────────────────────────────
CH₂F₂    Hydrogen source; raises nitride rate (HCN, NH formation);
         adds polymer (H scavenges F as HF)
CHF₃     Milder H source; polymer former; used in mask-open and
         some main-etch stages
CH₃F     Strong H source; very polymerizing; nitride-selective
         chemistries (not usually in non-selective slit etch)
```

Hydrogen does two things. It removes fluorine as HF, which lowers the F/C ratio of the plasma and increases polymer. It also helps etch nitride, because nitrogen leaves the surface more readily as HCN or NH-containing products than as FCN alone. Adding CH₂F₂ to a C₄F₆ recipe raises the nitride rate relative to the oxide rate. This is the main knob for the oxide/nitride balance (Section 4.3).

### 4.2.3 Oxygen

O₂ consumes polymer as CO and CO₂, and it also etches the carbon mask. It is the main knob for polymer thickness. A few sccm of O₂ change bow, taper, and mask selectivity together. Oxide releases its own oxygen into the polymer layer as it etches, so oxide etching is less sensitive to added O₂ than nitride etching is.

### 4.2.4 Argon and Other Diluents

Argon makes up most of the flow in many recipes. It sets the ion composition (Ar⁺ dominates the ion flux), dilutes the reactive gases to slow polymer build-up, and helps the plasma stay uniform. Heavier noble gases (Kr, Xe) have been studied for their different ion mass and sputter yield, but argon is standard.

### 4.2.5 Fluorine Sources and Passivating Additives

```
Additive         Role                                       Risk
──────────────────────────────────────────────────────────────────────────
NF₃ (small)      Extra F; cleans bottom polymer; raises    Mask erosion;
                 rate at depth                              bow
SF₆ (small)      Extra F; S can passivate                   Mask erosion
COS (small)      Sulfur-containing passivation on mask and  S residue;
                 upper sidewall; reported to reduce bow     tool compatibility
                 and faceting
SiF₄ / SiCl₄     Si-containing sidewall film; harder         Residue at
(small)          passivation                                bottom; particles
HBr (small)      Br passivation; mask selectivity           Corrosion of
                                                            exhaust; residue
```

These additives are used in small amounts to fine-tune where passivation forms. Their behavior is recipe-specific, and their effects are best measured rather than predicted. Chapter 10 discusses how they are evaluated against bow and taper.

### 4.2.6 Byproducts

```
Film       Main volatile products         Notes
──────────────────────────────────────────────────────────────────────────
SiO₂       SiF₄, CO, CO₂, COF₂            Oxygen released helps clear
                                          polymer at the oxide surface
Si₃N₄      SiF₄, FCN, (CN)₂, HCN, N₂      CN emission at 388 nm is a
                                          nitride marker (Chapter 15)
a-C mask   CO, CO₂, CₓFᵧ, HCN (with N)    Mask products add polymer
                                          precursors near the top
poly-Si    SiF₄, (SiFₓ in polymer)        Low rate under thick polymer
```

All main products are volatile. But they must leave a slit 60 times deeper than it is wide, and their transport out is as slow as reactant transport in. Products re-emitted from the walls can redeposit. Silicon-containing products, if partially oxidized, can form SiOₓFᵧ residue near the bottom.

---

## 4.3 Balancing Oxide and Nitride

### 4.3.1 Why Balance Matters

At the bottom, the two films alternate. An imbalance does not change the average rate much (Chapter 2, Section 2.2.2), but it does three things:

1. **It roughens the etch front.** If one film etches much faster, the front moves in steps, and any local rate variation is amplified at each interface.
2. **It striates the sidewall.** Lateral rates usually follow vertical rates, so the faster film recedes from the wall (Chapter 2, Section 2.2.3).
3. **It changes polymer balance by depth.** Nitride builds a thicker steady-state polymer. If nitride is the slow film, the bottom spends most of its time under thick polymer and is more prone to stopping.

### 4.3.2 Tuning the Ratio

```
Effect of CH₂F₂ on a C₄F₆/O₂/Ar main etch (illustrative, open field):

CH₂F₂ (sccm)   ER_ox (nm/min)   ER_N (nm/min)   Ox:N    Mask sel.
─────────────────────────────────────────────────────────────────────
  0             700               520            1.35    9.0
 10             690               610            1.13    9.5
 20             670               690            0.97    10.0
 30             640               740            0.86    10.5

Effect of O₂ at CH₂F₂ = 20 sccm (illustrative):

O₂ (sccm)      ER_ox (nm/min)   ER_N (nm/min)   Ox:N    Mask sel.
─────────────────────────────────────────────────────────────────────
 20             650              640            1.02    11
 30             670              690            0.97    10
 40             685              740            0.93    8.5
```

Hydrogen moves the ratio strongly at a small cost in oxide rate, and it slightly improves mask selectivity by adding polymer. Oxygen raises both rates and erodes the mask. The usual approach is to set the ratio with CH₂F₂, then set the overall polymer level with O₂ against bow and taper.

### 4.3.3 The Ratio Changes With Depth

Open-field rates are not bottom rates. At depth, the neutral mix reaching the bottom changes. Low-sticking F and H penetrate better than heavy, high-sticking CₓFᵧ fragments, and oxygen is partly consumed on the walls. A recipe balanced at the top can be nitride-slow or oxide-slow at the bottom. Striation that varies with depth reveals this directly. The remedy is to ramp the hydrogen or oxygen flow during the etch (Chapter 7).

---

## 4.4 Sidewall Passivation and Polymer Transport

### 4.4.1 Where Polymer Goes

From Chapter 3, the sticking probability of a precursor decides how deep it reaches:

```
Precursor (illustrative s)      Deposits mainly        Function
──────────────────────────────────────────────────────────────────────
Large CₓFᵧ (s ≈ 0.1–0.5)        Top ~0.5–1 µm, mask    Mask protection;
                                surfaces                facet control
CF₂, C₂F₂ (s ≈ 0.01–0.1)        Top few µm of           Bow protection
                                sidewall
CF, C (s varies; ion-assisted)  Bottom and lower        Bottom polymer;
                                sidewall                selectivity at
                                                        landing
```

The bow forms 1–2 µm below the top, where reflected ions strike (Chapter 3, Section 3.6). Protection there must come from precursors that stick moderately: enough to deposit in the upper few microns but not so much that they all deposit on the mask. That is part of why C₄F₆ and C₄F₈ fragments, rather than CF₄-derived species, are effective at bow control.

### 4.4.2 Necking and Clogging

Polymer that deposits on the top edges of the mask opening narrows the entrance. This is **necking**. A modest neck shadows the upper sidewall from reflected ions and reduces bow. A severe neck reduces both neutral and ion transmission and can close the slit at the top. In slit etch, necking is usually less severe than in holes, because the slot is open along its length and the top deposit is spread along a line rather than concentrated around a circle. Necking is most likely at slit ends and in narrow partial slits.

### 4.4.3 Polymer at the Bottom

From Chapter 3, Section 3.2.4, high-sticking precursors reach a slit bottom about a hundred times more readily than a hole bottom. A chemistry that leaves a thin, ion-cleaned film at a hole bottom can leave a thicker one at a slit bottom. Signs of excess bottom polymer:

- Taper increasing with depth and bottom CD shrinking
- Etch rate falling faster with depth than the ARDE model predicts
- Etch stop in narrow slit segments while wide segments continue

Raising O₂ slightly, adding a small amount of NF₃ late in the etch, or raising ion energy at depth are the usual remedies. Each costs mask selectivity or bow margin, so the remedy is applied only in the deep part of the etch.

---

## 4.5 The Amorphous-Carbon Mask

### 4.5.1 Why Carbon

A slit mask must be thick and must etch far more slowly than oxide and nitride in fluorocarbon plasma. Photoresist cannot do this. Amorphous carbon (a-C) deposited by PECVD does it well. It forms little volatile product with fluorine, it is easily patterned in oxygen plasma, and it is removed after the etch by ashing (Book #20). Book #19 covers carbon hard mask deposition and opening in detail.

```
Property (PECVD a-C, illustrative)    Standard a-C       High-density / doped
──────────────────────────────────────────────────────────────────────────────────
Density (g/cm³)                       1.5–1.8            1.9–2.2 (high-density);
                                                         higher with B or W doping
Hydrogen content (at.%)               15–30              5–15
sp³ fraction                          low–moderate       higher
Stress (MPa)                          −100 to −500       −500 to −1500
Selectivity ON : a-C (open field)     6–10               10–20+
Transparency for alignment            Good (thin)        Poor; needs alignment
                                                         windows or other aids
Strip                                 O₂ ash             O₂ ash (B-doped: may need
                                                         additional chemistry)
```

Denser, more highly cross-linked carbon etches more slowly and gives more selectivity. It also carries more compressive stress and is harder to see through for alignment. Doped carbons (boron or tungsten) can raise selectivity further but complicate the strip and can leave residue.

### 4.5.2 The Mask Stack and Its Opening

```
Reference mask stack (top to bottom):

  ArF immersion resist     ~100 nm
  BARC                     ~30 nm
  SiON cap                 40 nm     ← transfers pattern into a-C
  a-C                      3.0 µm
  ─────────────────────── cap oxide of the stack

Opening sequence:
  1. BARC/SiON open:  CF₄/CHF₃/Ar, low pressure (~1 min)
  2. a-C open:        O₂-based with a passivating additive (N₂, COS,
                      or SO₂ in some flows); low wafer temperature;
                      anisotropic to the cap oxide (~2–4 min)
  3. Optional CD trim or polymer cleanup
  4. Main etch begins in the same chamber or after transfer
```

Slits are wide lines by lithography standards. The patterning challenge is not resolution but **long-range uniformity**: a constant CD along millimetres of line, with no line-end shortening, local pinching, or defects that would leave a bridge.

### 4.5.3 Mask Consumption and Effective Selectivity

The mask sits at the open surface and is eroded at a nearly constant rate throughout the etch. The stack etches at a rate that falls with depth. Selectivity measured at the open field therefore overstates what the mask actually achieves:

```
Mask erosion rate:  r_m ≈ ER_open / S₀

Reference: ER_open = 0.686 µm/min (Chapter 3), S₀ = 10 (open field)
  r_m = 0.069 µm/min

Main etch to the source stack: 28.4 min (Chapter 3)
  Vertical mask loss = 0.069 × 28.4 = 1.95 µm

Effective selectivity = depth / mask loss = 11.5 / 1.95 = 5.9
```

**The effective selectivity is the open-field selectivity times the ratio of average to open-field etch rate:** 10 × 0.405/0.686 = 5.9. Deeper slits lower the ratio, so effective selectivity falls with depth even if the chemistry does not change.

```
Mask budget (reference, illustrative):

  Starting a-C                            3.00 µm
  SiON cap lost early; a-C open loss      −0.05 µm
  Main etch (28.4 min)                    −1.95 µm
  Landing stages (≈3 min, lower rate)     −0.12 µm
  Facet allowance (corner rounding)       —   (affects top CD, Ch. 13)
  ──────────────────────────────────────────────
  Remaining a-C (planar)                  ≈ 0.88 µm
  Specification                           ≥ 0.5 µm
```

The margin is about 0.4 µm, or about 6 minutes of main etch. Chapter 13 adds faceting, loading, and wafer-edge erosion to this budget and shows what happens as stacks get taller.

### 4.5.4 Mask Stress

The a-C mask carries strong compressive stress. Over the array, it is patterned into wide lines (1.8 µm between 0.2 µm slits), and wide lines are not prone to buckling. In narrow features, such as partial slits and select-gate cuts with narrow mask lines between them, fluorine uptake during the etch can swell the carbon and raise its compressive stress further. That can buckle narrow lines and make them wiggle. Chapter 11 covers wiggling.

---

## 4.6 Landing Chemistry

### 4.6.1 Stage 1: Stop on Poly-Si

As the main etch approaches the source stack, the recipe changes to a lower-oxygen, higher-polymer condition. Oxide and nitride still etch, because they release oxygen and nitrogen that help remove polymer. Polysilicon releases nothing to consume the polymer, so a thick film builds on it and its etch rate falls sharply:

```
Landing stage 1 (illustrative):
  Lower O₂ (or none); higher C₄F₆ fraction; similar ion energy
  ON rate at depth:          ≈ 0.25 µm/min
  Poly-Si rate at depth:     ≈ 0.015 µm/min
  ON : poly-Si selectivity:  ≈ 15–20
```

This stage must last long enough for the last regions of the wafer to clear the bottom of the stack. The early regions wait on the poly-Si. Chapter 12 sizes its duration and the poly-Si loss it causes.

### 4.6.2 Stage 2: Poly-Si and Liner Opening

The landing then has to go through 150 nm of poly-Si and a 10 nm oxide liner, and stop inside the 80 nm sacrificial layer:

```
Landing stage 2 options (illustrative):

  (a) Fluorine-rich breakthrough (NF₃ or CF₄ with Ar, some O₂)
      Etches poly-Si and oxide at comparable rates; ion-driven
      Timed; relies on the stage-1 stop having equalized the start
      Risk: lateral attack of the poly-Si under the stack if too
      chemical

  (b) Two-step: poly-Si etch selective to oxide (low-F, Br- or
      Cl-assisted chemistries), stopping on the 10 nm liner;
      then a short fluorocarbon oxide punch into the sacrificial layer
      More selective; slower at A ≈ 58; more steps
```

Option (a) is simpler and faster. Option (b) uses the thin liner as a second stop and lands more precisely. The choice depends on the landing window and on how uniform the stage-1 stop leaves the starting surface (Chapter 12).

### 4.6.3 Post-Etch Polymer and Mask Removal

After landing, the slit is lined with fluorocarbon polymer, and the remaining a-C mask is still in place. Both are removed by an oxygen-based ash (Book #20), often followed by a wet clean. The ash must:

- Remove polymer from the full depth of the slit, where oxygen transport is slow
- Not oxidize the exposed source-stack layers excessively
- Not leave fluorine on the sidewall that would attack the liner deposited next

Fluorine left in the slit is a quiet source of downstream trouble. Ashing at elevated temperature with some hydrogen or water vapor and a wet rinse are common countermeasures.

---

## 4.7 Summary & Key Takeaways

1. **Each gas has one main job.** C₄F₆ supplies polymer and mask selectivity. CH₂F₂ supplies hydrogen for nitride rate. O₂ trims polymer. Ar carries the ions. Small additives fine-tune passivation.

2. **Hydrogen sets the oxide/nitride balance; oxygen sets the polymer level.** The balance drifts with depth, because the neutral mix reaching the bottom changes.

3. **Sticking decides where protection forms.** Bow protection comes from moderately sticking fragments. High-sticking fragments threaten slit bottoms far more than hole bottoms.

4. **Effective mask selectivity is lower than open-field selectivity.** It equals the open-field value times the ratio of average to open-field rate. For the reference process, that is 10 × 0.59 ≈ 5.9, leaving about 0.9 µm of a 3.0 µm mask.

5. **Carbon mask density buys selectivity at the cost of stress and alignment.** Doped carbons go further but complicate the strip.

6. **Landing uses two chemistries.** A polymer-rich stage stops on poly-Si. A breakthrough stage opens the poly-Si and liner into the sacrificial layer. Afterward, the slit is ashed and cleaned of fluorine.

---

## Study Questions

1. Using the CH₂F₂ table in Section 4.3.2, interpolate the CH₂F₂ flow that gives an oxide/nitride ratio of exactly 1.0. Estimate ER_avg for the reference pair (25 nm oxide, 30 nm nitride) at that flow.

2. A recipe change raises open-field mask selectivity from 10 to 12 but lowers the average rate from 0.405 to 0.38 µm/min (open-field rate unchanged at 0.686 µm/min). Compute the new effective selectivity and the new main-etch mask loss for 11.5 µm. Is the change worth it for the mask budget?

3. A stack grows to 14.0 µm above the source. With the reference chemistry, the average rate through 14.0 µm falls to 0.37 µm/min. Compute the main-etch time, the mask loss, and the remaining a-C. What starting a-C thickness is needed to keep 0.5 µm at the end, with the same landing-stage loss?

4. During landing stage 1, the ON rate at the bottom is 0.25 µm/min and the poly-Si rate is 0.015 µm/min. The latest region reaches the poly-Si 52 s after the earliest. How much poly-Si does the earliest region lose while it waits? What fraction of the 150 nm stop is that?

5. Explain why a chemistry that gives no measurable polymer at the bottom of a channel hole might leave a significant film at the bottom of a slit at the same aspect ratio. Which gas flows would you change first, and in which part of the etch?

---

**Next Chapter:** [Chapter 5: Reactor Architecture for Deep Slit Etch](./05-reactor-architecture.md)

---

**Chapter 4 Development Status:** Complete  
**Version:** 1.0
