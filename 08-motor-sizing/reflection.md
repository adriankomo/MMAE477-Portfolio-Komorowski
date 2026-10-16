# Reflection — motor sizing

## What changed since `01`

- I did not change the motor, battery, ESC, or propeller selected in `01`. The final configuration remains the iFlight XING2 2207 2755KV motor, Ethix S5 5x4x3 propeller, 4S 1500 mAh 100C battery, and 50 A-per-channel ESC.

- I am still confident in the basic motor/propeller choice because the required hover thrust is only 135.465 g per motor, compared with approximately 1418.7 g of full-throttle thrust from the closest independent bench-test configuration. This gives a hover thrust ratio of only 9.55%, well below the 35% limit. For the bench-data calculations, the HQProp Durable 5x4.3x3 V2S was used as the closest tested substitute for the Ethix S5 5x4x3.

## Requirements

- **Hover thrust margin:** PASS.  
  T_hover / T_max = 135.465 / 1418.7 = **9.55%**, which is below the required 35%.

- **Hover throttle:** PASS.  
  The estimated hover throttle is approximately **21.18%**, which is below the target of about 60%.

- **ESC current rating:** FAILS the specified safety margin.  
  The measured full-throttle motor current is **45.16 A**. The required ESC rating is:

  **1.2 × 45.16 = 54.19 A**

  The selected ESC is rated at **50 A per motor channel**, so it is about 4.2 A below the required margin.

- **Battery maximum current:** FAILS the specified current requirement.  
  The selected 1500 mAh 100C battery has an estimated maximum current of:

  **1.5 Ah × 100 C = 150 A**

  The four motors require:

  **4 × 45.16 = 180.64 A**

  at full throttle, so the battery does not meet the required current margin.

- **Estimated hover time:** PASS.  
  The estimated hover time is approximately **8.64 minutes**, which is above the 5-minute target.

- To correct the current-limit failures, I would use a higher-rated ESC and a battery capable of more than approximately **181 A**. Another possible system-level change would be a lower-KV motor paired with a higher cell-count battery. Since

  **Kt = 9.55 / KV**,

  lowering KV increases the motor torque constant, allowing the motor to produce a given torque with less current. Increasing battery voltage can then recover the required motor speed. Any battery or motor change would require updating the vehicle mass and repeating the sizing loop.

## Model checks

- The motor's ideal no-load speed is:

  **KV × V = 2755 × 14.8 = 40,774 rpm**

  The measured full-throttle speed is approximately **30,290 rpm**, giving:

  **30,290 / 40,774 = 0.743**

  The full-throttle speed is therefore about **74.3% of the no-load speed**. This is reasonable because the no-load value assumes essentially no propeller torque. With a propeller attached, the motor must produce torque and draw current, so electrical and mechanical loading reduce the actual operating speed below the ideal KV × voltage value.

- The battery current at hover is approximately **2.084 A per motor**, but the estimated motor winding current is higher:

  **I_motor ≈ I_battery / throttle**

  **I_motor ≈ 2.084 / 0.2118 = 9.84 A**

  This occurs because the ESC uses PWM at part throttle. The battery supplies the average current over the PWM cycle, while the motor windings experience a larger current during the portions of the cycle when they are energized.

- The estimated hover torque is approximately:

  **Q = 0.03411 N·m = 3478.2 gf·mm**

  Dividing by hover thrust gives:

  **Q/T = 3478.2 / 135.465 = 25.68 mm**

  Lab 07 assumed **Q/T = 15 mm**, so the present estimate is about **71% higher**. The difference can come from the simplified assumed value used in Lab 07, as well as differences in the actual motor/propeller aerodynamic behavior. The present bench data also used a closely matched 5x4.3x3 propeller rather than the exact Ethix S5 5x4x3.

## Closing the loop

- The vehicle weight did not change because I did not change the actual motor, ESC, battery, or propeller selected in `01`. The vehicle weight therefore remains **541.86 g**, so:

  **T_hover = 541.86 / 4 = 135.465 g per motor**

  No additional mass-table iteration was required. The final configuration still meets the hover-margin, hover-throttle, and hover-time requirements, but it does not meet the required ESC or battery current margins.

## What is still uncertain

- The least reliable numbers are the exact hover throttle, hover current, and hover rpm. The required hover thrust of **135.465 g** is slightly below the lowest measured bench-test point of **159.9 g at 25% throttle**, so the hover throttle and current had to be extrapolated slightly below the measured range. The hover rpm was also estimated rather than directly read from a test point at exactly the required thrust.

- This could be improved later by testing the actual XING2 2207 2755KV motor with the exact Ethix S5 5x4x3 propeller and 4S battery on a thrust stand. Measuring thrust, current, torque, and rpm at the actual hover operating point would give more reliable values than interpolation or extrapolation from a similar propeller.# Reflection — motor sizing

**Write short answers based on your numbers in `results.csv`.**

## What changed since `01`

- Which earlier choices did you change (motor, KV, propeller, battery, ESC,
  or anything else), and why? Point to the `DECISIONS.md` rows.
- If you changed nothing, why are you confident your `01` choices still
  hold?

## Requirements

- Which requirements does your final choice meet, and which does it miss?
- For any requirement you miss, what would you change: KV, propeller, cell
  count, battery capacity, or something else? Explain using the lecture's
  ideas (for example, what KV does to speed per volt and current per unit
  torque).

## Model checks

- How does your full-throttle rpm compare with the no-load speed `KV × V`?
  Why must it be lower?
- Why is the motor current at hover larger than the battery current shown
  in the thrust table?
- How does your `Q/T` compare with the 15 mm assumed in Lab 07? Give one
  reason the two might differ.

## Closing the loop

- Did your vehicle weight change after Steps 3–5? If so, by how much, and
  did your choice still meet the requirements after you repeated the
  calculation?

## What is still uncertain

- Which number in your sizing is least reliable, and how could it be
  measured later in the course?
