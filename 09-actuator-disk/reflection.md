# Actuator-Disk Lab — Derivations and Reflection

**Name: Adrian Komorowski**

## Part A — Tip-speed dimensional analysis

**A1.** Give the fundamental dimensions of thrust, density, tip speed, and diameter. Solve for the powers a, b, and c, and define the dimensionless thrust coefficient C_T,U.
Assume

`T = C_T,U * rho^a * U_tip^b * D^c`

The fundamental dimensions are:

- Thrust: `[T] = M L T^-2`
- Density: `[rho] = M L^-3`
- Tip speed: `[U_tip] = L T^-1`
- Diameter: `[D] = L`

Therefore,

`M L T^-2 = (M L^-3)^a (L T^-1)^b (L)^c`

Matching exponents:

- Mass: `a = 1`
- Time: `-b = -2`, so `b = 2`
- Length: `-3a + b + c = 1`

Substituting `a = 1` and `b = 2`:

`-3 + 2 + c = 1`

`c = 2`

Therefore,

`T = C_T,U * rho * U_tip^2 * D^2`

where `C_T,U` is a dimensionless thrust coefficient based on blade-tip speed.

**A2.** Show the conversion between C_T,U and C_T,Omega. Why is it only a change of normalization?
Since

`U_tip = Omega*D/2`

substitute into the tip-speed equation:

`T = C_T,U * rho * (Omega*D/2)^2 * D^2`

`T = (C_T,U/4) * rho * Omega^2 * D^4`

The angular-speed form is

`T = C_T,Omega * rho * Omega^2 * D^4`

so

`C_T,Omega = C_T,U/4`

or

`C_T,U = 4*C_T,Omega`

This is only a change of normalization because both equations describe the same physical thrust. The numerical value of the coefficient changes because a different characteristic velocity is used.

**A3.** At constant thrust coefficient, how does thrust scale with diameter when (i) angular speed is fixed and (ii) tip speed is fixed? Explain.
At constant thrust coefficient and fixed angular speed:

`T proportional to Omega^2 * D^4`

Since Omega is fixed,

`T proportional to D^4`

At fixed blade-tip speed:

`T proportional to U_tip^2 * D^2`

Since `U_tip` is fixed,

`T proportional to D^2`

The difference occurs because at fixed Omega, increasing diameter also increases blade-tip speed. At fixed tip speed, that additional speed increase does not occur.

---

## Part B — Actuator-disk assumptions and mass conservation

**B1.** Briefly describe the streamtube control volume, the assumptions of the model, and why a fixed-area upstream cylinder is inappropriate.

The streamtube control volume follows the air that passes through the rotor disk. Its sides follow streamlines, so ideally no mass crosses the sides of the streamtube.

The actuator-disk model assumes steady, incompressible, axial and uniform flow at the disk. The air is stationary far upstream, pressure returns to local ambient far upstream and in the far wake, and effects such as wake swirl, viscosity, blade-profile drag, ground effect, and interaction between rotors are neglected.

The upstream streamtube cannot be treated as a constant-area cylinder. In hover, the velocity approaches zero far upstream while the velocity through the rotor disk is finite. To maintain the same mass flow, the streamtube area must change as the air accelerates toward the rotor.

**B2.** Obtain the mass-flow rate at the disk, define the pressure jump, and relate pressure jump to thrust.

At the disk,

`m_dot = rho*A*vi`

The pressure jump across the actuator disk is

`Delta_p = p'^+ - p'^-`

The pressure jump acting over disk area A produces thrust:

`T = A*Delta_p`

Therefore,

`Delta_p = T/A`

---

## Part C — Momentum conservation

**C1.** Show the axial momentum balance (downward positive) and substitute the mass flow rate.

Taking downward as positive for the air, the rotor exerts a downward force T on the airflow.

The steady momentum equation is

`T = m_dot*(vw - V_upstream)`

