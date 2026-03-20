This is a very simple version of how to play 31st of February.

## What You Are Trying To Do

You are stuck in a repeating day.

Your goal is to get Stability to 0.
When Stability reaches 0, you break the loop.

## Your Stats

- Battery starts at 100.
- Stability starts at 100.
- SIP starts at 0.

You assign your 3 pool values once:
- MSK
- SNS
- LOG

Use 1, 2, and 3 exactly once across those pools.

## The Day Loop

You play 13 checks in this order:

- Awakening: D, O, W
- Journey: G, L, Y
- Interview: S, T, A, R
- Return: B, U, M

## Core Check (Most Objectives)

For normal objectives:

1. Pick a pool (MSK, SNS, or LOG).
2. Roll that many d6.
3. Roll The OS die based on current Stability.
4. Add everything together.
5. Compare total to DC 13.

Result:
- 13 or more = Success Trap: Stability goes up by 5 per player die rolled.
- Below 13 = Glitch: Stability goes down by 5 per player die rolled.

Also:
- Every objective costs 5 Battery.
- Clamp Battery and Stability between 0 and 100.

## Special Checks

R (Interview Result):
- Roll d100 + d100.
- If total is below current Stability, it is a Glitch.
- If total is equal to or above Stability, you avoid a Glitch.

B (Commute Back):
- This is a normal pool check, but dice are capped by Exhaustion.
- Max dice you may roll = ceil(Battery / 20).

U (Recharge):
- Roll d100 at loop end.
- If the roll is higher than current Battery, next-loop Battery becomes that roll.
- Otherwise Battery carries over.

M (Receipt Printing):
- Record final Battery.
- Record final Stability.
- Record total Successes.
- Record total Glitches.

## SIP (Special Interest Points)

- Gain 1 SIP after each completed loop.
- Spend 1 SIP to negate one OS roll.
- SIP carries between loops.

## Optional Flavor Rule

If a normal objective total equals DC exactly:
- Apply glitch overlay.
- Lose 10 Stability.
- Roll on the d20 glitch table for flavor.

## One-Line Summary

You are trying to escape by glitching the system enough to drop Stability to 0, while managing Battery so you can keep completing loops.
