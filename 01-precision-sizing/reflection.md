# Reflection — precision-sizing pass

## What changed since your first pass (00)

I tightened the mass estimates by replacing rough ranges with actual component weights from verified product listings. I corrected the onboard mass by removing the RC transmitter, which should never be counted toward vehicle weight. I also switched to one of the officially provided motors and matched its thrust test to the correct battery voltage, ensuring the sizing aligns with the 4S system. Overall, this pass replaced assumptions with sourced values and eliminated early‑stage placeholders.


## Your numbers

- Total onboard vehicle mass, W (g): 541.86 g
- Battery cell count (S): 4S
- Hover thrust needed per motor, T = W / 4 (g): 541.86 / 4 = 135.47 g
- Motor you're checking against (one of the README's 3 candidates, or your own from `00`): iFlight XING2 2207 2755KV
- That motor's max thrust at a matching cell count (g), and where you found it (name + link): 1321 g at 16.0 V using 5.1 x 4.0 propeller. Source: Thingbits iFlight XING2 2207 Prop Test Report
- Margin = T / max thrust (%): (135.47 / 1321) * 100 = 10.25%
- Does this clear the 35% target? (yes / no, and if no, what would you
  change): Yes. Margin = 10.25%, which is below the 35% target, leaving substantial thrust required for hover.


## Anything still hard to pin down

The published thrust test does not use the same propeller as my build. My Ethix S5 prop is a 5×4 three‑blade, while the closest available test uses a 5.1×4.0 two‑blade. Because the diameter and pitch are similar, I used that test as the best available proxy, but actual thrust may differ due to blade geometry and loading. This remains an unavoidable assumption until I can test the exact prop‑motor combination.
