# Preface: The Etch That Divides

## Why This Book Exists

Most deep etches in a 3D NAND flow are holes. Channel holes, word-line contacts, and through-array vias are all round, and all are judged one hole at a time. The slit is different. It is a **trench**, a few hundred nanometres wide, more than ten microns deep, and millimetres long, and it must be good along its entire length. A slit that is perfect for 3.999 mm and bridged for 1 µm leaves two blocks shorted together. A slit that is straight at the wafer center and tilted by a quarter of a degree at the edge can graze the channel holes beside it and short a word line to the source.

Slit etch became a defining process of 3D NAND because of the **replacement-gate** architecture. The stack is deposited as alternating oxide and sacrificial nitride. Before the nitride can be swapped for tungsten or molybdenum word lines, something has to give the hot phosphoric acid a way in. Before the word lines can be separated from block to block, something has to cut them apart. Before the strings can return current to the source, something has to make a path down to it. The slit does all three, and in many designs it also becomes the common-source line. Every one of those jobs depends on the shape the etch leaves behind.

The method, a single long high-aspect-ratio dielectric etch through a carbon mask, looks simple. It asks a great deal of the plasma etch:

1. **Depth without slowdown.** The slit must reach a source layer 11–14 µm down. Etch rate falls as the trench deepens, because fewer radicals and fewer well-aimed ions reach the bottom. The recipe has to keep the bottom etching for half an hour.

2. **Straightness to a fraction of a degree.** At an 11.7 µm depth, a tilt of 0.1° moves the slit bottom 20 nm sideways. The clearance to the nearest channel hole is only 60–100 nm. Tilt is set mostly by the shape of the sheath at the wafer edge, which changes as the edge ring wears.

3. **A wide bottom.** Hot acid has to flow down the slit and remove nitride a micron sideways. Metal precursors have to diffuse down and fill every word-line cavity. Then the metal on the slit walls has to be etched back so neighboring word lines are separated. A slit that tapers or pinches near the bottom fails all three.

4. **A controlled landing.** The slit must open into the source stack, often into a sacrificial layer only tens of nanometres thick, without punching through it. Depth varies by several percent across the wafer, which is far more than the landing window. Only selectivity can close that gap.

5. **A mask that lasts.** A 3 µm carbon mask has to survive 25–40 minutes of kilovolt ion bombardment and still define the top of the slit at the end.

6. **A stack that moves.** The stack is under stress. Cutting it into long parallel walls releases that stress in one direction. Blocks lean, slits wiggle, and the wafer bends into a saddle that every later lithography layer has to correct for.

This book treats slit etch as a **precision high-aspect-ratio trench process in its own right**, not as a channel-hole recipe applied to a line.

---

## Unique Aspects of Slit Etch

### 1. A Trench Among Holes

The physics of high-aspect-ratio etch is usually taught with holes. A slot transmits neutrals far better than a hole of the same aspect ratio: about three times better at 60:1 for species that bounce, and around a hundred times better for species that stick on the first wall hit. Ions spread in only one direction across a slot instead of two. These differences change the balance between the radicals that etch, the polymer that protects, and the ions that drive the reaction. They also explain why a slit and a channel hole etched in the same chamber need different recipes.

### 2. Long-Range Continuity

A hole defect kills one string. A slit defect can kill a block or short two of them. Slit etch is judged by its worst point over millimetres of trench, so it must be robust against local disturbances: a particle on the mask, a local mask thin spot, a slit end or junction where the local geometry changes.

### 3. Clearance on Both Sides

A slit has channel holes on both sides. Bow widens it into both rows. Tilt moves it toward one row and away from the other. Wiggle moves it back and forth. Because the margin is shared, every profile error is spent from the same budget, and that budget is tens of nanometres.

### 4. The Etch Serves Wet and Deposition Steps

Unlike most etches, the most important customers of the slit are not electrical contacts but wet and deposition processes: nitride removal, metal deposition, metal recess, liner deposition, and fill. The bottom CD and the sidewall smoothness the etch leaves behind set how well those steps work.

### 5. Stress Changes the Geometry After the Etch

The geometry the etch produces is not the geometry the wafer keeps. When the slits open, the stack relaxes. Blocks can lean, and wafer bow changes shape. Slit etch is the step where the stack's stored mechanical energy is released, and the consequences show up in overlay several layers later.

---

## Why This Book Is Organized This Way

Book #24 follows the same four-part structure as Books #19–23:

**Part I: Fundamentals (Chapters 1–4)**
- Why slits exist, what they cut through and land on, the physics of deep trench etch, and the chemistry of the etch and its mask

**Part II: Hardware (Chapters 5–9)**
- The reactors, bias systems, gas and pressure control, temperature and chucks, and edge-sheath and conditioning strategies that let one chamber etch a straight 60:1 trench for half an hour

**Part III: Phenomena (Chapters 10–14)**
- Profile, tilt and stress-driven distortion, landing, mask budget and uniformity, and advanced slit schemes

**Part IV: Production (Chapters 15–16)**
- Endpoint, metrology, APC, the integration steps that use the slit, yield, and cost

### Reading Paths

**Process Engineers:** Chapters 3, 4, 7, 10, 12, 13  
→ Recipe design, profile control, landing, mask budget, uniformity

**Equipment Engineers:** Chapters 5–9, 15  
→ Reactor selection, bias systems, temperature and cryogenic control, edge sheath, endpoint hardware