In hover, the far-upstream air is stationary, so

`V_upstream = 0`

Therefore,

`T = m_dot*vw`

Using

`m_dot = rho*A*vi`

gives

`T = rho*A*vi*vw`

**C2.** Why is another equation needed to determine both induced velocity and far-wake velocity?

Mass and momentum conservation give

`T = rho*A*vi*vw`

but both `vi` and `vw` are unknown. Therefore, one equation is not sufficient to determine both velocities. An additional relationship is required, which is obtained by applying Bernoulli's equation separately above and below the actuator disk.

---

## Part D — Bernoulli and the pressure jump

**D1.** Apply Bernoulli separately above and below the disk. Derive the pressures p'^− and p'^+.

Above the disk, apply Bernoulli from far upstream to just above the rotor:

`0 + 0 = p'^- + (1/2)*rho*vi^2`

Therefore,

`p'^- = -(1/2)*rho*vi^2`

Below the disk, apply Bernoulli from just below the disk to the far wake:

`p'^+ + (1/2)*rho*vi^2 = 0 + (1/2)*rho*vw^2`

Therefore,

`p'^+ = (1/2)*rho*(vw^2 - vi^2)`

**D2.** Obtain the pressure jump and combine it with the momentum balance to derive the far-wake speed and actuator-disk thrust equation.

The pressure jump is

`Delta_p = p'^+ - p'^-`

Substituting the expressions above:

`Delta_p = (1/2)*rho*(vw^2 - vi^2) + (1/2)*rho*vi^2`

so

`Delta_p = (1/2)*rho*vw^2`

Since

`T = A*Delta_p`

then

`T = (1/2)*rho*A*vw^2`

From momentum conservation,

`T = rho*A*vi*vw`

Equating the two expressions:

`rho*A*vi*vw = (1/2)*rho*A*vw^2`

Canceling common terms gives

`vi = vw/2`

Therefore,

`vw = 2*vi`

Substituting this into the momentum equation:

`T = rho*A*vi*(2vi)`

so the actuator-disk thrust equation is

`T = 2*rho*A*vi^2`

**D3.** Why cannot Bernoulli be applied directly across the disk? Why can the gravitational term be removed from the pressure-perturbation form without neglecting the quadcopter's weight?

Bernoulli cannot be applied unchanged directly across the actuator disk because the rotor adds mechanical energy to the air. The pressure therefore has a discontinuous increase across the disk.

The gravitational term can be removed from the pressure-perturbation form because the hydrostatic ambient pressure variation balances the weight of the air. This does not mean gravity on the quadcopter is ignored. The vehicle still requires total upward thrust equal to `M*g` to hover.

---

## Part E — Power and diameter

**E1.** Derive induced velocity vi from a specified thrust and then derive ideal induced power Pi. Check the units.

Starting with

`T = 2*rho*A*vi^2`

solve for induced velocity:

`vi = sqrt(T/(2*rho*A))`

The ideal induced power is

`Pi = Delta_p*A*vi`

Since

`T = Delta_p*A`

then

`Pi = T*vi`

Substituting the induced-velocity equation:

`Pi = T*sqrt(T/(2*rho*A))`

or

`Pi = T^(3/2)/sqrt(2*rho*A)`

The units are

`N * m/s = W`

so the result correctly has units of power.

**E2.** Obtain total ideal hover power for N rotors supporting mass M. How does it depend on diameter at fixed vehicle weight and rotor count?


For N identical rotors,

`T = M*g/N`

and

`A = pi*D^2/4`

Total power is

`Ptot = N*Pi`

Therefore,

`Ptot = N*(M*g/N)^(3/2) / sqrt(2*rho*A)`

which simplifies to

`Ptot = sqrt(2)*(M*g)^(3/2) / (D*sqrt(N*rho*pi))`

For fixed vehicle mass, air density, and number of rotors:

`Ptot proportional to 1/D`

