---
layout: page
title: Core Mechanics
permalink: /mechanics/
---

## Core Loop

Play one full loop across four phases:

1. Awakening
2. Journey
3. Interview
4. Return

Roll one d100 event per phase.

Each event has a default probability value.
Multiply all rolled event probabilities to get Daily Success Probability.

## Probability Rule

- Daily Success Probability = p1 x p2 x p3 x p4
- Goal state is 0% Success Probability.
- 0% is mathematically unreachable, so the loop tends to continue.

## Threshold Trigger

If Daily Success Probability becomes 0.1% or lower during the loop:

- Stability -10
- SIP +1

This marks an anomaly event in the simulation.

## Battery Rule

- Battery starts at 100.
- Each rolled event applies its Battery delta.
- You may also spend Battery through Compliance (see below).
- If Battery reaches 0, the loop phase ends immediately.

## Stability Rule

- Stability starts at 100.
- Events apply Stability deltas based on event category.

### Stability Maintenance: Compliance Restore

Once per phase, you may choose Compliance:

- Battery -5
- Stability +5 (to a maximum of 100)

This represents performing the expected script to maintain internal order.

## SIP Rule

- SIP starts at 0.
- Gain SIP when you make self-directed choices that oppose expected behavior.
- Gain additional SIP from threshold anomaly triggers.

## Loop End and Repeat

The loop ends when:

- Return phase is resolved, or
- Battery hits 0 during any phase.

At loop end, record a receipt:

- Final Battery
- Final Stability
- Final SIP
- Final Daily Success Probability

Then begin the next loop on 31st of February.

