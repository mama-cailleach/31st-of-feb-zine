---
layout: page
title: Core Mechanics
permalink: /mechanics/
---

## Objective Flow

Each Objective follows this order:

1. Choose the pool for the Objective (from the station structure).
2. Roll your pool (d6 count equals your chosen pool value).
3. Roll The OS die based on current Stability.
4. Sum the result and compare to DC 13.
5. Apply Stability change and Battery drain.

## Pass/Glitch Rule

- Total 13 or more: Success Trap. Stability increases by 5% per player die rolled.
- Total below 13: Glitch. Stability decreases by 5% per player die rolled.

This reversed emotional logic is intentional: performing perfectly reinforces the simulation.

## Battery and Objective Cost

- Every Objective costs 5% Battery.
- Clamp Battery and Stability to 0-100 after each objective.

## Day Structure

- Awakening: 3 Objectives (D, O, W) -> `AW_A`, `AW_B`, `AW_C`
- Journey: 3 Objectives (G, L, Y) -> `CM_D`, `CM_E`, `CM_F`
- Interview: 4 Objectives (S, T, A, R) -> `IN_S`, `IN_T`, `IN_A`, `IN_R`
- Return: Commute Back check, Recharge check, then Receipt Printing summary (B, U, M) -> `RT_G`, `RT_H`, `RT_I`

## Station IV: Exhaustion and Recharge

- Exhaustion only applies to Commute Back (`RT_G`, letter B).
- For Commute Back, maximum dice rolled is `ceil(Battery / 20)`.
- Roll your normal pool, but cap dice to that Exhaustion limit.
- At loop end, Recharge (`RT_H`) is a d100 roll.
- If Recharge is higher than your current Battery, next loop Battery becomes that roll.

## Receipt Printing (M)

- Receipt Printing (`RT_I`) summarizes the completed loop.
- Include final Battery, final Stability, total Successes, and total Glitches.

After Receipt Printing, the loop resets unless Stability has reached 0%.

## The Result Check (R)

For R, use the contested check:

- Roll d100 (Player) + d100 (The OS)
- If the total is below current Stability, avoid a Glitch
- If the total is equal or above Stability, Glitch

This is deliberately backwards by design.

## Win Condition

You break the loop only when Stability reaches 0%.
