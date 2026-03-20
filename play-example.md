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

## Four-Phase Example

This example uses one d100 event roll per phase.

## Awakening Roll

- d100: 9
- Event: The lift stops on a floor that does not exist.
- Probability: 0.10
- Event deltas: Battery -8, Stability -10

State after phase:

- Battery 92
- Stability 90
- SIP 0
- Running probability: 0.10

## Journey

- d100: 41
- Event: A street vendor calls you Candidate.
- Probability: 0.25
- Event deltas: Battery -7, Stability -6

State after phase:

- Battery 85
- Stability 84
- SIP 0
- Running probability: 0.10 x 0.25 = 0.025 (2.5%)

## Interview

- d100: 76
- Event: A car slows to a crawl beside you.
- Probability: 0.50
- Event deltas: Battery -5, Stability -3

Ibis chooses Compliance in this phase to maintain Stability:

- Compliance deltas: Battery -5, Stability +5

State after phase:

- Battery 75
- Stability 86
- SIP 0
- Running probability: 0.025 x 0.50 = 0.0125 (1.25%)

## Return

- d100: 98
- Event: The OS speaks directly to you.
- Probability: 0.10
- Event deltas: Battery -8, Stability -10

Running probability becomes:

- 0.0125 x 0.10 = 0.00125 (0.125%)

This is above the 0.1% threshold, so no anomaly trigger applies this loop.

## What This Example Shows

- The loop uses exactly four d100 rolls.
- Battery and Stability move with event metadata.
- Compliance can trade Battery for short-term Stability maintenance.
- Probability can approach zero but still resist collapse into 0%.
