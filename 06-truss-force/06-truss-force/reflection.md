# Reflection — truss arm force paths

## Case 2A vs. Case 2B

- **Case 2A:** The largest member-force magnitude is 1000 gf in member BD. The force is -1000 gf, so BD is in compression.

- **Case 2B:** The largest member-force magnitude is 1000 gf in member CE. The force is +1000 gf, so CE is in tension.

- The maximum force magnitude is the same for Cases 2A and 2B: 1000 gf. Changing the orientation of the left-cell diagonal changes the load path and which member carries the critical force, but it does not change the maximum magnitude for this loading case.

- Even though the maximum magnitudes are equal, tension and compression still matter for a slender truss member. A member in tension mainly needs enough material strength to avoid tensile failure, while a slender member in compression can also fail by buckling. Therefore, a 1000 gf compression force can create a different structural risk than a 1000 gf tension force.

## The vertical member in Case 2B

- The force obtained in member BC is:

  **N_BC = 0 gf**

- At joint B, members AB and BD are both horizontal. Therefore, neither member provides a vertical force component. There is also no external vertical load applied directly at joint B. The only member at B that could contribute a vertical force is BC. For vertical equilibrium,

  **sum Fy = 0**

  **-N_BC = 0**

  so **N_BC = 0 gf**.

- This does not mean that BC would necessarily be unnecessary in a real quadcopter arm. The zero-force result applies only to this idealized geometry and upward static thrust load. BC could carry load during other conditions such as lateral maneuvering, a hard landing, motor torque, vibration, or other non-symmetric loading. It may also be useful for stiffness and maintaining the shape of the truss even when its axial force is zero in this particular case.

## Adding more cells at fixed arm size

For this section:

- L_total = 120 mm
- h = 30 mm
- P = 250 gf

As the number of cells increases, the cell width decreases:

- n = 2: width = 60 mm
- n = 3: width = 40 mm
- n = 4: width = 30 mm
- n = 6: width = 20 mm

The diagonal-member force magnitudes are:

- n = 2: 559.017 gf
- n = 3: 416.667 gf
- n = 4: 353.553 gf
- n = 6: 300.463 gf

As the number of cells increases, the magnitude of the diagonal-member force decreases. With a smaller cell width and the same 30 mm truss depth, the diagonal becomes steeper. Its vertical direction component therefore increases, so a smaller axial force is needed in the diagonal to provide the same vertical force component.

The overall maximum member-force magnitude does not decrease with additional cells. It remains approximately:

**max |N| = 1000 gf**

for n = 2, 3, 4, and 6.

This trend is different from the diagonal-force trend because the overall arm must still transmit the same bending moment near the body. The applied thrust and overall arm length remain fixed:

**M_root = P L_total**

**M_root = (250 gf)(120 mm) = 30,000 gf·mm**

With a truss depth of 30 mm, the required chord-force couple is approximately:

**N = M_root / h = 30,000 / 30 = 1000 gf**

Therefore, dividing the arm into additional cells reduces the force required in each diagonal but does not remove the global bending moment that must be carried near the root.

- **Family A:** The root-region top chord carries the largest load primarily in compression. At n = 6, the root chord force is approximately -1000 gf.

- **Family B:** The root-region bottom chord carries the largest load primarily in tension. At n = 6, the root chord force is approximately +1000 gf.

## Design interpretation

Based only on axial-force magnitude, increasing the number of cells does not make the truss unambiguously better. Increasing the number of cells lowers the diagonal-member force from about 559 gf at n = 2 to about 300 gf at n = 6, but the maximum member-force magnitude remains about 1000 gf because the same root bending moment still has to be transmitted.

Adding more cells can also introduce penalties. More cells require more members and joints, which can increase mass, the number of fasteners or connections, manufacturing complexity, assembly time, and the number of possible failure locations. Real compression members must also be checked for buckling, which is not included in this force-only analysis.

If choosing between Family A and Family B for this idealized upward-thrust case before performing a full buckling analysis, I would pay the most attention to the sign of the large root-chord force. Family A places the approximately 1000 gf root load primarily in compression, while Family B places the approximately 1000 gf root load primarily in tension. Since a slender compression member can fail by buckling, the Family A root chord would require particularly careful buckling analysis. The two layouts should not be judged only by their equal maximum force magnitudes.

## Anything still hard to pin down

The pin-jointed, force-only model makes several assumptions that are not completely realistic for an actual quadcopter arm. The members are assumed to carry only axial tension or compression, so bending and shear in the members are ignored. The joints are treated as perfect pins, while real joints and fasteners can have stiffness, eccentricity, clearances, and local stresses.

The analysis also considers a static upward motor thrust and ideal fixed root nodes. It does not include motor torque, vibration, self-weight, lateral maneuver loads, aerodynamic forces, impacts or hard landings, joint flexibility, member deflection, fatigue, or buckling. These effects would need to be considered before selecting the final truss geometry.