**Integration Engineers:** Chapters 1, 2, 11, 12, 14, 16  
→ Slit layout, clearance budget, landing stack, stress, multi-deck schemes, downstream steps

**Device Engineers:** Chapters 1, 11, 16  
→ How slit errors become shorts, leakage, word-line resistance shifts, and dead blocks

**Researchers:** Chapters 3, 4, 6, 8, 10, 14  
→ Transport, charging, sidewall passivation, cryogenic chemistry, next-generation schemes

---

## Key Questions This Book Answers

1. **Why does a replacement-gate 3D NAND array need slits, and what sets their width and pitch?**
2. **Why does a slit etch faster and more evenly than a channel hole of the same aspect ratio, and where does that advantage run out?**
3. **What causes bowing, and how much bow can a slit afford before it reaches the channel holes?**
4. **Why do slits tilt at the wafer edge, and how do edge-ring wear and sheath tuning control it?**
5. **How does a slit land in a source layer tens of nanometres thick when the etch depth varies by hundreds of nanometres across the wafer?**
6. **How much carbon mask does a slit consume, and what limits the depth one mask can reach?**
7. **What happens to the stack and the wafer when the slits are cut, and how does it reach overlay?**
8. **How are slits made through two or three decks, and what changes at 300+ layers?**
9. **What does a slit cost per wafer, and how do etch rate, chamber count, and consumables trade against each other?**

---

## How to Read This Book

**Complete study (2–3 weeks):** Read Part I closely, then work through Parts II and III in order. Finish with Part IV.

**Focused study (3–5 days):** Read Chapters 1 and 3, then follow the reading path for your role.

**Reference mode:** Go straight to the chapter you need. Use the INDEX, GLOSSARY, and the Appendix G troubleshooting guide.

**Every chapter includes:**
- Learning objectives
- Quantitative models with worked numerical examples
- Representative production values, labelled as illustrative where appropriate
- Summary and key takeaways
- Study questions

**Appendices provide:**
- A: Stack, mask, and landing-layer material properties
- B: Etch chemistry and reaction data
- C: Standard operating procedures
- D: Process windows and lookup tables
- E: Slit geometry, transport, and clearance-budget calculations
- F: Endpoint and metrology reference
- G: Troubleshooting guide

---

## A Note on Data and Depth

The relationships in this book (ion-enhanced etching, fluorocarbon polymer chemistry, free-molecular transport, sheath physics, charging, thin-film stress mechanics, error budgets) are well established in the plasma etch literature. The specific numbers in recipes, tables, and worked examples are **representative**. They are chosen to be physically consistent and close to typical practice, but they are not qualified conditions for any particular tool, stack, or mask. Where a value is illustrative, the text says so and shows the arithmetic, so readers can repeat the analysis with their own measurements.

Throughout the book, a **reference process** ties the examples together:

```
Reference stack:    2 decks × 100 SiO₂/Si₃N₄ pairs (25 nm / 30 nm, p = 55 nm)
                    = 11.0 µm, plus 0.2 µm inter-deck oxide and 0.3 µm cap oxide
                    → 11.5 µm of dielectric above the source stack
Reference source:   150 nm n⁺ poly-Si (etch stop) / 10 nm SiO₂ /
                    80 nm sacrificial poly-Si / 10 nm SiO₂ / 200 nm n⁺ poly-Si
Reference slit:     top CD 200 nm, bottom CD ≥ 130 nm, depth D = 11.7 µm
                    (aspect ratio ≈ 58); slit pitch 2.0 µm
Reference clearance: 80 nm nominal from slit edge to nearest channel-hole edge
Reference mask:     3.0 µm amorphous carbon + 40 nm SiON cap
Reference etch:     CCP, 60 MHz source + 400 kHz bias; average ON rate 0.40 µm/min
```

We assume you know basic plasma physics and fluorocarbon dielectric etch from earlier books. We do **not** assume you know 3D NAND architecture, replacement-gate integration, slit layout, high-aspect-ratio trench transport, or stack stress mechanics.

---

## Organization of This Repository

1. **README.md**: overview, scope, file structure, cross-references
2. **PREFACE.md**: this document
3. **INDEX.md**: detailed chapter outline, reading paths, estimated times
4. **chapters/**: Chapters 1–16
5. **appendices/**: Appendices A–G
6. **GLOSSARY.md**: technical terminology

---

## Acknowledgments & Scope

Book #24 is part of the **ChipFoundryServices Technical Series**. It draws on:

- The published plasma etch literature on high-aspect-ratio dielectric etch, fluorocarbon chemistry, charging, and cryogenic etch
- Classical results on free-molecular flow through channels (Knudsen, Clausing)
- Published descriptions of 3D NAND architecture and replacement-gate integration
- Representative industrial practice for 3D NAND slit modules
- The earlier books in this series, especially Books #19 and #23

It is a **technical reference for professionals**. Background in plasma processing is assumed.

---

## Final Thought

A slit is one line on a layout and one step in a flow. It is also a trench eleven microns deep that must stay within a few tens of nanometres of where it was drawn for every micron of its length, at every point on the wafer, on every wafer of a fab's output.

Mastering slit etch means seeing that **the bottom sets the integration, the edge sets the yield, and the stack decides what the geometry becomes after the plasma is off**. This book is meant to build that understanding.

---

**Welcome to Book #24: 3D NAND Slit Etch — Gate-Line Slit Formation for Replacement-Gate 3D NAND.**

---

**Preface Version:** 1.0  
**Last Updated:** 2026-10-04