Therefore, increasing rotor diameter decreases ideal induced hover power.

**E3.** Explain why ideal induced power alone is insufficient for selecting a commercial propeller.

Ideal induced power alone cannot determine the best commercial propeller because the actuator-disk model ignores real blade geometry, profile drag, motor and ESC efficiency, propeller mass, structural loads, noise, RPM limits, tip-speed effects, packaging, and frame clearance.

A larger rotor can reduce ideal induced power while still being impractical or inefficient when the real motor and propeller system is considered.

---

## Part F — Inflow ratio and model limitations

**F1.** Define lambda, derive the relationship between lambda and C_T,U, and show how this connects the tip-speed and induced-air-speed thrust formulas.


Define the inflow ratio as

`lambda = vi/U_tip`

Therefore,

`vi = lambda*U_tip`

The actuator-disk equation is

`T = 2*rho*A*vi^2`

Using

`A = pi*D^2/4`

and substituting `vi = lambda*U_tip`:

`T = 2*rho*(pi*D^2/4)*(lambda*U_tip)^2`

Simplifying:

`T = (pi/2)*lambda^2*rho*U_tip^2*D^2`

From Part A,

`T = C_T,U*rho*U_tip^2*D^2`

Therefore,

`C_T,U = (pi/2)*lambda^2`

This connects the blade-tip-speed description of thrust to the induced-air-speed actuator-disk description.

**F2.** Can dimensional analysis plus actuator-disk theory determine motor RPM? What additional information is needed?

No. Dimensional analysis and ideal actuator-disk theory cannot determine the RPM required for hover by themselves.

Actuator-disk theory determines the induced air velocity needed to produce a specified thrust, but it does not describe the actual aerodynamic behavior of the rotating blades. Determining RPM requires additional information such as measured motor-propeller thrust data, a known propeller thrust coefficient, or a detailed blade aerodynamic model.

Motor KV alone is not sufficient because KV represents approximately no-load speed per volt, not loaded hover RPM.

---

## Part G — Your quadcopter

**G1. Design inputs and units.** Give the all-up mass of your quadcopter (including battery and payload), planned commercial propeller diameter, and a comparison diameter. State whether the mass is measured or estimated, identify the propeller size/model if known, show the conversions to SI, and explain whether the comparison propeller would fit the frame.


The estimated all-up mass of the quadcopter is

`M = 600 g = 0.600 kg`

This is an estimated maximum ready-to-fly mass including the frame, battery, motors, electronics, propellers, wiring, sensors/payload, and other onboard components.

The planned propeller is a 5-inch commercial propeller, corresponding to the previously selected Ethix S5 size.

`D = 5 in * 0.0254 m/in`

`D = 0.1270 m`

For comparison, I selected a 7-inch propeller:

`D_comp = 7 in * 0.0254 m/in`

`D_comp = 0.1778 m`

The 7-inch propeller is treated as a hypothetical comparison for this calculation. Clearance on the current frame has not been verified, so it is not assumed to be a feasible direct replacement.

The common values are:

`rho = 1.225 kg/m^3`

`g = 9.81 m/s^2`

`N = 4`

**G2. Actuator-disk calculation.** Using the mass of your quadcopter and installed rotor diameter, show intermediate calculations for disk area `A`, hover thrust per rotor `T`, mass flow `m_dot`, induced velocity `vi`, far-wake velocity `vw`, pressure jump `Delta_p`, and ideal power per rotor `Pi`. Enter the selected outputs in `results.csv`.

Hover thrust per rotor:

`T = M*g/N`

`T = (0.600*9.81)/4`

`T = 1.4715 N`

Disk area for one 5-inch rotor:

`A = pi*D^2/4`

`A = pi*(0.1270)^2/4`

`A = 0.012668 m^2`

Induced velocity:

`vi = sqrt(T/(2*rho*A))`

