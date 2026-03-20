---
layout: page
title: Play Example
permalink: /play-example/
---

Candidate: Ibis

- MSK 2
- SNS 1
- LOG 3
- Battery 100
- Stability 100
- SIP 0

Reference IDs (from `tables.json`): `AW_A`, `AW_B`, `AW_C`

## Awakening A: Bed (LOG)

- Player rolls 3d6: 4, 3, 2 = 9
- Goddess at 100% Stability: +1d20 -> 6
- Total = 15 (Success Trap)
- Stability change: +5% per die rolled (3 dice) -> +15
- Clamp Stability to 100
- Battery: 100 -> 95

## Awakening B: Mirror (MSK)

- Player rolls 2d6: 2, 1 = 3
- Goddess +1d20 -> 10
- Total = 13 (Success Trap)
- Stability +10
- Battery: 95 -> 90

## Awakening C: Fuel (SNS)

- Player rolls 1d6: 2
- Goddess +1d20 -> 4
- Total = 6 (Glitch)
- Stability -5
- Battery: 90 -> 85

## End of Awakening Summary

- Battery: 85
- Stability: 95
- SIP: 0
- Next season: Commute (`CM_D`, `CM_E`, `CM_F`)

Continue through all stations.

At end of loop:

- Commute Back (`RT_G`) uses Exhaustion: max dice is `ceil(Battery / 20)` for that check only.
- Recharge (`RT_H`): roll d100. If it is higher than current Battery, next-loop Battery becomes that value.
- Receipt Printing (`RT_I`): record final Battery, final Stability, total Successes, and total Glitches.
- If Stability is above 0%, loop resets and SIP +1.
- If Stability is 0%, the loop breaks.

Loop carryover example:

- End Loop 1 with Stability above 0% -> reset to next loop and SIP becomes 1.
- Spend SIP at any future objective to negate one Goddess roll.
