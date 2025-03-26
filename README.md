# Quarter-Wave Monopole (NEC) with Perfect Ground and Offset

This repository contains a sample **NEC-2** input deck for a simple quarter-wave monopole above a perfect ground plane, tuned for the **87.5–108 MHz** FM broadcast range.

By splitting the whip into two wires, we avoid NEC's “segment lies in ground plane” error, which occurs if an entire wire segment resides exactly at z=0.

---

## File Contents

1. **quarterwave_ground.nec**  
   - Main NEC input file.  
   - Defines two wires:
     1. A **short, 1-segment** wire from z=0 up to a small offset.  
     2. The **main whip**, from that offset up to (offset + length).  
   - Uses `GE 1` and `GN 1` for an infinite, perfectly conducting ground plane.  
   - Sweeps frequencies from 87.5 MHz to 108.5 MHz in 1 MHz steps.

2. **README.md** (this file)  
   - Explains how to run the simulation and interpret results.

---

## Geometry & Cards Overview

- **SY L=0.76**  
  Approximate quarter-wave length at ~98 MHz (3.06 m / 4 ≈ 0.765 m).
- **SY r=0.003**  
  Conductor radius = 3 mm (helps provide slightly broader bandwidth).
- **SY offset=0.001**  
  A tiny gap (1 mm) between the ground plane and the first wire segment.  
  This prevents NEC from complaining that the wire “lies in ground plane.”

```text
GW 1  1   0 0 0      0 0 offset     r     <-- Short segment
GW 2 10  0 0 offset  0 0 Lplus      r     <-- Main whip

## How to Run
Open quarterwave_ground.nec in 4NEC2 (or another NEC-2 engine).

If you see any initial warnings about wires at z=0, you can safely ignore them; you’re intentionally using the perfect ground plane.

Click Calculate → Start in 4NEC2.

After the run completes, use the SWR or Frequency tabs in 4NEC2 to see how the feedpoint impedance and SWR vary from 87.5 MHz to 108.5 MHz.

Explore the Far Field menu to view the classic donut-shaped radiation pattern of a quarter-wave monopole over perfect ground, typically with ~5 dBi gain near the horizon.
