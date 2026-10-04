# Glossary: 3D NAND Slit Etch

Terms are defined as they are used in this book. Chapter references point to the main discussion.

---

## A

**a-C (amorphous carbon) mask:** Thick PECVD carbon hard mask (reference 3.0 µm) that defines the slit. Denser and doped variants give higher selectivity with more stress. (Ch. 4.5, Ch. 13.1)

**ACS (array common source):** Conductor (W or doped poly-Si) inside an insulating spacer in the slit, contacting the source at the slit bottom. Used where the source is in the substrate. (Ch. 1.2.3, Ch. 16.3)

**Actinometry:** Ratio of an emission line to a nearby Ar line to track the relative density of a species (e.g., F 703.7 / Ar 750.4). (App. B.5.1)

**APC (advanced process control):** Feed-forward and feedback adjustment of recipe parameters (main-etch time, edge setting, mask-open trim) from upstream data and post-etch measurements. (Ch. 15.4–15.5)

**ARDE (aspect-ratio-dependent etching):** Decline of etch rate with aspect ratio, caused by reduced neutral and ion transmission to the feature bottom. (Ch. 3.4)

**Arrival map:** Map of the times at which different regions of the wafer and die reach the source stack. Its span sets the LS-1 overetch. (Ch. 12.5)

**Aspect ratio (A):** Depth divided by width, D/W_t. Reference ≈ 58. (Ch. 1.3)

---

## B

**Bad-block allowance:** Number of blocks per die that may fail and be mapped out at test (≈ 2%, illustrative). Slit bridges cost blocks, not die, within this allowance. (Ch. 9.6.3)

**Bias (LF bias):** Low-frequency RF (100 kHz–2 MHz) power on the wafer electrode that sets ion energy. (Ch. 5.2.2, Ch. 6)

**Block:** Group of strings between two full slits that share word-line plates and are erased together. (Ch. 1.1.1)

**Bottom CD (W_b):** Slit width at the bottom of the stack. Set by the downstream fill and recess (≥ 130 nm reference). (Ch. 10.3, Ch. 16.1.3)

**Bow:** Widening of the slit below its top, peaking 1–2 µm down, caused mainly by ions reflected from the mask facet. (Ch. 10.2)

**Breakthrough (LS-2):** Landing step that opens the poly-Si stop and liner into the sacrificial layer. Timed non-selective (LS-2a) or selective with a liner stop (LS-2b). (Ch. 12.3)

---

## C

**CD-SAXS:** Transmission small-angle X-ray scattering. Measures the average CD-versus-depth profile, bow, taper, and tilt of periodic arrays non-destructively. (Ch. 15.2)

**Charge exchange:** Ion–neutral collision that transfers charge, creating a slow ion inside the sheath. Broadens ion energy and angle distributions at higher pressure. (Ch. 7.1)

**Clausing factor:** Free-molecular transmission probability of a channel. Classical values for cylinders and parallel plates validate the Monte Carlo used here. (Ch. 3.2, App. E.3)

**Clearance (s):** Distance between the slit wall and the nearest channel-hole wall, nominal 80 nm at the top (reference). It must be checked at every depth. (Ch. 1.4)

**CN emission (388 nm):** Emission from nitride etching (and N-containing mask chemistry). Its decline marks regions reaching the poly-Si stop. (Ch. 15.1)

**Cryogenic etch:** HAR etch with the wafer at roughly −70 to −20 °C, using adsorbed etchants and condensed passivants instead of fluorocarbon polymer. Faster, with lower fluorocarbon use, and far more temperature-sensitive. (Ch. 8.5, Ch. 14.4)

**CuA (CMOS under array):** Architecture with logic under the memory array and a poly-Si source plate. The slit lands in a source stack above the CMOS. (Ch. 1.2.4, Ch. 2.4)

---

## D

**Deck:** Separately deposited and hole-etched portion of a multi-deck stack. (Ch. 14.1)

**Depth series:** Set of partial etches stopped at different depths to see how the profile evolves step by step. (Ch. 7.6.2, App. C.1)

**Die-level distortion:** Repeating in-plane displacement pattern within each die, caused by stress release in slit arrays but not in unslit periphery and staircase. (Ch. 11.4.2)

