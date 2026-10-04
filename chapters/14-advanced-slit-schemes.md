# Chapter 14: Advanced Slits — Multi-Deck, Partial Slits, Select-Gate Cuts & Cryo

## Overview

The reference slit in this book is a single, continuous trench etched in one pass through a two-deck stack. Real products add complications. Stacks of three decks and 300+ layers push the aspect ratio toward 100. Blocks are subdivided by **partial slits**, which interrupt the trench to keep word lines connected, and by shallow **select-gate cuts**, which split the top select gates without touching the word lines. Bonded-wafer architectures change what the slit lands on. And at the deepest stacks, new etch technologies, cryogenic etch above all, compete with brute-force scaling of today's recipes.

This chapter covers each of these schemes: what it is for, what it asks of the etch, and the trade-offs that decide when it is used.

**Learning Objectives:**
- Compare single-pass and two-step slit schemes for multi-deck stacks
- Compute the overlay requirement and inner ledge of a two-step slit
- Explain the purpose of partial slits and the etch risks at their ends and gaps
- Describe the select-gate cut and its layer-counting landing requirement
- Estimate how tilt and taper budgets shrink at 300+ layers
- Weigh cryogenic etch, mask changes, and scheme changes for future slits

---

## 14.1 Slits Through Multi-Deck Stacks

### 14.1.1 Why Decks Exist

Channel holes cannot be etched through an arbitrarily tall stack in one pass. Multi-deck stacks are built in sections: the lower deck is deposited and its holes etched and filled with sacrificial material, then the upper deck is deposited and its holes are aligned to the lower ones. Slits face the same question: one etch through everything, or one per deck?

### 14.1.2 Scheme A: Single-Pass Slit

```
Single-pass slit (reference process):

  ┃       ┃   upper deck
  ┃       ┃
  ┃       ┃   inter-deck oxide
  ┃       ┃
  ┃       ┃   lower deck
  ┗━━━━━━━┛   source stack

One mask, one etch, after both decks (and staircases) are complete.
```

```
Advantages                              Disadvantages
──────────────────────────────────────────────────────────────────────
One lithography and one etch            Aspect ratio grows with total
                                        stack (58 → ~80–100 at 3 decks)
No internal joint in the slit           Mask budget and taper grow faster
                                        than depth (Chapter 13)
Straight, continuous sidewall for       Tilt displacement grows with depth;
liner and fill                          tilt budget set at lower-deck bow
                                        (Chapter 1)
Stress released once                    Long etch time per wafer
```

### 14.1.3 Scheme B: Two-Step Slit

```
Two-step slit:

  Step 1 (after lower deck):
    ┃     ┃     lower-deck slit etched (AR ≈ 30)
    ┃▓▓▓▓▓┃     filled with sacrificial material (e.g., poly-Si or
    ┗━━━━━┛     carbon), planarized

  Step 2 (after upper deck):
     ┃   ┃      upper-deck slit etched (AR ≈ 30), landing on the
     ┃   ┃      sacrificial plug
    ┃▓▓▓▓▓┃     sacrificial plug removed through the upper slit
    ┗━━━━━┛

Result: a slit with an internal joint where the two halves meet
```

```
Advantages                              Disadvantages
──────────────────────────────────────────────────────────────────────
Each etch at AR ≈ 30: faster, less      Two masks, two etches, plug fill,
taper, more mask margin                 planarization, and plug removal
Tilt displacement halved per etch       Deck-to-deck overlay error between
                                        the two slit halves
Each etch lands on a well-defined       Internal ledge where widths differ;
target (plug or source)                 residue trap; liner and metal
                                        recess must handle a step
Shares joint strategy with channel      Plug removal at full depth is its
holes                                   own HAR process
```

### 14.1.4 The Joint

The upper slit's bottom must land fully on the lower slit's plug. Any overlay error or width mismatch creates a ledge inside the finished slit:

