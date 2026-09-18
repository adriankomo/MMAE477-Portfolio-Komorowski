# Reflection — beam deflection, hand calc vs. Inventor

## Carried forward from 02 and 03

- Plate width, b (mm): 12.7 mm
- Plate thickness, h (mm): 3.175 mm
- Material (CF or aluminum): 6061 aluminum
- P = T_hover (gf): 135.465 gf
- I = b h^3 / 12 (mm^4), from `03`: 33.8730 mm^4

## Young's modulus

- E, from a datasheet or reference (GPa): 68.9 GPa
- Source (https://www.azom.com/article.aspx?ArticleID=6636&)): ASM/MatWeb, Aluminum 6061-T6 / 6061-T651 material data sheet
- E converted to gf/mm^2 (E_GPa x 101,972): 7,025,870.8 gf/mm^2

## Hand calc

- EI (gf*mm^2): 237,987,322.5 gf*mm^2
- y_hand = P L^3 / (3 E I), L = 120 mm (mm): 0.32787 mm

## Inventor model and simulation

- Material assigned in Inventor (exact match, or closest substitute — say which): Aluminum 6061. Inventor lists Young's modulus as 9.993E+06 psi, which is approximately 68.9 GPa and closely matches the value used in the hand calculation.
- Constraint and load setup (brief description — confirms it matches the hand-calc assumptions): One end face at x = 0 was fully fixed. A 1.328 N upward force was applied to the opposite end face at x = 120 mm, perpendicular to the beam, to represent the motor thrust load.
- y_fea, maximum displacement (mm): 0.3215 mm
- % difference between y_fea and y_hand: -1.94% (Inventor was about 1.94% lower than the hand calculation)
- If the % difference is large (over ~25%), what did you check, and what did you find?: The difference was only about 1.94%, so there was no large discrepancy. I checked that the beam dimensions, Aluminum 6061 material, fixed-end constraint, and tip-force magnitude/direction matched the hand-calculation assumptions.

## Stress check: root vs. mid-span

- sigma_vM, root, top surface — hand value (from `03`) (gf/mm^2): 725.111 gf/mm^2
- sigma_vM, root, top surface — Inventor probe (gf/mm^2): 485.387 gf/mm^2
- sigma_vM, mid-span (x = 60 mm), top surface — hand value (from `03`) (gf/mm^2): 371.740 gf/mm^2
- sigma_vM, mid-span, top surface — Inventor probe (gf/mm^2): 383.619 gf/mm^2
- Which station's hand and FEA values agree more closely?: The mid-span values agree much more closely. The Inventor mid-span result is about 3.20% higher than the hand value, while the root Inventor result is about 33.1% lower than the hand value.
- Does this match the prediction you made in `03`'s "thinking ahead to FEA" section? If not, what do you think explains the difference?: Yes. In 03 I predicted that mid-span would agree better with beam theory because it is farther away from the fixed support. That prediction was supported by the Inventor results. At the root, the fixed constraint creates a local stress field that does not behave exactly like the idealized beam-theory assumption, while the stress distribution farther from the support is closer to the simple beam model.

## Anything still hard to pin down

The root stress is sensitive to probe location, mesh, and how Inventor models the fixed support, so the value at x = 0 may differ from the hand calculation. The mid-span result is more reliable since it is farther from the boundary. Also, the Inventor model uses only the tip load, while the hand calculations from 03 used the earlier loading setup, which limits direct comparison.