**Dog-leg tilt:** Slit whose tilt differs between depth ranges because the edge mismatch changes from step to step. (Ch. 11.1.4)

---

## E

**Edge ring (focus ring):** Si or SiC ring around the wafer that sets the sheath at the wafer edge. Its wear tilts edge slits. (Ch. 9.3)

**Effective selectivity:** Depth etched divided by mask lost over the whole etch. Equal to open-field selectivity times ER_avg/ER_open (≈ 5.9 reference). (Ch. 4.5.3)

**ESC (electrostatic chuck):** Clamps the wafer and removes heat through a helium backside gap. Multi-zone versions tune radial temperature. (Ch. 8)

**EWMA:** Exponentially weighted moving-average controller used for run-to-run feedback. (Ch. 15.5.1)

---

## F

**Facet:** Sloped surface eroded at the mask edge. Reflects ions toward the opposite wall and drives bow. (Ch. 10.2.1, Ch. 13.1.2)

**Feed-forward:** Setting a recipe parameter from measurements made before the etch, e.g., main-etch time from stack thickness. (Ch. 15.4)

**Finger:** Sub-region of a block between a full slit and a partial slit (or between partial slits). (Ch. 1.1.1, Ch. 14.2)

---

## G

**Gate-line slit (GLS):** Another name for the slit. Also called word-line cut. (Ch. 1)

---

## H

**H-cut:** Gap between segments of a partial slit, through which word lines of adjacent fingers stay connected. (Ch. 14.2)

**Hammerhead:** Local widening at a slit end that restores slot-like transport and reduces end lag. (Ch. 12.4.1)

**He leak rate:** Backside-helium leak per chuck zone. Reports wafer seating and shape change during the etch. (Ch. 8.4)

**HV-SEM:** High-landing-energy SEM (10–30 keV) that images slit bottoms through the dielectric to measure bottom CD and top-to-bottom offset. (Ch. 15.2)

---

## I

**IED (ion energy distribution):** Distribution of ion energies at the wafer. Broad and bimodal for low-frequency sinusoidal bias, narrow for tailored waveforms. (Ch. 6.2)

**Ion transmission (K_i):** Fraction of ions reaching the bottom without striking the wall. ≈ 1 − 0.80 A σ_θ for a slot. (Ch. 3.3.2)

---

## L

**Landing:** Ending the slit at the intended depth: inside the sacrificial layer (CuA replacement source) or a set depth into the substrate or plate. (Ch. 12)

**Line-of-sight flux:** Neutrals that reach the bottom without touching a wall. ≈ 1/(2A) for a slot, ≈ 1/(4A²) for a hole. (Ch. 3.2.4)

**LS-1 / LS-2:** Landing stage 1 (polymer-rich stop on poly-Si) and stage 2 (breakthrough). (Ch. 4.6, Ch. 12.2–12.3)

---

## M

**Main etch (ME-1, ME-2, ME-3):** Depth-targeted main-etch steps for bow control, rate, and bottom opening. (Ch. 7.3)

**Metal recess:** Etch that removes word-line metal from the slit walls and recesses it into each cavity, separating word lines. Inherits slit ARDE. (Ch. 16.1.4)

**Microtrenching:** Deeper etching at the bottom corners from ions reflected off the lower sidewalls. (Ch. 10.5.1)

---

## N

**Necking:** Narrowing of the slit opening by polymer deposited at the mask edge. (Ch. 4.4.2)

**Neutral transmission (K_n):** Fraction of neutrals entering a feature that reach its bottom. Slot ≈ (ln A + 0.15)/A; hole ≈ 1/(1 + 0.75A). (Ch. 3.2)

---

## O

**ON stack:** Alternating SiO₂/Si₃N₄ layers of a replacement-gate 3D NAND stack (reference 25/30 nm, p = 55 nm). (Ch. 2.1)

**Overetch:** Etch time beyond the earliest arrival at the stop, sized to let the latest regions arrive. (Ch. 12.2.2)

---

## P

**Partial slit:** Slit interrupted by H-cuts, giving acid and precursor access to the middle of a block while keeping word lines connected. (Ch. 14.2)

