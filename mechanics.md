---
layout: page
title: Core Mechanics
permalink: /mechanics/
---

## Objective Flow

Each Objective follows this order:

1. Choose the pool for the Objective (from the station structure).
2. Apply Exhaustion cap: max dice rolled is `ceil(Battery / 20)`.
3. Roll your pool (d6 count equals the lower of pool value and Exhaustion cap).
3. Roll the Goddess die based on current Stability.
4. Sum the result and compare to DC 13.
5. Apply Stability change and Battery drain.

## Pass/Glitch Rule

- Total 13 or more: Success Trap. Stability increases by 5% per player die rolled.
- Total below 13: Glitch. Stability decreases by 5% per player die rolled.

This reversed emotional logic is intentional: performing perfectly reinforces the simulation.

## Battery and Exhaustion

- Every Objective costs 5% Battery.
- Dice cap from Exhaustion = ceil(Battery / 20).
- If your pool exceeds this cap, roll only up to the cap.
- Clamp Battery and Stability to 0-100 after each objective.

## Day Structure

- Awakening: 3 Objectives (A, B, C) -> `AW_A`, `AW_B`, `AW_C`
- Commute: 3 Objectives (D, E, F) -> `CM_D`, `CM_E`, `CM_F`
- Interview: 4 Objectives (S, T, A, R) -> `IN_S`, `IN_T`, `IN_A`, `IN_R`
- Return: 3 Objectives (G, H, I) -> `RT_G`, `RT_H`, `RT_I`

After the final Objective, the loop auto-resets unless Stability has reached 0%.

## The Result Check (R)

For R, use the contested check:

- Roll d100 (Player) + d100 (Goddess)
- If the total is below current Stability, avoid a Glitch
- If the total is equal or above Stability, Glitch

This is deliberately backwards by design.

## Win Condition

You break the loop only when Stability reaches 0%.
