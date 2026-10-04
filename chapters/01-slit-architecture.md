# Chapter 1: Replacement-Gate 3D NAND & the Role of the Slit

## Overview

A 3D NAND array is a forest of vertical channel holes threaded through a tall stack of horizontal word-line plates. In the dominant **replacement-gate** architecture, those plates are not deposited as metal. The stack is built from alternating silicon oxide and silicon nitride, the channel holes are etched and filled, and only then is the nitride removed and replaced with tungsten or molybdenum. That swap is impossible unless there is a way into the middle of the stack. The **slit** provides it.

A slit is a long, narrow trench cut through the full stack, from the top cap down into the source layer beneath the array. Slits run parallel to the word lines across the whole array, and they divide the array into **blocks**: groups of strings that share a set of word-line plates and are erased together. Through the slit, acid removes nitride, metal precursors fill the cavities, and an etchback separates the metal of one block from the next. Afterward, the slit is lined and filled. In many designs it becomes the common-source line.

This chapter explains why the array needs slits, what each of their jobs demands of the etch, how slit width and pitch are chosen, and how the clearance between a slit and its neighboring channel holes is budgeted. It ends with a specification sheet that frames the rest of the book.

**Learning Objectives:**
- Explain the replacement-gate flow and why it needs an access trench through the stack
- List the four jobs of a slit and the etch requirement each one creates
- Define slit top CD, bottom CD, depth, aspect ratio, pitch, and clearance
- Compute slit area overhead and lateral nitride-removal distance for a given layout
- Build a depth-resolved clearance budget and derive a tilt limit from it
- Place slit etch in the 3D NAND process flow and state its key specifications

---

## 1.1 The Replacement-Gate Array

### 1.1.1 Strings, Plates, and Blocks

In vertical NAND, each memory string is a vertical polysilicon channel inside a channel hole. The hole is lined from outside in with a blocking oxide, a silicon nitride charge-trap layer, a tunnel oxide, and the polysilicon channel, with an oxide core in the middle. Every word-line plate the hole passes through forms one memory cell with it.

```
Plan view of part of an array (simplified):

   slit          block (finger) n           slit        block n+1
  ═══════  ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○  ═══════  ○ ○ ○ ○ ○ ○ ○ ○
  ═══════   ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○   ═══════   ○ ○ ○ ○ ○ ○ ○
  ═══════  ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○  ═══════  ○ ○ ○ ○ ○ ○ ○ ○
     ▲      ◄──── rows of channel holes ────►   ▲
     │      (staggered, many rows deep)          │
  word lines run left–right; slits run left–right too, separating blocks
  bit lines run top–bottom (perpendicular to slits)
```