**Pulsing:** On/off or high/low modulation of bias or source power. Adds passivation and relieves charging, at some cost in bottom ion flux. (Ch. 6.4)

---

## R

**Replacement gate:** Flow in which sacrificial nitride is removed through the slit and replaced with W or Mo word lines. (Ch. 1.1.2, Ch. 16.1)

**Replacement source:** CuA flow in which a sacrificial layer in the source stack is removed through the slit, and doped poly-Si is deposited to contact the channel sidewall. (Ch. 1.2.4, Ch. 16.2)

**Residence time (τ):** pV/Q. Time a gas molecule spends in the plasma volume (≈ 10 ms reference). It affects fragmentation. (Ch. 5.4.1)

---

## S

**Sacrificial layer:** Layer in the source stack (reference 80 nm poly-Si) that is the landing target and is removed later. (Ch. 2.4, Ch. 12.1)

**Saddle (wafer shape):** Anisotropic bow after slit etch, from stress released across the slits but not along them. (Ch. 2.5.4, Ch. 11.4)

**Select-gate cut (SG cut, TSG/DSL cut):** Shallow trench that splits the drain-select gates without cutting word lines. A layer-counting etch. (Ch. 14.3)

**Sheath mismatch (Δ):** Difference in plasma-sheath boundary height over the ring and over the wafer. Drives edge tilt. (Ch. 9.1)

**Slit:** Long trench through the full stack that divides the array into blocks and provides access for replacement gate and source. (Ch. 1)

**Slit pitch (P_s):** Center-to-center distance between full slits (reference 2.0 µm). (Ch. 1.3.3)

**Staged chucking:** Chucking sequence that seats the wafer before helium is applied, so a bowed edge is not lifted. (Ch. 8.4.3)

**Staircase region:** Region at each array end where slits cut through staircase fill oxide as well as ON pairs. Usually the earliest-arriving region. (Ch. 2.1.3, Ch. 12.4.3)

**Sticking probability (s):** Probability that a neutral reacts or sticks on a wall hit. It sets where polymer deposits. (Ch. 3.2.4)

**Striation:** Sidewall ridges. Horizontal striation is level-by-level oxide/nitride recess. Vertical striation is mask-edge roughness carried down the wall. (Ch. 10.4)

**Synergy model:** 1/ER = 1/ER_n + 1/ER_i. Combines neutral-limited and ion-limited rates. (Ch. 3.1)

---

## T

**Tailored waveform:** Shaped bias voltage that holds the sheath at a nearly constant voltage, giving a narrow IED. (Ch. 6.3)

**Taper:** Steady narrowing with depth. 0.1° of extra taper costs ≈ 36 nm of bottom CD over 10 µm. (Ch. 10.3)

**Tilt (θ_t):** Inclination of the slit axis from the wafer normal. Mainly from the edge sheath. Only the component perpendicular to the slits costs clearance. (Ch. 9, Ch. 11.1)

**Tilt limit:** Maximum tilt that keeps clearance above s_min at every depth. Reference ≈ 0.29°, set at the lower-deck hole bow. Specified ≤ 0.25°. (Ch. 1.4.3)

**Two-step slit:** Slit made by etching and plugging a lower-deck slit, then etching an upper-deck slit onto the plug. Leaves an internal joint and ledges. (Ch. 14.1.3)

---

## V

**Virtual metrology:** Prediction of slit parameters for every wafer from in-situ and upstream data, trained on measured wafers. (Ch. 15.5.3)

**Voltage contrast (VC):** E-beam inspection that distinguishes slits electrically connected to the source (landed) from isolated ones. (Ch. 15.2.2)

---

## W

**WAC (waferless autoclean):** Plasma clean between wafers that resets wall polymer (O₂, with NF₃ for Si-containing deposits). (Ch. 9.5.2)

**Wiggle:** Long-wavelength lateral wandering of the slit centerline along its length. (Ch. 11.2)

**Word line (WL):** Horizontal metal plate at one level of a block, formed by replacement gate. Separated from the next block by the slit. (Ch. 1.1)

---

**Glossary Version:** 1.0  
**Last Updated:** 2026-10-04
