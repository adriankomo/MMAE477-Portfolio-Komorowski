# Quadcopter arm vibrations — reflection

**Name:** Adrian Komorowski

## Part 1 — Geometry and approximate natural frequencies

**Q1.** I modeled our ATLAS arm as a uniform solid rectangular beam made of 6061 aluminum. Inputs: `L = 0.052412 m`, `hy = 0.003 m`, `bz = 0.016 m`, `E = 68.9e9 Pa`, `rho = 2700 kg/m^3`, and `motor_mass = 0.0164 kg` (EMAX ECO II 2004). The length and cross-section came from our earlier CAD model; the rectangular beam simplifies the real arm's mounting features.

The approximate first frequencies were **904.242 Hz vertical** and **4822.624 Hz lateral** without the motor, and **269.678 Hz vertical** and **1438.284 Hz lateral** with it. Vertical bending is less stiff because the arm is much thinner vertically (3 mm) than it is wide (16 mm), making `Iz` smaller than `Iy`. The motor adds inertia without adding beam stiffness, lowering both frequencies. Torsional vibration is not included.

## Part 2 — Finite-element predictions

**Q2.** The finite-element results were **891.185 Hz vertical** and **4752.988 Hz lateral** without the motor, versus **269.647 Hz vertical** and **1438.119 Hz lateral** with it. Adding the point mass at the tip increases the mass matrix but not stiffness, so both frequencies drop. The bare-beam FE values are about 1.5% below the Part 1 estimates, while the with-motor values are almost identical. The simple estimate works well for the first mode.

## Part 3 — Mode shapes and mesh convergence

**Q3.** The first vertical mode has a smooth bend with no internal node, the second has one internal node, and the third has two. With 2 elements, `f1 = 269.65 Hz` and `f3 = 14942.64 Hz`. With 32 elements, `f1 = 269.65 Hz` and `f3 = 12766.35 Hz`. The third mode changes much more with mesh refinement because its more complicated bending shape needs more elements to represent accurately.

## Part 4 — Motor and propeller excitation

**Q4.** We selected the **EMAX ECO II 2004 2400KV** motor, **4S battery**, and **EMAX Avia 5030 three-blade propeller**. I assumed **10,000–25,000 rpm** as a loaded operating interval, not a measured range. Published 4S data for the same motor with a *different* 5-inch tri-blade prop (EMAX AVAN 5120-3) reports about 15,800–25,100 rpm at 40–90% throttle; I extended the lower end to represent lighter-throttle running. Source: https://www.fpv-db.com/motors/emax-eco-ii-2004/ . For comparison, the approximate no-load speed at nominal 4S voltage is `2400 × 14.8 = 35,520 rpm`, not the actual speed with a prop installed.

**1P** is a lateral imbalance force once per revolution. **BPF (3P)** represents an assumed vertical thrust fluctuation three times per revolution. **2×BPF (6P)** is its second harmonic. A balanced three-blade propeller can produce nearly constant total thrust in uniform flow, so these thrust fluctuations are assumptions in the model.

**Q5.** No forcing frequency exactly matches the first three relevant bending modes within 10,000–25,000 rpm. The 1P range is **167–417 Hz**, below the first lateral mode at **1438 Hz**. The vertical 3P range is **500–1250 Hz**, between vertical modes 1 (**270 Hz**) and 2 (**4002 Hz**). The 6P range is **1000–2500 Hz**, also between those modes. Higher modes only change the predicted 6P tip response slightly (about 3% near 25,000 rpm). Using three blades instead of two shifts BPF resonance speeds lower, without proving the real thrust fluctuation is stronger. Even a frequency match may have a small displacement if the forcing is weak, damping is significant, or that mode barely moves at the force location.

## Part 5 — Design sensitivity

**Q6.** Increasing each dimension separately by 15% gave:

| Change | Vertical f1 change | Lateral f1 change |
| --- | ---: | ---: |
| Length +15% | -19.45% | -19.45% |
| Width +15% | +6.53% | +22.51% |
| Height +15% | +22.51% | +6.53% |

Increasing height has the largest positive effect on vertical frequency; increasing width has the largest positive effect on lateral frequency. The code selected **length +15%** because it has the largest average absolute frequency change. It increases beam mass from **6.793 g to 7.811 g** and changes first frequencies to **217.199 Hz vertical** and **1158.392 Hz lateral**.

This is not necessarily better: the first vertical mode moves farther below the 3P range, but the first lateral mode moves closer to 1P. The second vertical mode also drops to about **3036 Hz**, closer to the high end of the 6P range (2500 Hz). The longer arm adds 15% mass while lowering both first frequencies.
