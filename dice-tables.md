---
layout: page
title: Dice Tables
permalink: /dice-tables/
---

All core roll rules in one place.

## Standard Checks

Use for most objectives.

- Roll pool dice (d6) from selected stat
- Add OS modifier based on Stability
- Compare total to DC 13

Formula:

- Total = Player Dice Sum + OS Modifier

Outcome:

- Total >= 13: Success
- Total < 13: Glitch

Stability shift:

- 5 x player dice count

## OS Modifier Thresholds

By current Stability:

- 90 to 100: +1d20
- 70 to 89: +1d12
- 50 to 69: +1d8
- 40 to 49: 0
- 21 to 39: -1d6
- 10 to 20: -1d8
- 0 to 9: -1d20

## Commute Back Roll (Objective B)

Roll size depends on current Battery:

- 100: 6d6
- 81 to 99: 5d6
- 61 to 80: 4d6
- 41 to 60: 3d6
- 21 to 40: 2d6
- 1 to 20: 1d6

Then:

- Add OS modifier
- Compare to DC 13
- Apply Stability change by dice count

## Result Roll (Objective R)

Roll d100 and compare to current Stability.

- Roll >= Stability: no penalty
- Roll < Stability: Stability penalty

Penalty tiers when roll is lower:

- Difference under 50: Stability -10
- Difference 50 or more: Stability -20

## Recharge Roll (Objective U)

Roll d100.

- If roll is higher than current Battery, Battery becomes that roll
- Otherwise Battery stays the same

## SIP Rule

Spend 1 SIP to negate next OS modifier.

- Player dice still roll
- Only OS modifier becomes 0 for that objective

## Battery Cost and Limits

- Objective battery cost: 5
- Battery floor: 0
- Battery ceiling: 100

If Battery reaches 0:

- Hard reset
- Battery becomes 60
- Loop +1
- SIP +1

## Stability Limits

- Floor: 0
- Ceiling: 100

If Stability reaches 0:

- Game over