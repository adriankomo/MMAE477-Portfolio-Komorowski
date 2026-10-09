# Reflection — 3D forces and moments on a quadcopter arm

**Write brief answers based on your calculations and the notebook plots.** Refer to the values in `results.csv` where useful.

## Reference inputs

All groups use the same prescribed beam: **L = 120 mm**, **b = 20 mm**, **h = 10 mm**, **E = 3.0 GPa**, **T = 250 gf**.

## Step 1 — Vertical bending

- How closely does the FEA vertical tip deflection agree with the beam-theory prediction? Give the approximate percentage difference.

  Beam theory predicts **0.282432 mm**, while FEA gives **0.277766 mm**, approximately **1.65% lower**.

- How can we extract a representative tip deflection from the 3D FEA displacement field for comparison with the centerline deflection predicted by beam theory?

  Fit the end-face motion to a rigid translation and small rotation, then use the fitted centroid translation as the representative tip deflection.

## Step 2 — Bending in a second plane

- Which is greater: the vertical tip deflection from `Fy` or the lateral tip deflection from `Fz`? By what approximate factor?

  Vertical deflection is greater: **0.277766 / 0.071026 ≈ 3.91**, or about **3.9 times** the lateral deflection.

- Explain the difference using the two second moments of area, `I_y` and `I_z`.

  `I_y = hb³/12` and `I_z = bh³/12`. Since `b = 20 mm` and `h = 10 mm`, **`I_y = 4I_z`**. Therefore, the arm is stiffer under `Fz` loading, producing less lateral deflection than under `Fy`.

## Step 3 — Thrust and motor reaction moment

- Which tip translations and rotations are expected to be nonzero under `Fy+My` according to the beam compliance matrix?

  **`v_L`, `w_L`, `theta_y`, and `theta_z`**. `Fy` causes vertical bending, while `My` causes lateral bending.

- Compare the results for vertical thrust alone (`Fy`) and combined thrust and motor reaction moment (`Fy+My`). Which tip displacement components change when the motor reaction moment is included? How significant is the additional displacement relative to the vertical deflection produced by thrust?

  With `Fy`, vertical displacement is **0.277766 mm** and lateral displacement is approximately zero. Adding `My` introduces lateral displacement of **−0.013129 mm**, about **4.73%** of the vertical deflection. The vertical response remains essentially unchanged. `My` causes lateral bending because it acts about the y-axis; `Mx` causes torsion.

## Step 4 — Torsion

- Compare the deformation produced by `Fy` and `Mx`. Why is the displacement of the tip center a useful measure of bending deformation but not torsional deformation? What quantity should be used to characterize torsion?

  `Fy` bends the beam centerline, while `Mx` twists the cross-section about the longitudinal x-axis. The tip center may barely move during twisting, so torsion is characterized by the **tip twist angle, `theta_x`**.

- How well does the FEA tip rotation agree with the beam-theory torsion prediction? Identify one reason why the two might differ.

  Beam theory predicts **0.026513°**, while FEA gives **0.026154°**, a difference of approximately **1.35%**. Cross-section warping, mesh discretization, and boundary conditions can explain the difference.

## Model limitations

What is one assumption of this idealized beam/FEA model that could have an important effect on an actual manufactured quadcopter arm?

The model assumes a homogeneous, isotropic, linearly elastic material. A real 3D-printed arm may have direction-dependent stiffness and strength, while mounting details, vibrations, and flight dynamics may also affect its response.