```
Joint condition:
  W_upper,bottom + 2 · OL_3σ ≤ W_lower,top

Example: W_lower,top = 220 nm, W_upper,bottom = 150 nm
  OL_3σ ≤ (220 − 150) / 2 = 35 nm

Ledge width on each side (zero overlay error):
  (220 − 150) / 2 = 35 nm

With 20 nm overlay error: ledges of 15 nm on one side and 55 nm on
the other
```

```
Joint cross-section (exaggerated):

     ┃     ┃    upper slit (tapered, bottom 150 nm)
     ┃     ┃
   ━━┛     ┗━━  ← ledges, 35 nm each side
  ┃           ┃ lower slit (top 220 nm)
  ┃           ┃
```

A ledge faces upward. During the later steps, it collects residue, shadows the liner below it, and creates a local metal recess problem, since metal on the ledge is hidden from a directional recess. Joint design widens the lower slit's top (so the upper bottom always lands within it) while keeping the ledge narrow enough for conformal processes to handle. Two-step slits trade the single-pass slit's depth problem for a joint problem.

### 14.1.5 Choosing

```
Factor                                   Favors
──────────────────────────────────────────────────────────────────────
Total AR < ~70 with available tools      Single pass
Cryogenic or very high-rate etch         Single pass
available
Total AR > ~80–90; taper or mask limits  Two-step (or more)
reached
Tight downstream liner/recess margins    Single pass (no ledge)
Strong deck-to-deck overlay capability   Two-step becomes viable
```

Both schemes are in use. The trend has been to keep single-pass slits as long as etch capability allows, because each extra step and joint adds cost and defect risk.

---

## 14.2 Partial Slits

### 14.2.1 Purpose

Wider blocks (more hole rows between full slits) save area (Chapter 1, Section 1.3.3), but they make nitride removal and metal fill longer. A common compromise splits each block into **fingers** with partial slits. A partial slit runs along the block like a full slit, but it is interrupted at intervals. Through the interruptions, the word-line plates of neighboring fingers stay connected, so the fingers share word lines and form one erase block:

```
Plan view (two fingers in one block):

  ════════════════════════════════════════════════   full slit
   ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○     finger 1
  ══════════════   ═════════════════   ═══════════   partial slit
                 ↑                   ↑                (gaps = "H-cuts":
   ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○        word lines connect
  ════════════════════════════════════════════════     across them)
                                                     full slit
```

The partial slit gives acid and metal precursors access to the middle of the block. The gaps keep the word lines continuous.

### 14.2.2 Etch Concerns

```
Concern                          Cause                              Remedy
─────────────────────────────────────────────────────────────────────────────────
Slit-end lag and recession at    Hole-like transport and charging   Hammerheads; end
depth (Chapter 12, Section       at every gap                       OPC; landing sized
12.4.1)                                                             for ends
Gap narrowing at the top         Line-end pull-in in lithography    Gap width rules;
                                 or a-C open; or end bowing         end OPC
Gap widening at depth            Ends recede with depth             Accept; size gaps
                                                                    for top
End bending                      Asymmetric charging at each end    Pulsing (Chapter 6);
                                                                    end geometry
Wiggle at the gap                Narrow mask features near the      Avoid narrow mask
                                 ends                               lines (Chapter 11)
Different landing from main      More ends per unit length          Arrival map includes
slits                                                               partial-slit ends
```

### 14.2.3 The Gap Must Survive

The gap between two partial-slit segments is what keeps the word lines connected. If the segments' ends grow toward each other, by bowing or by poor end definition, the remaining stack in the gap narrows. After nitride removal and metal fill, the word line passes through that remaining width:

```
Gap budget (illustrative):
  Drawn gap:                          1.0 µm
  End pull-back in litho/open:        +0.05 µm per end (gap grows)
  End bowing near the top:            −0.03 µm per end
  End recession at depth:             +0.05–0.10 µm per end (gap grows)

  Narrowest gap: near the top, ≈ 1.0 + 2 × (0.05 − 0.03) = 1.04 µm
```

