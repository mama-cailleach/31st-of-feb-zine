---
layout: page
title: Game Mechanics
permalink: /game-mechanics/
---

Core play loop, simplified.

## Objective of Play

Move through all stations in order.
Resolve each objective.
Track your state.
Repeat loops.

## Station Order

1. Awakening
2. Journey
3. Interview
4. Return

## Objective Order

D, O, W, G, L, Y, S, T, A, R, B, U, M

## Standard Objective Flow

1. Read station prompt.
2. Read objective prompt.
3. Choose pool (MSK, SNS, LOG) if prompted.
4. Roll dice.
5. Apply OS modifier from Stability band.
6. Compare total to DC 13.
7. Apply outcome:
   - Success: Stability increases
   - Glitch: Stability decreases and glitch flavor
8. Apply objective Battery cost.
9. Advance.

## Standard Roll Formula

Total = Player Dice Sum + OS Modifier

- If Total is 13 or higher: Success
- If Total is below 13: Glitch

Stability change size is based on dice rolled:

- Change = 5 x number of player dice used

## Pool Use Rule

Inside a station, each pool can be used once for normal pool objectives.
If all pools are spent and more pool objectives remain, the engine skips forward.

## Special Objectives

R: Result

- Roll d100
- Compare to current Stability
- If roll is lower, Stability penalty applies

B: Commute Back

- Roll battery-scaled d6 pool
- Resolve vs DC 13 with OS modifier

U: Recharge

- Roll d100
- If higher than current Battery, Battery becomes that roll

M: Receipt Printing

- Enter print receipt
- Record loop summary
- Continue to next loop

## Resource Rules

Battery:

- Usually minus 5 per resolved objective
- If Battery reaches 0, emergency reboot:
  - Battery resets to 60
  - Loop increases
  - SIP increases by 1

Stability:

- If Stability reaches 0, game ends

SIP:

- Spend 1 to negate next OS die modifier

## End States

- Ongoing loop play: default state
- Hard reboot: Battery depletion event
- Game over: Stability reaches 0