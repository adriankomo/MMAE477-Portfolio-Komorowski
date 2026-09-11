# Reflection — principal stresses at two stations

## Carried forward from 02

- Plate width, b (mm): 12.7 mm
- Plate thickness, h (mm): 3.175 mm
- Material (CF or aluminum): 6061 aluminum
- V(0), self-weight included, from `02` (gf): 122.401 gf
- M(0), self-weight included, from `02` (gf·mm): 15471.931 gf·mm
- V(60), self-weight included, from `02` (gf): 128.933 gf
- M(60), self-weight included, from `02` (gf·mm): 7931.933 gf·mm

## Cross-section properties (same at both stations)

- Area, A = b h (mm²): 40.3225 mm²
- Moment of inertia, I = b h^3 / 12 (mm^4): 33.8730 mm^4
- c = h / 2 (mm): 1.5875 mm

## Root (x = 0)

### Neutral axis

- tau_xy = 1.5 V(0) / A (gf/mm²): 4.553 gf/mm²
- sigma_1 (gf/mm²): 4.553 gf/mm²
- sigma_2 (gf/mm²): -4.553 gf/mm²
- theta_p (degrees): 45°
- sigma_vM (gf/mm²): 7.887 gf/mm²

### Top surface

- sigma_x = 6 M(0) / (b h^2) (gf/mm²): 725.111 gf/mm²
- sigma_1 (gf/mm²): 725.111 gf/mm²
- theta_p (degrees): 0°
- sigma_vM (gf/mm²): 725.111 gf/mm²

## Mid-span (x = 60 mm)

### Neutral axis

- tau_xy = 1.5 V(60) / A (gf/mm²): 4.796 gf/mm²
- sigma_1 (gf/mm²): 4.796 gf/mm²
- sigma_2 (gf/mm²): -4.796 gf/mm²
- theta_p (degrees): 45°
- sigma_vM (gf/mm²): 8.307 gf/mm²

### Top surface

- sigma_x = 6 M(60) / (b h^2) (gf/mm²): 371.740 gf/mm²
- sigma_1 (gf/mm²): 371.740 gf/mm²
- theta_p (degrees): 0°
- sigma_vM (gf/mm²): 371.740 gf/mm²

## Sanity checks

- Root neutral axis: does sigma_1 - sigma_2 equal 2 * tau_xy?  
  Yes. 4.553 - (-4.553) = 9.106 gf/mm², and 2(4.553) = 9.106 gf/mm².

- Root top surface: does sigma_1 equal your sigma_x there?  
  Yes. sigma_1 = sigma_x = 725.111 gf/mm².

- Mid-span neutral axis: does sigma_1 - sigma_2 equal 2 * tau_xy?  
  Yes. 4.796 - (-4.796) = 9.592 gf/mm², and 2(4.796) = 9.592 gf/mm².

- Mid-span top surface: does sigma_1 equal your sigma_x there?  
  Yes. sigma_1 = sigma_x = 371.740 gf/mm².

- Did both top-surface sigma_vM values come out equal to their sigma_x?  
  Yes. At the root both are 725.111 gf/mm², and at mid-span both are 371.740 gf/mm².

## Root vs. mid-span — thinking ahead to FEA

- Which of your four points has the largest sigma_vM, and does that match what you'd expect?

The root top surface shows the highest von Mises stress at 725.111 gf/mm², which is expected since the root carries the largest bending moment and the outer fibers see the peak bending stress.

- Given the Saint-Venant framing in the instructions: when you eventually check these hand-calculated numbers against an FEA model of the same arm, which station do you expect to match more closely, and why? What specifically about the root makes it a worse fit for the beam-theory idealization than mid-span?

The mid‑span station should align better with FEA. Beam theory is most accurate away from geometric disturbances, and the root is a real joint with mounting features, holes, fasteners, and contact effects that distort the local stress field. At x = 60 mm, the section is far enough from both the root and the motor mount that the beam assumptions hold more cleanly.

- What would you actually be looking at in an FEA contour plot to make that comparison — the same sigma_vM number, or something else?

I’d compare the von Mises stress contours at the same surfaces used in the hand calc — especially the root top surface and mid‑span top surface, while checking for root‑region stress concentrations that beam theory can’t capture.

## Anything still hard to pin down

The biggest uncertainty is how the actual root connection behaves compared to the ideal fixed support assumed in the hand calc. The real mounting geometry, holes, fasteners, and contact conditions aren’t modeled yet, so the root stress could deviate significantly. The mid‑span value is more trustworthy because it’s farther from those local effects.