The gap is usually wide enough that it does not close. The more subtle risk is that the metal fill through a gap with tapered, irregular end walls is uneven, which raises word-line resistance across the gap. Gap design is shared between layout and etch.

---

## 14.3 Select-Gate Cuts

### 14.3.1 Purpose

Each finger or block contains several rows of strings. To select one group of strings for reading or programming, the drain-side select gates at the top of the stack are split by a shallow trench that cuts only the top few layers. This is the **select-gate cut**, also called the top-select-gate (TSG) or drain-select-level (DSL) cut. It runs parallel to the slits, often through a row of dummy channel holes, and it must not cut any word line:

```
Cross-section (perpendicular to the slits):

   full slit        select-gate cut            full slit
     ┃               ┌─┐                          ┃
     ┃  SGD layers   │ │ ← cut through SGD only   ┃
     ┃  (e.g., 4)    └─┘                          ┃
     ┃  ───────────────────── top word line ───── ┃  ← must NOT be cut
     ┃  word lines ...                            ┃
```

### 14.3.2 What It Asks of the Etch

```
Requirement                       Detail (illustrative)
──────────────────────────────────────────────────────────────────────
Depth: through all SGD layers     e.g., 4 nitride layers + their oxides
                                  ≈ 4 × 55 nm + cap ≈ 0.4–0.6 µm
Stop above the top dummy or word  Landing window ≈ one oxide layer
line                              (25 nm) plus the dummy-layer margin
Narrow width                      50–120 nm (it costs array area)
Straight, continuous              Any bridge leaves SGDs connected
                                  between string groups
```

The landing problem is the staircase's problem in miniature (Book #23). The etch must count layers. Practical select-gate-cut etches use alternating oxide- and nitride-selective steps, or a non-selective etch with optical-emission layer counting (Chapter 15), and land on an oxide that sits between the last select-gate nitride and the first dummy or word-line nitride. Thicker oxide at that interface widens the window and is a common design choice.

### 14.3.3 Narrow-Feature Risks

```
Risk                              Why
──────────────────────────────────────────────────────────────────────
Mask-line buckling / wiggle       Narrow features with narrow mask lines
                                  nearby (Chapter 11, Section 11.2.3)
Microloading vs. main slits       Very different width and depth
Ordering with the slit etch       Usually etched and filled before the
                                  slit; the slit etch then crosses the
                                  filled cut at the array ends, which is a
                                  junction (Chapter 12, Section 12.4.2)
```

---

## 14.4 Slits at 300+ Layers

### 14.4.1 What Gets Harder

```
Example: 3 decks × 110 pairs at 50 nm pitch = 16.5 µm, plus 0.8 µm of
cap, inter-deck, and landing layers → depth ≈ 17.3 µm
Top CD 200 nm → AR ≈ 87

Budget item                    Reference (11.7 µm)     300+ example (17.3 µm)
────────────────────────────────────────────────────────────────────────────────
Tilt displacement at 0.25°     51 nm at bottom          75 nm at bottom
Taper for same bottom CD       0.28°                    ~0.18°
(100 nm total loss below bow)
Mask (a-C) needed               ≈ 2.6 µm                 ≈ 4.2 µm (Ch. 13 model)
Main etch time                  28.4 min                 ~50 min
Radial arrival spread (3%)      345 nm                   ~500 nm
```

Every budget in this book tightens. Tilt displacement at a given angle grows in proportion to depth, so the tilt specification must tighten in inverse proportion: about 0.17° to keep the reference 51 nm. Taper must fall by a third. The mask must grow by more than half, or the chemistry must become more selective.

### 14.4.2 Routes Forward

