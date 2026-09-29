# Reflection — the whole frame in FEA

## Carried forward

- Arm design used in the frame: flat plate
- Material: Aluminum 6061
- Arm width: 16 mm
- Arm thickness: 3 mm
- P = T_hover from 01: 135.465 gf = 1.328 N per motor
- P_max from 01: 1321 gf = 12.955 N per motor
- E from 04: 68.9 GPa
- I for the arm cross-section: I = b h^3 / 12 = 16(3^3)/12 = 36 mm^4

## Strength

- Strength value used: 275 MPa yield strength for 6061 aluminum
- Source: ASM/MatWeb Aluminum 6061-T6 / 6061-T651 material data sheet, same material reference used for Young's modulus in 04
- Converted strength: 275 MPa x 101.97 = 28,041.75 gf/mm^2

## Checking the model (Step 1)

- Frame mass from CAD model: 0.145 kg, or about 145 g
- FEA software used: Autodesk Inventor Stress Analysis
- Material assigned in the software: Aluminum 6061
- The actual frame is about 45% heavier than the 100 g frame mass assumed in 01.
- The original hover calculation corresponded to a total weight of 4(135.465) = 541.86 gf. Replacing the assumed 100 g frame with the actual 145 g frame adds about 45 gf, giving an updated estimated total weight of 586.86 gf.
- The updated hover thrust would therefore be about 146.715 gf per motor, or about 1.439 N per motor. The original 135.465 gf value was still used in this lab so the results remained directly comparable to 04.
- L_cad, measured from the body/arm root to the motor-mount center: 52.412 mm
- y_hand_Lcad = P L_cad^3 / (3 E I) = 0.02570 mm

## Hover setup (Step 2)

- A 30 mm x 30 mm square region at the center of the frame was split from the main face and assigned a Fixed constraint.
- The small fixed region was used instead of fixing the entire center plate so the body could still flex between the center and the arm roots.
- Four separate Force loads were applied, one at each motor mount.
- Each hover load was 1.328 N upward and perpendicular to the frame.
- Gravity was turned off so the setup matched the previous beam calculation.
- The frame was modeled as a single part rather than an assembly, so bonded-contact assumptions between separate frame components were not needed.

## Frame vs. beam (Steps 3-4)

- Maximum hover von Mises stress in the baseline filleted model: 4.644 MPa
- Maximum stress location: inside arm-root fillet / arm-to-body transition
- Arm tip displacement probed at the motor mount: 0.0758 mm
- Beam hand-calculated tip deflection: 0.02570 mm

Percent difference:

% difference = (0.0758 - 0.02570) / 0.02570 x 100
             = 194.9%

The complete frame deflected considerably more than the ideal beam calculation. The beam model in 04 assumed that the arm root was perfectly fixed and rigid. In the full-frame model, the body plate and the area around the arm root also deform, adding flexibility that the simple cantilever model does not include.

At the arm midpoint:

- FEA von Mises stress: 1.293 MPa
- Beam-theory stress:

M = P L_cad / 2

sigma = M c / I
      = 1.451 MPa approximately

The FEA midpoint stress was about 10.9% lower than the beam-theory value. This is much closer than the tip-deflection comparison and suggests that beam theory still represents the local bending stress reasonably well away from the arm root, even though the full frame is more flexible overall.

## Sharp vs. filleted corner (Step 5)

The mesh was refined by reducing the Average Element Size from 0.100 to 0.075 and then to 0.050. Von Mises stress was tracked because the frame material is aluminum.

### Filleted model

- Mesh 1: 8148 elements, max stress = 4.644 MPa, max displacement = 0.1003 mm
- Mesh 2: 8148 elements, max stress = 4.644 MPa, max displacement = 0.1003 mm
- Mesh 3: 9880 elements, max stress = 4.943 MPa, max displacement = 0.1007 mm

The highest stress occurred at the inside arm-root fillets. The maximum displacement changed very little with refinement, while the maximum stress increased slightly at the finest mesh. The filleted model therefore showed much more stable behavior than the sharp-corner model.

### Sharp-corner model

- Mesh 1: 7632 elements, max stress = 5.374 MPa, max displacement = 0.1030 mm
- Mesh 2: 7382 elements, max stress = 4.803 MPa, max displacement = 0.1029 mm
- Mesh 3: 9706 elements, max stress = 5.919 MPa, max displacement = 0.1032 mm

The sharp-corner maximum stress did not settle as cleanly as the displacement. The displacement remained nearly constant at about 0.103 mm, while the peak stress changed from 5.374 MPa to 4.803 MPa and then to 5.919 MPa.

The element counts did not increase perfectly monotonically for every mesh setting because Inventor generated the mesh differently around the detailed geometry. For this reason, the convergence behavior was judged using both the actual element counts and the stability of the results.

The sharp model was more mesh-sensitive than the filleted model. This is expected because a perfectly sharp inside corner creates a stress singularity, so the reported peak can continue changing as the mesh is refined. The 2 mm fillet removes the perfectly sharp corner and produces a finite, more physically meaningful stress concentration.

For a design decision, I would trust the filleted-corner results more than the sharp-corner peak stress.

## Full throttle and factor of safety (Step 6)

The finest filleted hover results were scaled using:

P_max / P = 1321 / 135.465 = 9.752 approximately

Predicted full-throttle maximum stress:

sigma_scaled = 4.943 MPa x 9.752
             = 48.20 MPa

Predicted full-throttle displacement:

y_scaled = 0.1007 mm x 9.752
         = 0.982 mm

Inventor full-throttle results:

- Simulated maximum von Mises stress: 48.22 MPa
- Simulated maximum displacement: 0.982 mm

The scaled predictions and the Inventor simulation agreed almost exactly. This confirms that the model behaved linearly over the load increase and that the full-throttle loads were entered consistently.

Highest trustworthy full-throttle stress:

- 48.22 MPa
- 48.22 x 101.97 = 4916.99 gf/mm^2
- Location: inside arm-root fillet / arm-to-body transition

Factor of safety:

FoS = yield strength / maximum von Mises stress
    = 275 / 48.22
    = 5.70

The frame therefore clears the required FoS >= 1.5 target at full throttle.

The full-throttle displacement is also small compared with the arm length:

0.982 / 52.412 x 100 = 1.87%

This is well below 10% of L_cad, so the linear-elastic model is still within a reasonable deformation range for this analysis.

## What I would change

The frame passes the full-throttle factor-of-safety requirement with a large margin, so strength is not currently the limiting issue. However, the actual CAD frame mass is about 145 g, compared with the 100 g frame mass assumed during the original sizing calculation.

Because the frame is heavier than the original target, the next design change I would focus on would be reducing unnecessary plate material while keeping the 2 mm arm-root fillets. The mesh study showed that the fillets reduce the arm-root stress concentration and give more stable stress results, so I would keep them in the design.

Any further material removal should avoid the arm roots and other high-stress transitions shown by the FEA results.

## Anything still hard to pin down

The model still contains several idealizations. The center of the frame is represented by a fixed 30 mm x 30 mm region even though a real drone is free in flight. Motor thrust was modeled as static upward force, with gravity, vibration, motor torque, hard landings, and maneuver loads excluded.

The analysis also assumes the tabulated 6061 aluminum properties represent the actual manufactured frame material. Manufacturing tolerances, fasteners, fatigue, impact loading, and local stresses around real hardware have not yet been modeled.

The mesh study also showed that local peak stress, especially at sharp corners, is sensitive to mesh density. Because of this, the exact peak stress at a mathematical sharp corner should not be treated as a physical design value.
