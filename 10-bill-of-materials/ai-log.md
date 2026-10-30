AI LOG 
# AI log — bill of materials

**Partners:** Jack Glod and Adrian Komorowski  
**AI tool(s) used:** ChatGPT

| # | Part | What the AI suggested or claimed | How we checked it | Source (link) | Kept / rejected, and why |
|---|---|---|---|---|---|
| 1 | Motor | AI suggested the EMAX ECO II 2004 2000KV as a lighter, lower-current replacement for our earlier 2207 2755KV motor. | We checked the motor specifications, mounting pattern, 4S compatibility, weight, and available thrust/current test data with a 5-inch propeller. We also checked that the propulsion requirements could still be met with our estimated vehicle mass. | https://pyrodrone.com/products/emax-eco-ii-2004-brushless-motor-2000kv | **Kept.** It is much lighter than the earlier motor, provides enough thrust for our design, and reduces ESC and battery current requirements. |
| 2 | Motor supplier | AI initially suggested buying the EMAX motor from B&H. | We opened the exact product page and found that the 2000KV version was temporarily out of stock. We then checked another seller for the exact same motor and KV. | https://www.bhphotovideo.com/c/product/1818735-REG/emax_eco220042000_eco_ii_2004_brushless.html | **Rejected.** The motor choice was still good, but this supplier was rejected because the required 2000KV version was unavailable. We switched to the exact PyroDrone listing instead. |
| 3 | Flight controller | AI compared the Holybro Kakute H7 with the Pixhawk 6C Mini and full-size Pixhawk 6C for autonomous operation. | We checked official PX4 support, physical size, mass, serial ports, sensors, battery compatibility, and current product listings. | https://docs.px4.io/main/en/flight_controller/kakuteh7 | **Kakute H7 kept; Pixhawk options rejected.** The Pixhawks had strong autonomy support but were substantially heavier, larger, and more expensive than necessary for our approximately 600 g 5-inch quadcopter. |
| 4 | Frame material | AI suggested keeping 6061-T6 aluminum and purchasing 1/8-inch sheet stock rather than changing materials late in the project. | We compared the suggestion with our previous 6061 FEA model and checked McMaster-Carr stock dimensions, temper, specification, and price. | https://www.mcmaster.com/89015K18/ | **Kept.** It matches the material already analyzed and a 12 × 12 × 1/8 in sheet provides enough stock for our approximately 200 × 200 mm machined frame. |