```
Route                               What it buys                  Cost / risk
───────────────────────────────────────────────────────────────────────────────────
Cryogenic etch (Chapter 8,          ~1.5–2.5× rate; less bottom   New hardware; tight
Section 8.5)                        polymer; better mask          temperature control;
                                    selectivity reported          condensation
Tailored-waveform bias              More yield per watt; less     New power supplies;
(Chapter 6)                         slow-ion bow                  recipe transfer
Denser or doped carbon masks        Higher selectivity            Stress, alignment,
                                                                  strip
Two-step slits (Section 14.1.3)     AR halved per etch            Masks, joint, plug
Wider slits                         Lower AR                      Array area
                                                                  (Chapter 1)
Edge sheath control with finer      Tighter tilt                  Hardware complexity
tuning (per step)
```

No single route is sufficient. Products at 300+ layers combine several: a more selective mask, high-energy tailored bias or cryogenic chemistry, finer edge control, and, where depth still exceeds capability, a split slit.

### 14.4.3 Word-Line Metal and the Slit

The move from tungsten to molybdenum word lines changes what the slit must deliver downstream. Molybdenum can be deposited without the thick titanium nitride barrier used for tungsten, so each word-line cavity is filled with more conductor, and the metal on the slit walls is a different material for the recess step. The slit etch's job is unchanged (open, straight, wide at the bottom), but the bottom-CD requirement is set by the new fill and recess processes, and it should be re-derived rather than carried over (Chapter 16).

### 14.4.4 Bonded Architectures

In wafer-bonded designs, the memory array is built on one wafer and the CMOS on another, and the two are bonded face to face. The array wafer's substrate can be thinned from the back, and the source can be formed from the backside. The slit may then land in the array wafer's substrate (architecture (a) of Chapter 2) rather than in a replacement-source stack, and the landing window widens. The slit etch is otherwise the same, but the downstream use of the slit as a source path may change.

---

## 14.5 Summary & Key Takeaways

1. **Multi-deck stacks raise the slit question: one pass or two.** Single-pass slits avoid joints but face AR 80–100. Two-step slits halve the AR at the cost of masks, plug fill and removal, and an internal joint.

2. **The joint costs a ledge.** The upper slit's bottom must land within the lower slit's top with overlay margin. The resulting ledges complicate liners and metal recess.

3. **Partial slits give access while keeping word lines connected.** Their many ends bring slit-end ARDE, bending, and gap-definition problems into the main array.

4. **Select-gate cuts are shallow layer-counting etches.** They must cut every select-gate layer and stop before the first word line, much like a single staircase step.

5. **Every budget tightens with depth.** At ~17 µm, tilt must tighten to about 0.17°, taper by a third, and the mask must grow by more than half.

6. **The future is a combination.** Cryogenic or tailored-bias etch, more selective masks, finer edge control, and split slits together extend single-module slit etch.

---

## Study Questions

1. A two-step slit has a lower-slit top CD of 230 nm and an upper-slit bottom CD of 160 nm. What deck-to-deck overlay (3σ) can it tolerate? With 25 nm of overlay error, what are the ledge widths on each side?

2. Compare the main-etch times of a single-pass slit through 17.3 µm and two 8.7 µm slits, using the time-to-depth values in Chapter 3 (extrapolate as needed). Add 15 minutes for plug fill, planarization, and plug removal, expressed as equivalent chamber time. Which scheme uses less etch-chamber time?

3. A partial slit has a drawn gap of 0.8 µm. Ends bow by 40 nm each near the top and recede by 80 nm each at depth. What is the narrowest and widest gap? Where in depth is each found?

4. A select-gate cut must cut through 4 SGD nitride layers (30 nm each) with 25 nm oxides between them and a 300 nm cap above, and stop in a 45 nm oxide above the first dummy word line. If the etch rate varies by ±4% across the wafer, can a timed etch land in the 45 nm oxide? What would you use instead?

5. For the 300+ layer example, the tilt budget at the bottom is to be kept at 51 nm. What tilt specification does this imply? Using the edge-sheath model of Chapter 9, what ring mismatch at 3 mm from the edge corresponds to that tilt?

---

**Next Chapter:** [Chapter 15: Endpoint, Metrology & Advanced Process Control](./15-endpoint-metrology-apc.md)

---

**Chapter 14 Development Status:** Complete  
**Version:** 1.0
