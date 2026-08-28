# Reflection — precision-sizing pass

## What changed since your first pass (00)

*(A few sentences: what did you tighten, fix, or catch in your original
sizing table? Real errors count as useful findings here, not embarrassing
ones.)*


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

*(What's still an assumption or a guess in your table, and why? It's fine
for this to be a real, unresolved list — that's the point of flagging it.)*