In the vertical direction, a block is a stack of word-line plates, each a continuous metal sheet perforated by every channel hole in the block. Slits bound the block on both sides along the bit-line direction. In the word-line direction, the block runs across the whole array to the staircases at its ends (Book #23).

Some vendors call the region between two slits a **finger** and group several fingers into an erase block. This book uses "block" for the region between two adjacent full slits unless the distinction matters (Chapter 14 covers partial slits and fingers).

### 1.1.2 The Replacement-Gate Sequence

```
Replacement-gate module (simplified):

  (a) As deposited            (b) Slit etched           (c) Nitride removed
      O N O N O N O               O N O ║ O N O             O   O ║ O   O
      ════════════                ══════║══════             ══  ══║══  ══
      ○ hole  ○ hole              ○     ║     ○             ○ cavities ○
                                        ║                     (oxide shelves
                                     slit                      held by holes)

  (d) Metal fill (ALD W/Mo)   (e) Metal recess          (f) Slit liner + fill
      O W O W ║ W O W O           O W O W │ │W O W O        O W O W │█│W O W O
      W also coats slit walls     metal removed from         oxide spacer, then
      and bottom                  slit walls; plates         conductor (common
                                  separated vertically       source) or oxide
```

Each step after (b) depends on the slit:

- **(c)** Hot phosphoric acid (≈160 °C) enters through the slit and etches nitride laterally, leaving oxide shelves held up by the channel holes.
- **(d)** Metal precursors diffuse down the slit and laterally into every cavity. The metal coats the slit walls too.
- **(e)** An etchback removes metal from the slit walls and recesses it a little into each plate, so no plate is shorted to the one above or below it.
- **(f)** The slit is lined with oxide and filled with a conductor or with oxide.

### 1.1.3 Why Not Deposit Metal Directly?

Gate-first stacks of oxide and polysilicon avoid replacement but give word lines with far higher resistance and complicate the charge-trap stack. Stacks containing tungsten from the start cannot be etched cleanly by the high-aspect-ratio channel-hole etch. Replacement gate lets the hole etch cut through two dielectrics and still produce metal word lines. The slit is the price of that choice.

---

## 1.2 The Four Jobs of a Slit

### 1.2.1 Job 1: Access for Replacement Gate

Nitride removal is a lateral wet etch. From each slit, the acid has to remove nitride up to the midline of the block, where it meets the etch front from the slit on the other side:

```
Lateral removal distance:

  d_lat = (P_s − W_slit) / 2

where P_s     = slit pitch
      W_slit  = slit width at the layer in question

Reference process: P_s = 2.0 µm, W_slit ≈ 0.2 µm (top), 0.13 µm (bottom)
  d_lat ≈ (2.0 − 0.2)/2 = 0.90 µm near the top
  d_lat ≈ (2.0 − 0.13)/2 = 0.94 µm near the bottom
```

Acid and dissolved silica have to move up and down the slit for the whole etch. A slit that is narrow at the bottom slows the exchange there, and silica can redeposit on the oxide shelves. **Requirement: a wide, open bottom.**

### 1.2.2 Job 2: Block Isolation

Word lines in different blocks must be electrically separate, because each block is selected and erased independently. The slit, once lined and filled, is the only thing between the plates of block *n* and block *n+1*. A bridge anywhere along its length, from an unetched spot, a particle, or a pinched bottom that the metal fill seals, shorts every plate it touches. **Requirement: a complete, continuous etch to full depth along the entire slit.**

### 1.2.3 Job 3: Common-Source Line

In flows where the source is a doped region of the substrate (non-CuA), the slit is filled with an insulating spacer and a conductor (tungsten or doped polysilicon) that contacts the source at the slit bottom. This **array common source (ACS)** carries read and program current for every string in the block. Its resistance depends on the conductor cross-section, so the slit's width over its full depth matters. **Requirement: enough width at every depth to hold spacer plus conductor.**

### 1.2.4 Job 4: Source Access in CuA Flows

In CMOS-under-array designs, the strings sit on a polysilicon source plate above the logic, not on the substrate. A common way to connect the channel to that plate is a **replacement source**: a sacrificial layer inside the source stack is removed through the slit, the charge-trap layers at the bottom of each channel are stripped from the side, and doped polysilicon is deposited to contact the channel sidewall. The slit must land precisely in the sacrificial layer (Chapter 12). **Requirement: an exact landing in a layer tens of nanometres thick.**

```
Job                       What it demands of the etch
──────────────────────────────────────────────────────────────────────────
Replacement-gate access   Open bottom; bottom CD large enough for wet
                          exchange and metal precursor transport
Block isolation           Full depth everywhere; no bridges; no pinch
Common-source line        Width at all depths; clean bottom contact
Source access (CuA)       Landing inside a thin sacrificial layer; no
                          punch-through
All of them               Straight walls clear of the channel holes
```

---

## 1.3 Slit Geometry

### 1.3.1 Definitions

```
Symbol     Name                      Typical (illustrative)
──────────────────────────────────────────────────────────────────────────
W_t        Top CD (at stack top)     150–250 nm (reference: 200 nm)
W_bow      Maximum CD (bow)          W_t + 10–40 nm
z_bow      Depth of maximum CD       1–2 µm below the top
W_b        Bottom CD                 100–170 nm (reference: ≥ 130 nm)
D          Etch depth                8–15 µm (reference: 11.7 µm)
AR         Aspect ratio D/W_t        40–80 (reference: 58)
P_s        Slit pitch                1.5–4 µm (reference: 2.0 µm)
L_s        Slit length               mm (full array plus staircases)
s          Slit-to-hole clearance    50–120 nm nominal at top
                                     (reference: 80 nm)
θ_t        Tilt from vertical        < 0.1° center; up to ~0.3° edge
```

### 1.3.2 Aspect Ratio Across Generations

```
Generation (approx.)  WL layers  Total pairs  Stack     Slit depth  Top CD   AR
──────────────────────────────────────────────────────────────────────────────────
Early mainstream      48–64      ~60–75       3.5–4 µm  ~4.5 µm     ~250 nm  ~18
Mid generations       96–128     ~110–140     6–7.5 µm  ~7.5 µm     ~220 nm  ~35
Recent                176–236    ~190–250     10–13 µm  ~11–14 µm   ~200 nm  ~55–70
Leading edge          280–330+   ~300–350     14–17 µm  ~15–18 µm   ~180 nm  ~80–100

(Illustrative. Thinner pairs at later generations partly offset the
 layer count. Multi-deck stacks may etch the slit in one pass or in
 steps; Chapter 14.)
```

The aspect ratio of the slit rises roughly in proportion to layer count, because the slit width cannot shrink much. It has to stay wide enough for the downstream steps described in Section 1.2.

### 1.3.3 Pitch, Rows, and Area Overhead

The space between two slits holds the channel holes of one block. With staggered holes on a hexagonal pattern of nearest-neighbor pitch *a*, rows sit *a*·√3/2 apart:

```
Reference hole pattern: hole top CD d_h = 120 nm, nearest-neighbor
pitch a = 160 nm, row spacing a·√3/2 = 139 nm

Width occupied by n rows:  (n − 1)·139 + 120 nm
  n = 12:  11 × 139 + 120 = 1649 nm ≈ 1.64 µm

Slit pitch = rows + slit + 2 clearances
  P_s = 1.64 + 0.20 + 2 × 0.08 = 2.00 µm
```

Everything that is not channel holes is overhead:

```
f_slit = (W_t + 2s) / P_s

Reference: (0.20 + 0.16) / 2.00 = 18%

At P_s = 3.0 µm (≈19 rows):  0.36 / 3.0 = 12%
At P_s = 1.4 µm (≈ 8 rows):  0.36 / 1.4 = 26%
```

Wider pitch reduces overhead, so it is tempting. But a wider pitch means a longer lateral nitride removal, a longer metal fill path with more risk of voids, longer shelves for the remaining oxide to support, and a larger block to erase at once. The pitch is an integration compromise. **The etch's contribution to the compromise is the clearance *s*.** Every nanometre of clearance the etch can give back, through less bow, less tilt, and less wiggle, can be turned into a narrower slit pitch or more rows of holes.

```
Value of clearance (reference layout):
  Reducing s from 80 to 60 nm saves 2 × 20 = 40 nm per pitch
  Area gain = 40 / 2000 = 2.0% of array area
```

---

## 1.4 The Clearance Budget

### 1.4.1 Clearance at Depth

The nominal clearance is defined at the top of the stack. What matters is the clearance at every depth, between the slit wall and the wall of the nearest channel hole. Both features have profiles. Both can be displaced:

```
s(z) = s_nom − ΔW_slit(z)/2 − Δr_hole(z) − z·tan θ_t − δ_rand

where ΔW_slit(z) = W_slit(z) − W_t      (slit widening; negative when narrower)
      Δr_hole(z) = r_hole(z) − r_hole,top (hole widening on one side)
      θ_t        = slit tilt toward the hole row
      δ_rand     = random terms combined in quadrature:
                   slit-to-hole overlay, slit wiggle, deck-to-deck
                   hole overlay
```

The minimum allowed clearance comes from what fills the space later. After metal fill, the metal is recessed back from the slit wall (Section 1.1.2, step e). The outermost hole still needs gate metal on its slit side:

```
s_min = lateral metal recess + minimum gate metal at outer hole
      ≈ 20 nm + 10 nm = 30 nm   (illustrative)
```

### 1.4.2 Worked Example: Reference Process at Wafer Center

Profiles (illustrative):

```
Slit:  W_t = 200 nm; maximum 230 nm at z = 1.5 µm; tapering linearly
       to 130 nm at D = 11.7 µm
       W(z) for z > 1.5 µm:  230 − 100 × (z − 1.5)/10.2  nm
Holes: two decks, each 5.5 µm of pairs
       Upper-deck hole: 120 nm top, 140 nm max at 1.5 µm, 70 nm bottom
       Lower-deck hole: 120 nm top at z ≈ 6.0 µm, 140 nm max at z ≈ 7.2 µm,
       70 nm bottom at z ≈ 11.5 µm
Random: overlay 12 nm, wiggle 5 nm, deck-to-deck hole overlay 10 nm (3σ)
  δ_rand = √(12² + 5² + 10²) = 16.4 nm
```

Check three depths with zero tilt:

```
Depth            ΔW_slit/2       Δr_hole     s(z) (θ_t = 0)
───────────────────────────────────────────────────────────────────────
Upper bow 1.5 µm  +15 nm          +10 nm      80 − 15 − 10 − 16.4 = 38.6 nm
Lower bow 7.2 µm  W = 174 nm      +10 nm      80 + 13 − 10 − 16.4 = 66.6 nm
                  → −13 nm
Bottom 11.5 µm    W = 132 nm      −25 nm      80 + 34 + 25 − 16.4 = 122.6 nm
                  → −34 nm
```

At wafer center, the critical depth is the **upper-deck bow**, where both slit and hole are at their widest. The margin over s_min is 8.6 nm. Bow is the term to control there.

### 1.4.3 The Tilt Limit

Tilt costs nothing at the top and grows with depth. The allowed tilt at each depth is the clearance margin divided by the depth:

```
tan θ_max(z) = [s(z)|θ=0 − s_min] / z

Upper bow:  (38.6 − 30) / 1.5 µm  = 8.6 / 1500   → θ_max = 0.33°
Lower bow:  (66.6 − 30) / 7.2 µm  = 36.6 / 7200  → θ_max = 0.29°
Bottom:     (122.6 − 30) / 11.5 µm = 92.6 / 11500 → θ_max = 0.46°
```

The tilt limit is set at the **lower-deck bow depth**, not at the bottom. There the lower-deck hole is wide again and the slit has not yet narrowed much. For the reference process, tilt must stay below about 0.29° everywhere on the wafer, including the extreme edge. A practical specification leaves margin: **≤ 0.25° at the 3σ edge**. Chapter 9 shows that edge-ring wear alone can move the edge tilt by this much, which is why tilt sets ring life.

### 1.4.4 Lessons From the Budget

```
Lever                              Clearance gained (reference)
─────────────────────────────────────────────────────────────────────
Reduce slit bow by 10 nm CD        +5 nm at upper bow
Reduce tilt by 0.1° at the edge    +12.6 nm at lower bow
Reduce overlay 3σ from 12 to 8 nm  δ_rand 16.4 → 13.7 nm: +2.7 nm
Move bow deeper (2.5 µm)           Bow no longer coincides with hole
                                   bow peak; gain depends on profiles
```

Bow control buys margin at wafer center. Tilt control buys margin at the edge. Most yield loss from slit-to-hole proximity occurs at the wafer edge, so tilt is usually the more valuable lever.

---

## 1.5 Where the Slit Sits

### 1.5.1 On the Die

```
Plan view of one plane (simplified):

  ┌──────┬───────────────────────────────────────────┬──────┐
  │stair │═══════════════════════════════════════════│stair │ ← slit
  │case  │  block 0                                  │case  │
  │      │═══════════════════════════════════════════│      │ ← slit
  │      │  block 1                                  │      │
  │      │═══════════════════════════════════════════│      │ ← slit
  │      │   ...                                     │      │
  └──────┴───────────────────────────────────────────┴──────┘
   Slits cross the array AND the staircases, so each block's
   word lines are separated all the way to their contacts.
```

Slits run through two very different regions. In the **array**, they cut through ON pairs between channel holes. In the **staircase**, they cut through a mix of ON pairs and thick staircase fill oxide, whose thickness changes from step to step (Book #23). The etch rate, the polymer balance, and the landing differ between the two (Chapter 12).

### 1.5.2 In the Process Flow

```
Representative replacement-gate CuA flow (two decks):

  1. CMOS periphery, interconnect, and poly-Si source stack  (Chapter 2)
  2. Lower-deck ON stack; lower channel-hole etch; sacrificial fill
  3. Inter-deck layer; upper-deck ON stack; upper channel-hole etch
  4. Remove sacrificial fill; channel-hole films; poly channel; core
  5. Staircase etch, staircase fill, CMP                     (Book #23)
  6. Select-gate cut (shallow)                               (Chapter 14)
  7. SLIT ETCH through both decks, landing in source stack   ← this book
  8. Slit liner; replacement source through slit (CuA flows)  (Chapter 16)
  9. Nitride removal (hot H₃PO₄) through slit
 10. Blocking film and metal word-line fill (W or Mo ALD)
 11. Metal recess from slit walls (word-line separation)
 12. Slit spacer and fill (conductor or dielectric)
 13. Word-line contacts on the staircase; bit-line contacts; BEOL

(Order varies by vendor. Some flows etch the slit in two parts,
 one per deck; Chapter 14.)
```

Note what the slit etches: **the stack before replacement**. All the word-line levels are still oxide and nitride, so the etch sees only two dielectrics through most of its depth. The channel holes are already filled with polysilicon and oxide but sit beside the slit, not in its path. Before the slit opens, the stack is a continuous, stressed film. After it opens, the stack is a set of parallel walls.

---

## 1.6 Specification Sheet for a Modern Slit

```
Parameter                        Target (illustrative)            Driven by
─────────────────────────────────────────────────────────────────────────────────────
Full-depth opening               100% of slit length; no bridges  Block isolation
Top CD                           W_t ± 6 nm (3σ, wafer)           Clearance, fill
Bow (max CD − top CD)            ≤ 30 nm                          Clearance
Bottom CD                        ≥ 130 nm; ≥ 65% of top CD        Wet, fill, recess
Tilt                             ≤ 0.25° at 3σ edge (any          Clearance at
                                 direction normal to slit)        lower-deck bow
Wiggle (line-edge deviation)     ≤ 5 nm (3σ) along slit           Clearance, fill
Landing                          Bottom inside sacrificial layer  Source contact
                                 (CuA) or ≥ 30 nm into substrate
Punch-through below landing      None                             Source integrity
Sidewall striation               ≤ 3 nm amplitude at interfaces   Liner, metal recess
Remaining mask after etch        ≥ 0.5 µm a-C                     Top CD, no top
                                                                  rounding
Depth uniformity (before         ≤ ± 3% (3σ) of depth             Landing window
landing step)
Particles / defects              Fab defect spec; no blocked      Yield
                                 slits
Throughput                       Platform target (Ch. 5, 16)      Cost
```

Every chapter that follows works toward one or more lines of this table.

---

## 1.7 Summary & Key Takeaways

1. **Replacement gate needs an access path.** The slit lets acid in to remove nitride and lets metal in to form the word lines.

2. **A slit has four jobs.** It provides access, isolates blocks, often carries the common source, and in CuA flows gives access for the replacement source. Each job places a demand on depth, width, straightness, or landing.

3. **Width cannot shrink with layer count.** The downstream steps need a wide bottom, so aspect ratio rises roughly in proportion to stack height.

4. **Pitch is a compromise; clearance is the etch's share.** Slit plus clearance costs 15–25% of array area. Each nanometre of clearance saved is area.

5. **Clearance must be checked at every depth.** At wafer center the upper-deck bow is critical. With tilt, the lower-deck bow becomes critical. For the reference process, tilt must stay under about 0.29°.

6. **The slit etch is where the stack stops being a film.** After it, the stack is a set of tall walls, and the stress stored in it is free to move them.

---

## Study Questions

1. A layout uses 16 rows of channel holes with 110 nm top CD, nearest-neighbor pitch 150 nm, a slit top CD of 180 nm, and 70 nm clearance on each side. Compute the slit pitch and the slit area overhead. What is the lateral nitride-removal distance near the top of the stack?

2. For the reference process, the upper-deck slit bow increases from 30 to 50 nm (max CD 250 nm at the same depth). Recompute s(z) at the upper bow depth with zero tilt. Is the clearance still above s_min = 30 nm? What tilt limit does the upper bow now impose?

3. Show that if the lower-deck bow moves from 7.2 µm to 8.0 µm depth with the same hole widening, the tilt limit from that depth changes. Compute the new slit width at 8.0 µm from the linear taper, the new s(z), and the new θ_max.

4. A product moves from 200 to 300 total pairs at 50 nm pitch. The top CD stays 200 nm. Estimate the new slit depth (assume 0.5 µm of cap, inter-deck, and landing layers in total) and aspect ratio. If tilt at the edge stays 0.25°, how much farther does the slit bottom move sideways than in the reference process?

5. Explain why a bridge in the slit 1 µm long can disable two whole blocks, while a missing channel hole disables only one string. Which of the four jobs in Section 1.2 does a bridge defeat?

---

**Next Chapter:** [Chapter 2: The Stack Beneath the Slit — Layers, Landing Stack & Stress](./02-stack-landing-materials.md)

---

**Chapter 1 Development Status:** Complete  
**Version:** 1.0
