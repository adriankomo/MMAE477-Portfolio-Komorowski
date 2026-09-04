# Reflection — shear force, bending moment, and self-weight

## What changed since your last pass (01)

I carried forward the total onboard weight from 01, which was 541.86 g. This gave a per-motor hover thrust of 135.465 gf. I did not need to revise the 01 numbers for this pass; I used T_hover as the point load P on one 120 mm arm.

## Your numbers

- P = T_hover, per-motor hover thrust from `01` (gf): 135.465 gf
- Arm length, L (mm): 120 mm
- M(0), idealized / point-load-only (gf·mm): 16255.800 gf·mm

**Analysis 1 — flat plate**

- Material (CF or aluminum): 6061 aluminum
- Part sourced (name + link): Online Metals 1/8" x 1/2" Aluminum Rectangle Bar 6061-T6511 — https://www.onlinemetals.com/en/buy/aluminum/0-125-x-0-5-aluminum-rectangle-bar-6061-t6511-extruded/pid/20371
- Width x thickness (mm): 12.7 mm x 3.175 mm
- Density, rho, and where it came from (g/mm³ or g/cm³ + source): 2.70 g/cm³ = 0.00270 g/mm³, standard density for aluminum given in the assignment
- Area, A (mm²): 40.3225 mm²
- w0 = rho x A (gf/mm): 0.108871 gf/mm
- Total arm self-weight, w0 x L (gf): 13.0645 gf
- M(0) with self-weight included (gf·mm): 15471.931 gf·mm
- Change in M(0) from self-weight, as a percent of the idealized value: -4.82%

**Analysis 2 — round tube**

- Material (the other one — CF or aluminum): Carbon fiber
- Part sourced (name + link): DragonPlate Carbon Tube, 10 mm OD x 0.288" ID x 24" — https://dragonplate.com/dragonplate-carbon-tube-394od-x-288id-x-24
- Outer diameter x wall thickness (mm): 10 mm OD x 1.3462 mm wall
- Density, rho, and where it came from (g/mm³ or g/cm³ + source): approximately 1.55 g/cm³ = 0.00155 g/mm³, from the DragonPlate product density of 0.056 lb/in³
- Area, A (mm²): 36.5988 mm²
- w0 = rho x A (gf/mm): 0.056728 gf/mm
- Total arm self-weight, w0 x L (gf): 6.8074 gf
- M(0) with self-weight included (gf·mm): 15847.358 gf·mm
- Change in M(0) from self-weight, as a percent of the idealized value: -2.51%

## Comparing the two

- Which of your two candidates has the lower M(0) — the plate or the tube?

The aluminum flat plate has the lower M(0), at 15471.931 gf·mm compared with 15847.358 gf·mm for the carbon fiber tube.

- Your best guess as to why: is it mostly the material (density difference), mostly the shape (area difference), or genuinely both? You don't have enough data here to prove it cleanly — say what you'd need to check to actually isolate the cause.

I think it is caused by both the material and the cross-sectional area. The aluminum has a higher density than the carbon fiber, and the aluminum plate also has a slightly larger cross-sectional area. Because of this, the aluminum plate has more self-weight per unit length. In the equations used for this pass, the self-weight acts opposite to the motor thrust, so the heavier aluminum plate reduces the net root bending moment more. To isolate whether material or shape is the main cause, I would need to compare the same geometry using both materials or the same material using both geometries.

- Is self-weight actually negligible for a build this size? What would have to change (bigger arm, heavier material, lighter thrust) for that answer to flip?

Self-weight is fairly small for this build, but I would not completely ignore it. It changed the root moment by about 4.82% for the aluminum plate and 2.51% for the carbon fiber tube. A longer arm, heavier material, or larger cross section would make self-weight more important. A lower motor thrust would also make the arm's own weight a larger percentage of the total loading. A shorter or lighter arm would make self-weight even less significant.

## Anything still hard to pin down

The main uncertainty is that this pass only compares shear force and bending moment from the loads. It does not yet show which arm would actually be stronger, stiffer, or better for the drone because stress, deflection, mounting details, and failure strength have not been checked yet. The final arm dimensions may also change later in the design.
