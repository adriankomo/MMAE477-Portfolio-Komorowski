# Design Decision Log

Every consequential design decision gets a row **when it is made**, not
reconstructed later. This log is the backbone of every design review and
defense this semester, they ask exactly these questions.

| # | Date | Decision | Alternatives considered | Criteria used | Evidence (link) | Assumptions still uncertain |
|---|---|---|---|---|---|---|
| 1 | 8.21.26 | *Sizing exercise: chose the unmanned/autonomous track* | *manned* | *component availability, familiarity, scope* | *`00-drone-sizing-exercise/sizing-table.csv`* | *how these numbers compare to the real course constraints, not yet set* |
| 2 | 8.28.26 | Refined the initial drone sizing by replacing rough component estimates with specific parts and verified masses. Selected the iFlight XING2 2207 2755KV motor and confirmed it provides sufficient hover thrust. | Original rough sizings & old motor | Actual component masses, 4S compatibility, documented motor thrust, and verified <35% hover margin | *`01-precision-sizing/sizing-table.csv`* | Actual thrust may vary with final propeller choice and real operating conditions |


**A good row survives the question: "Why should I believe this was the right
call?"** If the evidence link is empty, the decision isn't defensible yet.
That's a to-do, and the last column says what must be modeled or measured
before it's settled.
