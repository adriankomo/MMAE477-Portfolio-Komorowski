# Design Decision Log

Every consequential design decision gets a row **when it is made**, not
reconstructed later. This log is the backbone of every design review and
defense this semester, they ask exactly these questions.

| # | Date | Decision | Alternatives considered | Criteria used | Evidence (link) | Assumptions still uncertain |
|---|---|---|---|---|---|---|
| 1 | 8.21.26 | *Sizing exercise: chose the unmanned/autonomous track* | *manned* | *component availability, familiarity, scope* | *`00-drone-sizing-exercise/sizing-table.csv`* | *how these numbers compare to the real course constraints, not yet set* |
| 2 | 8.28.26 | Refined the initial drone sizing by replacing rough component estimates with specific parts and verified masses. Selected the iFlight XING2 2207 2755KV motor and confirmed it provides sufficient hover thrust. | Original rough sizings & old motor | Actual component masses, 4S compatibility, documented motor thrust, and verified <35% hover margin | *`01-precision-sizing/sizing-table.csv`* | Actual thrust may vary with final propeller choice and real operating conditions |
| 3 | 9.4.26 | Compared a 6061 aluminum flat plate with a carbon fiber round tube for the 120 mm drone arm. Paired aluminum with the flat plate and carbon fiber with the round tube. The carbon fiber tube had lower self-weight (6.81 gf vs. 13.06 gf), while both designs produced only a small change from the idealized bending moment. | Carbon fiber flat plate and aluminum round tube | Self-weight, cross-sectional area, material density, shear force, and bending moment | [Aluminum flat bar](https://www.onlinemetals.com/en/buy/aluminum-rectangle-bar-6061), [Carbon fiber tube](https://dragonplate.com/dragonplate-carbon-tube-10mm-od-x-288id-x-24), `02` calc-table.csv | This pass does not yet determine which arm is stronger or stiffer. Stress, deflection, mounting method, and final arm dimensions still need to be evaluated. |
| 4 | 9.11.26 | Continued the 6061 flat plate from 02 for the principal‑stress check, using the same 12.7 mm × 3.175 mm section and evaluating root and mid‑span stresses. | No new geometry or materials added; the round tube from 02 wasn’t used since this analysis requires the rectangular plate. | Alignment with the 02 design, rectangular‑section shear formula, principal‑stress and von Mises results | `02-shear-force-bending-moment/calc-table.csv`, `03-principal-stress/stress-table.csv` | Beam theory may under‑predict root stresses because the real joint introduces local effects. Final agreement still needs verification in FEA. |


**A good row survives the question: "Why should I believe this was the right
call?"** If the evidence link is empty, the decision isn't defensible yet.
That's a to-do, and the last column says what must be modeled or measured
before it's settled.
