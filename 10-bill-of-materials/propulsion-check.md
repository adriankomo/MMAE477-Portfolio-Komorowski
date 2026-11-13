# Final Propulsion Check

**Partners:** Jack Glod and Adrian Komorowski

## Final configuration

- Vehicle mass used: 600 g estimated all-up mass
- Motors: 4 x EMAX ECO II 2004 2000KV
- Propellers: Gemfan SL5125-3
- Battery: XILO 4S 1500 mAh 100C
- ESC: Holybro Tekko32 F4 4-in-1 50A

Motor/prop bench data on 4S:
- 40% throttle: 213 gf, 2.8 A per motor
- 100% throttle: 670 gf, 12.5 A per motor

## Hover thrust

T_hover = W / 4

T_hover = 600 / 4 = 150 gf per motor

## Hover thrust margin

T_hover / T_max = 150 / 670 = 0.224

Hover thrust margin = 22.4%

Requirement: <= 35%

PASS

## Hover throttle

150 gf is below the 213 gf measured at 40% throttle.

Estimated hover throttle:

40% x (150 / 213) = 28.2%

Requirement: below about 60%

PASS

## ESC requirement

I_max = 12.5 A

Minimum ESC rating:

1.2 x 12.5 = 15 A per motor

Selected ESC rating = 50 A per channel

PASS

## Battery current requirement

Battery capacity = 1500 mAh = 1.5 Ah

Battery current capability:

1.5 Ah x 100C = 150 A

Required battery capability:

4 x 12.5 = 50 A

150 A > 50 A

PASS

## Hover time

Estimated hover current:

I_hover = 2.8 x (150 / 213)

I_hover = 1.97 A per motor

Estimated hover time:

t = 60 x 0.8 x 1.5 / (4 x 1.97)

t = approximately 9.1 minutes

Requirement: aim for at least 5 minutes

PASS

As a conservative check, using the full measured 2.8 A per motor from the 40% throttle point:

t = 60 x 0.8 x 1.5 / (4 x 2.8)

t = approximately 6.4 minutes

This still passes the 5-minute target.

## Result

All five propulsion requirements are met:

- Hover thrust margin: PASS
- Hover throttle: PASS
- ESC current rating: PASS
- Battery current capability: PASS
- Hover time: PASS
