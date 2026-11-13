# Reflection — bill of materials

**Partners:** Jack Glod and Adrian Komorowski

## Design

- We chose a single-piece milled 6061-T6 aluminum frame for the final pair design. The frame is approximately 200 mm × 200 mm and is designed around 5-inch propellers. We kept aluminum because we had already modeled and analyzed a 6061 frame in the earlier structural labs, and the one-piece design gives us a simple, rigid structure that can be machined from one sheet.

- Several choices changed from our earlier work in Labs 01–09. The original iFlight XING2 2207 2755KV motors were replaced by EMAX ECO II 2004 2000KV motors, and the Ethix S5 propellers were replaced by Gemfan SL5125-3 propellers. The earlier FETtec ESC was replaced by a Holybro Tekko32 F4 4-in-1 50A ESC, and the earlier iFlight flight controller was replaced by the Holybro Kakute H7 V1.5. We kept a 4S 1500 mAh 100C battery but updated to the currently available XILO pack. We also finalized the frame material as McMaster-Carr 6061-T6 1/8-inch sheet. These changes are recorded in DECISIONS.md Rows 7–10.

## Propulsion

- At an estimated final all-up mass of about 600 g, each motor must produce about:

  `T_hover = 600 / 4 = 150 gf`

  The EMAX 2004 2000KV with the Gemfan SL5125 produces approximately 670 gf at full throttle on 4S, with about 12.5 A maximum current.

  The hover thrust margin is therefore:

  `150 / 670 = 0.224 = 22.4%`

  This meets the requirement of 35% or less.

  The estimated hover duty cycle is approximately 28–30%, which is well below the 60% maximum requirement.

  The ESC requirement is:

  `1.2 × 12.5 A = 15 A per motor`

  The selected Tekko32 ESC is rated at 50 A continuous per channel, so it passes with substantial margin.

  The battery must supply at least:

  `4 × 12.5 A = 50 A`

  The 1500 mAh 100C battery has a nominal current capability of:

  `1.5 Ah × 100C = 150 A`

  so the battery requirement also passes.

  Using the estimated hover current gives an idealized hover-time estimate of about 9 minutes. Even using the measured 40% throttle current of 2.8 A per motor as a conservative check gives approximately 6.4 minutes, so the design remains above the required 5-minute target.

- The propeller thrust/current behavior came from published bench-test data for the EMAX ECO II 2004 2000KV with the Gemfan SL5125 on 4S. We used those measured data as the main propulsion sizing source instead of relying only on theoretical motor KV. The thrust/current data are reasonably trustworthy because they come from an actual test of the motor/propeller combination. The torque coefficient is less certain because torque was not measured directly in our own setup and must be inferred using the motor and propeller relations from the lecture. We therefore trust the measured thrust and current numbers more than the torque estimate.

- The hover duty cycle is lower than the lecture rule-of-thumb of approximately 50%, but it still meets the required limit of less than 60%. This happened because the final drone is relatively light compared with the maximum thrust available from four motors. We accepted the lower hover duty cycle because it gives useful thrust reserve for climbing, disturbances, added hardware, and future payload while still using a lightweight motor.

## Mass and what comes later

- Our currently accounted BOM mass is approximately 541 g before the final installed wire length and the final mass of the printed battery/electronics mounts are known. We expect the finished all-up vehicle to remain around 600 g.

  About 102 g of the current mass budget is reserved for equipment that will be installed later: the receiver, Raspberry Pi companion computer and cooling/mount allowance, camera, and GPS/compass. These masses are planning values rather than measured masses on the finished aircraft, so the final all-up mass will need to be checked after assembly.

- The central area of the aluminum frame will include the 30.5 × 30.5 mm mounting pattern for the Kakute H7 and Tekko32 stack. Space is also reserved for the Raspberry Pi footprint and cable clearance. The receiver will use a small printed or adhesive mount with its antenna kept away from the conductive aluminum frame. The camera will mount toward the front of the drone, and the GPS/compass will be placed away from high-current wiring. The battery will sit in a custom printed mount underneath the aluminum frame.

## Print readiness

- The dimension we are least certain about is the exact clearance and geometry of the printed underbody battery mount and its relationship to the finished battery and frame. The design allows this part to be changed independently without remachining the main aluminum frame. We can also leave clearance around wiring and use adjustable or slotted features where needed.

- We have not printed the final battery mount yet. The underbody battery mount will be the first final-design part we print because it is inexpensive and quick to remake, and it lets us physically verify battery fit, clearance, and attachment before committing to any dependent geometry.

## Using AI

- AI helped us search a wider set of propulsion and flight-controller options than we had considered in the earlier labs. The most useful result was identifying lighter motor options and comparing the Kakute H7 against larger Pixhawk controllers using the actual requirements for firmware support, size, mass, serial ports, and future autonomy.

- AI was not always correct about product availability or links. For example, it initially suggested the EMAX motor from B&H even though the required 2000KV version was temporarily out of stock, and one early PyroDrone link went to a general collection rather than the exact product. We caught these issues by opening the live listings ourselves and replaced them with exact available product links. This reinforced that AI suggestions still need to be checked against manufacturer documentation and current seller pages.

## What is still uncertain

- The least reliable number in the BOM is the final all-up vehicle mass. The masses of the machined frame, final installed wire, printed battery mount, and small fasteners will change slightly from the current estimates. Before final assembly, the machined and printed components can be weighed individually, and the complete aircraft can be weighed on a scale. The propulsion check should then be repeated using that measured mass to confirm that the hover margin, duty cycle, and flight-time requirements are still satisfied.