`vi = sqrt(1.4715/(2*1.225*0.012668))`

`vi = 6.8857 m/s`

Far-wake velocity:

`vw = 2*vi`

`vw = 13.7714 m/s`

Pressure rise:

`Delta_p = T/A`

`Delta_p = 1.4715/0.012668`

`Delta_p = 116.16 Pa`

Mass flow rate through one rotor:

`m_dot = rho*A*vi`

`m_dot = 1.225*0.012668*6.8857`

`m_dot = 0.10685 kg/s`

Ideal induced power per rotor:

`Pi = T*vi`

`Pi = 1.4715*6.8857`

`Pi = 10.1323 W`

Total ideal induced hover power:

`Ptot = 4*Pi`

`Ptot = 40.5293 W`

**G3. Rotor diameter comparison.** Calculate total ideal induced hover power at your planned diameter and chosen comparison diameter at the *same total weight and rotor count*. Check your computed ratio against the diameter scaling law. What practical considerations might prevent choosing the larger rotor?

For the 7-inch comparison rotor:

`D_comp = 0.1778 m`

Disk area:

`A_comp = pi*(0.1778)^2/4`

`A_comp = 0.024829 m^2`

At the same vehicle mass and hover thrust per rotor:

`vi_comp = sqrt(T/(2*rho*A_comp))`

`vi_comp = 4.9184 m/s`

The total ideal hover power becomes

`P_comp = 4*T*vi_comp`

`P_comp = 28.9495 W`

The power ratio is

`P_comp/Ptot = 28.9495/40.5293`

`P_comp/Ptot = 0.7143`

The diameter scaling from Part E predicts

`P_comp/Ptot = D/D_comp`

`= 0.1270/0.1778`

`= 0.7143`

so the numerical calculation agrees with the theoretical `P proportional to 1/D` scaling.

The ideal actuator-disk model therefore predicts that the 7-inch rotors require about 28.6% less induced hover power than the 5-inch rotors for the same 600 g vehicle.

However, a larger propeller requires more frame clearance and may require a different motor, RPM range, and structural design. It also has greater rotational inertia and may affect maneuverability. Therefore, the ideal power result alone does not prove that 7-inch props are the better practical choice.

**G4. Connecting blade and air speeds (conditional).** If you have a measured or documented estimate of the **loaded hover RPM**, give the source, convert it to `Omega` and `U_tip`, and calculate `lambda` and `C_T,U` in two ways. If this information is unavailable, leave the three RPM-dependent CSV entries blank and explain why actuator-disk theory cannot determine them by itself. Note that a motor's `KV` value is not a loaded hover-RPM measurement.

A sufficiently reliable loaded hover RPM is not available for the exact motor-propeller operating condition used here. Therefore, the following `results.csv` entries are intentionally left blank:

- `hover_rotor_rpm`
- `inflow_ratio`
- `thrust_coefficient_tip_speed`

The motor KV rating cannot be substituted for loaded hover RPM because KV describes approximately the motor's no-load speed per volt. Actual operating RPM depends on the motor, propeller aerodynamic load, voltage, and operating point.

If reliable loaded hover RPM data become available later, it can be converted using

`Omega = (2*pi/60)*rpm`

then

`U_tip = Omega*D/2`

`lambda = vi/U_tip`

and

`C_T,U = (pi/2)*lambda^2`

---

## Final synthesis

The tip-speed equation `T = C_T,U*rho*U_tip^2*D^2` and the actuator-disk equation `T = 2*rho*A*vi^2` are compatible because the inflow ratio links blade-tip speed to the induced air velocity through `vi = lambda*U_tip`. Dimensional analysis describes how thrust scales with rotor size and blade speed, while actuator-disk theory predicts the air velocity and minimum ideal induced power required for a specified thrust. Neither model alone determines the actual hover RPM or electrical power of a commercial propeller; measured propeller data or a more detailed aerodynamic and motor model are required.

